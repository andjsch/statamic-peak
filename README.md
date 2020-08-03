<p align="center">
  <img src="https://cdn.studio1902.nl/assets/statamic-peak/statamic-peak-logo.svg" width="160" alt="Statamic Logo" />
</p>
<h1 align="center">
  Statamic Starter Kit
</h1>

![Statamic 3.0+](https://img.shields.io/badge/Statamic-3.0+-FF269E?style=for-the-badge&link=https://statamic.com)

Statamic Peak is an opinionated starter kit for all your Statamic sites. It's design agnostic but comes bundled with tools like Tailwind and AlpineJS and a workflow you can use to build anything you want. Peak features a page builder, a rich collection of starter templates, fieldsets, blueprints, configuration and more to get you started on your client site straight away. Peak is easy to extend or edit to fit your clients website needs. 

I made Peak to make it easy for me to start new projects as they share so much of the same principles. I hope Peak will help others to get started or learn a few new tricks. Wether you're new to Statamic and would like some examples, or wether you're a veteran: I hope you will like Peak and would would love it for you to participate and discuss how to make stuff better. Let's make this a common effort! I will continuously update the kit with new stuff I've used or learned while building my own sites. 

| Title | Description |
| --- | --- |
| [`Features`](#features) | All Peak's current features. |
| [`Knowledge assumptions`](#knowledge-assumptions) | Stuff you should know when using Statamic Peak. |
| [`Installation`](#installation) | How to install Statamic with Peak. |
| [`Tailwind config`](#tailwind-config) | How Tailwind is configured. |
| [`Page builder`](#page-builder) | How to use and extend the page builder. |
| [`Bard`](#bard) | How to use Bard as a block for long form content. |
| [`Typography`](#typography) | Typography partials and Tailwind Typography. |
| [`Buttons`](#buttons) | How to work with buttons. |
| [`Responsive images`](#responsive-images) | Easily responsive images to your site. |
| [`Globals`](#globals) | Global sets for site wide configuration. |
| [`Statamic login screen`](#statamic-login-screen) | How to customize the CP login screen. |
| [`Multilingual fields and localization`](#multilingual-fields) | Field localization. |
| [`Modernizr`](#modernizr) | How to use Modernizr with Peak. |
| [`Configuration changes`](#configuration-changes) | Differences with the default Statamic config. |
| [`Upcoming features`](#upcoming-features) | What's planned for the future. |
| [`Contributing`](#contributing) | Please do! |
| [`License`](#license) | MIT |

## Features
<span id="features"></span>

- [Tailwind](https://tailwindcss.com) as a CSS framework.
- Tailwind Custom Forms (with configuration).
- Tailwind Typography (with configuration).
- A custom Tailwind config file with added components and utilities used by Peak. 
- [AlpineJS](https://github.com/alpinejs/alpine/) as a JS framework.
- A block builder (replicator) with basic templates for your scaffolding your content. Easily extendible to your clients needs. 
- An article block (bard) with some default sets like a figure, pull quote and an embedded video set. Easily extendible.
- A button system for adding buttons to your site.
- Sane default configuration.
- The [Responsive Images](https://github.com/spatie/statamic-responsive-images) addon by Spatie to make using images in your templates a breeze.
- Asset compilation with Laravel Mix.
- Modernizr support (webp detection as a default).

## Knowledge assumptions
<span id="knowledge-assumptions"></span>

Before using Peak make sure you're familiar with:

* Statamic 
* Antlers
* Tailwind
* *And to lesser extend:* AlpineJS (JS framework)

## Installation
<span id="installation"></span>

**1. Create a new site** cloning the repo and removing the origin repo.
```bash
git clone git@github.com:studio1902/statamic-peak.git my-site
cd my-site
rm -rf .git
composer install
cp .env.example .env && php artisan key:generate
```

**2. Make a new user** – you'll want it to be a `super` so you have access to everything.
```bash
php please make:user
```

**3. Compile the fontend assets** 
The [TailwindCSS](https://tailwindcss.com/) compiled assets aren't included in this repo. You need to compile it yourself.
```bash
npm i && npm run watch
```
To compile for production run this (on your server). It will purge all unnecessary utility classes and greatly reduce file size:
```bash
npm run production
```

**4. Build!**
If you're using [Laravel Valet](https://laravel.com/docs/valet), your site should be available at `http://my-site.test`. You can access the control panel at `http://my-site.test/cp` and login with your new user. Build your site, read the [Statamic Docs](https://statamic.dev) and have fun!

## Tailwind config
<span id="tailwind-config"></span>

Peak comes with `tailwind.config.js` which dictates how Tailwind should be compiled. Everything is configured in a single Javascript file. This makes it very easy to define you're unique design system for each website you're building. The file is fully documented.

The config file also includes the [Tailwind Custom Forms](https://tailwindcss-custom-forms.netlify.app) and [Tailwind Typography](https://github.com/tailwindlabs/tailwindcss-typography) plugins. They're easy to customize and the config file already includes some basic configuration. The plugins are easy to remove if you don't plan on using them.

## Page builder
<span id="page-builder"></span>

While you could make different templates for all your page types. The idea is to make pages as modular as possible. Every unique element of your website could be a partial and a dedicated button in the page builder. 

If the layout of a page is totally different - or you really want to - you can always opt for using templates.

### Adding blocks
Edit `resources/fieldsets/page_builder.yaml` to add blocks (preferably imports) to the fieldset. In `resources/views/default.antlers.html` you can see the blocks being loaded. Antlers will look in the `resources/views/page_builder/` folder for partials with the handle of your block. 

If you for example add a fieldset to the `page_builder.yaml` with the handle `call_to_action` make sure you add a `_call_to_action.antlers.html` file to the `resources/views/page_builder` folder.

| Note: blocks are scoped under `block` to avoid collision with other fields. Make sure you reference variables in a block like this: `{{ block:field_name }}`

## Bard
<span id="bard"></span>

For long form content you can use the `Article` content block. This is a [Bard fieldtype](https://statamic.dev/fieldtypes/bard#content) with multiple sets of fields that are regularly used in longer articles. 

### Adding sets
Edit `resources/fieldsets/article.yaml` to add sets (preferably imports) to the article. In `resources/views/page_builder/_article.antlers.html` you can see the sets being loaded. Antlers will look in the `resources/views/components/` folder for partials with the handle of your set. 

If you for example add a fieldset to the `article.yaml` with the handle `table` make sure you add a `_table.antlers.html` file to the `resources/views/components` folder.

| Note: sets are scoped under `set` to avoid collision with other fields. Make sure you reference variables in a block like this: `{{ set:field_name }}`

### Sizing utilities
An article goes into a CSS Grid with 12 columns. By default all sets get the class `size-md`. As you can see in `tailwind.config.js` on mobile this means those elements span 12 columns. On larger screens however they just span 6 columns (centered). There are other sizing utilities as well:

* *size-sm*: 12 columns on mobile, 4 columns from medium screens up
* *size-md*: 12 columns on mobile, 6 columns from medium screens up
* *size-lg*: 12 columns on mobile, 8 columns from medium screens up
* *size-xl*: 12 columns on mobile, 10 columns from medium screens up

You can use the sizing utilities to let an image for example break out of it's content. In sets like `figure` and `video` the user can pick their own size using the `size` field in `resources/fieldsets/common.yaml`. 

| Note: the layout doesn't have to be centered and is easy to change in the `tailwind.config.js` file.

## Buttons
<span id="buttons"></span>

The files `resources/fieldsets/buttons.yaml` and `resources/views/components/_buttons.antlers.html` go together. The button fieldset is a set in Bard but can also be called from other fieldsets where you want to include buttons. Just call the buttons partial in your template and one or multiple buttons will be rendered. 

## Typography
<span id="typography"></span>

Peak contains a few basic typography partials in `resources/views/typography`. Whenever you need to render text in your partial you should call the relevant partial or add a new one. Let's say we have a block in our page builder with a `{{ title }}` field. In the template partial for your block you could do the following:

```html
{{ partial:typography/h1 :content="block:title" }}
```

This will render the title with the styling defined in `typography/h1`. This way you ensure the same styling throughout your website without having to add or edit Tailwinds utility classes in multiple template files. You can even change the tag and text color and add classes if need be:

```html
{{ partial:typography/h1 tag="span" color="text-error-600" class="mb-8" :content="block:title" }}
```

Peak comes with a few defaults that are easy to style. Feel free to add more partials for your current website.

## Responsive images
<span id="responsive-images"></span>

Peak comes with Spaties Responsive Images package for Statamic. This package will generate multiple sizes for your assets and will provide browser with instructions on which versions to use depending on the screen size and the way the image is rendered. Adding responsive images to your site *couldn't* be easier. Check out their [documentation](https://github.com/spatie/statamic-responsive-images).

## Globals
<span id="globals"></span>

Peak currently comes with two global sets you often need. One to edit content on error pages like the 404 page and one to add social media accounts to your website. There's already a basic 404 template in place (`resources/views/errors/404.antlers.html`) to display those messages. 

## Statamic login screen
<span id="statamic-login-screen"></span>

The Rad Mode on the login screen is disabled by default to give the login screen a more professional look. If you want to re-enable Rad Mode, delete `resources/views/vendor/statamic/auth/login.blade.php`.

If you want to use another logo on the login screen. For example the current sites logo, uncomment the code in `/public/vendor/app/css/cp.css` and point to an image file of choice.

## Multilingual fields and localization
<span id="multilingual-fields"></span>

It is currently not possible in Statamic to translate field labels and descriptions so I settled for English. Translate the labels and descriptions in all fieldsets (`resources/fieldsets/*.yaml`) and follow the [the instructions in the Statamic documentation](https://statamic.dev/cp-translations#content) to make the Statamic CP available in your language of choice.

## Modernizr
<span id="modernizr"></span>

Peak comes with Modernizr support. By default the only feature detect that's added is webp. It will add a `webp` class or a `no-webp` class to the `<html>` tag. If you want to add more feature detects you can edit `modernizr.config.js`.

## Configuration changes
<span id="configuration-changes"></span>

Peak changes the default Statamic config. The following is different:

| File | Default | Peak |
| --- | --- | --- |
| `config/app.php` | `'timezone' => 'UTC'` | `'timezone' => 'CET'` |
| `config/statamic/assets.php` | `'cache' => false` | `'cache' => env('SAVE_CACHED_IMAGES', true),` |
| `config/statamic/cp.php` | A getting started widget | A page collection widget |
| `config/statamic/cp.php` | `'date_format' -> 'Y-m-d'` | `'date_format' -> 'd-m-Y'` |
| `config/statamic/editions.php` | `'pro' -> false` | `'pro' -> true` |
| `config/statamic/live_preview.php` | Three breakpoints | All tailwinds breakpoints defined in `tailwind.config.js` |
| `config/statamic/static_caching.php` | `rules' => [ // ]` | `'rules' => 'all'` |
| `config/statamic/users.php` | `'avatars' => 'initials'` | `'avatars' => 'gravatar'` |


## Upcoming features
<span id="upcoming-features"></span>

* Unstyled multi-level responsive nav.
* More common (unstyled) content blocks like: link blocks and a call to action.
* Basic contact form with themable e-mail template.
* Partial for the social media global.
* Partial for pagination.
* Partial for responsive background images.

## Contributing
<span id="contributing"></span>

Contributions and discussions are always welcome, no matter how large or small. Treat each other with respect.

## License
<span id="license"></span>

The MIT License (MIT). Please see [License File](LICENSE.md) for more information. Statamic itself is commercial software and has it's own license.