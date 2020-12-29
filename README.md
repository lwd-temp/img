![Generated image](https://img.phuctm97.com/api/v2/%F0%9F%8E%86%20**Imagegen**%20as%20a%20Service?&icons=Next.js&icons=Vercel)

# 🎆 Imagegen as a Service

Imagegen (image generator) as a Service, built with Next.js and Vercel.

## What is this?

This is an API that generates dynamic images for different purposes, is especially useful to generate cover images for distributing content:

- Blogging & writing.

- Videos' thumbnails.

- Open-source repositories' social images.

- etc.

It's built and deployed serverless thanks to Next.js and Vercel, so there is nothing to maintain. Moreover, thanks to Vercel's generous hobby plan, this is **completely free** for non-commercial use.

### Example

The above image is a dynamic image generated by this service, copy the URL below and paste on your browser to see it yourself:

```
https://img.phuctm97.com/api/v2/%F0%9F%8E%86%20**Imagegen**%20as%20a%20Service?&icons=Next.js&icons=Vercel
```

## How should you use it?

There is a limit to Vercel's free plan, so feel free to test the API on my website, but please don't use it directly on yours. Instead:

- [Fork the repository](https://github.com/phuctm97/img/fork).

- Make changes to fit your need (see below, it's easy).

- Create a new Vercel project and import **your forked repository** (You'll need a Vercel account).

- Done 🎉. Vercel will give you a deployment URL, check it out!

## API

### V1

**URL**: `GET /api/v1/[slug]`

**Query params**:

```yml
text: string.(png|jpg);
theme: "light" | "dark";
md: boolean; # Enable basic Markdown syntax or not.
fontSize: string;
images: string[];
widths: string[];
heights: string[];
```

All query params are optional, a reasonable default will be used when necesssary.

**Example**:

```
https://img.phuctm97.com/api/v1/**Hello**%20World.png?theme=light&md=1&fontSize=100px&images=https%3A%2F%2Fassets.vercel.com%2Fimage%2Fupload%2Ffront%2Fassets%2Fdesign%2Fvercel-triangle-black.svg
```

### V2

**URL**: `GET /api/v2/[slug]`

**Query params**:

```yml
text: markdown.(png|jpg);
target: "devto" | "og";
theme: "light" | "dark";
icons: string[];
colors: string[];
```

- **text** supports Markdown syntax by default. Emojis are replaced with [Twemoji].

- **icons** are loaded from [Simple Icons], use names appearing on its website as inputs here. Not found icons will be ignored.

- **colors** are valid CSS colors, or `default` to use Simple Icons's suggested colors, or `invert` to invert the default colors.

- **target** helps generate images suitable for distribution to a specific platform, currently supports DEV.to (`devto`) and Open Graph (`og`).

All query params are optional, a reasonable default will be used when neccesary.

**Example**:

```
https://img.phuctm97.com/api/v2/%F0%9F%8E%86%20**Imagegen**%20as%20a%20Service?&icons=Next.js&icons=Vercel
```

## Project structure

The project uses [Puppeteer] to launch and capture screenshot from a headless Chrome. Responses are cached for 7 days to increase performance and reduce loads.

- **server/v1**: parse API v1 requests and generate static HTML.

  - Change `parser.ts` to update query API.
  - Change `template.ts` to customize output images.

- **server/v2**: parse API v2 requests and generate static HTML.

  - Change `parser.ts` to update query API.
  - Change `template.ts` to customize output images.

- **server/\*.ts**: utils to process HTML and capture screenshots.

- **pages/api/v1**, **pages/api/v2**: Next.js API routes to receive requests (You probably won't need to change this).

- **fonts**: Fonts are loaded locally in **server/\*\*/\*.ts**. Replace with your fonts (optionally).

**Recommended approach**: copy **api/v1** + **server/v1** or **api/v2** + **server/v2** and make changes arcordingly, it won't accidentially crash your code this way.

## Author

Made by ([@phuctm97]).

## Thanks

Heavily inspired by Vercel's [og-image].

<!-- Links -->

[img.phuctm97.com]: https://img.phuctm97.com
[@phuctm97]: https://twitter.com/phuctm97
[simple icons]: https://simpleicons.org
[twemoji]: https://twemoji.twitter.com
[og-image]: https://github.com/vercel/og-image
[puppeteer]: https://github.com/puppeteer/puppeteer
