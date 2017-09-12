# 60-fps-onscroll-event-listener

[Polyfill requestAnimationFrame and cancelAnimationFrame](https://github.com/webdeveric/animation-frame-polyfill)

### Scroll Listener
```javascript
(function() {
  var lastScrollY = 0;
  var ticking = false;

  var update = function() {
    // do your stuff
    ticking = false;
  };

  var requestTick = function() {
    if (!ticking) {
      var requestAnimationFrame = window.requestAnimationFrame
        || window.webkitRequestAnimationFrame
        || window.mozRequestAnimationFrame
        || window.msRequestAnimationFrame
        || function(callback) { return setTimeout(callback, 1000 / 60); };
    
      requestAnimationFrame(update);
      
      ticking = true;
    }
  };

  var onScroll = function() {
    lastScrollY = window.scrollY;
    requestTick();
  };

  $(window).on('scroll', onScroll);
})();
```
