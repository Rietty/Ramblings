+++
title = "Hello, World!"
date = 2022-10-03
[taxonomies]
tags = ["introduction", "zola", "terminimal", "lightsail"]
+++

Hello, World! It goes without saying that this is my first blog post. I figured I would take this time to document my process of setting up this website and the amount of effort that went into it. To begin with, I leveraged a few pieces of software to build the website, including: [Zola](https://github.com/getzola/zola) for the static site generator, [Terminimal](https://github.com/pawroman/zola-theme-terminimal) for the theme, and [AWS Lightsail](https://aws.amazon.com/lightsail/) for hosting. 

When I originally had this website, it was a simple wordpress instance I was not very happy with. It was buggy, relied on various plugins, was a pain to put anything on it, and above all it did not look how I wanted it to. Thus, I decided to explore other options and eventually someone pointed me in the direction of Zola. I had heard of static site generators before, but I had never really looked into them. I figured I would give it a shot and see what I could do with it.

Zola itself is a static site generator written in Rust, which happns to be my favourite language (currently), the generator itself is a single binary and can be dropped pretty much anywhere. Along with an impressive list of features and amazingly fast build times, it was a no-brainer to go with it.

Next, was figuring out the theme I wanted to go with. My requirements were that it had to be minimal, utilize a dark background and be fairly easy to customize. I found a few themes that fit the bill, but none of them were quite what I was looking for. I eventually stumbled upon Terminimal, which was exactly what I was looking for. Some other options I considered were: [Abridge](https://www.getzola.org/themes/abridge/), [d3c3nt](https://www.getzola.org/themes/d3c3nt/), and [Soapstone](https://www.getzola.org/themes/soapstone/).

Finally, the hosting was most likely the easiest portion to figure out, [Lightsail](https://aws.amazon.com/lightsail/) is such an easy option due to how simple they make it to get set up, pick a plan. I went with the cheapest option, which fits all my needs and is less than $5 a month. Lightsail also allows you to have a static IP address, which makes setting up some DNS and SSL ([Let's Encrypt](https://letsencrypt.org/)) a breeze. This website is served using an nginx server, which is one of the default instance choices when setting up the lightsail instance.

Once I had all of these things set-up, all that was left was customizing the site, which involved taking a look at the [various options](https://github.com/pawroman/zola-theme-terminimal/#how-to-start) provided by my theme and editing my [`config.toml`](https://github.com/Rietty/Ramblings/blob/main/config.toml) file. I also had to make a few changes to the theme template, adding some extra pages and fiddling around with the tag system in order to make titles and descriptions appear on the tag pages and work properly. 

Lastly, the final piece of the puzzle was setting up a script that built and deployed the website to my instance. I did this by using [Powershell](https://learn.microsoft.com/en-us/powershell/). The first step involved getting my ssh/ssl file from Amazon in the format of a `pem` file. Utilizing this and an SSH client, I could then connect to my instance. I then wrote this small script below.

```powershell
# Build the site.
.\zola.exe build
# Add the website files to the git repo.
git pull # Just in case I changed something on the repo itself.
git add .
git commit -am "Publishing site"
git push origin main
# Connect to the instance and download build, execute update serverside.
ssh -i security.pem <username>@<ip-address> "./update.sh"
```

This script is run on my local machine and pushes the latest build to GitHub. The `update.sh` script is a simple script that pulls the latest build from GitHub and places it in the correct location on the instance.

```bash
#!/bin/bash
# Change to the correct directory.
cd ~/my-website
# Pull the latest build from GitHub.
git pull
 # Copy the files to the correct location, only if they have changed.
rsync -av ~/my-website/public/ ~/stack/nginx/html
```

This is a very simple setup, and I'm sure there are better ways to approach this, however it currently works fine. I'm sure I will be tweaking this setup as I go along. Very excited to see where this goes from here as I continue to learn more about Zola and the various other tools I am using.