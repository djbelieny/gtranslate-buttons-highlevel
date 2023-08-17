# Custom Google Translate Integration for GoHighlevel

This guide will help you integrate a custom Google Translate functionality into your GoHighlevel funnel or site. Instead of using the default Google Translate widget, we're providing a custom solution that allows users to translate the site using dedicated buttons.

## Features:

1. Custom translation buttons for English, Portuguese (Brazil), and Spanish.
2. Hidden default Google Translate bar for a cleaner look.
3. Translation-proof buttons: The custom buttons won't be translated, ensuring consistent labels.

## How It Works:

1. **Custom Translation Buttons**: Three buttons are provided. Clicking on any of these buttons will trigger the translation of the site to the respective language. These buttons have a `notranslate` class to prevent them from being translated by Google Translate.
2. **Hidden Google Translate Bar**: The default Google Translate bar (`#\:1.container`) is programmatically hidden to provide a cleaner user experience.

## Integration Steps:

### 1. Add the Custom HTML/JavaScript Block:

In GoHighlevel, wherever you want the translation buttons to be displayed, add a custom HTML/JavaScript block. Then, paste the following code into the block:

```html
<!-- Custom html/javascript to add buttons and translate funciton -->
<!-- Copy this into a custom code block inside your GHL site/funnel -->

<div id="custom_translate_buttons">
    <button class="notranslate" onclick="translateTo('es')">Español</button>
    <button class="notranslate" onclick="translateTo('en')">English</button>
    <button class="notranslate" onclick="translateTo('pt')">Português</button>
</div>
<div id="google_translate_element" style="display: none;"></div>


<script type="text/javascript">
    function googleTranslateElementInit() {
        new google.translate.TranslateElement({ pageLanguage: 'pt' }, 'google_translate_element');
    }

    function hideGoogleTranslateBar() {
        var element = document.querySelector("#\\:1\\.container");
        if (element) {
            element.style.visibility = "hidden";
        }
    }

    hideGoogleTranslateBar();

    function translateTo(language) {
        var selectField = document.querySelector("select.goog-te-combo");
        if (selectField) {
            selectField.value = language;
            selectField.dispatchEvent(new Event('change'));
            setTimeout(hideGoogleTranslateBar, 100);
        }
    }

</script>

<script type="text/javascript"
    src="//translate.google.com/translate_a/element.js?cb=googleTranslateElementInit"></script>
```

### 2. Add the CSS:

Include the provided CSS in the `<head>` section of your GoHighlevel site or funnel to style the custom translation buttons and hide the default Google Translate bar.

```css
/*Translation CSS*/
/* Copy this at the end of your custom CSS section in your funnel/site */
/* Hide the outer container of the Google Translate toolbar */
.goog-te-banner-frame.skiptranslate {
    display: none !important;
    visibility: hidden !important;
    height: 0 !important;
}

#custom_translate_buttons {
    position: relative;
    z-index: 1000;
    padding: 10px 0;
    text-align: center;
}

#custom_translate_buttons button {
    padding: 5px 15px;
    margin: 0 5px;
    border: none;
    border-radius: 10px;
    font-family: var(--montserrat);
    background-color: #c69009;
    color: #000;
    cursor: pointer;
}

#custom_translate_buttons button:hover {
    background-color: #45a049;
}

/* Adjust the body top margin (change 0px to your site's original top margin if it's not 0) */
body {
    top: 0px !important;
}
```

### 3. Test the Functionality:

- Visit your GoHighlevel site or funnel.
- Use the custom translation buttons to translate the site. The button labels should remain consistent regardless of the current translation state of the page.

## Notes:

- Ensure that the provided JavaScript and CSS are correctly integrated into your GoHighlevel site or funnel.
- Adjust the CSS styles if needed to match your site's design.
- The translations are powered by Google Translate. While they are generally accurate, they might not always be perfect. Consider having native speakers review translations if accuracy is critical.
- The custom translation buttons are not translated by Google Translate. This ensures that the button labels remain consistent regardless of the current translation state of the page.
