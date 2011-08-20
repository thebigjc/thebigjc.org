---
layout: post
title: Unlocking Smartphones (or Feature phones) - specifically the Huawei u8100
tags: [unlock, unlocking, smartphones, featurephones, phones, huawei, u8100, 8100, 8105, 8109, dc-unlocker]
---

M is going on a trip to the US this week, and rather than paying the ridiculous roaming charges carriers charge, we thought it made sense to get a US SIM card. M had a Huawei u8100-9 in the house, from a failed experiment of trying out WIND Mobile, and we wanted to see if that could work in the US.

The first step to getting there is to unlock the phone. WIND will actually give you an unlock code for your phone if you call them and ask them for it, but let's be serious. Have you ever called a mobile phone operator and tried to ask anything vaguely technical? Hell - have you ever called them and asked for anything? Depending on your luck, it starts with a pain similar to running fingers down a chalk board, and ends with the constant dripping of water torture as you wait on hold.   

Plus, we're nerds. We can do this shit!

I proceeded to get into research mode, starting at the best source I knew - [Howard Forums](http://www.howardforums.com/). If you ever want to know anything about a carrier, a phone, it's firmware, hacking it, or just anything a good nerd would want to know about wireless service, this is the place to go. The signal to noise ratio is always low, with every from 12 year old kids to their mother trying to skirt the "system", but if you're willing to dig you can find the answer you're looking for.

It looked like there were four option at hand: 

1. Call WIND - we've already ruled that out due to pain factor, and non-nerdy factor
2. Find a local person who does this. Seems like the worse, sketchy version of #1
3. Use one of the many online 'unlock code providers'
4. Use unlocking software

In the interest of minimizing the risk of bricking, I thought I'd give 3 a try first. Finding a provider ended up being the easy part - just put the model of your phone and 'unlock' into Google, and you're in to the dark world of overly-SEOd sites offering services ranging from $2 to $15. The trick was finding one that didn't look like it was going to sell my credit card to the Russian Underground. I opted for picking one of the sites that was actually buying AdWords on my keywords. If they're willing to pay Google to get my traffic, so the theory went, they at least have some skin in the game. (Note that I'm purposely not linking to them here - the reason which will become evident *foreshadowing*)

The experience was pretty simple - enter your phone maker (no drop down?), model, carrier, IMEI, and email. They then take your info, quote you a price, and pass you off to PayPal for payment. As much as people deride PayPal, having gone through the process of getting my money back from eBay auctions gone bad, I know that if these guys are crooks, PayPal will have my back. And a quick read of the [IMEI](http://en.wikipedia.org/wiki/International_Mobile_Equipment_Identity) page on Wikipedia tells me that though they could be stealing it, its use is limited, so I handed over my details and did the PayPal dance.

$8.79 CAD later, I received an email telling me it would take them 12 to 24 hours to get back the unlock code. This seemed sketchy, but I had a bit of time. The next morning a received the following email:

---
Dear Customer

Thank you for you recent order. Please find your updated order details below.

Unlock Status: 

We have been unable to obtain an unlock code for your phone using the imei number supplied. Although this model is generally un-lockable, there are instances where codes cannot be generated. This is due to unique phone variables and cannot be predicted in our preliminary report.
As an apology for this, we would like to offer you a full refund and a free unlock code for your phone as soon as one becomes available on our database. Alternatively you can use this for a different phone.

We would like to offer you a full refund for this and we offer our apologies for the inconvenience. 
Refunds are usually processed within 48 hours, however please allow up to seven days for funds to reflect in your account. 

---

I clearly wasn't happy with the outcome, but at least they were quick getting back to me to tell me they couldn't do it. I know I'll get my $8.79 back from PayPal soon enough, but now it was time for Plan B.

More digging on the forums made tons of mention of the same package - [DC Unlocker](http://www.dc-unlocker.com/). Reading through their site they definitely seemed full featured, as they seemed to support a ton of Smart and Feature phones (I guess this is getting more and more blurry as to what is what, but I digress), including the u8100 and it's myriad variants. 

DC Unlocker uses a system of 'Credits' where by you pay them for units to unlock phones, and their software deducts from your account when it does its thing. It was 10 credits for the u8100, and each credit is 1 Euro, so for about $15 CAD I could unlock the phone. More than my friends above, but it seemed like a more likely result, and there would be no waiting. It would work and cost $15, or it wouldn't and I'd keep my cash. 

I grabbed their software, booted up my Windows VM (thanks Fusion!) and got to work. In DC Unlocker, you select the brand of phone you want to unlock, and tell it to 'detect' the phone. This proved to be the hardest step in the whole process. 

Plugging the phone in gave me a weird dialog asking me if I wanted the phone to be a USB Drive or to use it as a Modem. This was somewhat confusing as the options in DC Unlocker were for Huawei Phones or Huawei Modems. Ignoring the word 'modem', I put the device in to USB mode. The usual Windows XP bubbles started to pop up and the attach/unattach sounds kept beeping away, so I knew something was going on, and the phone eventually said it was in USB mode and ready to go.

I hit the Detect button (the magnifying glass), and crossed my fingers. The software went to work, but reported no phone. Oh oh. I looked back at the forums, and didn't find much help other than suggestions to make sure I had all the drivers installed. I unplugged the phone, plugged it back in, and picked the 'Modem' option this time. This resulted in a much longer series of steps - prompts to install software, and about 4 or 5 driver bubbles, one of which had the magic word 'ADB' in it. 

From my (limited) experience with Android software development, I know that ADB - the Android Debugger - is the key to any Android's heart. Once you have access to ADB, you can make the phone do pretty much what ever you want. At this point, I contemplated saving my $15 and trying to go hard core, but rather than waste my Saturday chasing ghosts, I thought I'd finish this process first, with ADB as a newly found Plan C should I need it.

The software install added a Windows app to use the phone as a tethered Internet device, and started that up. I quit it, went back to DC Unlocker, and hit Detect again. This time we got further - it found a phone! It even knew what kind it was, but then a new error crept on the scene:

'Application port not found'

It seems DC Unlocker needs two serial connections to the device to work - a Diagnostics port (which it found! yay!) and an Application port (which it didn't - boo!). Maybe we're still missing a driver - we have part of the picture, but not all of it? 

DC Unlocker itself offered a hint - for Huawei u8150 and similar models, you need to boot in a special mode by holding down Power, Volume Down, and End Call' when powering on the device. I ignored this initially, as it didn't seem to apply to this phone, but it was the next option in front of me so I gave it a try. The phone booted and froze on the Android screen, but then more Windows XP driver bubbles started to popup. And, with that, another ADB interface. Have we found our solution? 

I went back to DC Unlocker for a third go - hit Detect again, this time it went a step further and told me to was ready to UNLOCK THE PHONE! NICE! 

This is the point where you give DC Unlocker your money and buy the credits from them. Another quick dance with PayPal, handing off $14.62 CAD and creating an account with the DC Unlocker website, and giving their software the account info, and it looked like we were good to go.

I hit the magic 'unlock' button, and it got to work. But success was not to be had - instead the unlock failed, with little info as to why. Given that this method is supposed to be the one used for unlocking the later models, I wasn't too surprised, but wasn't sure what was next. I was considering getting M's PC at this point, thinking maybe VM Ware Fusion was confusing the issue, but before that, wanted to give the process that _nearly_ worked one more go. 

I rebooted the phone into it's normal mode, put it into 'Modem' mode, and hit the detect button. The results were encouraging - it found the device, it found the two serial connections it needed, and it told me the devices IMEI - it was actually talking to the phone! I hit the Unlock button again, and it did it's think. The screen rebooted into a purpley colour, and DC Unlocker was giving me a play by play. It was rebooting the phone into a mode where it could talk to it at a lower level. It said it was unlocking the phone, and the gave me the words I had been waiting for - SUCCESS!

It told me to disconnect the phone, and reboot it, and it was done. In my excitement, I pulled the USB cable, and reached for the power button. Nothing. Blackness. Sorrow. Despair. Did I just brick this phone? ARGH! NOO! But rationality kicked in, and I knew what to do. When phones freeze, pull their battery! I slid the back open, popped the battery out, put it back in, and it booted up. (Phew!). 

It still showed the carrier boot image, so I wasn't sure if it was successful or if I had undone my work here. If rebooting the phone locked it again, that wasn't very useful. I gave DC Unlocker another attempt, and it told me not to bother - my phone was unlocked!

Triumphant, I took the phone up to M, gave it to her, told her the short version of the above, and got my congratulatory hug for a job well done. 

M put another SIM in it, and though we knew the frequency was wrong, it didn't mention anything about being locked or needing an unlock code as it had before. Mission accomplished!

She's hitting the road tomorrow and we'll hit a T-Mobile store before hand to get a SIM with the right frequency. Which involves talking to someone (see above), but at least in this case, we'll be offering them money for their services, which tends to be more successful in these cases.

