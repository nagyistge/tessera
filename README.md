tessera
================

Tessera is an Angular module that provides three-way data-binding between Angular (DOM/Model) and PureWeb's AppState.  Changes made to any of the DOM/Model/AppState will be synchronized to the other two locations.

# Installation

```bower install tessera```

# Usage
Include the library:
```
<script src="/myApp/bower_components/tessera/tessera.js"></script>
```

Add the module to your main application:
```
angular
  .module('myApp', [
    'ngRoute',
    'tessera'
  ])
  .config(function ($routeProvider) {  
```

Reference the actual service in your controller:
```
angular.module('myApp')
  .controller('MainCtrl', function ($scope, $tessera) {
```
 
Specify the properties you want to bind to AppState:
```
$tessera.bind($scope, 'SharedMessage', '/SharedMessage');
```  
If an appstate path is not provided, then bind will simply use the property name as the app state path.

Bind supports binding to both basic data types and objects.  When binding to an object, any changes made to the children within that object (recursively), will be picked up and synchronized.  Additionally, all bound properties (and object values) will be recast as strings upon their first synch.

If you need to unbind a previously bound property just use $tessera.unbind:
```
$tessera.unbind('SharedMessage', '/SharedMessage'); 
```

Additionally, you can pass a traditional callback through for any PureWeb AppState changes, this will be called after the Angular digest loop:
```
var f = function(evt){var n = evt.getNewValue(); console.log(n);};
$tessera.bind($scope, 'ScribbleColor', '/ScribbleColor', f); 
```

If you want to unbind a property with a callback you must pass the callback into the unbind method to unregister the AppState callback.  If you unbind a property without passing the callback, the callback will be returned by unbind() and you can unregister the callback using traditional PureWeb methods (removeValueChangedHandler()).
  
# PureWeb

[The PureWeb platform](http://www.calgaryscientific.com/pureweb/) lets you expose your complex or graphics intensive application as a back end service so it can be hosted online and accessed from new interfaces on browsers and mobile devices.

## Author

Calgary Scientific Inc

## License

Apache 2.0 (See LICENSE file)

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

Copyright (c) 2014, Calgary Scientific Inc.
All rights reserved.

