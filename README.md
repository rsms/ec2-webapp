# EC2 web app template

This is a template I use to quickly set up Node.js-backed web apps on Amazon EC2

- Less than 15 minutes from start to finish
- Eligible/compatible with the ["AWS Free Usage Tier"](http://aws.amazon.com/free/)
- Ubuntu Linux
- High-performance Nginx HTTP server
  - Sensible default configuration (three flavors to chose from)
  - Automatically handles all static file requests
  - Delegates non-static requests to the Node.js web server
- Git-based deployment
- Init.d scripts

This template enables a very smooth, simple and scalable workflow

- When developing locally, the single command `bin/myapp-httpd.mv` runs your web server and takes care of serving static files
- When deploying changes (after a git push), `myapp-update restart` deploys changes and restarts services on your server
- Rolling back the server to an earlier version is a simple as `myapp-update restart v0.1.2`

> Here's a guide on getting started with Amazon EC2: <http://rsms.me/2011/03/23/ec2-wep-app-template.html>

**Let's get started!** Head over to [INSTALL.md](https://github.com/rsms/ec2-webapp/blob/master/INSTALL.md#readme)
