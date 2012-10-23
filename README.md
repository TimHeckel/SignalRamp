SignalRamp
==========

jQuery.signalRamp.js is a lightweight jQuery plugin that synchronizes UIs across all subscribed clients. Leveraging [SignalR](https://github.com/SignalR/SignalR) and [SignalGrr](https://github.com/TimHeckel/SignalGrr) as a SignalR proxy server, SignalRamp can quickly turn any segment of your HTML into a live wire for instant synchronization:

Given a snippet of HTML:
```
<div id="holdElements">
    <input type="text" id="txtFirst" />
```

You can simply call the below to automatically sychronize this data 

```
$("#holdElements").signalRamp({proxyName: 'someUniqueId'});
```

`SignalRamp` is automatically configured to leverage the SignalR proxy server provided by SignalGrr, so once you've wired up your page with the above, bring up the page in two separate browsers to see the sync happen in real-time. The `index.html` page has a complete example.

Below are all the configurable options
```
$("#holdElements").signalRamp({
      proxyName: 'uniqueName' //this string must be shared among all collaborating UIs
      , sensibility: 0 //defaults to 100 -- determines how often to send the keystrokes back and forth
      , url: '' //change the URL of the signalR proxy, defaults to http://signalGrr.apphb.com
      , bindable: {
        click: '' //name of the css class that triggers click synchronization (defaults to signalRampClick)
        , hover: '' //name of the css class that triggers click synchronization (defaults to signalRampHover)
        , mousedown: '' //name of the css class that triggers click synchronization (defaults to signalRampMouseDown)
        , mouseup: '' //name of the css class that triggers click synchronization (defaults to signalRampMouseUp)
      }
      , callbacks: {
          bridgeStarted: function (name) {
            //if no proxyName is specified, a unique one will be generated and provided here
          }
          , valueChanged: function (id, val) {
            //fired whenever the value changes on wired UI elements
          }
          , checkChanged: function (id, check) {
            //fired whenever the checked state changes on wired UI elements
          }
      }
  });
```

You can attach any of the `bindable` class names to elements to syncronize the corresponding `mousedown`, `mouseup`, hover (`mouseover`, `mouseout`) or `click` events in the UI.