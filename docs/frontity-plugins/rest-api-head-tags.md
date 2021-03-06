# REST API - Head Tags

## Description

This plugin adds all the tags in the `<head>` section of a site to WordPress REST API responses. You can download it [here](https://wordpress.org/plugins/rest-api-head-tags/).

It is perfect if you are using WordPress for a headless set-up and you would like to add the **meta tags** generated by your **WordPress** **SEO plugin** \(like Yoast SEO or All-in-One SEO Pack\) to the WordPress REST API output.

### Requisites

This package depends on the [PHP DOM library](https://www.php.net/manual/en/book.dom.php). It looks like not all PHP servers include it by default, so make sure you have it installed before using this plugin

> If you get some errors regarding this dependency have a look a this [thread](https://github.com/frontity/wp-plugins/issues/35)

### Compatibility

This plugin is compatible and works out of the box with most popular WordPress SEO plugins. These are the ones that we have tested:

* **Yoast SEO**
* **All in One SEO Pack**

Are you using a different SEO plugin and want to know if it's compatible? Feel free to ask in our [community forum.](https://community.frontity.org/) If you tested any other plugin, please let us know as well so we can update the list.

## How to use this plugin

### Entities with head tags

The plugin has been developed to include the `head_tags` field to the REST API response of most of the WordPress core entities:

* Posts, pages, attachments and custom post types
* Post types: for archive pages
* Categories, tags and custom taxonomies
* Authors

### In a Frontity project

In this case, you just have to install the [@frontity/head-tags package](rest-api-head-tags.md) and **it'll work automatically**.

### **In a different project**

You need to understand better how it works and **add the data manually**.

#### How to fetch the head\_tags field manually

You have to get each entity from its respective REST API endpoint.

For example, for fetching the posts you should go to `/wp-json/wp/v2/posts&id=123` endpoint, for fetching the categories you have to go to `wp-json/wp/v2/categories&id=123,` and for custom post types or custom taxonomies would be a different URL in each case.

In the case of the homepage, it could be less intuitive and you should go to `/wp-json/wp/v2/types/post.` As previously said, each entity has a different endpoint so if you aren't familiar with this, you should check the [WordPress REST API reference](https://developer.wordpress.org/rest-api/reference/) for more info.

Inside each endpoint, it will be a new field named `head_tags` , which will be an array of objects representing the tags that WordPress would normally include inside the HTML `head` element. These objects have the properties `tag`, `attributes` and `content`.

For example for these HTML tags:

```text
<title>Hello wordl! - My Site</title>
  <meta name="robots" content="max-snippet:-1, max-image-preview:large, max-video-preview:-1">
  <link rel="canonical" href="<http://mysite.com/hello-world/>" />
```

This would be the content of the `head_tags` field:

```text
"head_tags": [
  {
    "tag": "title",
    "content": "Hello world! - My Site"
  },
  {
    "tag": "meta",
    "attributes": {
      "name": "robots",
      "content": "max-snippet:-1, max-image-preview:large, max-video-preview:-1"
    }
  },
  {
    "tag": "link",
    "attributes": {
      "rel": "canonical",
      "href": "<http://mysite.com/hello-world/>"
    }
  }
]
```

## Settings

The settings of this plugin are really simple.

### Purge cache

In order to not affect the performance of your web, the `head_tags` field is cached for all your responses, but we've added a button to purge this cache in case something changes.

### Enable output

By default, the `head_tags` field is included in the common endpoint of each entity. You can configure it so it doesn't appear by default and to be shown when you include the `head_tags=true` query.

For example, with the output disabled, `https://mysite.com/wp-json/wp/v2/posts` won't show the `head_tags` field unless you have the query `? head_tags=true` at the end.

### Skip cache

In case you want to skip the cache, you can do so by adding to the query the parameter `skip_cache`.

There are some cache plugins for the REST API that also use the same parameter. In case you want to ignore the cache for the REST API call but not for the head tags, you can use `skip_cache&head_tags_skip_cache=false`.

## WordPress installation

1. First of all you have to [install the plugin](https://wordpress.org/plugins/rest-api-head-tags/). You can do it:
   * **Automatic**: from within WordPress dashboard go to Plugins, click `Add New` button, search for `REST API - Head Tags` \(by Frontity\) and click `Install Now`
   * **Manual**: this method requires to download the plugin and upload it to your web server via FTP.

     For a more detailed explanation, WordPress explains how to do this [on this guide](https://wordpress.org/support/article/managing-plugins/#manual-plugin-installation)
2. Once installed, you have to activate it and it will be running!

   The `head_tags` field is cached and enabled by default, but you can purge the cache or disable the output as explained on the [Settings](rest-api-head-tags.md#settings) section

## Troubleshooting

#### The REST API returns an HTML response or it shows an error

* This could happen with some plugins and themes that add hooks to the `wp_head` action.

  What the **REST API - Head Tags** plugin does is to call the `wp_head` action for every entity contained in the REST API response and transform the generated HTML code into a JSON object. That means, any hook registered to that action could be causing the problem if it:

  * generates invalid HTML
  * unexpectedly ends the PHP execution
  * throws an exception

  You can check these topics in the community for specific cases that might help you.

  * NewsPaper theme: [REST API - Head Tags Plugin error with NewsPaper theme](https://community.frontity.org/t/rest-api-head-tags-plugin-error-with-newspaper-theme/1593)
  * Password Protected plugin: [REST API - Head Tags Plugin Breaking with Password Protected](https://community.frontity.org/t/rest-api-head-tags-plugin-breaking-with-password-protected/1071)

* Another reason why it could return an error is when you make a request to a custom post type endpoint that is not expected to have the `head_tags` field \(like the `menu-items` endpoint\).

  The solution is just [disable](https://docs.frontity.org/frontity-plugins/rest-api-head-tags#enable-output) the **REST API - Head Tags** plugin output when making those requests, simply adding `head_tags=false` to the query, as explained in [REST API - Head Tags plugin not working with WordPress REST API Menus Endpoints](https://community.frontity.org/t/rest-api-head-tags-plugin-not-working-with-wordpress-rest-api-menus-endpoints/1212).

#### Missing tags inside `head_tags` field

* One possibility is that the WordPress theme or plugin generates those fields in a different action than `wp_head`. This is not easy to solve, you would have to find what hooks add the missing fields and attach them to `wp_head`, or write those hooks yourself.

  A known case for this is the **NewsPaper theme**, which adds the `<title>` tag in `header.php` directly - without using the `wp_head` action. You can take a look at [REST API - Head Tags Plugin error with NewsPaper theme](https://community.frontity.org/t/rest-api-head-tags-plugin-error-with-newspaper-theme/1593/14) for a specific solution if you are using this theme.

* This problem could also happen if there is no theme at all in your WordPress site, because themes are normally what add those tags inside `<head>`. You can try using one that comes with WordPress by default to fix this.
* Also, if you are using a plugin or any other system to cache the REST API responses you can try also clearing the cache.

#### Unexpected or outdated `head_tags` field

* Try [clearing the cache](https://docs.frontity.org/frontity-plugins/rest-api-head-tags#purge-cache).
* Try using [`skip_cache=true`](https://docs.frontity.org/frontity-plugins/rest-api-head-tags#skip-cache) as a parameter in a specific REST API request to regenerate the `head_tags` field values that appear in the response.

{% hint style="info" %}
Still have questions? Ask [the community](https://community.frontity.org/)! We are here to help 😊
{% endhint %}

