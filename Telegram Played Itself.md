# How Telegram played itself

Pavel Durov’s arrest over the weekend was shocking. It was also inevitable

---

By Casey Newton
Aug 27, 2024 12:35 AM
6 min. read
View original

---

By now you’ve surely heard that Telegram founder Pavel Durov is in French custody. On Saturday, [the Russia-born billionaire was arrested](https://www.reuters.com/world/europe/telegram-messaging-app-ceo-pavel-durov-arrested-france-tf1-tv-says-2024-08-24/?ref=platformer.news) after landing in a private plane at Le Bourget airport outside Paris. Durov is now being questioned as part of a wide-ranging investigation into criminal activity on the platform, and under French law can be held until at least Wednesday. If he is charged with a crime, though, he could be detained much longer. 

I’ve spent the past few days talking with sources who work on and study tech policy and international law, along with those who are fighting the spread of child sexual abuse material (CSAM) on digital platforms. Today let’s try to answer three big questions from the arrest: Why was Durov arrested? Why is Telegram under investigation? And what does France’s move here portend for platforms more generally? 

Many important details about the case remain secret, and most sources I spoke with declined to comment on the charges before evidence is made public.

But to anyone who has followed Telegram’s story over the past few years, the events of the past few days have appeared to be increasingly unavoidable.  

1. **Why was Durov arrested?**

On Monday, Laure Beccuau, a prosecutor in Paris, [issued a statement](https://www.tribunal-de-paris.justice.fr/sites/default/files/2024-08/2024-08-26%20-%20CP%20TELEGRAM%20.pdf?ref=platformer.news) saying that Durov had been arrested as part of an investigation that had begun on July 8 against an unnamed person on a dozen potential charges, including complicity in spreading CSAM, complicity in spreading drugs, money laundering, and refusing to cooperate with law enforcement. It also suggests that Telegram improperly used cryptography. 

Notably, these charges do not appear to stem from the European Union’s recently passed Digital Services Act, as some had speculated. Rather, they seem to be based on French law.

It’s unclear who that person under investigation is. But it would be strange if any investigation into how Telegram enables cybercrime did not center on the company’s CEO. 

Durov, who holds French citizenship, has long championed user privacy; he says he fled Russia after refusing to turn over user data from his previous company, the Facebook clone VKontakte, to the country’s security services. At the same time, Telegram’s aversion to content moderation has been hugely lucrative for the company and for Durov personally. Durov is a billionaire and Telegram is said to be nearing profitability on hundreds of millions of dollars in revenue; meanwhile, he [bragged to the _Financial Times_ earlier this year](https://www.ft.com/content/8d6ceb0d-4cdb-4165-bdfa-4b95b3e07b2a?ref=platformer.news) that each user only cost him 70 cents a year to support.

Ramping up the teams necessary to respond to law enforcement requests, disrupt networks of CSAM traders and other criminals, and address other content moderation needs would eat into Durov’s profit margin — and potentially disrupt his planned initial public offering. 

That hasn’t stopped him from becoming an overnight free speech martyr on some corners of the internet, particularly among the richest cohort of X users. And indeed, it _is_ startling to see the CEO of a social platform being arrested in any context, particularly when the arrest may be connected to content posted by the platform’s users rather than the CEO himself.

“Telegram abides by EU laws,” the company posted on X. “Its moderation is within industry standards and constantly improving.  Telegram's CEO Pavel Durov has nothing to hide and travels frequently in Europe. It is absurd to claim that a platform or its owner are responsible for abuse of that platform. … We're awaiting a prompt resolution of this situation.”

But saying that Telegram’s moderation is “within industry standards” seems obviously false. In some important ways, Telegram stands alone among its peers.

Daphne Keller, an expert on platform legal liability at the Stanford Cyber Policy Center, noted that there is a history of prosecuting platform owners when they host criminal activity.

"I am usually one of the people making noise about free expression consequences when lawmakers go overboard regulating platforms," Keller [wrote on LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7233889294673657857/?ref=platformer.news). "Possibly this will turn out to be one of those cases. But so far, I don't think so."

2.  **Why is Telegram under scrutiny?**

Launched in 2013, Telegram is a messaging app that boasts more than 900 million users. Over time, it has added more public content and other features familiar from social networks. For example, some of its public “channels” have millions of followers, all of whom can repost content from those channels to their own group chats.

Officially, Telegram’s [terms of service](https://telegram.org/tos?ref=platformer.news) prohibit users from posting illegal pornographic content or promotions of violence on public channels. But as the Stanford Internet Observatory noted last year [in an analysis of how CSAM spreads online](https://cyber.fsi.stanford.edu/io/news/addressing-distribution-illicit-sexual-content-minors-online?ref=platformer.news), these terms implicitly permit users who share CSAM in private channels as much as they want to.

“There's illegal content on Telegram. How do I take it down?” asks a question on Telegram’s [FAQ page](https://telegram.org/faq?ref=platformer.news#q-what-are-your-thoughts-on-internet-privacy). The company declares that it will not intervene in any circumstances: “All Telegram chats and group chats are private amongst their participants,” it states. “We do not process any requests related to them."

Telegram is often described as an “encrypted” messenger. But as Ben Thompson [explains today](https://stratechery.com/2024/telegram-ceo-arrested-telegrams-non-encrypted-advantage-telegram-complexities/?ref=platformer.news), Telegram is not end-to-end encrypted, as rivals WhatsApp and Signal are. (Its “secret chat” feature _is_ end-to-end encrypted, but it is not enabled on chats by default. The vast majority of chats on Telegram are not secret chats.) That means Telegram can look at the contents of private messages, making it vulnerable to law enforcement requests for that data.

Anticipating these requests, Telegram created a kind of jurisdictional obstacle course for law enforcement that (it says) none of them have successfully navigated so far. From the FAQ again:

> To protect the data that is not covered by end-to-end encryption, Telegram uses a distributed infrastructure. Cloud chat data is stored in multiple data centers around the globe that are controlled by different legal entities spread across different jurisdictions. The relevant decryption keys are split into parts and are never kept in the same place as the data they protect. As a result, several court orders from different jurisdictions are required to force us to give up any data. […] To this day, we have disclosed 0 bytes of user data to third parties, including governments.

As a result, investigation after investigation finds that Telegram is a significant vector for the spread of CSAM. (To take only the most recent example, [here’s one from India’s _Decode_ last month](https://www.boomlive.in/decode/csam-investigation-child-sexual-abuse-material-social-media-instagram-telegram-india-paedophiles-selling-videos-25848?ref=platformer.news), which like others found that criminals often advertise their wares on Instagram and direct buyers to Telegram to complete their purchases.) 

The French investigation appears to have a wide scope, including an apparent focus on Telegram’s use of encryption that bears close scrutiny. (Encryption has been [under global assault](https://www.platformer.news/inside-facebooks-encryption-conundrum/) since I began writing this newsletter.) At the moment, it’s unclear what crimes will be alleged, and which will have evidence to support them. It’s entirely possible that French prosecutors could overreach.

At the same time, child safety advocates have been begging authorities to do something about Telegram for years now. The company’s refusal to answer almost any law enforcement request, no matter how dire, has enabled some truly vile behavior.

“Telegram is another level,” Brian Fishman, Meta’s former anti-terrorism chief, wrote in [a post on Threads](https://www.threads.net/@brian.fishman.5/post/C_Gjo7lSoyh?ref=platformer.news). “It has been the key hub for ISIS for a decade. It tolerates CSAM. Its ignored reasonable [law enforcement] engagement for YEARS. It’s not ‘light’ content moderation; it’s a different approach entirely.

3. **What does Durov’s arrest mean for other platforms?**

We don’t know quite yet.

On one hand, platforms have faced increasing pressure [for years now](https://www.platformer.news/a-rough-year-for-internet-freedom/) to crack down on speech globally and cooperate more with law enforcement agencies — including by breaking end-to-end encryption. Building platforms responsibly means reaching compromises with law enforcement agencies that allow for the investigation of serious crimes while protecting users’ privacy to the greatest extent possible. It’s a difficult, expensive dance, and when it’s working right neither the platforms or the law enforcement agencies are satisfied with the outcome.

A worrisome outcome of France’s ultimate prosecution of Telegram, assuming there is one, is that it will embolden countries around the world to prosecute platform CEOs criminally for failing to turn over user data. We have already come worryingly close to this reality, and I have covered it closely here over the years. [India](https://www.platformer.news/twitter-struggles-in-india/) and [Russia](https://www.platformer.news/apple-and-google-bow-to-russia/) were among the first countries to use so-called “hostage-taking laws” to threaten platform employees with jail over content moderation decisions, but many more have followed since. 

On the other hand, Telegram really does seem to be actively enabling a staggering amount of abuse. And while it’s disturbing to see state power used indiscriminately to snoop on private conversations, it’s equally disturbing to see a private company declare itself to be above the law.

Given its behavior, a legal intervention into Telegram’s business practices was inevitable. But the end of private conversation, and end-to-end encryption, need not be. Fending off onerous speech regulations and overzealous prosecutors requires that platform builders act responsibly. Telegram never even pretended to.
([Link](https://bsky.app/profile/themountaingoats.bsky.social/post/3l2ls4q4xxd27?ref=platformer.news))