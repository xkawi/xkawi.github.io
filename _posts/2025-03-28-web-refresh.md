---
title: "Porfolio Website Refresh"
date: 2025-03-28
description: "Introductory notes on my portfolio website refresh with the help of AI"
tags: []
---

As I was having the infrequent reflection moment and with the recent trends of AI model, my mind was brought back into this portfolio website that I have not been maintaining since 2016, almost 10 years.

It was using unsplash API as the background image (fullscreen too, no less), which I believe has been broken for ages. My bio sounded "old" in today's age, or rather "still young" as it was written when I just started my career.

My profile picture on the favicon was when I still skinny (not that I grew wider horizontally now, but let's just say, I have... changed.) wearing a formal shirt which was taken during one of the bank recruitment event (iirc it was Credit Suisse) that I attended back in school time, which of course I did not take up.

I also had a "buy me coffee" button which led to a paypal page for people to "donate" (it is still [working by the way](https://www.paypal.com/paypalme/KawiXiao/3usd), so if you feel like it, my paypal wallet still open to accept your donation 😉), and in 10 years of the website's life, I managed to receive USD 3 from "Digital Karma", and the reason? "Redux-saga module project is awesome." Someone appreciated my open source contribution apparently, felt good back then regardless of the amount. Hey Digital Karma, if you read this article somehow, thank you for your coffee!

### Claude enters the chat

Fast forward to 2026, where AI is everywhere, equipped with my curiousity to learn more about it, I was like: "_hey why not refresh my bio page using Claude?_"

It started with me asking for a design/styling refresh only with this prompt on Claude Code web:

> study this portfolio website and its design - _link to website design that I like_ - build something similar for me and commit it in a new branch and create a PR for review; but explain to me first your proposed design theme before writing any code

imo the output is pretty decent, with light/dark mode theme supports too without me asking for it. But there were still a few back and forth prompt iterations regarding the layout, until it churns out current layout.

Then I moved into VS Code on my local machine to continue the Claude Code sessions and follow its implementation closely. At some point, I raised a bug where the hamburger button not working on mobile, and here is my prompt:

> Me: for the hamburger icon that toggle the sidebar, I don't think that works, same for the theme toggle, they don't seems to do anything when I tried mobile view on browser, please investigate

which it fixes correctly:

```
Found it. The .drawer-overlay has display: block on mobile (from the media query) and position: fixed; inset: 0; z-index: 60 — making it an invisible full-screen element sitting on top of the mobile header (z-index: 50). Every tap on the hamburger or theme toggle is swallowed by that transparent overlay layer.

The fix is pointer-events: none on the overlay by default, only enabling interaction when the drawer is actually open:
...
...
Root cause: The mobile media query sets .drawer-overlay { display: block }, but the overlay is position: fixed; inset: 0; z-index: 60 — so it silently covers the entire screen as a transparent layer. Since the mobile header is only z-index: 50, all taps (hamburger + theme toggle) were absorbed by the invisible overlay before reaching the buttons.

pointer-events: none makes it pass-through when closed; pointer-events: auto restores interactivity only when the drawer is open and the dim background should be tappable to close it.
```

At this point, rather than impressed with the actual code fix/output, I find the explanation of the problem more useful because it gives me additional knowledge too.

All of the above happens within a few minutes of my iteractions with Claude, which arguably if you write them by hand probably going to take days.

As my excitement grows, I wanted "test more", and thought of "why not add articles in as well?". I am aware of the latest framework for static articles/blogs, such as Astro or Gatsby, but I was not so keen on dealing with the setup. Then I prompted Claude for suggestions:

> how can I host the articles within this static website? ideally I can commit the articles (ideally markdown format) into git and have it rendered automatically. This static website is hosted by github pages. Propose some options that I can choose from.

It gave me 4 options with Pros and Cons. Here are 2 of them worth highlighting:

```
Option 2 — Jekyll (native GitHub Pages build)
GitHub Pages has built-in Jekyll support — push .md files with YAML front matter and GH Pages builds + serves them automatically. No CI/CD workflow needed.


_posts/
  2024-01-15-redux-saga.md   ← becomes /2024/01/15/redux-saga/
_layouts/
  article.html               ← your article template
Pros: Zero CI setup, native GH Pages integration, full SEO (static HTML output), front matter for metadata, Liquid templating

Cons: Tied to Jekyll/Ruby conventions, slower build on large sites, limited plugin set on GH Pages' safe mode

...

Option 4 — Astro
Modern framework designed for content sites. Supports .md/.mdx files natively, has a file-based routing system, and outputs pure static HTML. Also needs GH Actions.

Pros: Best-in-class content authoring (MDX = markdown + components), excellent DX, island architecture for minimal JS

Cons: Most migration effort (your current HTML/CSS needs to be ported into Astro components), overkill if you just want a simple blog
```

"__Overkill__"? yes exactly what I thought. It also presented a table of recommendation:

---
__My recommendation__

|| Build step	| SEO	| Effort |
| --- | ---	| ---	| --- |
|Client-side JS| None	| ✗	| Minimal |
|Jekyll| Auto on GH Pages| ✓	| Low |
|Eleventy| GH Actions	| ✓	| Medium |
|Astro| GH Actions	| ✓	| High |

Jekyll is the pragmatic pick here — it's the only option with zero CI setup (GH Pages runs it natively), outputs real HTML for SEO, and markdown with front matter is exactly what you described. If you later outgrow it, migrating to 11ty or Astro is straightforward since both consume the same .md + front matter format.

---

Since I am happy with the suggestion, Jekyll it is. The final result is what you are viewing right now. Pretty happy with the deliverable.

At the end of this experience, I am left with a few insights:

1. You can prompt them a vague request, and you get back vague answer
2. Provide a lot of context and details on how exactly you want the output to be, then most likely you get what you want (e.g. the layout I was talking about)
3. When in doubts (e.g. not sure what or how you want it to be), you can get them "propose some suggestions" that you can ponder further. Continue asking further clarification questions on those suggestions.
4. They can write codes well, but not necessarily "good code", which depends on what you asked and how much context the model can hold. Hence use them to just write codes. Or in this case, since it is just a portfolio website, I closed my eyes on the generated code, and focus more on the outcome.

I have pretty good feeling about how these whole AI agent evolves so far, and I am fine with the future where I do not have to write codes anymore, but rather focus more on managing and defining the product requirements to build that solves actual problems.

Closing remarks, with regards to the portfolio website, I hope to use this avenue to express my opinions surrounding certain topics more on the internet. First affair is to consolidates all my past writings and projects that were scattered around the internet. After that, I hope to be able to write/publish more contents, so stay tuned!

If you would like to stay in touch with me, feel free to connect with me on LinkedIn, follow my GitHub profile, or just drop me an email message.

Cheers!
