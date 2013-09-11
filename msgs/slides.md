!SLIDE subsection
# The Client Side

!SLIDE smaller bullets incremental
# Client-side Libraries

* [sockjs-client](https://github.com/sockjs/sockjs-client)
* [stomp.js](https://github.com/jmesnil/stomp-websocket)

!SLIDE small bullets
# Reference Application
<br><br>
* [https://github.com/rstoyanchev/](https://github.com/rstoyanchev/spring-websocket-portfolio)<br><br>[spring-websocket-portfolio](https://github.com/rstoyanchev/spring-websocket-portfolio)

!SLIDE smaller bullets incremental
# Advanced Client Architecture
<br><br>
* [AMD](http://requirejs.org/docs/whyamd.html) modules
* [Bower](http://bower.io/) package manager
* [curl.js](https://github.com/cujojs/curl) for loading modules (cujoJS)
* [msgs.js](https://github.com/cujojs/msgs) for messaging (cujoJS)

!SLIDE center
## Improving the client-side with [cujoJS](http://cujojs.com/)

!SLIDE smaller
# WebSocket Support in msgs.js
<br>
    @@@ javascript
      var bus = require('msgs').bus(),
          SockJS = require('sockjs');

      bus.channel('toServer');
      bus.channel('fromServer');

      bus.webSocketGateway(
        new SockJS('/msgs'),
        { output: 'fromServer', input: 'toServer' } 
      );


!SLIDE smaller
# STOMP support in msgs.js
<br>
    @@@ javascript
      var bus = require('msgs').bus(),
          SockJS = require('sockjs');

      bus.stompWebSocketBridge('broker', new SockJS('/broker'));

      // subscribe
      bus.on('broker!/topic/price.stock.*', function(quote) {
          portfolio.processQuote(quote);
      });

      // publish
      var execTrade = bus.inboundAdapter('broker!/app/trade');
      execTrade(trade);



