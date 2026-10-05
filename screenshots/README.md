# Hardening a Web Server with Nginx and UFW

## What this project is
A short paragraph: I built a small web server and protected it using
an Nginx reverse proxy, HTTPS, and a UFW firewall, on Ubuntu (WSL).

## Architecture
Client -> Nginx (reverse proxy, HTTPS) -> UFW firewall -> App server (127.0.0.1:8000)

(Add your diagram image here if you made one.)

## What I built
1. A tiny app listening only on 127.0.0.1:8000 (hidden from outside)
2. Nginx as a reverse proxy in front of it
3. A self-signed HTTPS certificate
4. Security headers and hidden Nginx version
5. UFW rules: deny all incoming, allow only 22, 80 and 443

## Key commands
- `sudo ufw default deny incoming` : block everything by default
- `sudo ufw allow 443/tcp` : open only the HTTPS door
- `sudo nginx -t` : test the config before reloading
(add a sentence on each one in your own words)

## Proof it works
### App is private
![app private](screenshots/01-app-private.png)
(One sentence explaining what the image shows.)

### HTTPS and redirect
![https](screenshots/04-https-works.png)
![redirect](screenshots/05-http-redirect.png)

### Firewall rules
![ufw](screenshots/06-ufw-status.png)

### Scan from outside
![nmap](screenshots/07-nmap-scan.png)
![port 8000](screenshots/08-port-8000-hidden.png)

## What I learned by breaking it
- Closing port 443 made the site unreachable even though Nginx was running.
- `nginx -t` caught my deliberate typo before it broke the server.
- (Add your own.)

## How to run it
1. Start the app: `python3 -m http.server 8000 --bind 127.0.0.1`
2. Copy `nginx-myapp.conf` to `/etc/nginx/sites-available/myapp`
3. Create the certificate (see command in the config)
4. Enable the site, run `sudo nginx -t`, reload Nginx
5. Apply the UFW rules
