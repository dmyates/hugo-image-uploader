# Hugo Image Uploader

A Hugo theme component that leverages [image render hooks](https://gohugo.io/render-hooks/images/) to provide drag-and-drop image upload functionality in development mode. See [this blog post](https://davidyat.es/2024/10/19/render-hook-image-upload/) for more about the development and rationale behind it.

## Usage

Video demonstration:

https://github.com/user-attachments/assets/c0a276b2-f475-4d96-9055-85f732d905f1

When your site is in development mode, image tags with empty paths (`![]()`/`![alt text]()`) will be rendered as partially transparent image drop boxes. Drag an image file onto the box, and it will be uploaded to `static/content/images/YYYY/MM/` in your site directory. The image will be temporarily displayed over the upload box and its path will be copied to the clipboard -- paste it into the original Markdown.

## Installation

Requires `hugo` and `nodejs`.

1. Add the theme component to your Hugo site:
   ```bash
   git clone https://github.com/dmyates/hugo-image-uploader.git themes/hugo-image-uploader
   ```
2. Add the theme to your site's `config.toml`:
   ```toml
   theme = ["your-main-theme", "hugo-image-uploader"]
   ```
3. Include the script partial in your main template (e.g., `layouts/_default/baseof.html`):
   ```html
   {{ partial "image-upload-script.html" . }}
   ```
4. Move `uploader.js` and `hugoserverwithuploader.sh` to your site's base directory:
   ```bash
   mv uploader.js ../../
   mv hugoserverwithuploader.sh ../../
   ```
5. `hugoserverwithuploader.sh` wraps `hugo server` and the NodeJS image upload server. Run it to start both. Arguments passed to this script will be forwarded to `hugo server`. For example:
   ```bash
   ./hugoserverwithuploader.sh
   ./hugoserverwithuploader.sh --buildDrafts --buildFuture
   ```

Manage the dependency with [Hugo Modules](https://gohugo.io/hugo-modules/use-modules/) or [Git Submodules](https://github.blog/open-source/git/working-with-submodules/). Alternatively, `rm -rf .git` and include it with your site repo, as you will probably want to change my code.

## Customisation

* To change the appearance of the upload box or the directory to which images should be uploaded, edit or override the `image-upload-control.html` partial. 
* To change what file types are accepted, edit `uploader.js`.

## Potential future work

If any of these catch your fancy, feel free to submit a PR:

* Visual feedback to confirm that the image path has been copied to the clipboard.
* Support for saving images to page bundles.
* Processing of image uploads (compression, conversion, etc).
* Image uploads from a file picker.
