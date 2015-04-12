# FileSelect
Simple file selection library for Phonegap\Cordova

Features:
- supports masks
- has callbacks for many situations (you can do some interesting things with them)
- can be styled (default style is included)

Future development:
- abandon clicks in favour of quick taps

<b>Example:</b>
```javascript
var path = localStorage['lastPath'] || 'file:///storage/';
// Constructor takes FileSelector(elem, path, masks, success, fail, cancel, menu, pathChanged, openFile)
// Only elem is really required, but you'll have to provide the path sooner or later anyway.
// If you don't provide a mask *.* will be used
var fileSelector = new FileSelector($('#container'), path, 'Documents (html, txt)|*.htm;*.html;*.txt|All files|*.*');
// Mask can be changed later using setMasks method.
fileSelector.onCancel = function(e) // Fires on the back button
{
	// Add code for closing the file selector, going one folder back (like below) or something else
	$(fileSelector.elem).find('.file-container .item.back').click();
	e.stop(); // prevent other backbutton event listners from firing
};
fileSelector.onSuccess = function(path)
{
  // If you click on a file, this function will be called with the name of the file
};
fileSelector.onPathChanged = function(path)
{
	// Each time you change directory this callback will be launched (here we're saving lastpath in local storage)
	localStorage['lastPath'] = path;
};
fileSelector.onFail = function(error)
{
	// If something goes wrong this code will be executed
	alert(error.message);
};
// There are also onMenu() and onOpenFile(fileEntry, path) callbacks.
// First is called when you press menu button, the other when path leads to a file and not a directory.

// Make the selector load file\directory list from a path (if no path is provided, component will try using previous path)
fileSelector.open(path);
// Directories and files will be alphabetically ordered and directories will be listed before the files.
```
<hr/>
License <a href="http://www.wtfpl.net/about/">WTFPL</a>
