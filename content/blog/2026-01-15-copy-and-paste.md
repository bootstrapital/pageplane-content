---
title: Copy & Paste Deployments
date: 2026-01-15
slug: copy-and-paste-deployments
tags: [web-development, deployment, static-sites, indie-hacking, 
developer-tools, html, python]
---

# Copy & Paste Deployments

I struggled to learn web development when I first got hooked on the web in the early aughts.

I was comfortable automating data workflows at work using VBA and eventually Python, but for whatever reason, I just could not grok full-stack coding. The gap between a script that ran on my machine and a living, breathing web application felt insurmountable.

Then I discovered No-Code, and I was elated. It felt like the promise of the internet was finally at my fingertips. You could really go from an idea to a functional prototype in a weekend. I was so convinced that I even wrote about [not learning to code](https://medium.com/@thedatadavis/don-t-learn-to-code-6c2b69c65a42) because the tools were getting so good.

But as I became more sophisticated and had my first experience building a fast-growing startup from the ground up, the cracks in the No-Code stack became apparent.

I started evolving my thinking around what an optimal stack for a bootstrapper might look like. I experimented with what I called [Slender Stack Development](https://medium.com/@thedatadavis/slender-stack-development-d1a4ac729ffa): a way to stay lean without getting trapped in walled gardens. Even as I refocused on the Modern Data Stack in my day job, I kept hacking on side projects, picking up product engineering skills, and helping other founders bootstrap their MVPs.

### The Inflection Point

Like many, I was skeptical of the early promises made by GenAI proponents. And then, like some, my socks were knocked off by GPT-3.5.

Suddenly, the possibilities were expansive again. My intolerance and impatience with boilerplate, JavaScript frameworks, and build steps were no longer bottlenecks. I could build things that popped into my head within hours instead of days.

One of the first things I built during this era was [Tab Tally](https://chromewebstore.google.com/detail/tab-tally/kbhboaenebhhbcekfjeffmclocigjenn?pli=1), a Chrome extension that simply shows how many tabs you have open. I was annoyed that the desktop browser didn't do this natively like the iOS app does. With ChatGPT, I had a working version in minutes and polished it over a ~3-hour session.

Today, I mostly use Gemini (thanks to a free student pro plan), and the workflow has only gotten faster.

### The Rise of HTML Tools

Lately, I’ve taken this a step further. I’ve been spinning up high-fidelity prototypes in raw HTML to explore ideas, following a pattern similar to [Simon Willison’s HTML tools](https://simonwillison.net/2025/Dec/10/html-tools/).

The workflow is liberating: simple, single-file applications that do one thing well. No complex build pipelines, no framework fatigue. Just an idea, a chat with an LLM, and a working demo in minutes.

But I needed a place to put them.

### Enter Pageplane

I created [Pageplane](https://pageplane.app) as a minimalist static site host for this exact workflow.

![pageplane-overview](https://github.com/user-attachments/assets/04fee244-ee3b-4b29-83b8-de690c7d0694)

The premise is dead simple:
1. Generate full HTML from the chat of your choice.
2. Copy it.
3. Paste it into a new Pageplane project.
4. Deploy.

That’s it. You can even add custom domains (my personal site, [cdavis.xyz](https://cdavis.xyz), is proudly hosted on Pageplane). It’s also a PWA, so you can install `pageplane.app/new` to your homescreen and deploy ideas directly from your phone.

If GitHub Pages is the "heavy" way to deploy static sites, think of Pageplane as Carrd meets GitHub Gists. It is a home for your tools, demos, experiments, and objects-thrown-at-the-wall-to-see-what-sticks.



This blog post itself is a product of this philosophy. I needed a way to handle content without breaking the single-file constraint or setting up a CMS. So, I wrote [Flatcontent](https://github.com/bootstrapital/flatcontent) in about 30 minutes. It turns markdown files into a JSON artifact that can be fetched by the HTML file on Pageplane.

### Under the Hood

Because I built Pageplane to help people avoid over-engineering, I made sure not to over-engineer Pageplane itself. It runs on a boring, reliable stack designed for speed and low maintenance.

*   **Core:** Python 3.13 & Flask. Simple, proven, and fast enough.
*   **Database:** SQLite on Fly.io. For a read-heavy application like this, SQLite is performant and drastically simplifies the infrastructure (no separate database server to manage).
*   **Storage:** Cloudflare R2 (via Boto3). S3-compatible but with zero egress fees, which is critical for a platform designed to serve static sites.
*   **Infrastructure:** Deployed on Fly.io with OpenTelemetry for observability.
*   **Billing:** Polar.

This efficient architecture allows me to keep the service sustainable. The Free Plan lets you host up to 3 active projects on subdomains. Adding custom domains starts at just $29/year.

### What’s Next?

I’m currently building out the roadmap, which includes:
*   **Analytics:** Basic views on traffic (using Posthog).
*   **API & White Labeling:** For more sophisticated use cases like personalized marketing campaigns or programmatic SEO.
*   **Multi-page Support:** Handling generic static assets (JSON, Markdown) alongside the HTML entry point.

If you don’t have a dedicated workflow for deploying tiny things quickly, or if you just want to save a few clicks by skipping the *repo creation -> push -> Vercel/Netlify* loop, give [Pageplane](https://pageplane.app) a spin.
