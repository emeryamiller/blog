---
title: Know the limits of OpenDNS and Google when protecting your loved ones on the internet
date: 2013-12-08 16:55 UTC
tags: opendns google protect online
---
# Know the limits of OpenDNS and Google when protecting your loved ones on the internet
<time pubdate="2013-12-08">8 Dec 2013</time>
<address>Emery A. Miller</address>

## TL,DR
- [OpenDNS](http://www.opendns.com) cannot protect you from the pornographic images Google caches on it's site
- Shockingly, this is Google's default behaviour
- Google's SafeSearch mechanism is easy to get around
- Another key issue is that [OpenDNS](http://www.opendns.com) relies on DNS resolution, meaning that it is easy to circumvent by setting an alternate DNS ip address on your devices DNS settings, or by simply using an IP addresses
- In the end, education is the best way to protect your family

## Motivation

As a father of two young boys who are begining to use the internet, I want to protect them from explicit and inappropriate content. In today's environment, the protection must work on:

- different types of devices,
- possibly different operating systems (iOS, Mac, Linux, Android, Windows),
- many different browsers that can be found on those devices

It should also be non-trivial to bypass the protection. *[OpenDNS](http://www.opendns.com)* has been my goto tool for the past two years. It meets these requirements quite well:

- It is installed by configuring your router. This is easy, and means that it impacts all devices on your home network regardless of what operating system, or browser they run,
- it has a simple interface where you can specify what kinds of websites to block,
- you can customize the categories of content that should be blocked (pornography, hate sites, weapons sites, and so forth)
- and can either allow or block specific sites by specifying their name (like www.bbc.com).
On the whole, I have been very happy with this service. But recently I bumped into an issue in the form of *Google Images*.

## Google Images breaks OpenDNS

Simply put, Google caches pornographic images on it's servers. This means that if you search for anything that could bring up explicit images in Google and click the Images button, you get all sorts of explicit content. This was shocking to say the least, especially as it's the default behaviour.

Google provides a safe search option to help prevent this, which has three levels of security:
1. Safe search option to block explicit content
2. Safe search lock to prevent others from changing the setting without your password
3. Safe search by having your router add a query string to the end of all searches sent to google. This last one requires some skill to setup, and I don't think a typical home router is capable of doing it.

The issue with measures 1 and 2 above are that they are very easy to bypass. With option 1, you can simply log out of the account. Option 2 prevents this unless you type in the account password, but that only works if your cookie is still set.  Which means bypassing it is as simple as clearing the cookies in your browser or worse yet, by using a different browser.

I felt it was time to use OpenDNS to block `google.com` and use a service like [Duck Duck Go](http://www.duckduckgo.com) to search the web. Alas, it isn't that simple.

### Other sites like Google

It turns out that Google isn't the only site that bypasses [OpenDNS](http://www.opendns.com) be serving both explicit and normal content. Reddit, Tumblr, and photo sharing sites like Imgur, also create gaps. While much of their content is not explicit, these sites also have portions dedicated to pornography. So blocking content from these sites is getting harder as I'm not clear where you'd get a list of sites like these. OpenDNS does have a category for photo sharing sites, but that is a bit broad as it includes sites like Flickr, which are fine (as far as I can tell).

## What does "protecting" mean?

There are two types of protection that are relevant here. The first is protecting your family from inadvertently finding explicit content. OpenDNS is excellent for this, though as we've discovered, Google images makes this much harder since now we need to activate safe search across all browsers on all our devices.

However, protecting your family can also mean preventing them from accessing explicit sites even when they are actively searching for them. I remember my young adult years, and if I had been a google search away from any explicit content I wanted at the age of 12... well I can't imagine my parents would have been happy. This is where Google safe search falls flat, and sadly where OpenDNS falls flat too.

## Bypassing DNS on a Device

I recently also became aware that on an iPhone or iPad, the network settings for a given internet connection have editable DNS settings. ![iDevice DNS Settings](/images/idevice_dns_settings.jpg)
Does changing the DNS settings here bypass our router's setting? Sadly, Yes. By typing in the GoogleDNS address of 8.8.8.8 into our iPhone settings, you can completely bypass the [OpenDNS](http://www.opendns.com) settings on your router.

While this might seem surprising at first, the reason for this is simple and obvious. A DNS service is like an address book. With an address book you have a person's name, and it will translate the name into an address. With a DNS service you tell it a sites name, like www.google.com, and it returns the actual address of the server, in this case '173.194.43.96'. If, on the other hand, you have the address to begin with (like 8.8.8.8 for Google DNS server), then you don't need the DNS server at all.

Incidently, I looked for a way to set the restrictions on the iPhone and iPad to prevent the internet DNS settings from being edited, but I couldn't find a way to do that.

## Bypassing DNS with IP addresses

At this point the last issue with [OpenDNS](http://www.opendns.com) should be apparent. If you have the address for a site, then a DNS server is no longer needed. This means that if you have the IP address of a pornogrphic site, then OpenDNS can't prevent you from going to it. If it was hard to get an IP address, then there is nothing to worry about, but getting them isn't all that hard.  There is a command line utility, installed on most computers, that does just this:

`nslookup www.explicitsite.com`

If you have [OpenDNS](http://www.opendns.com) installed, then this will return the IP address of an OpenDNS server which displays the blocked content message we're used to. That's how OpenDNS works. However the nslookup command takes a second option:

`nslookup www.explicitsite.com 8.8.8.8`

The second option is the DNS server to use in order to resolve the address. In the case above it's Google's DNS server, but it could also be the settings for your local Internet Service Provider, or an IP address for a DNS Server you find through a google search.

In the end it seems a determined or educated user will be able to bypass this protection quite easily.

## Conclusion?

It's important to realize how far [OpenDNS](http://www.opendns.com) protection can go, and at what point it ends. I still think it's a useful service, it protects your family in the same way an house alarm sticker on your front windows proctects your house even without a security system. It's a deterent, but it won't stop a determined user. Sadly the user doesn't need to be that determined. In my case, I'm thinking of young boys, with access to google, and the resources of all of their peers at school. In the end, only one of them needs to figure this out, and share it with his or her friends.

I am forced to agree with [Googles family saftey advice](http://www.google.com/goodtoknow/familysafety/advice), the best defence against bad content in to sit down with your children and explain to them the dangers and issues with this kind of content, and how to avoid it. There is no way that I know of to prevent a determined person from finding explicit content, so education and monitoring are your best approaches.
