---
layout: default
title:  "Talk-Talk (2015 Data Breach)"
description: "My views about the amazing Talk-Talk data breach of 2015"
author: "0x5ubt13"
date:   2020-11-10 16:00:00 +0000
categories: Blog
---

November 10th, 2020 - Blog post.
Last edited: November 19th, 2020.

# TalkTalk (2015 Data Breach)

 

## Table of contents:
1. <a href="https://0x5ubt13.github.io/blog/2020/11/10/Talk-Talk-(2015-Data-Breach).html#keys">Key Takeaways</a>
2. <a href="https://0x5ubt13.github.io/blog/2020/11/10/Talk-Talk-(2015-Data-Breach).html#what">What happened?</a>
3. <a href="https://0x5ubt13.github.io/blog/2020/11/10/Talk-Talk-(2015-Data-Breach).html#how">How did it happen?</a>
4. <a href="https://0x5ubt13.github.io/blog/2020/11/10/Talk-Talk-(2015-Data-Breach).html#why">Why did it happen?</a>
5. <a href="https://0x5ubt13.github.io/blog/2020/11/10/Talk-Talk-(2015-Data-Breach).html#refs">References</a>


 

## <a id="keys"></a> Key Takeaways:

| Title     |                                  Feature                                                       |
|:------------------------------------------|:-----------------------------------------------------------------                                    |
| CEO                                      | [Dido Harding](https://en.wikipedia.org/wiki/Dido_Harding)                                           |
| Number of customers affected        | 157,000                                                                                              |
| Number of non-notified customers         | 4,545                                                                                                |
| Type of personal information leaked      | Full names, addresses, email addresses, DoB, phone numbers, customer numbers and bank details        |
| Type of breach                           | SQL injection                                                                                        |
| Number of encrypted credit cards taken  | 90,000                                                                                               |
| Number of attacks                        | 14,000 attacks over Oct 2015                                                                         |
| ICO fine                                | £400,000                                                                                             |


 
 

## <a id="what"></a> What happened?

In 2003, a big UK company called Carphone Warehouse that used to sell phones but wasn't affiliated to any specific mobile provider, decided to broaden their game surface and created a mobile carrier called __TalkTalk__. Being able to sell you both the phone *and* the subscription plan for the phone service, they started growing exponentially.

In 2009, they decided to buy for [£236 million](https://www.itpro.co.uk/610777/carphone-warehouse-buys-tiscali-for-236-million) a competing an Italian mobile carrier operating in the UK under the branch Tiscali UK, so they absorbed the entirety of their network in the country. This made TalkTalk merge into their systems all the infrastructure Tiscali owned, leading afterwards to some consequences we'll review shortly. 

7 years after creating the mobile carrier, in 2010 Carphone Warehouse [decided to separate from TalkTalk](https://www.computerweekly.com/microscope/news/2240154193/Carphone-Warehouse-completes-TalkTalk-split), with TalkTalk holding about 60% of the old firm.

To cope with the huge demand, TalkTalk outsourced their customer support services to a company in Kolkata called Webpro, so that they were able to ramp their staff in just 6 months to over 1,000. 

Three rogue employees at Webpro gained access to privileged logins that had permissions to view more than one TalkTalk customer account at a time. They began harvesting customer accounts out of the database of the company, 500 at a time without being detected. The exfiltrated data included the name, home address, phone number and account number of the customer. Then, the rogue employees would put all these customer records in hands of phone scammers to try and trick the customers to pay, allegedly, back to TalkTalk.

In August 2015, 3 Carphone Warehouse's websites go offline: onestopphoneshop.com, etosave.com, and mobiles.co.uk. The next day, the company sends a letter to their customer saying:

> “Our investigation indicates that some of the data held in our systems has been accessed and this may include some of your personal details including your name, address, date of birth, and bank details. We take the security of your data extremely seriously and we have put in place additional security measures to prevent further attacks. Nevertheless, we felt it was important to let you know as soon as possible. To reduce the risk of fraudulent activity, we recommend you consider taking the following steps: notifying your bank and credit card company so they can monitor activity on your account. You can check your credit rating and make sure no one has taken a loan out and credit in your name.  You can do this by visiting Experian or Equifax.”

They then said 2.5 million customer records were taken from their database. 90,000 encrypted credit cards were taken. Since TalkTalk and Carphone Warehouse were still in the process of de-merging, out of the 2.5 million customer stolen records, 480,000 of them belonged to TalkTalk, so they had to inform the ICO again.

In 2016, the three rogue employees of Webpro were arrested for stealing the customer records off of the TalkTalk database.

 
 
## <a id="how"></a> How did it happen?
A normal employee at Webpro could only see the data of the customer they were speaking to, but a privileged employee could see 500 records at a time by doing a lookup using the * wildcard. For example, typing the letter A followed by the wildcard * would give them the records of the first 500 customers their name began with A.

When they merged Tiscali UK with TalkTalk, the Tiscali website remained open for 3 years being absolutely disregarded. A SQL injection vulnerability was found to be there, with access to the TalkTalk customers records. [A SQL injection attack, #1 in Owasp's top 10 vulnerabilities](https://owasp.org/www-project-top-ten/2017/A1_2017-Injection), happens when a regular user can make hostile calls to the interpreter of the backend server.

Then with all the customer records, a scammer can use [social engineering skills](https://us.norton.com/internetsecurity-emerging-threats-what-is-social-engineering.html#:~:text=Social%20engineering%20is%20the%20act,natural%20tendencies%20and%20emotional%20reactions.) to trick a victim into thinking they are legitimate employees of the company and then they can request a payment to repay an amount of money that hadn't been correctly assigned to their bills at the time of calculating them.

 

## <a id="why"></a> Why did it happen?
A lot of people is still in 2020 unaware of all the potential risks they suffer if they get their identity stolen. If we are at this stage yet, imagine back in 2014. Scammers were able to trick a lot of people. For them, this was easy money.

In the world today, there still exists a big vector of attack for this kind of people to exploit. We have to educate people about data security and how it affects our lives. 

 

### <a id="refs"></a> References:

Jack Rhysider, 15 Oct 2017. Darknet Diaries - "Ep 4: Panic! at the TalkTalk Board Room" [Online] \
Available at: [https://darknetdiaries.com/episode/4/](https://darknetdiaries.com/episode/4/) \
[Last accessed Nov 19th, 2020]  

Warwick Ashford, 22 May 2019. Computer Weekly - "TalkTalk admits new failings in 2015 data breach notification" [Online] \
Available at: [https://www.computerweekly.com/news/252463792/TalkTalk-admits-new-failings-in-2015-data-breach-notification](https://www.computerweekly.com/news/252463792/TalkTalk-admits-new-failings-in-2015-data-breach-notification) \
[Last accessed Nov 19th, 2020]  

Stuart Turton, 05 Jun 2009. ITPro. - "Carphone Warehouse to spin off TalkTalk by 2010" [Online] \
Available at: [https://www.itpro.co.uk/611404/carphone-warehouse-to-spin-off-talktalk-by-2010](https://www.itpro.co.uk/611404/carphone-warehouse-to-spin-off-talktalk-by-2010) \
[Last accessed Nov 19th, 2020]

Alex Scroxton, 29 Mar 2010. Computer Weekly - "Carphone Warehouse completes TalkTalk split" [Online] \
Available at: [https://www.computerweekly.com/microscope/news/2240154193/Carphone-Warehouse-completes-TalkTalk-split](https://www.computerweekly.com/microscope/news/2240154193/Carphone-Warehouse-completes-TalkTalk-split) \
[Last accesed Nov 19th, 2020]

Anon, 2017. OWASP Top Ten 2017 - "Injection" [Online] \
Available at: [https://owasp.org/www-project-top-ten/2017/A1_2017-Injection](https://owasp.org/www-project-top-ten/2017/A1_2017-Injection) \
[Last accessed Nov 19th, 2020] 

Steve Symanovich. NortonLifeLock - "What is social engineering? Tips to help avoid becoming a victim" [Online] \
Available at: [https://us.norton.com/internetsecurity-emerging-threats-what-is-social-engineering.html#:~:text=Social%20engineering%20is%20the%20act,natural%20tendencies%20and%20emotional%20reactions.](https://us.norton.com/internetsecurity-emerging-threats-what-is-social-engineering.html#:~:text=Social%20engineering%20is%20the%20act,natural%20tendencies%20and%20emotional%20reactions.) \
[Last accessed Nov 19th, 2020] 