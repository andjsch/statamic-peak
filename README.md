<p align="center">
  <img src="https://cdn.studio1902.nl/assets/statamic-peak/statamic-peak-logo.svg" width="160" alt="Statamic Logo" />
</p>
<h1 align="center">
  Statamic Starter Kit
</h1>

![Statamic 3.0+](https://img.shields.io/badge/Statamic-3.0+-FF269E?style=for-the-badge&link=https://statamic.com)

Statamic Peak is an opinionated starter kit for all your Statamic sites. It's design agnostic but comes bundled with tools like Tailwind and AlpineJS and a workflow you can use to build anything you want. Peak features a page builder, a rich collection of starter templates, fieldsets, blueprints, configuration and more to get you started on your client site straight away.

I will continuously update the kit with new stuff I've used or learned while building my own sites. If you enjoy Peak I would love it for yo to participate and discuss how to make stuff better.

| Title | Description |
| --- | --- |
| [`Features`](#features) | All Peak's current features. |
| [`Installation`](#installation) | How to install Statamic with Peak. |
| [`Page builder`](#page-builder) | How to use and extend the page builder. |
| [`Bard`](#bard) | How to use Bard as a block for long form content. |
| [`Typography`](#typography) | CONTENT MISSING |
| [`Buttons`](#buttons) | CONTENT MISSING |
| [`Responsive images`](#responsive-images) | CONTENT MISSING |
| [`Globals`](#globals) | CONTENT MISSING |
| [`Statamic login screen`](#statamic-login-screen) | How to customize the CP login screen |
| [`Multilingual fields and localization`](#multilingual-fields) | Field localization |
| [`Modernizr`](#modernizr) | CONTENT MISSING |
| [`Configuration changes`](#configuration-changes) | CONTENT MISSING |
| [`Upcoming features`](#upcoming-features) | What's planned |
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

## Buttons
<span id="buttons"></span>

CONTENT MISSING

## Typography
<span id="typography"></span>

CONTENT MISSING

## Responsive images
<span id="responsive-images"></span>

CONTENT MISSING

## Globals
<span id="globals"></span>

CONTENT MISSING

## Statamic login screen
<span id="statamic-login-screen"></span>

The Rad Mode on the login screen is disabled by default to give the login screen a more professional look. If you want to re-enable Rad Mode, delete `resources/views/vendor/statamic/auth/login.blade.php`.

If you want to use another logo on the login screen. For example the current sites logo, uncomment the code in `/public/vendor/app/css/cp.css` and point to an image file of choice.

## Multilingual fields and localization
<span id="multilingual-fields"></span>

It is currently not possible in Statamic to translate field labels and descriptions so I settled for English. Translate the labels and descriptions in all fieldsets (`resources/fieldsets/*.yaml`) and follow the [the instructions in the Statamic documentation](https://statamic.dev/cp-translations#content) to make the Statamic CP available in your language of choice.

## Modernizr
<span id="modernizr"></span>

CONTENT MISSING

## Configuration changes
<span id="configuration-changes"></span>

CONTENT MISSING

## Upcoming features
<span id="upcoming-features"></span>

* Unstyled mobile nav with toggle.
* More common (unstyled) content blocks like: link blocks and a call to action.
* Basic contact form with themable e-mail template.
* Partial for pagination.
* Partial for responsive background images.

## Contributing
<span id="contributing"></span>

Contributions and discussions are always welcome, no matter how large or small. Treat each other with respect.

## License
<span id="license"></span>

The MIT License (MIT). Please see [License File](LICENSE.md) for more information. Statamic itself is commercial software and has it's own license.

| Title | Description |
| --- | --- |
| [`Features`](#features) | All Peak's current features. |
| [`Installation`](#installation) | How to install Statamic with Peak. |
| [`Page builder`](#page-builder) | How to use and extend the page builder. |
| [`Bard`](#bard) | How to use Bard as a block for long form content. |
| [`Typography`](#typography) | CONTENT MISSING |
| [`Buttons`](#buttons) | CONTENT MISSING |
| [`Responsive images`](#responsive-images) | CONTENT MISSING |
| [`Globals`](#globals) | CONTENT MISSING |
| [`Statamic login screen`](#statamic-login-screen) | How to customize the CP login screen |
| [`Multilingual fields and localization`](#multilingual-fields) | Field localization |
| [`Modernizr`](#modernizr) | CONTENT MISSING |
| [`Configuration changes`](#configuration-changes) | CONTENT MISSING |
| [`Upcoming features`](#upcoming-features) | What's planned |
| [`Contributing`](#contributing) | Please do! |
| [`License`](#license) | MIT |

<!-- ```html
<html>
``` -->