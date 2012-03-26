# local.js

LocalJS is a [RequireJS](http://requirejs.org) plugin that provides a mechanism to define "local" modules
that are defined on the client only and will never require a remote request. These can be used to integrate
other framework's asynchronous loading mechanisms with RequireJS.

Example usage: We want to depend on a GWT module that will be loaded. This module's name is "gwtModule".

```JavaScript
require(['local!gwtModule'], function (gwtModule) {
  // Do something
});

// Our GWT Module will call this function when it has been initialized and can be used
var gwtLoaded = function() {
  // Define a module representing our gwt module. The GWT Module creates a JSNI object to
  // work with in global space called "jsniGwtModule".
  require(['local'], function(local) {
    local.define('gwtModule', function() {
      return jsniGwtModule;
    });
  });
};
```