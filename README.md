Unfix
=======

Seems that half the pages on the web these days
have annoying fixed navigation headers at the top
and/or bottom of the page breaking the use of
the space-bar or page-up/down for paging text.

I finally had enough of it so I made a bookmarklet
to remove them.

It just spiders the DOM and changes and "Position:fixed"
elements into "position:absolute".

<h2>Install</h2>

Install it by dragging the big button on the
<a href="http://revpriest.github.io/unfix/">install page</a>
into your bookmarks tool-bar.

Then next time some website is being annoying with
it's fixed headers, click the bookmarklet.

Personally I don't have a bookmarks-toolbar since
I use <a href="http://5digits.org/pentadactyl/">Pentadactyl</a>
and do most of my web-driving by keyboard (or by
voice control mapped to keyboard).

You can add this line to your .pentadactylrc if you'd
sooner:

```
command! unfix -description "Unfix DOM Nodes" open javascript:(function(){ function walk(n, f) { f(n); n = n.firstChild; while (n) { walk(n, f); n = n.nextSibling; } } walk(document.body, function (n) { if(n.nodeType==1){ var s = window.getComputedStyle(n); var d = s.getPropertyValue('position'); if(d=='fixed'){ n.style.position='absolute'; } } }); })();
```

Here's the javascript in that bookmarklet formatted
nicely. The short variable names are:
"n" is for "node", 
"f" is for "function", 
"s" for "style" and 
"d" for "display".

```javascript
    (function(){
      function walk(n, f) {
        f(n);
        n = n.firstChild;
        while (n) {
            walk(n, f);
            n = n.nextSibling;
        }
      }

      walk(document.body, function (n) {
        if(n.nodeType==1){
          var s = window.getComputedStyle(n);
          var d = s.getPropertyValue('position');
          if(d=='fixed'){
            n.style.position='absolute';
          }
        }
      }); 
    })();
```

Tested in Firefox (well, Iceweasel) and only that,
will test it in Chrome shortly. Can't test IE or
Safari coz I don't have OS X or Windows.


