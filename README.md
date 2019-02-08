# A by no means exhaustive inclusive design checklist

## Useful tools

- The [tota11y bookmarklet](http://khan.github.io/tota11y/) shows:

    - a breakdown of heading levels used on a page
    - colour contrast for all text/background colour combinations and highlights elements with insufficient contrast
    - links that may be confusing when read by a screen reader
    - inputs with missing labels
    - images without alt text
    - ARIA landmarks

- [Google PageSpeed insights](https://developers.google.com/speed/pagespeed/insights/) gives you suggestions for optimisations you can apply to your website to improve real-world performance.

- [a11y.css](https://ffoodd.github.io/a11y.css/) is a CSS file you can load via a bookmarklet to detect common risks and mistakes that exist in HTML code.

- [Pa11y](https://github.com/pa11y/pa11y) is a JavaScript tool (with a command-line interface) that can be used to automatically test a given URL for accessability issues. [It's also available as a standalone app](https://open-indy.github.io/Koa11y/).

## Accessibility

1. Has a language Attribute been specified?

    - Declaring a language attribute on the html element enables a screen reader to read out the text with correct pronunciation.
        ``` html
        <html lang="en-GB">
        ```

    - If there are subsections in different languages, use the `lang="[ISO code]"` attribute on the containing element to indicate this.

2. Support "pinch zoom"

    - Remove `user-scalable=no` if present in the following meta tag:
        ``` html
        <meta name="viewport" content="width=device-width, initial-scale=1">
        ```

3. Make sure heading levels describe a logical section/subsection structure

    - Headings should cascade from h1 downward and should only be used to introduce sections of content.

    - Do not mark up subheadings/straplines with separate heading elements.

4. Provide alternative text for images that require it

    - Apply `alt=""` or `aria-hidden="true"` to images that are purely decorative or contain content that is already conveyed in text.
    - Describe the image as specifically as possible, whilst keeping it short and succinct.
    - Don’t include  ‘Image of ’ or ’Picture of’ in your alt text—a screen reader will announce this by default.

5. Are all interactive elements visible and keyboard-accessible?

    - This includes links, buttons, audio and video controls, as well as any type of form input (input, textarea, select)

    - Ensure all interactive elements have a clear, unambiguous `:focus` state, preferrably different from the `:hover` state. If removing the browser-default focus outline, an alternative is required.

    - Links should have `text-decoration: underline;` (at least in body copy) and colour should be used as a redundant cue. i.e. not the sole indicator that an element is a link.

6. Does all text meet the minimum contrast ratio?

    - For **AA**, text and images of text have a contrast ratio of at least 4.5:1. Large text, 24px or 18.66px bold, has a contrast ratio of at least 3:1.

    - For **AAA**, text and images of text have a contrast ratio of at least 7:1. Large text, 24px or 18.66px bold, has a contrast ratio of at least 4.5:1.

7. Is site still usable when zoomed in?

    - Make sure every feature can be used when text size is increased to 200%.

8. Is all text of a legible size?

    - Make sure body text is no smaller than default (user agent) size — usually 16px.

    - Avoid very thin font weights - check rendering across browsers and operating systems.

9. Are forms accessible?

    - Field order should follow the DOM

    - All form elements should have permanently visible labels, linked either by wrapping the input itself or using the `for=""` attribute matching the id of the input.

    - Group related form elements (e.g. radio and checkbox) inside a fieldset and describe the group with a legend.

    - Required form elements or form elements that require a specific format, value, or length should provide this information within the element’s label.

    - Any 'help text' that is not part of a label, should be linked by adding the id of the help text element as the `aria-describedby=""` attribute on the input.

    - If there is an asterisk used to denote ‘required’ inputs, there should be a sentence that explains this e.g. "Form fields marked with an asterisk are required".

    - All error / validation messages on the form should be listed above the form with anchor links to the fields producing the errors below.

    - If the user can change or delete important data, the changes/deletions should need verification/confirmation.

## Performance

1. Minify CSS, JS and SVGs and remove any unused/redundant code.

    - Ensure your build process is correctly set up to minify assets

    - Make sure all compiled CSS and JS only contains code that is used on the site — remove any components/features that are not.

2. Remove render-blocking JavaScript

    - This forces the browser to wait for the JavaScript to be fetched, which may slow down page rendering. If they are small they can be included directly in the HTML document.

3. Don’t force the user to download images that are unnecessarily large.

    - For img elements, instead use the picture element and `srcset` attribute to tailor images to the size they will be displayed.

    - For background images, use media queries to load an appropriately sized version of the image at different media queries.

    - Use 'Next-Gen' image formats like WebP if the target browser supports them. Some CDN providers offer support detection as part of their service.

4. Lazy-load non-critical resources

    - For CSS, use a tool like [Critical](https://github.com/addyosmani/critical) to determine the _critical_ styles needed to render only “above-the-fold” content. These can then be inlined directly into the `<head>` of your pages to drastically speed up the initial render.

5. Speed up server response time

    - Enable gzip compression
    - Use the most up-to-date compatible PHP version
    - Set the site to use PHP FPM, if available

6. Optimise your use of web fonts
    - Keep the number of different web fonts loaded low and even consider using system fonts instead unless completely necessary
    - **woff** and **woff2** are the most efficient file formats for web fonts. If you're using font-face rules in your CSS, ensure these appear before formats such as ttf, as the browser will use the first one it understands. Using the following example, modern browsers will use the **woff2** font, as they do not support eot fonts.
        ```css
        @font-face {
            font-family: 'MyWebFont';
            src: url('webfont.eot'); /* IE9 Compat Modes */
            src: url('webfont.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
                url('webfont.woff2') format('woff2'), /* Super Modern Browsers */
                url('webfont.woff') format('woff'), /* Pretty Modern Browsers */
                url('webfont.ttf')  format('truetype'), /* Safari, Android, iOS */
                url('webfont.svg#svgFontName') format('svg'); /* Legacy iOS */
        }
        ```
        Note: eot, ttf and svg are only required for older browsers. For most cases, the following will be sufficient:
        ```css
        @font-face {
            font-family: 'MyWebFont';
            src: url('myfont.woff2') format('woff2'),
                url('myfont.woff') format('woff');
        }
        ```

## References

- https://github.com/Heydon/inclusive-design-checklist
- https://webaim.org/standards/wcag/checklist