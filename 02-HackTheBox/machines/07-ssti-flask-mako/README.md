# SSTI – Flask / Mako

This lab demonstrates a Server-Side Template Injection (SSTI)
vulnerability in a Flask application using the Mako template engine.

**Category:** Web Security  
**Vulnerability:** Server-Side Template Injection  
**Impact:** Remote Code Execution (RCE)

## Quick Summary

The vulnerable Flask application accepts user input through a GET parameter and directly inserts it into a Mako template without proper sanitization. This allows attackers to inject malicious template syntax to execute arbitrary Python code on the server.

## Exploitation Method

Mako templates allow Python expressions within `${}` syntax. By injecting payload like `${''.join(__import__('os').popen('command').readlines())}`, an attacker can execute system commands.

## Key Concepts

- **SSTI (Server-Side Template Injection):** A vulnerability where untrusted user input is embedded into server-side templates
- **Template Engine:** Mako is a Python templating library that allows embedded Python expressions
- **Attack Vector:** GET parameter or form input that flows directly into template rendering
- **Risk Level:** CRITICAL - Allows unauthenticated remote code execution