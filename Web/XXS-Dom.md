---
title: "DOM-based cross-site scripting"
permalink: /XXS-Dom/
layout: single
author-profile: true
---

DOM-based XSS (also known as DOM XSS) arises when an application contains some client-side JavaScript that processes data from an untrusted source in an unsafe way, usually by writing the data back to the DOM.

In the following example, an application uses some JavaScript to read the value from an input field and write that value to an element within the HTML:
```
var search = document.getElementById('search').value;
var results = document.getElementById('results');
results.innerHTML = 'You searched for: ' + search;
```
If the attacker can control the value of the input field, they can easily construct a malicious value that causes their own script to execute:

You searched for: ``<img src=1 onerror='/* Bad stuff here... */'>``

In a typical case, the input field would be populated from part of the HTTP request, such as a URL query string parameter, allowing the attacker to deliver an attack using a malicious URL, in the same manner as reflected XSS.

## What is DOM-based cross-site scripting?
DOM-based XSS vulnerabilities usually arise when JavaScript takes data from an attacker-controllable source, such as the URL, and passes it to a sink that supports dynamic code execution, such as `eval() or innerHTML`. This enables attackers to execute malicious JavaScript, which typically allows them to hijack other users' accounts.

To deliver a DOM-based XSS attack, you need to place data into a source so that it is propagated to a sink and causes execution of arbitrary JavaScript.

The most common source for DOM XSS is the URL, which is typically accessed with the window.location object. An attacker can construct a link to send a victim to a vulnerable page with a payload in the query string and fragment portions of the URL. In certain circumstances, such as when targeting a 404 page or a website running PHP, the payload can also be placed in the path.

For a detailed explanation of the taint flow between sources and sinks, please refer to the DOM-based vulnerabilities page.

## How to test for DOM-based cross-site scripting
The majority of DOM XSS vulnerabilities can be found quickly and reliably using Burp Suite's web vulnerability scanner. To test for DOM-based cross-site scripting manually, you generally need to use a browser with developer tools, such as Chrome. You need to work through each available source in turn, and test each one individually.

## Testing HTML sinks
To test for DOM XSS in an HTML sink, place a random alphanumeric string into the source (such as location.search), then use developer tools to inspect the HTML and find where your string appears. Note that the browser's "View source" option won't work for DOM XSS testing because it doesn't take account of changes that have been performed in the HTML by JavaScript. In Chrome's developer tools, you can use Control+F (or Command+F on MacOS) to search the DOM for your string.

For each location where your string appears within the DOM, you need to identify the context. Based on this context, you need to refine your input to see how it is processed. For example, if your string appears within a double-quoted attribute then try to inject double quotes in your string to see if you can break out of the attribute.

Note that browsers behave differently with regards to URL-encoding, Chrome, Firefox, and Safari will URL-encode location.search and location.hash, while IE11 and Microsoft Edge (pre-Chromium) will not URL-encode these sources. If your data gets URL-encoded before being processed, then an XSS attack is unlikely to work.

## Testing JavaScript execution sinks
Testing JavaScript execution sinks for DOM-based XSS is a little harder. With these sinks, your input doesn't necessarily appear anywhere within the DOM, so you can't search for it. Instead you'll need to use the JavaScript debugger to determine whether and how your input is sent to a sink.

For each potential source, such as location, you first need to find cases within the page's JavaScript code where the source is being referenced. In Chrome's developer tools, you can use Control+Shift+F (or Command+Alt+F on MacOS) to search all the page's JavaScript code for the source.

Once you've found where the source is being read, you can use the JavaScript debugger to add a breakpoint and follow how the source's value is used. You might find that the source gets assigned to other variables. If this is the case, you'll need to use the search function again to track these variables and see if they're passed to a sink. When you find a sink that is being assigned data that originated from the source, you can use the debugger to inspect the value by hovering over the variable to show its value before it is sent to the sink. Then, as with HTML sinks, you need to refine your input to see if you can deliver a successful XSS attack.

## Testing for DOM XSS using DOM Invader
Identifying and exploiting DOM XSS in the wild can be a tedious process, often requiring you to manually trawl through complex, minified JavaScript. If you use Burp's browser, however, you can take advantage of its built-in DOM Invader extension, which does a lot of the hard work for you.

## Exploiting DOM XSS with different sources and sinks
In principle, a website is vulnerable to DOM-based cross-site scripting if there is an executable path via which data can propagate from source to sink. In practice, different sources and sinks have differing properties and behaviour that can affect exploitability, and determine what techniques are necessary. Additionally, the website's scripts might perform validation or other processing of data that must be accommodated when attempting to exploit a vulnerability. There are a variety of sinks that are relevant to DOM-based vulnerabilities. Please refer to the list below for details.

The document.write sink works with script elements, so you can use a simple payload, such as the one below:

``document.write('... <script>alert(document.domain)</script> ...');``

### Example

Enter a random alphanumeric string into the search box.

Right-click and inspect the element, and observe that your random string has been placed inside an img src attribute.

Break out of the img attribute by searching for:

``"><svg onload=alert(1)>``

## Taking account of surrounding context

Note, however, that in some situations the content that is written to document.write includes some surrounding context that you need to take account of in your exploit. For example, you might need to close some existing elements before using your JavaScript payload.

### Example
1. On the product pages, notice that the dangerous JavaScript extracts a storeId parameter from the location.search source. It then uses document.write to create a new option in the select element for the stock checker functionality.
2. Add a storeId query parameter to the URL and enter a random alphanumeric string as its value. Request this modified URL.
3. In the browser, notice that your random string is now listed as one of the options in the drop-down list.
4. Right-click and inspect the drop-down list to confirm that the value of your storeId parameter has been placed inside a select element.
5. Change the URL to include a suitable XSS payload inside the storeId parameter as follows:

``product?productId=1&storeId="></select><img%20src=1%20onerror=alert(1)>``


