# CB Online Custom template page

Citybreak Online enables customization by offering the possibility to include a template page for header and footer. The template page is provided by setting an absolute URL to an HTML page containing a placeholder element where the Citybreak Online booking engine will be injected. This gives the user ability to use their own header and footer as well as other static resources such as style sheets and JavaScripts. 

**A responsive template page is strongly recommended as of 2016-06-01.**

INSERT IMAGE HERE


## Brief description

### Restrictions

1. **Valid HTML5 markup.** Online will parse the template page as HTML5 markup and it will therefore need to consist of valid HTML5 markup. The validity of the markup is determined by the tool we use for parsing, which is currently HtmlAgilityPack, but the markup can be validated with a tool such as the W3C validator using the HTML 5 doctype setting. The DOCTYPE is replaced or set by Online to <!DOCTYPE html>.
2. **No Online widgets** included in the header/footer template page. Loading an Online widget (via script) in the header/footer template page will cause serious conflicts and JavaScript errors. It is therefore not supported at this moment.
3. **No Google Analytics tracking scripts** (calls to _trackPageview, _trackEvent etc) are allowed in the template page. This would cause double page views.
4. **Contain a div element with id attribute set to ‘cb_init_bookingengine’.** This will be the placeholder where the Online booking engine will be injected.
5. **All meta tags except 'viewport' will be removed.**

### Optional functionality
Language select feature (if multiple languages are configured for the specific guide and a span with id attribute ‘cb_replace_languages_select’ is encountered).

### Features

1. Relative href/src rewriting.
2. Title inject from Citybreak.
3. Meta keyword inject
4. Meta description inject
5. Preserves CSS links and script references in original document.
6. Injects CSS links and scripts from Citybreak Online.
7. Possibly remove form tags if interfering with Citybreak Online.
8. Possibly remove VIEWSTATE hidden input field.


## Detailed description
This section will go into the details of how to create your external header footer.

### Error reporting
If something goes wrong during the creation of the header/footer include from Citybreak, the error will be reported as a .NET stack trace in a comment at the bottom of the HTML generated. The standard header footer of Citybreak Online will be used meanwhile.

### Features
#### Form tags
If a form tag is encountered in the header/footer include document that has a child element that defines special functionality for Online (such as the content div or language span, described below), the form will simply be removed and replaced by an HTML comment that states that the tag was removed. Form tags that do not interfere with Citybreak functionality will be preserved.

#### .NET Viewstate
If a hidden input field with the name attribute set to *‘__VIEWSTATE’* is encountered, it will be replaced with a comment stating the field was removed. If you are using .NET WebForms a form tag will most likely wrap the entire page. That form element will be removed (since it wraps all elements of the page, and we want to make sure that we don’t pass too much unnecessary data back and forth from the client to the server).

#### Citybreak Online content div

```html
<div id="cb_init_bookingengine"> 
     <h1>Booking engine goes here.</h1> 
</div>
```

The Citybreak Online will download the file, parse it, modify it as necessary and split the content in two parts: one header and one footer. You should define a div tag with the id attribute set to *‘cb_init_bookingengine’*  where you would like the Online content to be injected.

Everything within this div element will be ignored and replaced by the Online content. In this case will the h1 tag be ignored and the specific requested Online page will be inserted there instead. If this tag is omitted the header/footer has no meaning in the context of Online and will be dealt with according to section Error reporting.

#### Change language

```html
<span id="cb_replace_languages_select"></span> 
```

If the online guide implements more than one language, a change language control can be included into the header/footer document. Just include a span tag where you wish to insert the language change controls.

The id attribute must be the specific *‘cb_replace_languages_select’*. Everything in the span will be ignored and replaced with a form element which has some hidden fields as well as select box with available languages and an input type submit control. This will enable the user to change language and still end up at the same page as currently is viewed.

#### Title tag
The contents of the title tag will be replaced with a title appropriate for the CB Online page that is displayed. This title is generated from Online and can not be changed from the include file.

#### Relative href/src URL rewriting
All elements that have attributes named href or src will be tried to be rewritten in the context of the URL where the page was downloaded from. That is, Online will try to rewrite relative paths to absolute paths.

If the include file was found at http://somesite.com/templ/cb.htm and a tag in that document is defined as /css/base.css the tag will be rewritten to the definition http://somesite.com/css/base.css. It applies to all elements with the attribute href or src, meaning it applies to link tags, script tags, img tags etc, etc.

#### Meta keyword inject
If a specific page in Online defines specific keywords to be used, it will create a new meta tag with them. If a meta keywords tag already exists in the header/footer document, Online will append the specific keywords to it.

#### Meta description inject
If no meta description tag is defined on the page, Online will create one and append it to the document. If one exists in the include document, CB Online will append its own description to the tag.

#### Meta refresh
If meta refresh is defined on the include page, it will be removed. In rare cases Citybreak Online will define a refresh tag.

#### Meta content charset

```html
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
```

Online will remove all elements that define meta http-equiv and replace it with the following: 

#### Robots
If meta tags to hint robots are encountered they are preserved, except for pages that Citybreak Online defines as local. Those pages will be tagged as noindex, nofollow.

#### Head re-ordering
Citybreak Online will reorder the tags in the head. The elements will be rearranged according to 
this order:

1. Title element.
2. Meta tags.
3. Link definitions from header.
4. Citybreak Online link definitions.
5. Explicit style definition from header.
6. Script definitions from header.
7. Script definitions from Citybreak Online.
8. Content Script definitions.

#### Injected CSS classes
The Citybreak Online will inject class names on specific tags in the include file where applicable for styling purposes.


### Conventions used

#### CSS class names
To make it harder for CSS class names to interfere, the Citybreak Online team preambles all its internal CSS classes with either ‘Citybreak’ or ‘cb_’.

#### CSS web fonts
When using custom fonts in the header/footer template, access must be granted for your Online sub-domain. This applies to both 3rd party services such as Typekit, as well as hosted fonts declared via @font-face CSS rules.

#### jQuery
Citybreak Online uses the jQuery JavaScript library. The specific jQuery handle is called ‘citybreakjq’ and should never be interfered with.
