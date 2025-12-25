---
layout: post
title: Hello, World!
---
## Intro

Welcome to my blog! This is my very first website, where I'll be sharing my thoughts, experiments, and experiences as I learn and grow. I'm excited to document my journey here and connect with others along the way.

This site is built with [Jekyll](https://jekyllrb.com/), a simple and powerful static site generator that makes it easy to create and manage content. I look forward to exploring more features and customizing my site as I go!

---
## Infrastructure

This site is hosted on an [Amazon S3 Bucket](https://aws.amazon.com/) and served as a static site.

### DNS Management

DNS and routing is handled via Amazon's Route 53 and CloudFront.

### SSL Certificates with Amazon

Amazon provides free SSL/TLS certificates via CloudFront. Certificates are set up with automatic renewal and do not need to be managed.

---
## Storage and Deployment

All of the site's raw files are stored in a public [GitHub repository](https://github.com/Rietty/Ramblings). This makes it easy to track changes and roll back if needed.

For deployment, I use GitHub Actions to automate the build and deployment process:

- **Build:** On every push to the main branch, GitHub Actions runs a workflow that installs dependencies (including Jekyll and Bundler) and builds the static site.
- **Deploy:** After building, the workflow uses SSH and SCP to securely copy the generated site files to my S3 bucket, updating the live site automatically.

This setup ensures that publishing new content or making changes is as simple as committing and pushing to GitHub.

---
## Final Words

Thank you for visiting my blog! I don't plan on having a specific post schedule but I do look forward to writing for this! Hopefully you all enjoy reading it! :)