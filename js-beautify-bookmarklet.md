Make a bookmarklet from this, use when on a web browser page displaying an ugly javascript file
(just create a new bookmark, enter "javascript:" and then paste the following code)
```
function loadJS(url, callback) 
{
    var s = document.createElement('script');
    s.src = url;
    if (s.addEventListener) {
      s.addEventListener('load', callback, false);
    } 
    else {
      s.onreadystatechange = function () {
        if (this.readyState == 'complete') {
          callback();
          s = null;
        }
      }
    }
    s.type = 'text/javascript';
    document.getElementsByTagName('head')[0].appendChild(s);
};

loadJS("https://raw.githubusercontent.com/beautify-web/js-beautify/master/js/lib/beautify.js", function()
{
  var pre = document.querySelector("body > pre");
  var text = pre.textContent;
  var fmt = js_beautify(text);
  pre.textContent = fmt;  
});