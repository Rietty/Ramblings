---
layout: post
title: Hello, World!
---
## Intro

Welcome to my blog! This is my very first website, where I'll be sharing my thoughts, experiments, and experiences as I learn and grow. I'm excited to document my journey here and connect with others along the way.

This site is built with [Jekyll](https://jekyllrb.com/), a simple and powerful static site generator that makes it easy to create and manage content. I look forward to exploring more features and customizing my site as I go!

---
## Infrastructure

This site is hosted on [Amazon Lightsail](https://lightsail.aws.amazon.com/), a simple cloud platform for deploying web applications and websites. Lightsail provides me with a static IP address, ensuring the site is always reachable at the same address, even if the underlying server changes or I rebuild the instance.

### DNS Management

DNS records are configured to point the domain to the static IP address. This means I can just add or remove records from the DNS to increase

### NGINX Stack with Bitnami

The server uses the [Bitnami NGINX stack](https://bitnami.com/stack/nginx), which bundles [NGINX](https://nginx.org/) with other useful tools for easy deployment and management.

### SSL Certificates with Let's Encrypt

[Let's Encrypt](https://letsencrypt.org/) provides free SSL/TLS certificates for HTTPS. Certificates are set up with automatic renewal via `cron` so I don't need to worry about renewing it manually every 90 days.

### Custom Routing with NGINX

NGINX is configured for custom routing, allowing different subdomains (such as [twitch.rietty.com](https://twitch.rietty.com)) to serve specific content, apps or just plain old redirects as I need them.

---
## Storage and Deployment

All of the site's raw files are stored in a public [GitHub repository](https://github.com/Rietty/Ramblings). This makes it easy to track changes and roll back if needed.

For deployment, I use GitHub Actions to automate the build and deployment process:

- **Build:** On every push to the main branch, GitHub Actions runs a workflow that installs dependencies (including Jekyll and Bundler) and builds the static site.
- **Deploy:** After building, the workflow uses SSH and SCP to securely copy the generated site files to my Lightsail instance, updating the live site automatically.

This setup ensures that publishing new content or making changes is as simple as committing and pushing to GitHub.

---
## Final Words

Thank you for visiting my blog! I don't plan on having a specific post schedule but I do look forward to writing for this! Hopefully you all enjoy reading it!