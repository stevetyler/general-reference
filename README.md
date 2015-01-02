<a name='toc'>Table of Contents</a>
------

  1. [Document Object Model](#dom)
  1. [Progressive Enhancement vs Graceful Degradation](#pegd)
  1. [Optimizing a Site's Assets / Resources](#optimization)
  1. [Serving site assets from multiple domains](#multidomains)
  1. [Ways to decrease page load (perceived or actual load time)](#pageload)
  1. [Long-polling, websockets and SSE](#longpolling)
  1. [The importance of standards and standards bodies](#standards)
  1. [FOUC and how to avoid it](#FOUC)
  1. [The process from the time you type in a URL to it finishing loading on your screen](#url)
  1. [Semantic HTML](#semantic)
  2. [Projects using tabs instead of spaces or vice versa](#tabs)
  3. [API Explanation](#API)


<a name='dom'>Document Object Model<a/>
------

The Document Object Model is a cross-platform and language independent convention for representing and interacting with objects in HTML, XML &amp; XHTML documents. (taken from Wikipedia)

To <a href="http://en.wikipedia.org/wiki/Web_browser_engine">render</a> a document such as an HTML page, most web browsers use an internal model similar to the DOM. The nodes of every document are organized in a <a href="http://en.wikipedia.org/wiki/Tree_structure">tree structure</a>, called the <i>DOM tree</i>, with topmost node named "Document object". When an HTML page is rendered in browsers, the browser downloads the HTML into local memory and automatically parses it to display the page on screen. The DOM is also the way JavaScript transmits the state of the browser in HTML pages.</p> <p>Web browsers rely on layout engines to parse HTML into a DOM. Some layout engines, such as <a href="http://en.wikipedia.org/wiki/Trident_(layout_engine)">Trident/MSHTML</a>, are associated primarily or exclusively with a particular browser, such as Internet Explorer. Others, such as <a href="http://en.wikipedia.org/wiki/Blink_(layout_engine)">Blink</a>, <a href="http://en.wikipedia.org/wiki/WebKit">WebKit</a>, and <a href="http://en.wikipedia.org/wiki/Gecko_(layout_engine)">Gecko</a>, JavaScript rendered in HTML pages, collection of web pages shared by a number of browsers, such as <a href="http://en.wikipedia.org/wiki/Google_Chrome">Google Chrome</a>, <a href="http://en.wikipedia.org/wiki/Opera_(web_browser)">Opera</a>, <a href="http://en.wikipedia.org/wiki/Safari_(web_browser)">Safari</a>, and <a href="http://en.wikipedia.org/wiki/Firefox">Firefox</a>. The different layout engines implement the DOM standards to varying degrees of compliance.

<a name='pegd'>Progressive Enhancement vs Graceful Degradation<a/>
------

Progressive Enhancement has the following principles:

*  Basic content and functionality should be accessible to all web browsers
*  Sparse, semantic markup contains all content  
*  Enhanced layout &amp; behaviour is provided by externally linked CSS and JavaScript  
*  End-user web browser preferences are respected 

Graceful Degradation provides fall-backs for older browsers


<a name='optimization'>Optimizing a Site's Assets / Resources<a/>
------

* File concatenation
* Minification
* CDN Hosted
* Caching
* Use task runner like Grunt / Gulp
 
<a name='multidomains'>Serving site assets from multiple domains<a/>
------

This can increase the number of assets a browser can download in parallel.

* IE7 allows only 2 concurrent connections
* IE8 and Chrome allows 6
* Firefox allows 8

Be aware that additional DNS lookups would be involved and could be 150ms or longer. This added delay could easily offset any benefit of parallel downloads.

<a name='pageload'>Ways to decrease page load (perceived or actual load time)<a/>
------

Profiling a web page usually involves a tool such as Firebug to determine what components (i.e. images, CSS files, HTML documents, and JavaScript files) are being requested by the user, how long the component takes to load, and how big it is.

*  Save images in the right format to reduce their file size  *  Minify your CSS and JavaScript and combine files to reduce HTTP requests  
*  Use server-side compression to reduce file sizes  
*  Avoid inline CSS and JavaScript - if you use a lot of CSS and JavaScript in your HTML document, you won’t be taking advantage of the web browser’s caching features.  
*  Monitor website performance  
*  For a website it’s responsible for getting/sending HTTP requests/responses to the right people and serves all of your web page components. If your web server isn’t performing well, you won’t get the maximum benefit of your optimization efforts  *  Use Google Webmaster Tools 

<a name='longpolling'>Long-polling, websockets and SSE<a/>
------

Regular HTTP: 

*  A client requests a webpage from a server  
*  The server calculates the response  
*  The server sends the response to the client 

AJAX Polling:

* A client requests a webpage from a server using regular HTTP  
* The requested webpage executes JavaScript which requests a file from the server at regular intervals (e.g. 0.5 seconds)  
* The server calculates each response and sends it back, just like normal HTTP traffic

AJAX Long-Polling:

*  The difference with long-polling is the server does not immediately respond with the requested information but waits until there's <em>new</em> information available  
*  When there's new information available, the server responds with the information  
*  The client receives the new information and immediately sends another request to the server re-starting the process 

HTML5 Server Sent Events (SSE) / EventSource:

* A client requests a webpage from a server using regular HTTP  
* The requested webpage executes JavaScript which opens a connection to the server. The server sends an event to the client when there's new information available in real-time. Server will need to have an event loop  
* Not possible to connect with a server from another domain

HTML5 Websockets:

* A client requests a webpage from a server using regular HTTP  
* The requested webpage executes JavaScript which opens a connection with the server  
* The server and the client can now send each other messages when new data (on either side) is available in real-time. Server will need to have an event loop  <li>With WebSockets it is possible to connect with a server from another domain  
* It is also possible to use a third party hosted WebSockets server, for example <a href="http://pusher.com/">Pusher</a> or <a href="http://www.leggetter.co.uk/real-time-web-technologies-guide">others</a>. This way you'll only have to implement the client side 

<a name='standards'>The importance of standards and standards bodies.<a/>
------

Standards bodies such as the World Wide Web Consortium (W3C) were created as forums to establish agreement across the industry and among vendors. Other standards groups have formed since, most notably the HTML5-focused Web Hypertext Application Technology Working Group (WHATWG).

<a name='FOUC'>FOUC and how to avoid it<a/>
------

Flash of unstyled content. FOUC occurs with certain JavaScript and jQuery implementations where the scripts are used for styling and images, typically content that takes longer or hangs after the page loads.

* Include your link tag(s) to stylesheets within the &lt;head&gt; of your web page documents  
* Put all scripts at the bottom  
* Modernizr adds a class="no-js" to the html tag, and then he adds one &lt;script&gt; within the &lt;head&gt; that changes it back to 'js'&nbsp;

<a name='url'>The process from the time you type in a URL to it finishing loading on your screen<a/>
------

* Enter the URL to the address bar  
* A request will be sent to the DNS server based on your network configuration  
* DNS will route you to the real IP of the domain name. The DNS layer can help direct clients to different servers based on geographical location to help with load balancing and latency minimization, and one server can respond to requests from many different DNS names.  
* A request (with complete HTTP header) will be sent to the server (with IP to identify)'s 80 port (suppose we don't specify another port) A browser can make different types of requests (GET, POST, HEAD, etc.), and usually includes several different headers including cookies, browser capabilities, language preferences, etc.  
* Server will search the listening ports and forward the request to the app which is listening to 80 port (let's say nginx here) or to another server for load balancing.  <li>nginx will try to match the URL to its configuration and serve as an static page directly, or invoke the corresponding script interpreter (e.g PHP/Python) or other app to get the dynamic content (with DB query, or other logics)  
* Most browsers usually maintain a cache in order to avoid downloading stuff many times, and use various techniques to determine whether the cached version of a file is valid.  
* HTML will be sent back to the browser with a complete HTTP response header  
* Browser will parse the DOM of HTML using its parser  
* External resources (JS/CSS/images/flash/videos..) will be requested <em>in sequence </em>for JS, it will be executed by JS engine for CSS, it will be rendered by CSS engine and HTML's display will be adjusted based on the CSS (<em>also in sequence or not</em>?)  
* If there's an iframe in the DOM, then a separate same process will be executed from step 1-10
 
<a name='semantic'>Semantic HTML<a/>
------

The use of syntactic markup to reinforce the meaning of the information in webpages. e.g. &lt;nav&gt; &lt;header&gt; &lt;footer&gt; &lt;audio&gt; &lt;video&gt;


<a name='tabs'>Projects using tabs instead of spaces or vice versa<a/>
------

Conform to conventions and stay consistent. Suggest using EditorConfig plugins (<a href="http://editorconfig.org">http://editorconfig.org</a>) 


<a name='api'>API Explanation<a/>
------

Application Programming interface
<p><a title="https://zapier.com/learn/apis/" href="https://zapier.com/learn/apis/">https://zapier.com/learn/apis/</a></p>
