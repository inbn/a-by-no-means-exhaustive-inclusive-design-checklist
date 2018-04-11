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

## Accessibility

1. Has a language Attribute been specified?

    - Declaring a language attribute on the html element enables a screen reader to read out the text with correct pronunciation.
        ``` html
        <html lang="en-GB">
        ```

    - If there are subsections in different languages, use `lang="[ISO code]"` to indicate this.

2. Support "pinch zoom"

    - Remove `user-scalable=no` if present in the following meta tag:
        ``` html
        <meta name="viewport" content="width=device-width, initial-scale=1">
        ```

3. Make sure heading levels describe a logical section/subsection structure

    - Headings should cascade from h1 downward and should only be used to introduce sections of content.

    - Do not mark up subheadings/straplines with separate heading elements.

4. Provide alternative text for salient images

    - Apply `alt=""` or `aria-hidden="true"` to images that are purely decorative or contain content that is already conveyed in text.

5. Are all links visible and keyboard-accessible?

    - Links should have `text-decoration: underline` (at least in body copy)

    - Ensure all links have a clear, unambiguous `:focus` state

6. Does all text meet the minimum contrast ratio?

    - For **AA**, text and images of text have a contrast ratio of at least 4.5:1. Large text, 24px or 18.66px bold, has a contrast ratio of at least 3:1.

    - For **AAA**, text and images of text have a contrast ratio of at least 7:1. Large text, 24px or 18.66px bold, has a contrast ratio of at least 4.5:1.

8. Is site still usable when zoomed in?

    - Make sure every feature can be used when text size is increased by 200%

7. Is all text of a legible size?

    - Make sure body text is no smaller than default (user agent) size — usually 16px.

    - Avoid very thin font weights - check rendering across browsers and operating systems.

9. Are forms accessible?

    - Field order should follow the DOM

    - All form elements should have permanently visible labels, linked either by wrapping the input itself or using the `for=""` attribute matching the id of the input.

    - Group related form elements (e.g. radio and checkbox) inside a fieldset and describe the group with a legend.

    - Required form elements or form elements that require a specific format, value, or length should provide this information within the element's label.

    - Any 'help text' that is not part of a label, should be linked to input by adding the id of the help text element in input's `aria-describedby=""` attribute.

    - If we use an asterisk to denote ‘required’ we should have a sentence that explains this e.g. Form fields marked with a red asterisk are required.

    - All error / validation messages on the form should be listed above the form with anchor links to the fields producing the errors below.

    - If the user can change or delete important data, the changes/deletions should need verification/confirmation.

## Performance

1. Minify CSS, JS and SVGs and remove any unused/redundant code.

    - Ensure your build process is correctly set up to minify assets

    - Make sure all compiled CSS and JS only contains code that is used on the site — remove any components/features that are not.

2. Remove render-blocking JavaScript

    - These force the browser to wait for the JavaScript to be fetched, which may slow down page rendering. If they are small they can be included directly in the HTML document.

3. Don't force the user to download images that are unnecessarily large.

    - For img elements, instead use the picture element and `srcset` to tailor images to the size they will be displayed.

    - For background images, use media queries to load multiple versions of the image at different media queries.

4. Speed up server response time

    - Enable gzip compression
    - Use the most up-to-date compatible PHP version
    - Set the site to use PHP FPM, if available
    - Wrap complex for loops in `{% cache %}` tags *(Craft-specific)*


## References

- https://github.com/Heydon/inclusive-design-checklist
- https://webaim.org/standards/wcag/checklist