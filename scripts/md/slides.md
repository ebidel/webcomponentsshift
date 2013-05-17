title: Who is this guy?
id: who

<p class="avatar rounded"></p>

<p>Eric Bidelman</p>
<p>Staff Developer Programs Engineer, <img src="images/logos/google_logo.png" style="height: 30px;margin: 0;"> <img src="images/logos/chrome_logo.png" style="height:27px;margin:0;vertical-align: top;"></p>

<hr>

<p>
  <a rel="author" href="http://google.com/+EricBidelman">
    <img src="http://www.google.com/images/icons/ui/gprofile_button-44.png" width="44" height="44"></a> <a rel="author" href="http://google.com/+EricBidelman">google.com/+EricBidelman</a>
</p>
<p style="margin:0;">
  <a rel="author" style="margin-left:-8px;" href="http://twitter.com/ebidel">
    <img src="images/logos/twitter_newbird_blue.png" width="58" height="58"></a> <a rel="author" href="http://twitter.com/ebidel" style="margin-left:-5px;">@ebidel</a>
</p>

<hr>

<p style="margin-top:10px;">
<img src="images/logos/h5rlogo.png" style="width: 50px;"><a href="http://html5rocks.com">html5rocks.com</a>
</p>

"[Using the HTML5 Filesystem API](http://www.amazon.com/Using-HTML5-Filesystem-Eric-Bidelman/dp/1449309453 )" - O'Reilly 

<a rel="author" href="http://www.ericbidelman.com">ericbidelman.com</a>

---
class: futureweb large
content_class: flexbox vcenter centered

<h2 class="auto-fadein">I have <b class="yellow">40 min</b> to cover the <b class="green">entire</b> future web <b class="blue">platform</b> <span>:(</span></h2>

<div class="fail build">
  <h2>FAIL</h2>
</div>

---

class: nobackdrop nobackground
content_class: flexbox vcenter centered animatedfull

<img src="images/gifs/slowmowaterballoon.gif" class="rounded reflect">

---

class: nobackdrop nobackground
content_class: flexbox vcenter centered animatedfull

<img src="images/gifs/awwwyeah.gif" class="rounded reflect">

---

class: large
content_class: flexbox vcenter centered

<h2 class="auto-fadein">Web Components?</h2>

---
content_class: flexbox vcenter centered

<iframe data-src="http://html5-demos.appspot.com/static/webcomponents/demos/components/my-components/blink/blink.html" style="height:160px;border:none"></iframe>

<span class="source"><s>[Dead](https://www.w3.org/Bugs/Public/show_bug.cgi?id=21712)</s>?</span>

---
content_class: flexbox vcenter centered

<p class="centered">
  <code class="prettyprint custom-element-snippet">&lt;gangnam-style>&lt;/gangnam-style></code>
</p>

<iframe data-src="http://html5-demos.appspot.com/static/webcomponents/demos/components/my-components/gangnam.html" style="height:170px;border:none"></iframe>

---

content_class: flexbox vcenter centered

<p class="centered">
  <code class="prettyprint custom-element-snippet" style="font-size:35px">&lt;button is="mega-button">Mega button&lt;/button></code>
</p>

<iframe data-src="http://html5-demos.appspot.com/static/webcomponents/demos/components/my-components/mega-button/megabutton.html" style="height:380px;width:380px;border:none"></iframe>

---

title: Building blocks of Web Components
build_lists: true

- [Shadow DOM](https://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/shadow/index.html) - *mortar/glue*
    - DOM &amp; style encapsulation boundaries
- [HTML Templates](http://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/templates/index.html) - *scaffold/blueprint*
    - inert chunks of clonable DOM. Can be activated for later use (e.g. MDV)
- [Custom Elements](https://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/custom/index.html) - *toolbelt*
    - create new HTML elements - expand HTML's existing vocabulary
    - extend existing DOM objects with new imperative APIs
- [HTML Imports](https://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/imports/index.html)

<p class="centered build" style="margin-top:2em;font-size:35px;font-style:italic;">
  <span class="green"><b>A collection of new API primitives in the browser</b></span>
</p>

---

class: nobackdrop nobackground yum
content_class: flexbox vcenter centered

<h2 class="auto-fadein" style="font-size:100px">HTML Templates</h2>

---

hidden: true
id: template-segue
title: HTML Templates
class: segue nobackground highlight fill
image: images/bgs/drinksblueprint.jpg

---

title: Declaring HTML templates
#subtitle: <code>&lt;template&gt;</code>
spec_link: http://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/templates/index.html
build_lists: true

Contains inert chunks of markup intended to be used later:

<pre class="prettyprint" data-lang="html">
<b>&lt;template id="mytemplate"></b>
  &lt;img src=""> &lt;!-- dynamically populate at runtime -->
  &lt;div class="comment">&lt;/div>
<b>&lt;/template></b>
</pre>

1. <label class="good"></label> Working directly w/ DOM
- <label class="good"></label> Parsed; not rendered
    - `<script>` not run, stylesheets/images not loaded, media not played
- <label class="good"></label> Hidden from document. Cannot traverse into its DOM
    - e.g. `document.querySelector('#mytemplate .comment') == null`

---

title: Using template content

Two ways to access the guts:

1. `template.content` (a document fragment)
- `template.innerHTML`

<p class="centered">Clone <code>.content</code> &rarr; stamp it out &rarr; goes "live"</p>

<pre class="prettyprint" data-lang="html">
&lt;template id="mytemplate">
  &lt;img src="">
  &lt;div class="comment">&lt;/div>
&lt;/template>
&lt;script>
  var t = document.querySelector('#mytemplate');
  <b>t.content.querySelector('img').src = 'logo.png';</b> // Populate the src at runtime.
  document.body.appendChild(<b>t.content.cloneNode(true)</b>);
&lt;/script>
</pre>

---

id: template-demo
title: Demo
content_class: code-example html

<pre class="prettyprint" data-lang="html" data-run-demo>
<b>&lt;template></b>
  &lt;span>Instance: &lt;b>0&lt;/b>&lt;/span>
  &lt;script>alert('kthxbai!')&lt;/script>
<b>&lt;/template></b>
&lt;button onlclick="useIt()">Stamp&lt;/button>
&lt;script>
  function useIt() {
    <b>var content = document.querySelector('template').content;</b> // 1. Get guts.

    var b = <b>content.querySelector('b')</b>;
    b.textContent = parseInt(b.textContent) + 1; // 2. Modify template's DOM at runtime.

    document.body.appendChild(<b>content.cloneNode(true)</b>); // 3. Clone to stamp it out.
  }
&lt;/script>
</pre>

<template>
  <div>Instance: <b>0</b></div>
  <script>
  // Don't want browsers that don't support template to run this.
  // Also, FF seems to run <script> even though it's supposed to be inert until use.
  if ('HTMLTemplateElement' in window) {
    if (!navigator.userAgent.match('Firefox')) {
      alert('kthxbai!');
    }
  }
  </script>
</template>
<output></output>

---

title: HTML Templates
subtitle: browser support
class: nobackdrop nobackground browser-support
content_class: flexbox vcenter

<div class="browser-support-row">
  <div><img src="images/logos/browsers/safari_logo.png"></div>
  <div class="mobile supported"><img src="images/logos/browsers/ff_nightly.png"></div>
  <div class="mobile supported"><img src="images/logos/chrome_logo.png"></div>
  <div class="mobile"><img src="images/logos/browsers/opera_logo.png"></div>
  <div><img src="images/logos/browsers/ie10_logo.png"></div>
</div>

---

title: Building blocks of Web Components
class: checkbox

<span class="auto-fadein"><img src="images/icons/checkcircle.svg" class="checkbox"></span> HTML Templates

<span class="spacer">Shadow DOM</span>

<span class="spacer">Custom Elements</span>

<span class="spacer">HTML Imports</span>


---

class: nobackdrop nobackground yum shadow
content_class: flexbox vcenter centered

<h2 class="auto-fadein"><img src="images/logos/incognito.jpg" height="90" width="90" class="rounded" alt="Shadow DOM Dude" title="Shadow DOM Dude"> DOM</h2>

---

class: nobackground highlight fill
image: images/bgs/shadowdom-car-front.jpg

---

content_class: flexbox vcenter quote

<div>
<img src="images/logos/incognito.jpg" height="140" width="140" class="rounded" style="box-shadow:1px 3px 7px #aaa;float:right;" alt="Shadow DOM Dude" title="Shadow DOM Dude">
<blockquote>
  Shadow DOM gives us <span class="green">markup encapsulation</span>, <span class="red">style boundaries</span>, and exposes (to web developers) the same <span class="blue">mechanics browsers vendors have been using</span> to implement their internal UI.
</blockquote>
</div>

<div class="author">
  <span>-<a href="http://google.com/+EricBidelman">me</a></span>
</div>

---

id: web-has-encapsulation
title: The web has encapsulation...
class: large
content_class: flexbox vcenter centered

<h2 class="build" style="margin-top:-1em;"><code>&lt;iframe&gt;</code></h2>

<div class="fail build">
  <h2>BLOATED</h2>
</div>

---

title: But there's more lurking in the shadows...
build_lists: true

- <span class="green"><em>Truth #1</em></span>: DOM nodes can already "host" hidden DOM
- <span class="green"><em>Truth #2</em></span>: The hidden DOM can't be accessed from outside JS

<p class="build centered" style="zoom:2">
<input type="date" /> <input type="time">
</p>
<p class="build centered" style="font-size:35px;margin-top:-20px">
  <code>&lt;input type="date"&gt;</code> <code>&lt;input type="time"&gt;</code>
</p>

- Other examples: <code>&lt;video&gt;</code> <code>&lt;textarea&gt;</code> <code>&lt;details&gt;</code>

<p class="topmargin centered build red" style="font-size:35px;font-style:italic;"><b>Browser vendors have been holding out on us!</b></p>

---

hidden: true
id: shadow-dom-host
title: Attaching Shadow DOM to a host
spec_link: http://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/shadow/index.html
content_class: flexbox vcenter centered

<img src="images/shadow/shadow-trees.svg" style="height: 100%;">

---

hidden: true
id: shadow-dom-render
title: Shadow tree is rendered instead
spec_link: http://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/shadow/index.html
content_class: flexbox vcenter centered

<img src="images/shadow/shadow-rendering.svg" style="height:100%;">

<div class="devtools" title="click me" alt="click me"></div>

---

id: shadow-dom-creating
title: Creating Shadow DOM
spec_link: http://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/shadow/index.html#extensions-to-element
h5r_link: http://www.html5rocks.com/tutorials/webcomponents/shadowdom/

<aside class="note">
  <section>
    <img src="images/shadow/shadow-rendering.svg" style="width: 100%;">
  </section>
</aside>

<div class="cols">
<pre class="prettyprint" data-lang="Logical DOM">
&lt;div id="host">
  &lt;h1>My Title&lt;/h1>
  &lt;h2>My Subtitle&lt;/h2>
  <span style="white-space: nowrap;">&lt;div>...other content...&lt;/div></span>
&lt;/div>
</pre>

<pre class="prettyprint" data-lang="Composed tree">
&lt;div id="host">
  <span style="opacity:0.5">#document-fragment</span>
    &lt;h2>Yo, you got replaced!&lt;/h2>
    &lt;div>by my awesome content&lt;/div>
&lt;/div>
</pre>
</div>

<pre class="prettyprint" data-lang="js" style="clear:both">
var host = document.querySelector('#host');
<b>var shadow = host.<a data-tooltip-property="createShadowRoot" data-tooltip-support='["webkit"]' data-tooltip-js>createShadowRoot</a>();</b>
<b>shadow.innerHTML = '&lt;h2>Yo, you got replaced!&lt;/h2>' +
                   '&lt;div>by my awesome content&lt;/div>';</b>
</pre>

<div class="host">
  <h1>My Title</h1>
  <h2>My Subtitle</h2>
  <div>...other content...</div>
</div>

<script>
(function() {
var shadow = document.querySelector('#shadow-dom-creating .host').createShadowRoot();
shadow.innerHTML = '<h2>Yo, you got replaced!</h2>' +
                   '<div>by my awesome content</div>';
})();
</script>

---

hidden: true
id: shadow-dom-style-encapsulation
title: Style encapsulation
h5r_link: http://www.html5rocks.com/en/tutorials/webcomponents/shadowdom-201/

<aside class="note">
  <section>
    <img src="images/shadow/shadow-rendering.svg" style="width: 100%;">
  </section>
</aside>

Styles defined in a `ShadowRoot` are scoped by default.

<pre class="prettyprint" data-lang="js">
var shadow = document.querySelector('#host').<a data-tooltip-property="createShadowRoot" data-tooltip-support='["webkit"]' data-tooltip-js>createShadowRoot</a>();
shadow.innerHTML = '<b>&lt;style>h2 { color: red; }&lt;/style></b>' + 
                   '&lt;h2>Yo, you got replaced!&lt;/h2>' + 
                   '&lt;div>by my awesome content&lt;/div>';
</pre>

<div class="host">
  <h1>My Title</h1>
  <h2>My Subtitle</h2>
  <div>...other content...</div>
</div>

<script>
(function() {
var shadow = document.querySelector('#shadow-dom-style-encapsulation .host').createShadowRoot();
shadow.innerHTML = '<style>h2 { color: red;}</style>' + 
                   '<h2>Yo, you got replaced!</h2>' + 
                   '<div>by my awesome content</div>';

})();
</script>

---

id: shadow-style-control
title: Style encapsulation for free
h5r_link: http://www.html5rocks.com/tutorials/webcomponents/shadowdom-201/#toc-style-scoped

<aside class="note">
  <section>
    <img src="images/shadow/shadow-rendering.svg" style="width: 100%;">
  </section>
</aside>

- Styles defined in Shadow DOM are scoped by default
- Page's styles don't bleed across the shadow boundary (unless we let them)

<pre class="prettyprint" data-lang="js">
var shadow = document.querySelector('#host').<a data-tooltip-property="createShadowRoot" data-tooltip-support='["webkit"]' data-tooltip-js>createShadowRoot</a>();
shadow.innerHTML = '<b>&lt;style>h2 { color: red; }&lt;/style></b>' + 
                   '&lt;h2>Yo, you got replaced!&lt;/h2>' + 
                   '&lt;div>by my awesome content&lt;/div>';
<b data-action-resetstyleinheritance title="click me">// shadow.resetStyleInheritance = true;</b> // click me
<b data-action-applyauthorstyles title="click me">// shadow.applyAuthorStyles = true;</b> // click me
</pre>

<div class="host" style="margin-bottom:1em;">
  <h1>My Title</h1>
  <h2>My Subtitle</h2>
  <div>...other content...</div>
</div>

<script>
(function() {
var shadow = document.querySelector('#shadow-style-control .host').createShadowRoot();
// See crbug.com/162517 - !important needed for some reason.
shadow.innerHTML = '<style>h2 { color: red; }</style>' + 
                   '<h2>Yo, you got replaced!</h2>' + 
                   '<div>by my awesome content</div>';

var resetStyles = document.querySelector('#shadow-style-control [data-action-resetstyleinheritance]');
resetStyles.addEventListener('click', function(e) {
  shadow.resetStyleInheritance = !shadow.resetStyleInheritance;
  this.textContent = 'shadow.resetStyleInheritance = ' + shadow.resetStyleInheritance.toString() + ';';
});
var applyAuthorStyles = document.querySelector('#shadow-style-control [data-action-applyauthorstyles]');
applyAuthorStyles.addEventListener('click', function(e) {
  shadow.applyAuthorStyles = !shadow.applyAuthorStyles;
  this.textContent = 'shadow.applyAuthorStyles = ' + shadow.applyAuthorStyles.toString() + ';';
});

})();
</script>

---

id: shadow-host-at
title: Styling the host
spec_link: http://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/shadow/index.html#host-at-rule
h5r_link: http://www.html5rocks.com/tutorials/webcomponents/shadowdom-201/#toc-style-host

- `@host` at-rule selects the ShadowRoot's host element.
- Allows reacting to different states:

<pre class="prettyprint" data-lang="Shadow DOM CSS">
&lt;style>
<b>@host</b> {
  * { opacity: 0.2; <a data-tooltip-property="transition" data-tooltip-support='["webkit", "moz", "ms", "o", "unprefixed"]'>transition</a>: opacity 400ms ease-in-out; }
  *:hover { opacity: 1; }
}
&lt;/style>
</pre>

<div class="host">
  <h1>My Title</h1>
  <h2>My Subtitle</h2>
  <div>...other content...</div>
</div>

<script>
(function() {
var shadow = document.querySelector('#shadow-host-at .host').createShadowRoot();
shadow.innerHTML = '<style>h2 { color: red;}' +
'@host {\
  * {\
    opacity: 0.2;\
    -webkit-transition: opacity 400ms ease-in-out;\
  }\
  *:hover {\
    opacity: 1;\
  }\
}</style>' + 
'<h2>Yo, you got replaced!</h2>' + 
'<div>by my awesome content</div>';

})();
</script>

---

hidden: true
id: pseduo-element-styling
title: Custom pseudo elements
spec_link: https://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/shadow/index.html#custom-pseudo-elements

<p class="input-list centered">
<input type="range">
</p>

<div class="build">
<pre class="prettyprint" data-lang="css">
input[type=range].custom {
  -webkit-appearance: none;
  background-color: red;
}
input[type=range].custom<b>::-webkit-slider-thumb</b> {
  -webkit-appearance: none;
  background-color: blue;
  width: 10px;
  height: 40px;
}
</pre>
 
<p class="build input-list centered">
<span><input type="range" class="custom"></span>
<span><input type="range" class="custom bling"></span>
</p>
</div>

List of pseudo elements: [Blink](http://src.chromium.org/viewvc/blink/trunk/Source/WebCore/css/html.css), [FF](https://developer.mozilla.org/en-US/docs/CSS/CSS_Reference/Mozilla_Extensions#Pseudo-elements_and_pseudo-classes)

---

hidden: true
title: Style hooks with custom pseudo elements

Component author can designate certain elements be styleable by outsiders.

<pre class="prettyprint" data-lang="html">
&lt;style>
  #host<b>::x-slider-thumb</b> {
    background-color: blue;
  }
&lt;/style>
&lt;div id="host">&lt;/div>
&lt;script>
document.querySelector('#host').<a data-tooltip-property="createShadowRoot" data-tooltip-support='["webkit"]' data-tooltip-js>createShadowRoot</a>().innerHTML = '&lt;div>' +
  '&lt;div <b>pseudo="x-slider-thumb"</b>>&lt;/div>' + 
'&lt;/div>';
&lt;/script>
</pre>

- *Note*: name needs to be prefixed with "`x-`"
    - string name creates association with element in shadow tree
- Can't access these elements from outside JS, but can style them!

---

hidden: true
title: Style hooks using CSS Variables
subtitle: theming
spec_link: http://dev.w3.org/csswg/css-variables/

Component **author** includes variable placeholders:

<pre class="prettyprint" data-lang="shadow dom css">
button {
  color: <a data-tooltip-property="var" data-tooltip-support='["webkit", "unprefixed"]'>var</a>(button-text-color);
  font: <a data-tooltip-property="var" data-tooltip-support='["webkit", "unprefixed"]'>var</a>(button-font);
}
</pre>

Component **embedder** applies styles to the element:

<pre class="prettyprint" data-lang="css">
#host {
  <b><a data-tooltip-property="var" data-tooltip-support='["webkit", "unprefixed"]'>var</a>-button-text-color</b>: green;
  <b><a data-tooltip-property="var" data-tooltip-support='["webkit", "unprefixed"]'>var</a>-button-font</b>: "Comic Sans MS", "Comic Sans", cursive;
}
</pre>

<p class="centered">
<a href="demos/page.html" class="demo">DEMO</a>
</p>

---

hidden: true
title: Remember our host node

<pre class="prettyprint" data-lang="Light DOM">
&lt;div id="host">
  &lt;h1>My Title&lt;/h1>
  &lt;h2>My Subtitle&lt;/h2>
  &lt;div>...other content...&lt;/div>
&lt;/div>
</pre>

it was nuked with:

<pre class="prettyprint" data-lang="html">
&lt;div id="host">
  <span style="opacity:0.5">#document-fragment</span>
    &lt;style>h2 {color: red;}&lt;/style>
    &lt;h2>Yo, you got replaced!&lt;/h2>
    &lt;div>by my awesome content&lt;/div>
&lt;/div>
</pre>

<label class="bad"></label> Light DOM is being completely replaced with Shadow DOM

---

id: shadow-dom-insertion-pts-example
title: Insertion points
subtitle" allow us to define a declarative API
spec_link: https://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/shadow/index.html#shadow-trees

- `select` uses CSS selectors to specify where **top level** Light DOM gets funneled into.
<!-- - `content.getDistributedNodes()` - list of element distributed at an insertion point. -->

<div class="columns-2">
<pre class="prettyprint" data-lang="HOST">
&lt;div id="host"&gt;
  &lt;h1 class="title"&gt;My Title&lt;/h1&gt;
  &lt;h2&gt;My Subtitle&lt;/h2&gt;
  &lt;div&gt;...amazing description...&lt;/div&gt;
&lt;/div&gt;
</pre>

<pre class="prettyprint" data-lang="SD" style="-webkit-column-break-before: always;">
&lt;style>h2 { color: red; }&lt;/style>
&lt;hgroup>
  <b>&lt;content select="h2">&lt;/content&gt;</b>
  <b>&lt;content select=".title">&lt;/content&gt;</b>
&lt;/hgroup>
&lt;div&gt;You got enhanced&lt;/div&gt;
<b>&lt;content select="*">&lt;/content&gt;</b>
</pre>
</div>

<div class="host">
  <h1 class="title">My Title</h1>
  <h2>My Subtitle</h2>
  <div>...amazing description...</div>
</div>

<script>
(function() {
var shadow = document.querySelector('#shadow-dom-insertion-pts-example .host').createShadowRoot();
shadow.innerHTML = '<style>\
h2 { color: red; }\
</style>\
<hgroup>\
  <content select="h2"></content>\
  <content select=".title"></content>\
</hgroup>\
<div>You got enhanced</div>\
<content select="*"></content>';
})();
</script>

---
id: shadow-dom-visualizer
title: Tool: Shadow DOM Visualizer
#content_class: flexbox vcenter centered

<iframe data-src="http://html5-demos.appspot.com/static/shadowdom-visualizer/index.html#body" style="border:none;height:460px;background: rgba(0, 0, 0, 0);"></iframe>

<p class="centered">
<a href="http://html5-demos.appspot.com/shadowdom-visualizer">html5-demos.com/shadowdom-visualizer</a>
</p>

---

hidden: true
content_class: flexbox vcenter centered

<h2 class="auto-fadein">Encapsulation / Boundaries / Re-usability</h2>
<h3 class="auto-fadein">baked into the web platform...</h3>

---

hidden: true
class: nobackdrop nobackground yum
content_class: flexbox vcenter centered

<h2 class="auto-fadein">Yum.</h2>

---

title: Shadow DOM
subtitle: browser support
class: nobackdrop nobackground browser-support
content_class: flexbox vcenter

<div class="browser-support-row">
  <div><img src="images/logos/browsers/safari_logo.png"></div>
  <div><img src="images/logos/browsers/ff_logo.png"></div>
  <div class="mobile supported"><img src="images/logos/chrome_logo.png"></div>
  <div class="mobile"><img src="images/logos/browsers/opera_logo.png"></div>
  <div><img src="images/logos/browsers/ie10_logo.png"></div>
</div>

---

title: Building blocks of Web Components
class: checkbox

<img src="images/icons/checkcircle.svg" class="checkbox"> HTML Templates

<span class="auto-fadein"><img src="images/icons/checkcircle.svg" class="checkbox"></span> Shadow DOM

<span class="spacer">Custom Elements</span>

<span class="spacer">HTML Imports</span>

---

class: nobackdrop nobackground
content_class: flexbox vcenter centered animatedfull

<img src="images/gifs/slowmowaterballoon.gif" class="rounded reflect">

---

class: nobackdrop nobackground yum
content_class: flexbox vcenter centered

<h2 class="auto-fadein">Custom Elements</h2>

---

hidden: true
id: custom-elements-segue
title: Custom Elements
class: nobackground highlight fill
image: images/bgs/traffic.jpg

<footer class="source right black"><a href="http://www.flickr.com/photos/gabludlow/6280888544/">flickr.com/photos/gabludlow/6280888544/</a></footer>

---
title: Creating new HTML elements
spec_link: https://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/custom/index.html
build_lists: true

Element definition registers the new tag with the browser:

<pre class="centered" style="font-size:25px;">
<b alt="Mechanism to bundle HTML, CSS, and JS
into reusable, encapsulated components" data-tooltip="Mechanism to bundle HTML, CSS, and JS
into reusable, encapsulated components">&lt;element</b> <b class="red" alt="Custom tag's name. Must contain a '-'." data-tooltip="Custom tag's name. Must contain a '-'.">name</b>="x-foo" <b class="red" alt="DOM element's constructor.
(goes on global scope)." data-tooltip="DOM element's constructor.
(goes on global scope).">constructor</b>="XFoo">...<b>&lt;/element></b>
</pre>

- `<x-foo>` is an `HTMLElement` until registered
- Use `:unresolved` pseudo-class to prevent [FOUC](http://en.wikipedia.org/wiki/Flash_of_unstyled_content) (Chrome 28)

      <pre class="prettyprint" data-lang="CSS"><b>:unresolved { opacity: 0; }</b>
<b>x-foo</b> { opacity: 1; <a data-tooltip-property="transition" data-tooltip-support='["webkit", "moz", "ms", "o", "unprefixed"]'>transition</a>: opacity 300ms; }
</pre>

- Lifecycle callbacks (ready, inserted, removed) give insight to element's life
     - e.g. `readyCallback()` is invoked when the custom element is created AND its definition has been registered

---

title: Basic <code>&lt;element></code> definition
spec_link: https://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/custom/index.html

<aside class="note">
  <section>
    <p><b>Note:</b> The declarative syntax on this page is still being discussed!</p>
  </section>
</aside>

<!-- <pre data-url="demos/components/x-foo.html" class="prettyprint" data-lang="x-foo.html">
</pre>
 -->

<pre class="prettyprint" data-lang="x-foo.html">
<b>&lt;element name="x-foo" constructor="XFoo"></b>
&lt;section>I'm an x-foo!&lt;/section>
&lt;script>
  var section = this.querySelector('section');
  this.register({
    prototype: {
      <b>readyCallback: function() {
        this.textContent = section.textContent; // this == &lt;element>
      },</b>
      <b>foo: function() { alert('foo() called'); }</b>
    }
  });
&lt;/script>
<b>&lt;/element></b>
</pre>

<link rel="import" href="demos/components/x-foo.html">
<div class="component-demo">
  <x-foo></x-foo>
</div>

---

title: Using a custom element

After registration, use it like any standard DOM element

<div class="build">
<div>
  <p>By <b>declaring</b> it</p>
<pre class="prettyprint" data-lang="HTML">
&lt;x-foo>&lt;/x-foo>
</pre>
</div>
<div>
  <p>By <b>creating DOM</b> in JS</p>
<pre class="prettyprint" data-lang="JS">
var elem = document.createElement('x-foo');
elem.addEventListener('click', function(e) {
  <b>e.target.foo();</b> // alert 'foo() called'.
});
</pre>
</div>
<div>
<p>By <b>using <code>new</code></b> (if the <code>constructor</code> attribute was defined)</p>
<pre class="prettyprint" data-lang="JS">
var elem = <b>new XFoo()</b>;
document.body.appendChild(elem);
</pre>
</div>

</div>

---
title: Registering elements in JS
subtitle: going the imperative route
spec_link: https://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/custom/index.html#registering-custom-elements

- `document.register()` takes the tag name and description `prototype`: 

<pre class="prettyprint" data-lang="JS">
var XFooProto = <b>Object.create(HTMLElement.prototype)</b>;

// Setup optional lifecycle callbacks: ready, inserted, removed.
XFooProto.readyCallback = function() {
  this.textContent = "I'm an x-foo!";
};

// Define its JS API.
XFooProto.foo = function() { alert('foo() called'); };

<b>var XFoo = document.<a data-tooltip-property="register" data-tooltip-support='["webkit"]' data-tooltip-js>register</a>('x-foo', {prototype: XFooProto});</b>
//var xFoo = new XFoo();
//var xFoo = document.createElement('x-foo');
</pre>

---

title: Extending existing HTML elements
subtitle: declarative version
build_lists: true

In an `<element>` definition, use the `extends` attribute:

<!-- <pre class="prettyprint" data-lang="HTML">
&lt;element name="mega-button" <b>extends="button"</b> constructor="MegaButton">
  ...
  &lt;script>
  Element.extend('mega-button', {
    readyCallback: {
      value: function() { ... }
    },
    ...
  });
  &lt;/script>
&lt;/element>
</pre> -->

<pre class="prettyprint" data-lang="mega-button.html">
&lt;element name="mega-button" <b>extends="button"</b>
         constructor="MegaButton">
  ...
  &lt;script>
    // 1. Register.
    // 2. Define an API on prototype to play moo onclick.
  &lt;/script>
&lt;/element>
</pre>

---

title: Extending existing HTML elements
subtitle: imperative version

Rock the `prototype` you want to inherit from:

<pre class="prettyprint" data-lang="JS">
var MegaButtonProto = Object.create(<b>HTMLButtonElement.prototype</b>);
...
var MegaButton = document.<a data-tooltip-property="register" data-tooltip-support='["webkit"]' data-tooltip-js>register</a>('mega-button', {prototype: MegaButtonProto});
</pre>

<div class="build">
<div>
<p>An instance is called a <span class="blue">type extension custom element</span></p>
<pre class="prettyprint" data-lang="JS">
// &lt;button is="mega-button">
var megaButton = <b>document.createElement('button', 'mega-button')</b>;

// megaButton instanceof MegaButton === true
</pre>
</div>
</div>

---
class: large futureweb
content_class: flexbox vcenter

<h2 class="auto-fadein">What about <b class="yellow">template</b>s and <b class="blue">Shadow DOM</b>?</h2>

---
title: Custom elements <b class="red jitter" style="display: inline-block;">&hearts;</b> Shadow DOM
content_class: smaller

Wrap markup in a `<template>` to make it inert. Create Shadow DOM from content:

<!-- <pre data-url="demos/components/x-foo-shadow.html" class="prettyprint" data-lang="x-foo-shadow.html">
</pre> -->

<pre class="prettyprint" data-lang="x-foo-shadow.html">
&lt;element name="x-foo-shadow" constructor="XFooShadow">
  <b>&lt;template></b>
    <b>&lt;style>
      @host { * { display: block; background: #ffcc00; ... } }
    &lt;/style></b>
    &lt;section>I'm an x-foo-shadow. Gots me some Shadow DOM!&lt;/section>
  <b>&lt;/template></b>
  &lt;script>
    var template = this.querySelector('template');
    this.register({ // this == &lt;element>
      prototype: {
        <b>readyCallback: function() {
          this.<a data-tooltip-property="createShadowRoot" data-tooltip-support='["webkit"]' data-tooltip-js>createShadowRoot</a>().appendChild(template.content.cloneNode(true));
        }</b>
      }
    });
  &lt;/script>
&lt;/element>
</pre>

<link rel="import" href="demos/components/x-foo-shadow.html">
<div class="component-demo">
  <x-foo-shadow></x-foo-shadow>
</div>

---

id: insertion-point-api
title: Define an internal structure with insertion points

<pre class="prettyprint" data-lang="my-tabs.html">
<b>&lt;element name="my-tabs"></b>
  &lt;template>
    &lt;style>...&lt;/style>
    &lt;content select="h2">&lt;/content>
    &lt;content select="section">&lt;/content>
  &lt;/template>
<b>&lt;/element></b>
</pre>

<pre class="prettyprint" data-lang="html">
<b>&lt;my-tabs></b>
  &lt;h2>Title&lt;/h2>
  &lt;section>content&lt;/section>
  &lt;h2>Title 2&lt;/h2>
  ...
<b>&lt;/my-tabs></b>
</pre>

<div class="build" style="position: absolute;bottom:70px;
right: 190px;">
<img src="images/screenshots/tabs.png" style="height: 300px;
width: auto;
box-shadow: 0 0 5px #999;">
</div>

---

title: Custom Elements
subtitle: browser support
class: nobackdrop nobackground browser-support
content_class: flexbox vcenter

<aside class="note">
  <section>
    <p>Support:</p>
    <p>Chrome 27 contains <code>document.register()</code> - <b>Enable Experimental WebKit features</b> in <code>about:flags</code>.</p>
  </section>
</aside>

<div class="browser-support-row">
  <div><img src="images/logos/browsers/safari_logo.png"></div>
  <div class="supported partial"><img src="images/logos/browsers/ff_nightly.png"></div>
  <div class="supported partial"><img src="images/logos/chrome_logo.png"></div>
  <div><img src="images/logos/browsers/opera_logo.png"></div>
  <div><img src="images/logos/browsers/ie10_logo.png"></div>
</div>

---

title: Building blocks of Web Components
class: checkbox

<img src="images/icons/checkcircle.svg" class="checkbox"> HTML Templates

<img src="images/icons/checkcircle.svg" class="checkbox"> Shadow DOM

<span class="auto-fadein"><img src="images/icons/checkcircle.svg" class="checkbox"></span> Custom Elements

<span class="spacer">HTML Imports</span>

---

class: nobackdrop nobackground yum
content_class: flexbox vcenter centered

<h2 class="auto-fadein">HTML Imports</h2>

---

title: HTML Imports
subtitle: Package. Distribute. Share. Reuse.
spec_link: https://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/imports/index.html

<pre class="prettyprint" data-lang="HTML">
&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    <b>&lt;link rel=&quot;import&quot; href=&quot;x-foo.html&quot;&gt;</b>
  &lt;/head&gt;
  &lt;body&gt;
    <b>&lt;x-foo&gt;&lt;/x-foo&gt;</b> &lt;!-- Element definition is in x-foo.html --&gt;
  &lt;/body&gt;
&lt;/html&gt;
</pre>

- `link.import.content` is the Document `x-foo.html`
- `link.import.href` - the link's `href` attribute, but resolved relative to the element.
- `.import` is `null` for non-import links.

---

title: Reusing other components

<pre class="prettyprint" data-lang="awesome-menu.html">
<b>&lt;link rel="import" href="x-toolbar.html">
&lt;link rel="import" href="menu-item.html"></b>

&lt;element name="awesome-menu">
  &lt;template>
    <b>&lt;x-toolbar responsive="true">
      &lt;menu-item src="images/do.png" selected>Do&lt;/menu-item>
      &lt;menu-item src="images/re.png">Re&lt;/menu-item>
      &lt;menu-item src="images/mi.png">Mi&lt;/menu-item>
    &lt;x-toolbar></b>
  &lt;/template>
  ...
&lt;/element>
</pre>

<pre class="prettyprint" data-lang="app.html">
&lt;link rel="import" href="awesome-menu.html">
&lt;awesome-menu>&lt;/awesome-menu>
</pre>

---

title: HTML Imports
subtitle: browser support
class: nobackdrop nobackground browser-support
content_class: flexbox vcenter

<div class="browser-support-row">
  <div><img src="images/logos/browsers/safari_logo.png"></div>
  <div><img src="images/logos/browsers/ff_logo.png"></div>
  <div><img src="images/logos/chrome_logo.png"></div>
  <div><img src="images/logos/browsers/opera_logo.png"></div>
  <div><img src="images/logos/browsers/ie10_logo.png"></div>
</div>

---

title: Building blocks of Web Components
class: checkbox

<img src="images/icons/checkcircle.svg" class="checkbox"> HTML Templates

<img src="images/icons/checkcircle.svg" class="checkbox"> Shadow DOM

<img src="images/icons/checkcircle.svg" class="checkbox"> Custom Elements

<span class="auto-fadein"><img src="images/icons/checkcircle.svg" class="checkbox"></span> HTML Imports

---

class: nobackdrop nobackground
content_class: flexbox vcenter centered animatedfull

<img src="images/gifs/awwwyeah.gif" class="rounded reflect">

---

title: Demos
class: segue dark nobackground highlight

---

title: Meme Generator

<pre class="prettyprint" data-lang="html" data-run-demo="http://html5-demos.appspot.com/static/webcomponents/demos/components/my-components/meme.html">
&lt;my-meme src="images/beaches.jpg">
  &lt;h1 contenteditable>Stay classy&lt;/h1>
  &lt;h2 contenteditable>Web!&lt;/h2>
&lt;/my-meme>
</pre>

---

content_class: flexbox vcenter centered

<p class="centered">
  <code class="prettyprint custom-element-snippet">&lt;photo-booth>&lt;/photo-booth></code>
</p>

<link rel="import" href="demos/components/x-photo-booth.html">
<photo-booth class="rounded"></photo-booth>

<!-- 
<iframe data-src="demos/components/photobooth.html" class="rounded" style="height:450px;border:none;width:450px;background:transparent" seamless></iframe>
 -->

---

hidden: true
content_class: flexbox vcenter centered

<p class="centered">
  <code class="prettyprint custom-element-snippet">&lt;g-plus>&lt;/g-plus></code>
</p>

---

hidden: true
content_class: flexbox vcenter centered

<p class="centered">
  <code class="prettyprint custom-element-snippet">&lt;ga-dashboard>&lt;/ga-dashboard></code>
</p>

---

hidden: true
title: Self-documenting custom elements
content_class: flexbox vcenter centered

<p class="centered">
  <code class="prettyprint custom-element-snippet">&lt;wc-documentation>&lt;/wc-documentation></code>
</p>
<br>
<p class="centered">
<a href="http://html5-demos.appspot.com/static/webcomponents/demos/components/my-components/wc-docs/index.html" class="demo">DEMO</a>
</p>

---

title: Try it today? Yes!

- Use Chrome Canary, turn on:
	- **Enable Experimental WebKit features** in `about:flags`
	- **Enable experimental JavaScript** in `about:flags`
	- Enable **Show Shadow DOM** in DevTools

- - -

- Watch [Cr-Blink-WebComponents](https://code.google.com/p/chromium/issues/list?q=label:Cr-Blink-WebComponents) bug hotlist

- Check out the <img src="images/logos/toolkit_logo.svg" style="vertical-align:middle;height:30px;">
[Polymer](http://polymer-project.org/) polyfills:
    - [HTML Imports](https://github.com/polymer-project/HTMLImports)
    - [Shadow DOM](https://github.com/polymer-project/ShadowDOM)
    - [Custom Elements](https://github.com/polymer-project/CustomElements)
    - [MDV](https://github.com/polymer-project/mdv)
---

content_class: flexbox vcenter centered

<h2>"<a href="https://developers.google.com/events/io/sessions/324149970" style="border: none;">Web Components in Action</a>"</h2>
<h3 style="margin-top:1em;">Up next. This room.</h3>
