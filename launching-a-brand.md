# SEO

## Sitemap

Deploy a sitemap. Most frameworks make it easy.

## robots.txt

> []

> [robots.txt](https://moz.com/learn/seo/robotstxt) from moz.com

I wanted to keep it simple and use the following by default:

```
User-agent: *
Disallow: /static/

Sitemap: https://<my.web.site>/sitemap.xml
```

### Twitterbot

> [Twitter Developer: Getting Started Guide](https://developer.twitter.com/en/docs/twitter-for-websites/cards/guides/getting-started) – URL Crawling & Caching

### Test your robots.txt

> https://www.google.com/webmasters/tools/robots-testing-tool

## Google _My Business_

Register your business and site at https://business.google.com/

## Google _Search Console_

Register your business and site at https://search.google.com/search-console/

You will submit the sitemap here so that Google knows more about you
and can deliver better search results.

## Bing _Places_

Register your business at https://www.bingplaces.com/

Bing allows you to connect to Google Business and maintain listings on their
platform by syncing to Google Business.

## Description

This sould be no more than 160 chars and ideally in the 120 char range
to satisfy the Google SERP.

Active sentences are good. Short sentences that communicate simply and clearly are good. Anything that complicates, confuses, or takes effort to understand is bad.

``` html
<meta name="description" content="<text_of_description>">
```

> Example: BatteryOS is an operating system for the future of energy.

## Social Media

### Google Email

Create a google email account that reflects the handle you wish to use,
and is available, on all your other social media accounts.

### Twitter

**Account**
Create a twitter account with the email account you just created above.

To start with, the twitter profile is a screen shot of the landing page
resized to fit 1500x500 and the profile description matches the meta
description of the website.

This can change later as one becomes more sophisticated.

**Add Twitter card meta headers**

Add twitter card meta headers. It's an easy way to make sure that your card looks like you want it to.

> [Twitter Cards](https://developer.twitter.com/en/docs/twitter-for-websites/cards/overview/abouts-cards)

> https://developer.twitter.com/en/docs/twitter-for-websites/cards/overview/markup

**Card validator**

> Twitter [Card Validator](https://cards-dev.twitter.com/validator)

## Facebook

Create a Facebook page for the company

Make sure to connect to WhatsApp and provide as much of the information requested.

I continue to use the same description for the page as in meta description, and
on twitter, etc.

# Security

## SPF

We didn't know who we were going to use for email when we started. So we
set SP to disallow all email initially.

```
"v=spf1 -all"
```

The plan is to move to the following SPF record as soon as we start using
email and amend the record to allow email sent for the domain while
prohibiting all others

```
"v=spf1 mx -all
```

or something like...

```
"v=spf1 include:_spf.google.com ~all"
```

- `v=spf1`: This sets the SPF version being used.
- `mx`: The "mx" mechanism allows the domain's MXers to send mail
- `include:_spf.google.com`: The "include" mechanism includes Google
  mail servers in our list of authorized sending servers
- `~all`: If mail is received from a server not previously listed,
  mark it as a 'soft fail' - this allows the mail to be scrutinized further.
- `-all`: This means that any server not previously listed is not authorized
   - no questions asked. It is unclear to me why we shouldn't use `-all` instead
   of `~all` always.
- `+all`: !! The domain owner thinks that SPF is useless and/or doesn't care.


Reference:

> https://www.digitalocean.com/community/tutorials/how-to-create-a-spf-record-for-your-domain-with-google-apps

## Apache

Add the following lines to /etc/apache2/apache2.conf

```
ServerSignature Off
ServerTokens Prod
```
