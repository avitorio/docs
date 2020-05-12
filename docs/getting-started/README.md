# 🚀 Getting started

👋 Welcome! You've just taken your first step on the path to mastering Frontity.

Frontity is a **React-based framework** that enables you to easily build a frontend for a headless (or decoupled) WordPress site. Your WordPress site serves its data via the REST-API. Frontity framework is open source and free to use.

## Requirements

To get started with Frontity you will need:

### 1. WordPress (REST API)

Frontity uses the data provided by a WordPress REST-API, so first you will need a WordPress installation. If the [version of your WordPress is equal or higher than 4.4](https://wordpress.org/support/wordpress-version/version-4-4/#for-developers) or if you're using [wordpress.com](https://wordpress.com/), your REST API will automatically available.

However, when you spin up your first Frontity project you will initially be connected to our test site so you won't be without content when you first try Frontity.

You can connect your Frontity project to WordPress installed locally (using [local by flywheel](https://localwp.com/) for example) or to a WordPress To work locally you can use a 


##### REST API

What is REST API? It's just 

To check that the WordPress REST-API is working you can type one of the following into your browser's address bar. You should get a lot of complicated looking stuff in your browser. Don't worry, this is JSON and Frontity is very happy with this.









 or you can also use a site hosted on wordpress.com.




To check that the WordPress REST-API is working you can type one of the following into your browser's address bar. You should get a lot of complicated looking stuff in your browser. Don't worry, this is JSON and Frontity is very happy with this.

For a self-hosted WordPress site (i.e. local or web based):

```text
http://your-wp-domain.com/wp-json
```

For wordpress.com:

```text
https://public-api.wordpress.com/wp/v2/sites/your-wp-site.wordpress.com
```





**Frontity** accesses your content through a special URL on your site that retrieves data in a format called JSON, instead of the usual HTML.

If you haven't modified it, the URL where it lives is: [`https://www.your-blog.com/wp-json/`](https://test.frontity.io/wp-json/).

> You can take a look at the REST API of our test blog to see what it looks like: [`https://test.frontity.io/wp-json/wp/v2/posts`](https://test.frontity.io/wp-json/wp/v2/posts). For a human, it looks pretty ugly but Frontity is ok with that 🤓

If your **`/wp-json`** URL is not working, visit [our community forum](https://community.frontity.org/) and ask for help!



* **Node.js** - To launch your first Frontity project locally you need **node.js**.js installed in your machine (get it from [the official site](https://nodejs.org/) if you don't have it already). This will also install **npm** and **npx** along with Node. You will use these to run Frontity commands during the set-up and development of your project.

> For those coming from WordPress it might be worth noting that **Frontity** runs on **Node**, so it needs to be deployed in a different server than your WordPress. If you want to learn more about this, visit our [GitHub repo](https://github.com/frontity/frontity#why-a-different-nodejs-server) or see the [Architecture](../architecture.md) section of these docs.

## Initial checks

### WordPress

Frontity depends on the WordPress REST-API. If you have a recent version of WordPress installed, or if you're using wordpress.com then you should be good to go.

To check that the WordPress REST-API is working you can type one of the following into your browser's address bar. You should get a lot of complicated looking stuff in your browser. Don't worry, this is JSON and Frontity is very happy with this.

For a self-hosted WordPress site (i.e. local or web based):

```text
http://your-wp-domain.com/wp-json
```

For wordpress.com:

```text
https://public-api.wordpress.com/wp/v2/sites/your-wp-site.wordpress.com
```

### Node

To test if you have Node installed open your terminal and run:

```text
node -v
```

```text
npm -v
```

Once you have a WordPress site and Node you're good to go and all set to get up and running....

## Get up and running

No time to waste? Then head straight over to our [**Quick start guide**](quick-start-guide.md) to get up and running right away.

Want all the gen before you get started? Then read through our [**Learning Frontity**](../learning-frontity/) section for in-depth insights into working with Frontity.

Need more info? Our [**Community forum**](https://community.frontity.org/) is the perfect place to ask any questions and share your feedback. We look forward to seeing you there.

Frontity is open source and welcomes contributions. There are many ways to support the project and get involved. Please see the [**Contributing**](../contributing/) section for more info.

{% hint style="info" %}
Still have questions? Come and join us in [the community](https://community.frontity.org/) and ask there! We are here to help 😊
{% endhint %}

