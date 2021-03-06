## node-webkit-window-manager

This is a utility to help manage all windows in a node-webkit application. It gives all open windows a global reference to other windows and allows passing data between windows.


### Example

#### Instantiate the window manager and store as a global reference.

```javascript

	var WindowManager = require('node-webkit-window-manager').windowManager;
	var gui = require('nw.gui');
	
	global.windowManager = new WindowManager(gui, {
		"login": {							// the name "key" of the window
			page: "html/login.html",        // the path to the HTML page.
			options: {						// Standard nw.gui Window options
	            frame : true,
	            toolbar: true,
	            width: 500,
	            height: 600,
	            show: true
    		}
		},
		"dashboard": {
			page:"html/dashboard.html",
			options: {
	            frame : true,
	            toolbar: true,
	            width: 900,
	            height: 700,
	            show: true
			}		
		},
		"index": {
			page:"html/index.html",
			options: {
				frame: true,
				toolbar: true,
				width: 900,
				height: 700,
				show: true
			}
		}
	});
```

#### Open the login page and pass a user object

```javascript
    var loginWindow = global.windowManager.open('login', { 
        username: 'johndoe',
        auth_token: 'abc123',
        location: 'Earth'
    });
```

#### On login.html, get reference to user object

```javascript
    var loginWindow = global.windowManager.get('login');
    console.log('username is ' + loginWindow.data.username);
    console.log('and is located on ' + loginWindow.data.location);
```

#### Close the login window

```javascript
	global.windowManager.get('login').close();
```

#### Close all opened windows, except the background page.

```javascript
	global.windowManager.openWindows.forEach(function(windowRef) {
		windowRef.close();
	});
```


