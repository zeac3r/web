---
title: Hacking the photo booths of HamaFilms
published: true
---

In early October, my friend dragged me to a photo booth place called HamaFilms at 272 Lonsdale St, Melbourne VIC 3000 (in the Melbourne CBD) while we were waiting to meet some other friends.

<p style="text-align:center; margin: 1rem 0;">
  <img src="/assets/2025-12-17-hamafilm-photo-booth-hack/image-3.png"
       alt="HamaFilms"
       style="height:50vh; width:auto; display:inline-block;">
</p>

We went in, took some photos, and received physical printouts. After returning to where we were sitting, my friend showed me that you could download the images we took, as well as a video of our session in front of the booth, by scanning the QR code located at the bottom-right corner.

<p style="text-align:center; margin: 1rem 0;">
  <img src="/assets/2025-12-17-hamafilm-photo-booth-hack/image.png"
       alt="HamaFilms"
       style="height:50vh; width:auto; display:inline-block;">
</p>

I took out my phone, scanned the QR code, and it took me to a website that linked to our media. I was greeted with a page like this:

<p style="text-align:center; margin: 1rem 0;">
  <img src="/assets/2025-12-17-hamafilm-photo-booth-hack/image-1.png"
       alt="HamaFilms"
       style="height:50vh; width:auto; display:inline-block;">
</p>

Later that same week, I scanned it again and started to poke around. At the time of writing this (18/12/2025), this vulnerability has not yet been patched. Therefore, I legally cannot disclose its exact nature.

I wrote a script to exploit the vulnerability, and it worked.

<p style="text-align:center; margin: 1rem 0;">
  <img src="/assets/2025-12-17-hamafilm-photo-booth-hack/image-2.png"
       alt="HamaFilms"
       style="height:50vh; width:auto; display:inline-block;">
</p>

I further discovered that I could download both images and videos from sessions of all users from the past 2–3 weeks due to their file retention approach.

I then looked into what “HamaFilms” actually is in order to find an email address to report this issue.

It appears to be a photo booth franchise with booths installed worldwide, including in [Australia](https://hamafilm.com.au/#home), the [USA](http://www.usahamafilm.com/), the [UAE](https://www.burjuman.com/entertainment/virtual-reality/hama-film-x-kono-karaoke), and many other locations. The linked websites all look identical, differing only in their contact information. In Melbourne, they have booths at three locations—two in the CBD and one in Glen Waverley. Their booth at 272 Lonsdale St, Melbourne VIC 3000 is the most popular and has also been featured on [WhatsOnMelbourne](https://whatson.melbourne.vic.gov.au/things-to-do/hama-film-self-photo-studio).

I reported this vulnerability, along with multiple simple fixes that would mitigate the issue entirely, by emailing `info@vibecast.com.au` on 8 October 2025. I did not receive a response. I tested my script once every 2–3 weeks to check whether the issue had been patched, and each time I was left disappointed. Vibecast appears to be the parent company.

In mid-November, I visited the location in person and asked to speak with the manager, but they refused, even after I explained the issue. Instead, they asked me to message them on their Instagram account, which I did as requested. My message was left on seen, with no reply.

After that, I got in touch with [Lorenzo](https://www.linkedin.com/in/lorenzofb/) from [TechCrunch](https://techcrunch.com/) after speaking with [Jason](https://x.com/foilmanhacks). Lorenzo attempted to contact HamaFilms on behalf of TechCrunch. He also reached out to Vibecast’s co-founder, Joel Park, on LinkedIn, but received no response.

In mid-December, I visited all of their branches again, at times when there were customers present, to confirm the continued existence of the vulnerability. It appeared that they had reduced the file retention period from 2–3 weeks to just 24 hours and made cloud storage of images optional. However, neither Lorenzo nor I heard back from them. Most users will likely still choose to upload their media to the server, as this is the only way to access the recorded video.

<p style="text-align:center; margin: 1rem 0;">
  <img src="/assets/2025-12-17-hamafilm-photo-booth-hack/image-4.png"
       alt="HamaFilms"
       style="height:50vh; width:auto; display:inline-block;">
</p>

Changing the file retention policy and making cloud storage optional may have been a response to our report, or it may have been a complete coincidence—we have no way of knowing. Some machines display this screen (shown above), while others do not.

All of these machines are connected to a Canon DSLR, which is responsible for capturing the photos and videos for each session. In the machine shown below, a Canon 2000D was connected and controlled in an automated manner.

<p style="text-align:center; margin: 1rem 0;">
  <img src="/assets/2025-12-17-hamafilm-photo-booth-hack/image-5.png"
       alt="HamaFilms"
       style="height:50vh; width:auto; display:inline-block;">
</p>

However, reducing the file retention period does not fix the vulnerability; it only reduces the attack surface by limiting the number of exposed images.

In Melbourne, this venue is extremely popular among people of all age groups, including underage teenagers.

<p style="text-align:center; margin: 1rem 0;">
  <img src="/assets/2025-12-17-hamafilm-photo-booth-hack/image-6.png"
       alt="HamaFilms"
       style="height:50vh; width:auto; display:inline-block;">
</p>

After confirming all of this, on 12 December 2025, Lorenzo published a TechCrunch article titled ["Flaw in photo booth maker’s website exposes customers’ pictures"](https://techcrunch.com/2025/12/12/flaw-in-photo-booth-makers-website-exposes-customers-pictures/), which details what happened from both of our perspectives.

On 16 December, Danny Bradbury from the Malwarebytes blog published an article referencing this issue—["Photo booth flaw exposes people’s private pictures online"](https://www.malwarebytes.com/blog/news/2025/12/photo-booth-flaw-exposes-peoples-private-pictures-online)—followed by a TechRadar post, ["Talk about a snappy attack – popular photo booth maker allegedly leaves user images at risk"](https://www.techradar.com/pro/security/talk-about-a-snappy-attack-popular-photo-booth-maker-allegedly-leaves-user-images-at-risk).

> "You would expect that such a site would be properly protected, so only you get to see yourself wearing nothing but a feather boa and guzzling from a bottle of Jack Daniels at your mate’s stag do. But reportedly, that wasn’t the case."

> "At first glance, random photo theft might not sound that dangerous. But consider the possibilities. Facial recognition technology is widespread. People at events often wear lanyards with corporate affiliations or name badges. And while you might shrug off an embarrassing photos, it’s a different story if it’s a family shot and your children are in the frame. Those pictures could end up on someone’s hard drive somewhere, with no way to get them back or even know that they’ve been taken." - [Malwarebytes](https://www.malwarebytes.com/blog/news/2025/12/photo-booth-flaw-exposes-peoples-private-pictures-online)

All of this is true, but Malwarebytes has also addressed the elephant in the room: their ethical responsibility to respond. There are many companies, including but not limited to startups, that do not care about cybersecurity at all. They all rely on digital infrastructure—because without it, they would not be able to survive in the modern world—yet they completely overlook the security aspects of it.

The vulnerability that I discovered can be mitigated with a very simple and obvious fix. This not only demonstrates the incompetence of many modern software developers, but also highlights how AI has contributed to the degradation of good coding practices. This has been further evidenced by major vulnerabilities, such as the poorly configured Firebase setup that exposed the PII of users of the Tea app.

When a company—no matter how big or small—is handling user data, it has an ethical responsibility to respond to researchers like myself who report issues of this nature.

The goal here was to have the issue fixed properly on their end so that a bad actor could not abuse this vulnerability. However, due to poor cybersecurity practices, that will not happen.

This is a very serious issue seen across many new startups and small to medium-sized businesses, and it is simply unacceptable.
