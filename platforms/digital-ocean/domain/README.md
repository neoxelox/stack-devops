# Domain - FREE DNS management

## Connexion

---

## Errors

> **Email service does not work after porting MX DNS record.**

Although lesser is better, check the record's priority is > 1. 0 priority records do not work very well. Use an standard value of 10.

## Documentation

> **Porting DNS records to Digital Ocean servers without losing email service of your provider.**

In your provider DNS settings do not deactivate MX records. In Digital Ocean create a MX DNS record in your domain as: `MX DOMAIN MX_SERVER_HOST. 10 14400`.

---
