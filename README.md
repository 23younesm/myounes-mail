# Local Mail Server with Roundcube (ccso.local)

This repository sets up a local mail server with SMTP, IMAP, and Roundcube webmail using Docker.  
The mail server domain is `maguireyounes.com` and is intended for local network or lab use.

---

## Components

- **Mailserver**: Uses [docker-mailserver](https://github.com/docker-mailserver/docker-mailserver) (Postfix + Dovecot)
- **Webmail**: Roundcube (webmail client)
- **Docker**: Services run as Docker containers managed with `docker-compose`

---

## Ports

| Host Port | Service                 | Purpose                                   | Notes                        |
|-----------|-------------------------|-------------------------------------------|------------------------------|
| 25        | SMTP                    | Receiving emails from other mail servers | May be blocked by ISP/firewall |
| 587       | SMTP Submission         | Sending emails with authentication       | Use for authenticated email sending |
| 143       | IMAP                    | Mail retrieval (unencrypted)              | Used by mail clients          |
| 993       | IMAP (SSL/TLS)          | Secure mail retrieval                      | Use for secure mail clients   |
| 8080      | Roundcube Webmail UI    | Access webmail in a browser               | Default web UI port           |

---

## Setup & Usage

1. **Edit your hosts file (on your Windows machine):**

Add this line to `C:\Windows\System32\drivers\etc\hosts` (run editor as Administrator):
```bash
127.0.0.1 mail.maguireyounes.com
```

2. **Start the mail server:**

```bash
docker-compose up -d
```

3. **Create a mail user:**

```bash
docker exec -it mailserver setup email add <user>@maguireyounes.com <password>
```

4. **Access Roundcube webmail:**

Open a browser and navigate to:
```bash
http://mail.maguireyounes.com:8080
```
Log in using your created email and password.