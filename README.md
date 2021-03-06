# webextensions-lib-l10n

Provides ability to localize your HTML file with i18n messages.

## Required permissions

This does not require any special permission.

## Basic usage

In `manifest.json`, specify to load the file `l10n.js` for your HTML pages:

```json
{
  "default_locale": "en_US",
  "options_ui": {
    "page": "path/to/options.html",
    "chrome_style": true
  }
}
```

`options.html` is:

```html
<!DOCTYPE html>

<script type="application/javascript" src="./l10n.js"></script>

<p title="__MSG_config_enabled_tooltip__">
  <label><input type="checkbox">
         __MSG_config_enabled_label__</label></p>
<p title="__MSG_config_advanced_tooltip__">
  <label><input type="checkbox">
         __MSG_config_advanced__</label></p>
<p title="__MSG_config_attributes_tooltip__">
  <label>__MSG_config_attributes_label_before__
         <input type="text">
         __MSG_config_attributes_label_after__</label></p>
```

`_locales/en_US/messages.json` is:

~~~json
{
  "config_enabled_label":           { "message": "Activate basic features" },
  "config_enabled_tooltip":         { "message": "This is for general users." },
  "config_advanced_label":          { "message": "Activate advanced features" },
  "config_advanced_tooltip":        { "message": "This is for power users." },
  "config_attributes_label_before": { "message": "List of attributes:" },
  "config_attributes_label_after":  { "message": "" }}
  "config_attributes_tooltip":      { "message": "You can specify mutlipe items delimited with \"|\"." }
}
~~~

Then, after the options page is loaded all texts in the document like `__MSG_*__` are filled with messages defined in locales.

## Advanced usage

This library has a method to resolve `__MSG_*__` text labels in the document at any time. For example, labels generated by [webextensions-lib-shortcut-customize-ui](https://github.com/piroor/webextensions-lib-shortcut-customize-ui) are appear in a form like this. In such case, you just need to execute `l10n.updateDocument();` after those labels are embedded to the document.

```javascript
ShortcutCustomizeUI.build().then(list => {
  document.getElementById('shortcuts').appendChild(list);
  l10n.updateDocument(); // resolve labels after initialized!
});
```
