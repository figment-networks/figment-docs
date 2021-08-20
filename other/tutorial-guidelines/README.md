---
description: Some do's and dont's on hwo to write a tutorial for Figment Learn
---

# 👀 Tutorial Guidelines

So you've decided to write a tutorial for Figment Learn? We're excited to have you among our contributors! Make sure you read the guidelines below to make sure your contributions follow what other tutorials are doing.

When you are ready to submit it, [**open a PR on Github**](https://github.com/figment-networks/datahub-learn).

## **General**

* **Do not copy and paste existing content**. If the tutorial is inspired by some existing content \(for example forking an ETH tutorial to convert it to Avalanche\), reference it and link to it. When you link to other tutorials/resources, do it with Figment Learn resources as much as possible.
* **Include any potential walkthrough video** in the PR by uploading it to Google Drive
* **Funding of accounts from faucets needs to be explained clearly** as to which account is being funded, from where and why.
* **Display sample outputs** to help learners know what to expect, in the form of Terminal snippets or screenshots. Trim long outputs.
* **Take an error-driven approach** where you bump into errors on purpose to teach learners how to debug them. Eg. If you need to fund an account to be able to deploy a contract, first try and deploy without funding, observe the error that is returned, then fix the error \(by funding the account\) and try again.
* **Add potential errors and troubleshooting.** Of course, the tutorial shouldn't list all potential errors but the main important one.
* **Use React or Vue** for the client-side.
* **Before making the PR run the code by yourself first** to avoid any future unknown errors and to make sure it works as expected. 
* **Provide** pictures/screenshots where needed.
* **Avoid Including external/cross-links** to different sources in between the tutorials. 
* **Image links** need to be in a relative path format: `![](../../../.gitbook/assets/image_filename.png)`

## **Structure**

* The **Title** should be direct and clear, summarizing the tutorial's goal.
* Include an **Introduction** section explaining _why_ this tutorial matters and what the context is. Don't assume this it's obvious.
* Include **Prerequisites**: any prior knowledge needed or existing tutorials that need to be completed first, any tokens needed
* Include **Requirements**: any technology that needs to be installed **prior** to starting the tutorial and that the tutorial will not cover \(`Metamask`, `node`, `truffle`, etc\). Do not list packages that will be installed in the tutorial \(`dotenv`\).
* Include a **Conclusion** section that summarizes what was learned, reinforces key points and also congratulates the learner.
* \(Optional\) Include a **What's Next** section pointing to good follow up tutorials or other resources \(projects, articles, etc\)
* \(Optional\) Include an **About The** **Author** section at the end. Your bio should include your Github handle \(which will have your name, website, etc\) and a link to your [Figment Forum](https://community.figment.io) profile \(so users can contact/tag you on Forum for help and questions\).
* **References** section must be present if you have taken any help in writing this tutorial from other documents, GitHub repos and other tutorials. Credit sources by adding their name and a link to the document when possible \(if it is not a digital document, include an ISBN or other means of reference\).

## **Style**

* **Explain your code.** Don't just ask learners to blindly copy and paste
  * Function names, variables and constants must be consistent across the entire document.
  * Use of UI tabs to indicate a relative path & filename \[as in Polkadot tutorials\] \(?\) - similarly, use a UI tab to indicate a block of expected terminal output
* **Use a linter & prettifier** before submitting your code. We recommend `eslint` for Javascript/React.
* **Use Markdown properly** throughout the tutorial. You can refer to Gitbook's markdown guide [here](https://gitbookio.gitbooks.io/documentation/content/format/markdown.html).
* **Select the appropriate language** for code blocks' syntax highlighting
* **The code blocks should be well commented**. Comments should be short \(usually two or three lines max at a time\) and effective. If you more space to explain a piece of code, do it outside the code block.
* **Writing Tone -** Learn Tutorials are written by community contributors for their peers. As such, we recommend creating a tone of inclusion and interaction throughout the tutorial. Use words like “we”, “us”, “our”, like “We have successfully deployed our contract”. When providing direct instructions feel free to use “you”, “your” etc. like _“Your file should look like this”_.

## **App setup**

* Create a folder to hold all the code \(eg. `mkdir example && cd example`\)
* If you use `npm init` explain the prompts or use the `-y` flag
* If you use `npm install` use the `--save` flag
* If you mention `.env` and `.gitignore` during the tutorial setup, you can reference the Guides [document](https://learn.figment.io/network-documentation/extra-guides/dotenv-and-.env) we wrote on this.

## Sample Tutorial

**Please check Sample Tutorial Structure on the next page** 📑

{% page-ref page="sample-tutorial-structure.md" %}



