# DFD Responsive Images

A Hugo module for creating and using responsive images wherever images are used.

## Netlify Status

[![Netlify Status](https://api.netlify.com/api/v1/badges/2a80fcb8-8f32-498d-ace3-563dfa1db57d/deploy-status)](https://app.netlify.com/sites/hugo-dfd-responsive-images/deploys)

## Demo Site

<https://hugo-dfd-responsive-images.wildtechgarden.ca>

## Features

* From Hugo content files
  * via a render-image hook
  * via a shortcode
* TODO: #6 Cover images
* TODO: #7 Microformat (e.g. OpenGraph/Twitter) support
* TODO: #8 Thumbnails (e.g. for blog/taxonomy/HTML sitemap/etc listings)
  * TODO: Configurable between thumbnail and full width or height image
  * TODO: Sitewide defaults
  * TODO: Configurable per list page
  * TODO: Configurable per listed page
* Fallback for non-resource images
* Image conversion (e.g. to webp)
* Allow adding a wrapping link to original size image 
  * (optionally original format image)
* TODO: Configurable responsive behaviour (sizes attribute and sizes of images)
* Allow disabling responsive (autoselection of differently sized) images

## Basic Usage
### Importing the Module

1. The first step to making use of this module is to add it to your site or theme.  In your configuration file:

   ``config.toml``
   ```toml
   [module]
     [[module.imports]]
       path = "github.com/danielfdickinson/hugo-dfd-responsive-images"
   ```
   OR
   ``config.yaml``
   ```yaml
   module:
     imports:
       - path: github.com/danielfdickinson/hugo-dfd-responsive-images
   ```
2. Execute
   ```bash
   hugo mod get github.com/danielfdickinson/hugo-dfd-responsive-images
   hugo mod tidy
   ```

### Add the Image

1. Place your image (e.g. ``screenshot.png``) in a [Page Bundle](https://gohugo.io/content-management/page-bundles/)
   * **NB** You can only use subdirectories with leaf bundles. For branch bundles the image must be in the same directory as the ``_index.md``.
2. OR under ``assets`` in your project root (in which case you can use subdirectories under ``assets`` (e.g. ``assets/path/to/screenshot.png``))

**NB** If you don't use a page bundle or ``assets`` (e.g. if you place the image under ``static``, the image will still be used, but will not be responsive).

### Add CSS to Style the Images

For example for the demo site we use:

```css
img {
    height: auto;
    width: auto;
    max-height: 50vh;
    max-width: 100%;
}

figcaption {
    font-style: italic;
}

.responsive-figure figcaption h2 {
    font-size: 1rem;
}

.responsive-figure figcaption p {
    font-size: .875rem;
}
```

If you wanted full width images with the figure shortcode in example #2 below, you could instead use:

```css
.responsive-figure.fullwidth img {
    height: auto;
    width: 100%;
    max-height: unset;
}
```

### Use Markdown (render-image render hook makes it responsive)

E.g.

```markdown
![Screenshot of a web page with an aqua theme](screenshot.png)
```

Which you can [view on this module's demo site](https://hugo-dfd-responsive-images.wildtechgarden.ca/post/testimage1/#via-markdown).

### Use Figure Shortcode

E.g.

### Example #1

```markdown
{{< figure class="responsive-figure" title="Figure 1: Differences between markdown figures and figure shortcode" src="screenshot.png" alt="Screenshot of a web page with an aqua theme" caption="For a figure caption can be different than alt text">}}
```

Which you can [view on this module's demo site](https://hugo-dfd-responsive-images.wildtechgarden.ca/post/testimage1/#via-figure-shortcode).

### Example #2

```markdown
{{< figure class="responsive-figure fullwidth" title="Figure 1: Differences between markdown figures and figure shortcode (full width)" src="screenshot.png" alt="Screenshot of a web page with an aqua theme" caption="For a figure caption can be different than alt text">}}
```

Which you can [view on this module's demo site](https://hugo-dfd-responsive-images.wildtechgarden.ca/post/testimage1/#via-figure-shortcode-fullwidth).

See [partial below](#responsive-images-partial) for the full set of parameters you can use with the shortcode (except 'destination' is named 'src' for the shortcode).
## Advanced Usage

### Responsive Images Partial

You have access to the ``helpers/responsive-images`` partial in your layouts and shortcodes.
Not all combinations of parameters make sense. (E.g. a caption with image_wrapper other than 'figure' will results in \<figcaption> that is not inside a '\<figure>' element)

```html
{{ partial "helpers/responsive-images" (
    dict "width" 1900px
    "height" 1080px
    "alt" "Screenreader text"
    "title" "Title (screenreaders and often tooltip)"
    "destination" "Image source (usually relative to page bundle or assets)"
    "page" .Page (Hugo page context; it is unlikely  that you will want this to be other than .Page)
    "link" "A link in which to wrap the image"
    "target" "For link: E.g. ('_blank')"
    "rel" "For link: E.g. ('no')"
    "image_wrapper" "element in which to wrap <img> element"
    "caption" "A <figcaption>"
    "attr" "More <figcaption> text (but can be wrapped by a hyperlink via attrlink)"
    "attrlink" "A hyperlink wrapped around attr in a <figcaption>"
    "class" "Classes (space separated string) to add to the wrapper element, or the img element if there is no image_wrapper"
    "noImageWrapper" (If true you get a bare <img> element; default for render-image render hook)
    ) 
-}}

```

### Site or Page Params

| Param | Default | Description |
|-------|---------|-------------|
| imageResponsive | true | Make images responsive (have srcset and sizes) |
| imageLinkFull | _(nil)_ | Link in which to wrap image if not provided by shortcode or partial (always applies to markdown images) |
| imageAddWrapper | _(nil)_ | Element in which to wrap image if not provided by shortcode or partial (always applies to markdown images) |
| imageAddClass | _(nil)_ | Classes (space separated string) to add to wrapper element or img element if no image wrapper |
| imageAltAsCaption | false | Use alt text as caption when using image wrapper (unless caption specified) |
| imageConvertTo | _(nil)_ | Convert all images to specified format (must be an a format supported by Hugo; "webp" requires Hugo Extended) |

## Examples

### Test Image #1 on the [DFD Responsive Images Demo Site](https://hugo-dfd-responsive-images.wildtechgarden.ca/)

#### Source
<https://github.com/danielfdickinson/hugo-dfd-responsive-images/blob/main/exampleSite/content/post/testimage1/index.md>

#### CSS

Which uses [the above CSS](#add-css-to-style-the-images) and ``imageConvertTo = "webp"`` in ``config.toml``

#### The Result

<https://hugo-dfd-responsive-images.wildtechgarden.ca/post/testimage1/>
