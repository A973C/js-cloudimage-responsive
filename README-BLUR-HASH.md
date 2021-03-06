[![Release](https://img.shields.io/badge/release-v3.4.9-blue.svg)](https://github.com/scaleflex/js-cloudimage-responsive/releases)
[![Free plan](https://img.shields.io/badge/price-includes%20free%20plan-green.svg)](https://www.cloudimage.io/en/home#b38181a6-b9c8-4015-9742-7b1a1ad382d5)
[![Contributions welcome](https://img.shields.io/badge/contributions-welcome-orange.svg)](#contributing)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Scaleflex team](https://img.shields.io/badge/%3C%2F%3E%20with%20%E2%99%A5%20by-the%20Scaleflex%20team-6986fa.svg)](https://www.scaleflex.it/en/home)

## VERSIONS

* [__Low Quality Preview__](https://github.com/scaleflex/js-cloudimage-responsive/blob/master/README.md)
* __Blur Hash__
* [__Plain (CSS free)__](https://github.com/scaleflex/js-cloudimage-responsive/blob/master/README-PLAIN.md)

<p align="center">
	<img
		height="175"
		alt="The Lounge"
		src="https://demo.cloudimg.io/height/350/n/https://scaleflex.airstore.io/filerobot/filerobot-cloudimage.png?sanitize=true">
</p>

<h1 align="center">
   JS Cloudimage Responsive | Cloudimage v7
</h1>

<h3 align="center">
   (blur-hash version)
</h3>

[Documentation for v2 | Cloudimage v6](https://github.com/scaleflex/js-cloudimage-responsive/blob/v7/README_v6.md)

<p align="center">
	<strong>
		<a href="#table_of_contents">Docs</a>
		•
		<a href="https://cdn.scaleflex.it/plugins/js-cloudimage-responsive/demo/blur-hash/index.html" target="_blank">Demo</a>
		•
		<a href="https://codesandbox.io/s/js-cloudimage-responsive-blur-hash-lopvu" target="_blank">Code Sandbox</a>
		•
		<a href="https://medium.com/@dmitry_82269/responsive-images-in-2019-now-easier-than-ever-b76e5a43c074" target="_blank">Why?</a>
	</strong>
</p>

This plugin detects the width of any image container as well as the device pixel ratio
density to load the optimal image size needed.
Images are resized on-the-fly via the <a href="https://cloudimage.io" target="_blank">Cloudimage service</a>, thus offering a comprehensive
automated image optimization service.

When an image is first loaded on your website or mobile app,
Cloudimage's resizing servers will download the origin image from
the source, resize it for the client's screen size and deliver to your users through one or multiple
Content Delivery Networks (CDNs). The generated image formats are cached in the CDN and will be delivered rocket fast on any subsequent request.

**NOTE:** Your original (master) images should be stored on a server
or storage bucket (S3, Google Cloud, Azure Blob...) reachable over
HTTP or HTTPS by Cloudimage. If you want to upload your master images to
Cloudimage, contact us at
[hello@cloudimage.io](mailto:hello@cloudimage.io).

<p align="center">
	<img
		alt="The Lounge"
		src="https://demo.cloudimg.io/width/1400/n/https://scaleflex.airstore.io/filerobot/cloudimage-process.jpg?sanitize=true">
</p>

powered by [Cloudimage](https://www.cloudimage.io/)
([Watch the video here](https://www.youtube.com/watch?time_continue=2&v=JFZSE1vYb0k))

## <a name="table_of_contents"></a> Table of contents

* [Demo](#demo)
* [Requirements](#requirements)
* [Step 1: Installation](#installation)
* [Step 2: Initialize](#initialize)
* [Step 3: Implement](#implement)
* [Configuration](#configuration)
* [Image properties](#image_properties)
* [Lazy loading](#lazy_loading)
* [Process dynamically loaded images](#dynamically-loaded)
* [Browser support](#browser_support)
* [Filerobot UI Family](#ui_family)
* [Contributing](#contributing)
* [License](#license)


## <a name="demo"></a> Demo

To see the Cloudimage Responsive plugin in action, please check out the
[Demo page](https://cdn.scaleflex.it/plugins/js-cloudimage-responsive/demo/blur-hash/index.html).
Play with your browser's window size and observe your
Inspector's Network tab to see how Cloudimage delivers the optimal
image size to your browser, hence accelerating the overall page
loading time.

## <a name="requirements"/> Requirements

### Cloudimage account

To use the Cloudimage Responsive plugin, you will need a
Cloudimage token to deliver your images over CDN. Don't worry, it only takes seconds to get one by
registering [here](https://www.cloudimage.io/en/register_page).
Once your token is created, you can configure it as described below.
This token allows you to use 25GB of image cache and 25GB of worldwide
CDN traffic per month for free.

### Layout/CSS

In order to use smooth transition between preview image and good quality and size image, the plugin uses absolute positioning for images and wraps an image tag with div element with relative positioning. 

You have to pay attention on the following things:

- the plugin sets 100% width for img tag and position absolute (You should not apply other sizes or change position property. If you need to change width of image or position, you have to set it to wrapper)

## <a name="installation"></a>Step 1: Installation

Add script tag with CDN link to js-cloudimage-responsive

```javascript
<script src="https://cdn.scaleflex.it/plugins/js-cloudimage-responsive/3.4.9/blur-hash/js-cloudimage-responsive.min.js"></script>
```

You may also use major version number instead of fixed version to have the latest version available.

```javascript
<script src="https://cdn.scaleflex.it/plugins/js-cloudimage-responsive/3/blur-hash/js-cloudimage-responsive.min.js"></script>
```

or using npm

```
$ npm install --save js-cloudimage-responsive
```

## <a name="initialize"></a>Step 2: Initialize

After adding the js-cloudimage-responsive lib, simply iniatialize it with your **token** and the **baseUrl** of your image storage:

```javascript
<script>
    const ciResponsive = new window.CIResponsive({
      token: 'demo',
      baseUrl: 'https://cloudimage.public.airstore.io/demo/' // optional
    });
</script>
```

or in new style with npm:

```javascript

import 'js-cloudimage-responsive/blur-hash';

const ciResponsive = new window.CIResponsive({
  token: 'demo',
  baseUrl: 'https://cloudimage.public.airstore.io/demo/' // optional
});
```

## <a name="implement"></a>Step 3: Implement in img tag or use it as background image

### img tag

Finally, just use the `ci-src` instead of the `src` attribute in image tag:

```html
<img ci-src="magnus-lindvall.jpg" ci-ratio="1.5" ci-blur-hash="LNAyTi9ZVsQ,.TM{WAkW4T%2WBt7"/>
```

NOTE:

"ci-ratio" is recommended to prevent page layout jumping. The parameter is used to calculate image height to hold the image position while image is loading.

"ci-blur-hash" is A very compact representation of a placeholder for an image. <a href="https://github.com/woltapp/blurhash">read more</a>

<a href="https://codesandbox.io/s/js-cloudimage-responsive-blur-hash-lopvu"><img src="https://codesandbox.io/static/img/play-codesandbox.svg" alt="edeit in codesandbox"/></a>

### background image

Use the `ci-bg-url` instead of CSS background-image property `background-image: url(...)`:

```html
<div ci-bg-url="magnus-lindvall.jpg"></div>
```

<a href="https://codesandbox.io/s/js-cloudimage-responsive-background-imxdm"><img src="https://codesandbox.io/static/img/play-codesandbox.svg" alt="edeit in codesandbox"/></a>

## <a name="configuration"></a> Config

### token

###### Type: **String** | Default: **"demo"** | _required_

Your Cloudimage customer token.
[Subscribe](https://www.cloudimage.io/en/register_page) for a
Cloudimage account to get one. The subscription takes less than a
minute and is totally free.

### domain

###### Type: **String** | Default: **"cloudimg.io"**

Use your custom domain.

### doNotReplaceURL

###### Type: **bool** | Default: **false**

If set to **true** the plugin will only add query params to the given source of image.

### baseUrl

###### Type: **String** | Default: **"/"** | _optional_

Your image folder on server, this alows to shorten your origin image URLs.

### <a name="lazy_loading_config"></a>lazyLoading

###### Type: **Bool** | Default: **false** | _optional_

Only images close to the client's viewport will be loaded, hence accelerating the page loading time. If set to **true**, an additional script must be included, see [Lazy loading](#lazy_loading)

### params

###### Type: **String** | Default: **'org_if_sml=1'** | _optional_

Applies default Cloudimage operations/ filters to your image, e.g. brightness, contrast, rotation...
Multiple params can be applied, separated by "```&```" e.g. wat_scale=35&wat_gravity=northeast&wat_pad=10&grey=1

```javascript
{
 ...,
 params: 'org_if_sml=1'
}
```

#### alternative syntax: type: **Object**

```javascript
{
 ...,
 params: {
    org_if_sml: 1,
    grey: 1,
    ...
 }
}
```

[Full cloudimage v7 documentation here.](https://docs.cloudimage.io/go/cloudimage-documentation-v7/en/introduction)

### exactSize

###### Type: **Bool** | Default: **false** | _optional_

Forces to load exact size of images.
By default the plugin rounds container width to next possible value which can be divided by 100 without the remainder.
It’s done for cache reasons so that not all images are cached by 1px, but only 100px, 200px, 300px …

## <a name="image_properties"></a> Image properties

Cloudimage responsive plugin will make image on your page responsive if you replace the `src` with `ci-src` attribute in the `<img>` tag:

### ci-src

###### Type: **String** | Default: **undefined** | _required_

Original image hosted on your web server. You can use absolute path or
relative to baseUrl in your config.

**NOTES:** 

The plugin uses a special algorithm to detect the width of image container and set the image size accordingly. This is the recommended way of using the Cloudimage Responsive plugin.

Images where `ci-src` is not used will be delivered in a standard, non-responsive way.

### ci-blur-hash

###### Type: **String** | Default: **undefined** | _required_

BlurHash is a very compact representation of a placeholder for an image. <a href="https://github.com/woltapp/blurhash">read more</a>

```javascript
ci-blur-hash="LNAyTi9ZVsQ,.TM{WAkW4T%2WBt7"
```
### ci-params

###### Type: **String** | Default: **undefined** | _optional_

You can apply any Cloudimage operations/ filters to your image, e.g. brightness, contrast, rotation...
Multiple params can be applied, separated by "```&```" e.g. wat_scale=35**&**wat_gravity=northeast**&**wat_pad=10**&**grey=1

```javascript
ci-params="gray=1&bright=10"
```

#### alternative syntax: type: **Object**

```javascript
ci-params="{
    bright: 10,
    grey: 1,
    ...
}"
```

[Full cloudimage v7 documentation here.](https://docs.cloudimage.io/go/cloudimage-documentation-v7/en/introduction)

### ci-ratio (or data-ci-ratio)

###### Type: **Number** | _optional_

It is recommended to prevent page layout jumping. The parameter is used to calculate image height to hold the image position while image is loading.

To see the full cloudimage documentation [click here](https://docs.cloudimage.io/go/cloudimage-documentation)

### ci-fill (or data-ci-fill)

###### Type: **String** | Default: **100%**

Image width (%) according to its container.

### ci-align (or data-ci-align)

###### Type: **String** | Default: **auto**

**possible values**: ['auto', 'center']

If ci-fill (image width (%) according to its container) was set, ci-align makes it possible to center an image.

### ci-not-lazy (or data-ci-not-lazy)

###### Type: **Bool**

Switch off lazyload per image.

## <a name="lazy_loading"></a> Lazy Loading

Lazy loading is not included into js-cloudimage-responsive by default. If you [enable lazy loading](#lazy_loading_config) in the configuration, you need to add an additional library.

The example below uses [lazysizes](https://github.com/aFarkas/lazysizes)
library using Intersection Observer API.

[Code Sandbox example](https://codesandbox.io/s/6jkovjvkxz)

add the following scripts right after js-cloudimage-responsive script

```javascript
<script>
  window.lazySizesConfig = window.lazySizesConfig || {};
  window.lazySizesConfig.init = false;
</script>
<script src="https://cdn.scaleflex.it/plugins/js-cloudimage-responsive/3/blur-hash/js-cloudimage-responsive.min.js"></script>
<script src="https://cdn.scaleflex.it/filerobot/js-cloudimage-responsive/lazysizes.min.js"></script>
```

the initialization script

```javascript
<script>
    const ciResponsive = new window.CIResponsive({
      token: 'demo',
      baseUrl: 'https://cloudimage.public.airstore.io/demo/', // optional
      lazyLoading: true                                       // optional
    });

    window.lazySizes.init();
</script>
 ```
 
 ## <a name="dynamically-loaded"></a>Process dynamically loaded images!
 
 In case you load some images dynamically you need to trigger `ciResponsive.process()` manually.

```javascript
<script>
    const ciResponsive = new window.CIResponsive({
      token: 'demo',
      baseUrl: 'https://cloudimage.public.airstore.io/demo/', // optional
      lazyLoading: true                                       // optional
    });

    window.lazySizes.init();
    
    ciResponsive.process(); -> call when you need to process dynamically loaded images
</script>
 ```

All contributions are super welcome!

## <a name="dynamically-loaded"></a>Process dynamically loaded images!

In case you load some images dynamically you need to trigger `ciResponsive.process()` manually.

```javascript
<script>
const ciResponsive = new window.CIResponsive({
   token: 'demo',
   baseUrl: 'https://cloudimage.public.airstore.io/demo/', // optional
   lazyLoading: true                                       // optional
});

window.lazySizes.init();

ciResponsive.process(); -> call when you need to process dynamically loaded images
</script>
```

## <a name="browser_support"></a> Browser support

Tested in all modern browsers and IE 11,10,9.

If you want to address the use case where your visitors disable JS. You have to add noscript tag.

```html
<noscript><img src="path-to-original-image"/></noscript>
```

NOTE: If you use lazy loading with IntersectionObserver, you must
manually add the [IntersectionObserver polyfill](https://github.com/w3c/IntersectionObserver/tree/master/polyfill)
for cross-browser support.

## <a name="ui_family"></a>Filerobot UI Familiy

* [React Cloudimage Responsive](https://github.com/scaleflex/react-cloudimage-responsive)
* [Angular Cloudimage Responsive](https://github.com/scaleflex/ng-cloudimage-responsive)
* [JS Cloudimage 360 view](https://github.com/scaleflex/js-cloudimage-360-view)
* [Image Editor](https://github.com/scaleflex/filerobot-image-editor)
* [Uploader](https://github.com/scaleflex/filerobot-uploader)

## <a name="contributing"></a>Contributing!

All contributions are super welcome!


## <a name="license"></a>License
JS Cloudimage Responsive is provided under the [MIT License](https://opensource.org/licenses/MIT)

