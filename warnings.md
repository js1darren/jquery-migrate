
# jQuery Compat Plugin - Warning Messages

To allow developers to identify and fix compatibility issues, the development (uncompressed) version of the plugin generates console warning messages whenever any of its functionality is used. The messages only appear once on the console for each unique message. In most cases they are simply _warnings_ and the code should continue to work properly when the jQuery Compat plugin is used.

**The production (compressed) version of the plugin does not generate these warnings.** To continue using jQuery code that has compatibility issues without making any changes, simply use the production version. See the [README](README.md) for download instructions.

The warnings, causes, and remediation instructions are listed below.

### JQCOMPAT: jQuery.attrFn is deprecated

**Cause:** Prior to jQuery 1.8, the undocumented `jQuery.attrFn` object provided a list of properties supported by the `$(html, props)` method. It is no longer required as of jQuery 1.8, but some developers "discovered" it by reading the source and began to use it. Their code still expects `jQuery.attrFn` to be present, attempts to assign values to it, and will throw errors if it is not present.

**Solution:** Ensure that you are using the latest version of jQuery UI (1.8.21 or later) and jQuery Mobile (1.2.1 or later); they no longer use `jQuery.attrFn`. Examine any third-party plugins for the string `attrFn` and report its use to the plugin authors (not to jQuery team).

### JQCOMPAT: jQuery is not compatible with Quirks Mode

**Cause:** A browser runs in "quirks mode" when the HTML document does not have a `<!doctype ...>` as its first non-blank line, or when the doctype in the file is invalid. This mode causes the browser to emulate 1990s-era (HTML3) behavior. In Internet Explorer, it also causes many high-performance APIs to be hidden in order to better emulate ancient browsers. jQuery has never been compatible with, or tested in, quirks mode.

**Solution:** Put a [valid doctype](http://www.w3.org/QA/2002/04/valid-dtd-list.html) in the document and ensure that the document is rendering in standards mode. The simplest valid doctype is the HTML5 one, which we highly recommend: `<!doctype html>` .

### JQCOMPAT: jQuery.browser is deprecated

**Cause:** `jQuery.browser` was deprecated in version 1.3, and finally removed in 1.9. Browser sniffing is notoriously unreliable as means of detecting whether to implement particular features. 

**Solution:** Use feature sniffing to make code decisions rather than trying to detect a specific browser. The [Modernizr](http://modernizr.com) library provides a wide variety of feature detections. As a last resort, you can directly look at the `navigator.userAgent` string to detect specific strings returned by the browser.

### JQCOMPAT: jQuery.sub() is deprecated

**Cause:** The `jQuery.sub()` method provided an imperfect way for a plugin to isolate itself from changes to the `jQuery` object. Due to its shortcomings, it was deprecated in version 1.8 and removed in 1.9.

**Solution:** Rewrite the code that depends on `jQuery.sub()`, use the minified production version of the jQuery Compat plugin to provide the functionality, or extract the `jQuery.sub()` method from the plugin's source and use it in the application.

### JQCOMPAT: 'hover' pseudo-event is deprecated, use 'mouseenter mouseleave'

**Cause:** Until jQuery 1.9, the string "hover" was allowed as an alias for the string "mouseenter mouseleave" when attaching an event handler. This unusual exception provided no real benefit and prevented the use of the name "hover" as a triggered event. _Note: This is not related to the `.hover()` _method_, which has not been deprecated._

**Solution:** Replace use of the string "hover" with "mouseenter mouseleave" within any `.on()`, `.bind()`, `.delegate()`, or `.live()` event binding method.

### JQCOMPAT: jQuery.fn.error() is deprecated

**Cause:** The `$().error()` method was used to attach an "error" event to an element but has been removed in 1.9 to reduce confusion with the `$.error()` method which is unrelated. It also serves to discourage the temptation to use `$(window).error()` which does not work because `window.onerror` does not follow standard event handler conventions.

**Solution:** Change any use of `$().error(function)` to `$().on("error", function)`.

### JQCOMPAT: jQuery.fn.toggle(handler, handler...) is deprecated

**Cause:** There are two completely different meanings for the `.toggle()` method. The use of `.toggle()` to show or hide elements is _not_ affected. The use of `.toggle()` as a specialized click handler was deprecated in 1.8 and removed in 1.9. 

**Solution:** Rewrite the code that depends on `$().toggle()`, use the minified production version of the jQuery Compat plugin to provide the functionality, or extract the `$().toggle()` method from the plugin's source and use it in the application. 

### JQCOMPAT: jQuery.fn.live() is deprecated; jQuery.fn.die() is deprecated

**Cause:** The `.live()` and `.die()` methods were deprecated in 1.7 due to their [performance and usability drawbacks](http://api.jquery.com/live), and are no longer supported. 

**Solution:** Rewrite calls to `.live()` using `.on()` or `.delegate()`. 



