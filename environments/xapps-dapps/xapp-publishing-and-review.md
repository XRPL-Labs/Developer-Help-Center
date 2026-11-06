---
description: >-
  What we require, what we expect, and what happens before and after your xApp
  goes live in Xaman
---

# xApp publishing and review

Anyone can build an xApp. While you build it, your xApp is sandboxed: only you and your testers can open it. To make it available to other Xaman users, it needs to pass our review process.

We set a high bar. We only approve xApps that add value for a significant share of Xaman users, are built specifically for Xaman, and keep users safe.

{% hint style="info" %}
**Test your xApp against both checklists below before you request a review.** With the growing number of xApps being built, many with the help of AI tools, we can only review finished xApps. We can't review them step by step during development.
{% endhint %}

#### Sandboxed, approved, and listed

An xApp can be in one of three states:

* **Sandboxed:** only you and up to 10 testers can open it. You add testers by their Device ID in the Xaman Developer Console.
* **Approved:** your xApp has passed review and gets a public link. You can share the link, and any Xaman user can open it. An approved xApp isn't listed in Xaman's xApp list.
* **Listed:** your xApp appears in Xaman for everyone to find.&#x20;

#### Required: what every xApp must do

Each item below is a yes or no. If your xApp doesn't meet any one of them, we'll send it back to you.

**You and your project**

* **You've completed KYC.** See [How to verify your identity (KYC)](https://help.xaman.app/app/learning-more-about-xaman/kyc).
* **You're not anonymous.** We need to know the person or company behind the xApp.
* **Your source code is public.** Provide a public GitHub link for your xApp, and for its backend if it has one.
* Working links to **Support**, a **Privacy Policy**, and **Terms & Conditions**, easy to find inside the xApp.
* A support channel that actually responds, and a clear way for users to reach you, including on social media.

**Clearly independent**

* Your xApp makes clear that it's developed by you, and isn't affiliated with XRPL Labs or Xaman.

**Xaman sign-in**

* No "Login with Xaman", "Connect Xaman", or "Disconnect Xaman" flows.
* Use the user and account details Xaman already provides through the xApp OTT. See [Authorization & Credentials](https://docs.xaman.dev/concepts/authorization.md).
* Never ask users to connect or reconnect Xaman.

**Signing and security**

* **Never ask for an account secret** (Secret Numbers, Family Seed, Mnemonic) or private keys, in any form.
* Signing requests only appear when the user chooses to start them. A request that opens on its own, when the xApp loads, or as a side effect of another button will fail the review.
* Before each signing request, explain in plain language what the user is signing and why.
* Show any fees up front, including fees your xApp or a third party charges.
* Name every third-party service the xApp uses.
* **No account-governance transactions.** Your xApp can't ask users to sign SetRegularKey or SignerListSet transactions. There are no exceptions.
* Show a clear warning before any other high-risk transaction, such as deleting an account (AccountDelete) or anything else that can't be undone.
* If your xApp has a backend, it's secure, and you can tell us how and where it's hosted.

{% hint style="warning" %}
**Changes to who can sign for an account must always be made by the account owner, never through an xApp.** Transactions that change an account's signing authority are the most common route for phishing and account takeovers. If an xApp asking for them were ever misused or compromised, users could lose their accounts completely, however trustworthy the developer.
{% endhint %}

**App store rules and speculation**

* Your xApp doesn't break Apple App Store or Google Play rules. For example, it can't unlock features based on NFTs the user owns.
* Your xApp doesn't promote speculation or push users towards buying tokens.

**Styling**

* The `<html>` and `<body>` tags have a transparent background as soon as the page loads, so your xApp doesn't flash white while it loads.
* Your xApp either has its own colour scheme that works in every Xaman theme, or follows Xaman's themes (Light, Dark, Moonlight, and Royal). Xaman passes the active theme in the `xAppStyle` query parameter. See the [xApp style guide](https://docs.xaman.dev/environments/xapps-dapps/style-guide).
* **Technical**
  * Your xApp meets the [technical requirements](https://docs.xaman.dev/environments/xapps-dapps/requirements), including opening external links with `openBrowser`, storing user data with `userstore`, and not polling for payload status.

**Works on every phone**

* Works on both iOS and Android.
* Tested at a screen width of 360 px, with nothing cut off, overlapping, hidden behind the keyboard, or needing horizontal scrolling.
* Body text is at least 16 px.
* Buttons and other touch controls have a touch area of at least 40 × 40 px.
* Scrolling and zooming behave as expected. Prevent page zooming where it would break the layout.

**Finished**

* No broken links, placeholder text, test content, or unfinished screens.
* Tested for bugs, by you and your testers.

#### Expected: what we look for

These are the qualities we assess across your xApp as a whole.

**Value for many Xaman users**

Your xApp should add value for a significant share of Xaman users. An xApp that's only useful to a small group is unlikely to be approved.

**Built for Xaman**

Your xApp should feel like part of Xaman, not a website opened inside it.

* Mobile-first design, with simple, consistent navigation.
* No desktop menus, cookie banners, oversized footers, or other website elements it doesn't need.
* It's fine to have a website for your project. The xApp itself should be designed for use inside Xaman, not a copy of your site.
* If your xApp has no real interaction with Xaman or the XRP Ledger, it should be a website, not an xApp.

**Clear and simple**

* It's obvious straight away what your xApp does.
* Clear instructions, so users know what to expect at every step.
* Simple workflows, with clear buttons, labels, and confirmations.
* Designed so users can't make dangerous mistakes.

**Polished**

* A professional, consistent design, with consistent fonts.
* Smooth, responsive performance.

**Careful with data**

* Collect only the user data your xApp needs, and explain it in your Privacy Policy.
* Say so if your xApp uses third-party analytics or tracking.

#### How to request a review

Request a review by creating a ticket in the [Xaman Support xApp](https://xaman.app/detect/xapp:xumm.support-md). Tap the link on the phone where Xaman is installed.

Include:

* **What your xApp does,** in one or two sentences, and who it's for.
* **Its title, description, and app icon.**
* **Public GitHub links** to your xApp, and to its backend if it has one.
* **Who's releasing it:** your personal details, or your company's details.
* **Your KYC-verified account,** and the XRP Ledger addresses your xApp uses.
* **Any tokens it uses,** whether yours or someone else's, and which ones.
* **How it makes money,** if it does.
* **Every transaction type** it asks users to sign, and why.
* **Any third-party services** it uses.
* **Its backend,** if it has one: how it's secured, and where it's hosted.
* **Any fees** your xApp charges.
* **How long you've tested it,** and with how many testers.
* **Your support contacts.**
* **Testnet access,** if your xApp supports it, so we can test signing without real funds.
* **Confirmation** that you've checked your xApp against both the Required and Expected lists, and that you agree we can revoke your xApp at any time, even after it's approved.

#### What happens next

Your xApp is reviewed in stages, by different people on our team:

1. **Initial review:** your project details, the Support, Privacy Policy and Terms links, and basic functionality.
2. **Technical and functional review:** your source code, how the xApp works, and its transactions, signing, and security.
3. **Overall review:** your xApp as a whole. We use it as a user would, check it against the Expected list, make sure it does what it says, and look at the project behind it, including how it makes money and any tokens it involves.
4. **Final sign-off:** your xApp gets its public link.

At any stage, the outcome is one of:

* **Approved:** your xApp moves to the next stage, or gets its public link after the final sign-off.
* **Changes needed:** we'll tell you which items in the Required or Expected lists your xApp doesn't meet. Fix them, test your xApp against both lists again, and resubmit. Every resubmission starts again from the initial review.
* **Not approved:** your xApp can't be approved as it is, for example because it doesn't add enough value, is built around speculation, or misleads users. We'll tell you why.

**Number of rounds.** If your xApp still needs changes after 3 rounds, we'll close your submission.

**Submitting again.** Whether your submission was closed or not approved, you can submit again after 3 months, with 3 new rounds. If your xApp wasn't approved because of its idea or design, your new submission must be substantially different. If it was misleading or malicious, you can't reapply, and this can affect any other xApps you've built.

**Disagree with a decision?** Reply to your Support ticket explaining why. Someone who wasn't involved in the original review will take a second look. Their decision is final.

**How long does a review take?**

We'll confirm we've received your request within 1 working day. A full review usually takes 1 to 2 weeks, and can take longer when we receive many requests, or when your xApp needs closer checks.

Every resubmission and every change goes back into the queue, so the best way to get approved quickly is to test your xApp thoroughly against both checklists before you submit it. Please don't send follow-up messages asking for updates: they don't speed up your review.

#### Every change is reviewed

Approval covers the version of your xApp we reviewed. **Every change, however small, needs a new review before it goes live.** This includes bug fixes, design changes, new features, new transaction types, new third-party services, new fees, and a change in who owns or runs the xApp.

To request a review of a change, reply to your original Support ticket in the [Xaman Support xApp](https://xaman.app/detect/xapp:xumm.support-md) with a short changelog describing what you changed.

We also re-review all xApps after each new Xaman release.

{% hint style="warning" %}
**Publishing changes that we haven't reviewed will get your xApp removed.**
{% endhint %}

#### When we remove an xApp

XRPL Labs can revoke any xApp, approved or listed, at any time and without prior notice, when we need to protect our users. Reasons include, but aren't limited to:

* Potential harm to users, or putting their funds at risk.
* Misleading users, or behaving differently from what we reviewed.
* Changes published without review.
* Lack of customer support.
* Lack of updates or maintenance.
* Promoting speculation, such as pushing users towards buying tokens.
* Involvement in criminal activity, or behavior that harms the XRP Ledger community.
* Licensing problems or infringements.

#### What helps get your xApp listed

Users can see a listing as an endorsement from us, so we're selective about which xApps we list. Most developers have good intentions, though we occasionally come across xApps that are misleading, unsafe, or malicious.

New projects usually stay unlisted for a while, even after they're approved. This gives us, and the wider community, time to get to know the project and its developers, and to see how it's developed, maintained, and supported over time.

Beyond the requirements above, these help:

* **A registered business** in your country.
* **Taking part** in the XRP Ledger ecosystem and community.
* **A transparent public presence:** a website, social media channels, and support contacts people can reach.
* **A track record** of development, maintenance, and user support.

None of these guarantees a listing. Listing decisions are based on the project's maturity, credibility, security, and value to the XRP Ledger ecosystem.

#### Frequently asked questions

**Can you review my xApp while I'm still building it?**

No. We review finished xApps only. Test against both checklists yourself, and request a review once you're confident it's ready.

**Who can use my xApp before it's approved?**

Only you and up to 10 testers, added by their Device ID in the Xaman Developer Console.

**My xApp was approved. Why isn't it listed?**

Listing is a separate decision. New projects usually stay unlisted for a while, even after approval, while we get to know the project over time.

**Do small fixes need a review?**

Yes. Every change needs a review before it goes live, however small.

**Does my source code really have to be public?**

Yes. Public source code lets us, and anyone else, check what your xApp actually does.

**Can my xApp ask users to set a regular key or a signer list?**

No. xApps can't request SetRegularKey or SignerListSet transactions, without exception. These transactions change who controls an account, so account owners must make these changes themselves, directly. If your xApp's workflow depends on them, you'll need to change its design before you request a review.

#### Questions?

If you have questions, please create a Support ticket in the [Xaman Support xApp](https://xaman.app/detect/xapp:xumm.support-md).

