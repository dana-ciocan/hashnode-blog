---
title: "The European Accessibility Act (EAA)"
datePublished: Tue Nov 26 2024 16:13:51 GMT+0000 (Coordinated Universal Time)
cuid: cm3ynpktc000109kzh7n6gi1k
slug: the-european-accessibility-act
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/yCdPU73kGSc/upload/86b4204bc53e373f5ae20bd2f524d5aa.jpeg
tags: web-development, accessibility, a11y, european-accessibility-act-eaa, eaa, accessibility-tooling

---

If you’re working in tech and especially the web side of things, you’ve probably heard of this new accessibility law that is coming into force in 2025. If not, I was curious about it, so I had a bit of a read around it and summarised my findings so you don’t have to.

# What is the EAA?

The European Accessibility Act or EAA is a directive that aims to level the playing field among the different member states of the EU in terms of accessibility. Before the EAA, each member state had their own accessibility laws that were not standardised from country to country. This meant that people with accessibility needs in certain countries were less able to access services than in others. The EAA aims to change that and to make it so everyone across the EU is able to access the services they need.

# When was it passed?

I found it rather interesting that the EAA was actually passed in 2019, but companies were given some time to implement its requirements. The law will start being enforced on the 28th of June 2025, which means companies that do not comply will start facing consequences from that point onwards. This explains why everyone is scrambling to get everything ready now, as it takes a while to audit all digital products and fix all the issues, especially for larger companies with a lot of services.

# Why is it important?

The main reason it’s important is obviously that making content accessible to all humans is a really good thing to do. Not making websites accessible automatically excludes a significant proportion of the population from being able to use your product and that is not okay.

On top of that, there are consequences for those who do not comply. Each member state has the power to determine its own penalties and these can include fines and criminal sentences, so this is serious stuff.

One of the other penalties is that your product could be taken off the market, which would obviously have dire financial consequences as well as causing damage to your reputation.

# Do companies outside the EU have to comply?

If your company is based in a non-EU country (like the UK, where I live) and you have customers in the EU, you will still need to comply. I would say that even if you don’t currently trade with the EU, but plan to in the future, it is worth investing time in making sure you are compliant now so that you don’t have to do it later.

# Is anyone exempt?

If you run a small business (they call it “microenterprises” in the text) with fewer than ten employees or an annual turnover or balance sheet of no greater than two million Euros, you do not have to worry about the EAA. However, it is in your interest to start considering this now so that you are prepared for when your business grows.

All other businesses will have to make sure they comply to the rules set out in the EAA or face some pretty serious penalties, as explained above.

# So, what should you do?

In order to prove that your digital products meet the EAA requirements, they will need to conform with the “[EN 301 549](https://www.deque.com/en-301-549-compliance/)” standard. This in turn requires conformance with WCAG (Web Content Accessibility Guidelines) version 2.1 at AA level - the [WCAG guidelines are available on the W3C website](https://www.w3.org/TR/WCAG21/).

Additionally, you will need to make sure your products meet the four success criteria set out in the WCAG:

* **Perceivable:** information and user interface components must be presentable to users in ways they can perceive
    
* **Operable:** user interface components and navigation must be operable
    
* **Understandable:** information and the operation of the user interface must be understandable
    
* **Robust:** content must be robust enough that it can be interpreted by a wide variety of user agents, including assistive technologies
    

If you have the means, your best option is probably to hire a third party auditor to run an accessibility audit, as they are likely to pick up issues you may miss. It is going to be much less expensive to get someone to tell you what to fix than to wait and face lawsuits, or worse.

If you do not have the means for an external audit, an internal one may be your best option. You will need to find someone who is familiar with accessibility - there are automated tools out there you can use to help (see the next section for tooling info), but these will never pick up every single issue that a human would. The key will be to make sure that all your digital products meet WCAG 2.1 at AA level, as mentioned.

The [gov.uk](http://gov.uk) website has some [excellent guidance on how to run an accessibility audit](https://www.gov.uk/service-manual/helping-people-to-use-your-service/getting-an-accessibility-audit), so it is worth having a look at that if you want more information.

# Some suggested tools

There is a fair bit of accessibility tooling out there that you can use to help make sure that you are compliant and stay that way. Here are some suggestions, though there are plenty more so do have a look around for what best suits your particular situation.

## WAVE

This is a browser extension. It was developed by [WebAIM.org](http://WebAIM.org) and provides visual feedback during development by injecting icons and indicators onto the page.

This tool is available for [Chrome](https://chromewebstore.google.com/detail/wave-evaluation-tool/jbbplnpkjmmeebjpijfedlgcdilocofh), [Firefox](https://addons.mozilla.org/en-GB/firefox/addon/wave-accessibility-tool/) and [Edge](https://microsoftedge.microsoft.com/addons/detail/wave-evaluation-tool/khapceneeednkiopkkbgkibbdoajpkoj).

## AXE devtools

Similar to WAVE, this is a browser extension. It was developed by Deque that will check for accessibility issues during development. This tool adds a tab to your Devtools and displays all accessibility issues inside it.

This tool is available for [Chrome](https://chromewebstore.google.com/detail/axe-devtools-web-accessib/lhdoppojpmngadmnindnejefpokejbdd), [Firefox](https://addons.mozilla.org/en-GB/firefox/addon/axe-devtools/) and [Edge](https://microsoftedge.microsoft.com/addons/detail/axe-devtools-web-access/kcenlimkmjjkdfcaleembgmldmnnlfkn).

## AXE accessibility linter

Deque also make a plugin for IDEs that will check your code for accessibility issues as you type.

You can [download the AXE accessibility linter from the VS Code website](https://marketplace.visualstudio.com/items?itemName=deque-systems.vscode-axe-linter) and there is also a [JetBrains version](https://docs.deque.com/linter/4.0.0/en/axe-linter-jetbrains).

## Pa11y

This tool can be used on the command line to run accessibility tests and is particularly useful for integrating accessibility tests into your build pipelines.

See the [Pa11y website](https://pa11y.org/) for more information.

## Playwright

Playwright, an end to end testing tool created by Microsoft, can also be used to run accessibility tests. If you are already running your end to end tests in Playwright, this may be a good option for you.

See the [Playwright website](https://playwright.dev/docs/accessibility-testing) for more information.

# Final words

Accessibility is incredibly important and it shouldn’t take legal action to force companies to make their products available for users with diverse accessibility needs - we should be building this kind of support into our designs from the very beginning. However, sometimes things slip through the cracks and it’s not always easy to catch every single little issue, so it is vital that we build up tooling and processes around all of this so that we are best placed to support all of our users in the best ways we can.

Doing the research for this article has definitely made me aware of some new tools to try and I hope it’s helped you too. If you know of any other tools or have advice that I haven’t mentioned here, do feel free to leave a comment - I’m always keen to learn!