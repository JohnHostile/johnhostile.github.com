---
layout: post
title: The state of free email for custom domains - 2016 edition
---
It used to be that you could get Google apps for a personal domain free for up to 10 users. The lowest price for the current Google apps service is $5 per month per user. At that price, I'd say that the Google option is really only a consideration for businesses that are going to use Google products as a part of their workflow (as we do where I currently work). I wanted to be able to supply email addresses to my family, and I didn't want to have to pay a lot just to do so.

After some digging, I found a solution that allows me to keep everything in Gmail, and is almost entirely cost-free. I'm using Mailgun, which is free for up to 10,000 emails (sent and received count the same towards this quota).

The first step is to create a Mailgun account, and go through the steps to verify your domain (by simply adding a few DNS records). I'm going to assume you're savvy enough to get that done.

<img src="/img/mailgun_new_route_01.jpg" class="centered">

At this point, Mailgun is ready to be receive email at any arbitrary address at your custom domain. All it needs are some `route`s to know what to do with the mail that comes in.

<img src="/img/mailgun_new_route_02.jpg" class="centered">

New `route`s look scarier than they are. The `Show Options` buttons will show you the valid options for each field. All you need to do is supply what goes in quotes. In the above example, the custom domain in question is `example.com`. This `route` will take any email that is sent to `name@example.com`, and forwards it directly to `your_personal_email@gmail.com`. The filter expression also accepts Regex, so you can create a catch-all `route` (e.g. `".*@example.com"`), or get really creative. Any email sent to your domain that fails to get routed will bounce.

For sending mail, Mailgun offers an API, and SMTP. If you feel like writing your own email sending app using their API, knock yourself out. I chose to add a `Send mail as` account to my main personal Google account using SMTP. This is the only downside to this system that I can come up with - sending email requires a little bit more technical ability from each user, because it involves SMTP credentials.

<img src="/img/mailgun_smtp_01.jpg" class="centered">

On your domain's admin page on Mailgun (how to get there shown above), you will see that there is a default SMTP login and password. Next to that should be a clickable label that reads `Manage SMTP credentials`.

<img src="/img/mailgun_smtp_02.jpg" class="centered">

Here you can add any accounts that you want to be able to send as. In my case, I added one for me (john@domain.tld), and two more for my brothers. After that,

<img src="/img/mailgun_smtp_03.jpg" class="centered">

Once in gmail, follow Google's instructions for sending from an external address [here](https://support.google.com/mail/answer/22370?hl=en).

After that, you're all set. I hope this was helpful.
