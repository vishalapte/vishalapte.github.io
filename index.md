# SEO

## Table of Contents

1. [Sitemap](#sitemap)
2. [robots.txt](#robotstxt)
   - [twitterbot](#twitterbot)
   - [testing robots.txt](#test-your-robotstxt)
3. [Security](#security)
   - [Configuring SPF](#spf)
   - [Configuring Apache](#apache)
4. [Meta Information](#meta-information)
   - [Description](#description)
   - [Facebook Open Graph](#facebook-open-graph)
   - [Twitter Cards](#twitter-cards)
   - [Canonical URLs](#canonical-urls)
5. [Social Media](#social-media)
   - [Email](#email)
   - [LinkedIn](#linkedin)
   - [Twitter](#twitter)
   - [Facebook](#facebook)
   - [Instagram](#instagram)
6. [Directory Listings](#directory-listings)
   - [Google _My Business_](#google-my-business)
   - [Bing _Places_](#bing-places)

## Sitemap

Deploy a sitemap. Most frameworks make it easy.

## robots.txt

> Google Search Central – [robots.txt Specification](https://developers.google.com/search/reference/robots_txt)

> Learn about [robots.txt](https://moz.com/learn/seo/robotstxt) from moz.com

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

## Security

### SPF

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

### Apache

Add the following lines to /etc/apache2/apache2.conf

```
ServerSignature Off
ServerTokens Prod
```

## Meta Information

### Description

This sould be no more than 160 chars and ideally in the 120 char range
to satisfy the Google SERP.

Active sentences are good. Short sentences that communicate simply and clearly are good. Anything that complicates, confuses, or takes effort to understand is bad.

``` html
<meta name="description" content="<text_of_description>">
```

> Example: BatteryOS is an operating system for the future of energy.

### Facebook Open Graph

```html
<!-- Facebook Open Graph -->
<meta property="og:url" content="canonical_url_is_best"/>
<meta property="og:title" content="page_title"/>
<meta property="og:description" content="meta_description"/>
<meta property="og:image" content="url_cover_image_or_logo"/>
```

### Twitter Cards

**Add Twitter card meta headers**

Add twitter card meta headers. It's an easy way to make sure that your card looks like you want it to.

> [Twitter Cards](https://developer.twitter.com/en/docs/twitter-for-websites/cards/overview/abouts-cards)

> https://developer.twitter.com/en/docs/twitter-for-websites/cards/overview/markup

**Example:**

```html
<!-- Twitter Card -->
<!-- twitter:card = [summary|summary_large_image|app|player]-->
<meta name="twitter:card" content="summary"/>
<!-- site and side:id are congruent -->
<meta name="twitter:site" content="@twitter_handle"/>
<meta name="twitter:site:id" content="@twitter_handle"/>
<!-- creator and creator:id are congruent -->
<meta name="twitter:creator" content="@twitter_handle"/>
<meta name="twitter:creator:id" content="@twitter_handle"/>
```

```html
<meta name="twitter:title" content="page_title"/>
<meta name="twitter:description" content="meta_description"/>
<meta name="twitter:image" content="url_cover_image_or_logo"/>
```

Will default to Open Graph protocol if not defined...
- twitter:title &rightarrow; og:title
- twitter:description &rightarrow; og:description
- twitter:image &rightarrow; og:image

**Card validator**

> Twitter [Card Validator](https://cards-dev.twitter.com/validator)

### Canonical URLs

> https://developers.google.com/search/docs/advanced/crawling/consolidate-duplicate-urls

```html
<link rel="canonical" href="url_absolute_path">
```

### Google _Search Console_

Register your business and site at https://search.google.com/search-console/

You will submit the sitemap here so that Google knows more about you
and can deliver better search results.

## Social Media

### Email

Create a google email account that reflects the handle you wish to use,
and is available, on all your other social media accounts.

### LinkedIn

### Twitter

**Account**

Create a twitter account with the email account you just created above.

To start with, the twitter profile is a screen shot of the landing page
resized to fit 1500x500 and the profile description matches the meta
description of the website.

This can change later as one becomes more sophisticated.

### Facebook

Create a Facebook page for the company

Make sure to connect to WhatsApp and provide as much of the information requested.

I continue to use the same description for the page as in meta description, and
on twitter, etc.

### Instagram

## Directory Listings

### Google _My Business_

Register your business and site at https://business.google.com/

### Bing _Places_

Register your business at https://www.bingplaces.com/

Bing allows you to connect to Google Business and maintain listings on their
platform by syncing to Google Business.
