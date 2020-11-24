---
theme: style.css
verticalSeparator: -v-
highlightTheme: github
revealOptions:
  transition: none
---

<!-- .slide: data-background="./images/akshar-dave-1GRvY9WUu08-unsplash.jpg" -->
<h1 class="title" style="text-align:left;">Serverless <span class="translucent">Functions +</span> Netlify</h1>
<h2 class="subtitle" style="color:#333;text-align:left;">Sia Karamalegos</h2>

---

## hi, i'm sia

[sia.codes](https://sia.codes/)

<img src="./images/champagne_sia.jpg" alt="Sia dressed up as a champagne bottle at Mardi Gras" height="450px" class="no-outline">

---

<!-- TODO: update -->
## [sia.codes/posts/webmentions-eleventy-talk/](https://sia.codes/posts/webmentions-eleventy-talk/)

---

<!-- TODO: update -->
## Show + Tell

Webmentions are cool 😎

[sia.codes/posts/architecting-data-in-eleventy/](https://sia.codes/posts/architecting-data-in-eleventy/)

Note: Show site with webmentions at bottom. Point out that this isn't a commenting and liking system, and it's my own website. Most come from Twitter because of how I share, but also other websites. In this talk

---

## Serverless Architecture

&nbsp;

<div class="align-left">
  <p class="fragment fade-in-then-semi-out"><span class="icons"><i class="fas fa-function"></i></span> Applications are broken up into individual functions </p>
  <p class="fragment fade-in-then-semi-out"><span class="icons"><i class="far fa-cloud-upload-alt"></i></span> Hosted by a 3rd party service </p>
  <p class="fragment fade-in-then-semi-out"><span class="icons"><i class="far fa-chart-line"></i></span> Can be invoked and scaled individually </p>
  <p class="fragment fade-in-then-semi-out"><span class="icons"><i class="far fa-server"></i></span> No need for server management by the developer</p>
</div>

&nbsp;

<small>[Serverless Architecture](https://www.twilio.com/docs/glossary/what-is-serverless-architecture)</small>

---

<!-- .slide: data-background="./images/duotone-yell.jpg" class="dark-highlight-quote" -->

## Jamstack <!-- .element: class="dark-background" -->

> A modern web development architecture based on client-side JavaScript, reusable APIs, and prebuilt Markup <!-- .element: class="dark-background" -->

<small class="dark-background">— Mathias Biilmann (CEO & Co-founder of Netlify) [jamstack.wtf](https://jamstack.wtf/)</small>

---

<img src="./images/how-it-works.svg" class="plain" alt="Screenshot of how Jamstack works">

<small>[www.netlify.com/jamstack/](https://www.netlify.com/jamstack/)</small>

Note: Step 1 is to decouple the frontend from the backend. The APIs can be from many sources - like a CMS, Stripe, Square, Auth0, FaunaDB, Hasura Cloud, etc.

---

## Prebuild static pages for speed

<div class="logo-grid">
  <img src="./images/eleventy.svg" class="plain" alt="Eleventy" width=60% style="background-color:black;">
  <img src="./images/nextjs.png" class="plain" alt="Next.js">
  <img src="./images/jekyll-logo-light-solid.png" class="plain" alt="Jekyll">
  <img src="./images/nuxtjs.svg" class="plain" alt="Nuxt.js">
  <img src="./images/gatsby.svg" class="plain" alt="Gatsby.js">
  <img src="./images/hugo.png" class="plain" alt="Hugo">
</div>

Note: you can also use vanilla html, css, and javascript.

---

<!-- TODO: explain what netlify does - maybe show a basic site like sia.codes -->

---

<!-- .slide: data-background="./images/balloon-feet.jpg" -->

# Netlify CLI <!-- .element: style="color:#fff;" -->

Note: Netlify CLI lets us more easily build serverless functions in a dev environment and then port them to productions. We can also do other things like easily manage secrets between both environments.

---

```
$ npm install netlify-cli -g
$ netlify
$ netlify login
```

<small>Create a Netlify account if you haven't yet - it's free!</small>

Note: install, learn about the command, then login which opens up web auth. Do the above and explain the commands we will use - init, deploy, login, functions, env, dev.

<small>[Get started with Netlify CLI](https://docs.netlify.com/cli/get-started/)</small>

---

```
Success! Netlify CLI has been installed!

Your device is now configured to use Netlify CLI to deploy and manage
your Netlify sites.

Next steps:

  netlify init     Connect or create a Netlify site from current
                   directory
  netlify deploy   Deploy the latest changes to your Netlify site

For more information on the CLI run netlify help
Or visit the docs at https://cli.netlify.com
```

---

## Hello, Netlify!

1. **Fork** [the demo](https://github.com/siakaramalegos/serverless-netlify-demo) (don't clone!)
2. Clone **your** repo.
3. `cd serverless-netlify-demo`
4. `npm install`
5. `netlify init`

<small>Build command is `npm run build` and deploy directory is `_site`.</small>

<small>[bit.ly/yo-serverless](https://github.com/siakaramalegos/serverless-netlify-demo)</small>

---

## Hello, Netlify!

Commit changes and push, then run `netlify open`.

# 🎉

---

<!-- .slide: data-background="./images/bucography-r7eBv7pnP2E-unsplash.jpg" -->

# Environment<br> Variables <!-- .element: class="text-left color-secondary" -->

---

## webmention.io

Send webmentions as a POST request <br> to the webmention endpoint with:
- a source (your URL)
- the target (post you're replying to)

```
curl -si https://webmention.io/yourdomain/webmention \
  -d source=https://yourdomain/page_with_reply.html \
  -d target=https://page_being_replied.com
```

---

Form on my blog pages for people to manually send replies:

```html
<form action="https://webmention.io/sia.codes/webmention" method="post">

  <input type="url" name="source">

  <input type="hidden" name="target"
    value="https://sia.codes/{{ page.url }}">

  <input type="submit">
</form>
```

---

<img src="./images/bridgy.jpg" class="no-outline" alt="Screenshot of brid.gy website" width="70%">

<small>[brid.gy/](https://brid.gy/)</small>

Note: allows you to easily grab webmentions from these social media platforms as well - for example, Twitter likes, replies, and retweets.

---

<img src="./images/bridgy-polling.jpg" class="no-outline" alt="Brid.gy table of responses with a column matching to any existing webmention targets" width="70%">

---

## Set up Webmention Services

<span class="icons"><i class="fas fa-2x fa-concierge-bell"></i></span>

<ol>
  <li class="fragment fade-in-then-semi-out">Set up <a href="https://indieauth.com/setup">IndieAuth</a> so you can log in with your domain.</li>
  <li class="fragment fade-in-then-semi-out">Sign in on <a href="https://webmention.io/">webmention.io</a> to get your link tags so webmention.io can collect webmentions for your site.</li>
  <li class="fragment fade-in-then-semi-out">Securely save your webmention.io API key.</li>
  <li class="fragment fade-in-then-semi-out">Optionally sign up for a social media webmention service like <a href="https://brid.gy/">Bridgy</a>.</li>
</ol>

Note: I didn't know about Netlify-cli when I wrote the post - that is a better option for managing env variables.

---

<!-- .slide: data-background="./images/duotone-road.jpg" -->

# Eleventy <!-- .element: class="dark-background" -->

---

<img src="./images/webmention_article.png" class="no-outline" alt="Screenshot of my Webmention + Eleventy tutorial" width="70%">

<small>[An In-Depth Tutorial of Webmentions + Eleventy](https://sia.codes/posts/webmentions-eleventy-in-depth/) on sia.codes</small>

Note: This talk won't be an in-depth tutorial - we'll focus on the high-level how. The good news is I already have a detailed tutorial published!

---

## The Process <span class="icons"><i class="far fa-project-diagram"></i></span>

- In production, fetch new webmentions during the build<!-- .element: class="fragment fade-in-then-semi-out" -->
- Store them in a cache file<!-- .element: class="fragment fade-in-then-semi-out" -->
- Render the webmentions<!-- .element: class="fragment fade-in-then-semi-out" -->
- Set up periodic builds<!-- .element: class="fragment fade-in-then-semi-out" -->

---

## Fetch new webmentions

&nbsp;

```javascript
// `since` comes from the `lastFetched` attribute in our cache file
const API = 'https://webmention.io/api'
const url = `${API}/mentions.jf2?domain=${domain}&token=${TOKEN}
  &per-page=${perPage}&since=${since}`
// ...
```
&nbsp;

<small>**Prior art**: I started with Max Böck's post [Static Indieweb pt2: Using Webmentions](https://mxb.dev/blog/using-webmentions-on-static-sites/) and the code for Zach Leatherman's [personal site](https://github.com/zachleat/zachleat.com), sprinkled in microformats from Keith Grant's [Adding Webmention Support to a Static Site](https://keithjgrant.com/posts/2019/02/adding-webmention-support-to-a-static-site/), and made my own changes.</small>

---

## Write to cache file

```javascript
// save combined webmentions in cache file (simplified)
function writeToCache(data) {
  const dir = '_cache'
  const fileContent = JSON.stringify(data, null, 2)

  // write data to cache json file
  fs.writeFile(CACHE_FILE_PATH, fileContent, err => {
    if (err) throw err
    console.log(`>>> webmentions cached to ${CACHE_FILE_PATH}`)
  })
}
```

---

## Render webmentions: Filters

New Nunjucks [filters](https://mozilla.github.io/nunjucks/templating.html#filters) for handling the data:

```javascript
function getWebmentionsForUrl (webmentions, url) {
  return webmentions.children.filter(entry => {
    return entry['wm-target'] === url
  })
}

function size (mentions) {
  return !mentions ? 0 : mentions.length
}

function webmentionsByType (mentions, mentionType) {
  return mentions.filter(entry => !!entry[mentionType])
}
```

---

## Render webmentions: Template

Set all the variables needed:

```html
<!-- _includes/webmentions.njk -->

<!-- Filter the cached mentions for the post's url -->
{% set mentions = webmentions | getWebmentionsForUrl(metadata.url + webmentionUrl) %}
<!-- Set likes as mentions that are `like-of`  -->
{% set likes = mentions | webmentionsByType('like-of') %}
<!-- Count the total likes -->
{% set likesSize = likes | size %}
<!-- Set replies as mentions that are `in-reply-to`  -->
{% set replies = mentions | webmentionsByType('in-reply-to')  %}
<!-- Count the total replies -->
{% set repliesSize = replies | size  %}

<!-- ... -->
```

---

## Render webmentions: Loop through data

```html
<!-- _includes/webmentions.njk -->

<!-- ... -->
{% if repliesSize > 0 %}
<div class="webmention-replies">
  <h3>{{ repliesSize }} {% if repliesSize == "1" %}Reply{% else %}Replies{% endif %}</h3>
  {% for webmention in replies %}
    {% include 'webmention.njk' %}
  {% endfor %}
</div>
{% endif %}
```

---

## Render webmentions

```html
<!-- _includes/webmention.njk - simplified -->
<article>
  {% if webmention.author %}
    <strong class="p-name">{{ webmention.author.name }}</strong>
  {% else %}
    <strong>Anonymous</strong>
  {% endif %}

  <p>
    {{ webmention.content.text | truncate }}
    {% if webmention.url %}
      <a href="{{ webmention.url }}">source</a>
    {% endif %}
  </p>
</article>
```

---

## Fake Netlify cron jobs with GitHub actions!

```yaml
# .github/workflows/build-scheduler.yml
name: Scheduled build
on:
  schedule:
  # At minute 20 past every 4th hour from 0 through 23.
  - cron: '20 0/4 * * *'
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Trigger our build webhook on Netlify
      run: curl -s -X POST "https://api.netlify.com/build_hooks/${TOKEN}"
      env:
        TOKEN: ${{ secrets.NETLIFY_BUILD_TOKEN }}
```

<small>[Scheduling Netlify deploys with GitHub Actions](https://www.voorhoede.nl/en/blog/scheduling-netlify-deploys-with-github-actions/), [crontab guru](https://crontab.guru/#15_0/3_*_*_*)</small>

---

<!-- .slide: data-background="./images/duotone-small-hiss.jpg" -->
# 🎉<!-- .element: style="font-size:4em;" -->

---

<!-- .slide: data-background="./images/akshar-dave-1GRvY9WUu08-unsplash.jpg" -->
<h1 class="title" style="text-align:left;">Thanks!</h1>

<p style="color:#333;text-align:left;">Slides:<br> <a href="http://bit.ly/web-images-2020" class="link-secondary">bit.ly/web-images-2020</a></p>
<p style="color:#333;text-align:left;">Tutorial:<br> <a href="https://sia.codes/posts/webmentions-eleventy-in-depth/" class="link-secondary">sia.codes/posts/webmentions<br>-eleventy-in-depth/</a></p>
<p style="color:#333;text-align:left;">Writing, resources, and more:<br> <a href="https://sia.codes/" class="link-secondary">sia.codes</a></p>

---

## Photo credits

- Road possum - Image by <a href="https://pixabay.com/users/csbonawitz-10920947/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=3861107">csbonawitz</a> from <a href="https://pixabay.com/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=3861107">Pixabay</a>
- Hissing possum - Image by <a href="https://pixabay.com/users/xandepontes-13842118/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=4787791">Alexandre Pontes Gomes xande</a> from <a href="https://pixabay.com/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=4787791">Pixabay</a>
- Snow possum - [University of Texas biodiversity blog](https://biodiversity.utexas.edu/news/entry/campus-biodiversity-awesome-opossums)
- Possum with babies - [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Didelphis_virginiana_with_young.JPG)
- Balloons <span>Photo by <a href="https://unsplash.com/@buco_balkanessi?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Bucography</a> on <a href="https://unsplash.com/?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>
- Heart balloons <span>Photo by <a href="https://unsplash.com/@akshar_dave?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Akshar Dave</a> on <a href="https://unsplash.com/?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>
- Balloon and feet dangling - <span>Photo by <a href="https://unsplash.com/@edrecestansberry?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Edrece Stansberry</a> on <a href="https://unsplash.com/?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>
- Possum yelling [tweet](https://twitter.com/PossumEveryHour/status/1325951348291072000)   by [@PossumEveryHour](https://twitter.com/PossumEveryHour)