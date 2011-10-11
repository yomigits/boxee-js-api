boxee-api.js
---

a javascript library to control how the Boxee remote interacts with your html5 app and trigger special Boxee browser specific functionality.

Using boxee-api.js is intended as an easier alternative to using a boxee control script.

TO USE IT
---
You must include it on your page after including the jQuery and Underscore libraries


Example usage
---
The boxee-api.js library is used to put the example apps in the `html5-examples` project into keyboard mode.

https://github.com/Boxee/html5-examples


API
---

The library will create a global variable called `boxeeAPI`.

  // Set the remote to keyboard mode.  
  //   -> The d-pad on the remote will map to the keyboard's arrow keys.  
  //   -> The center button will map to the Enter key.
	boxeeAPI.keyboardMode();

  // Set the remote to cursor mode.  
  //   -> The d-pad will move around the mouse cursor on the screen.  
  //   -> The center button will map to a mouse click
	boxeeAPI.cursorMode();
	
	// Prompt the user with a message and the option to pick "OK" or "CANCEL"
	//   title: string, displayed as a header on popup
	//   text:  string, displayed as content text
	//   callback: string or function, called with one boolean argument - true only if user selected "OK"
	boxeeAPI.promptDialog(title, text, callback);
	
	boxeeAPI.promptDialog('A Header', 'Some details', function(confirmed) {
	  if (confirmed) {
	    console.log('user selected OK');
	  } else {
	    console.log('user selected CANCEL');
	  }
	});
	
	window.myPromptCallback = function(confirmed) { ... };
	boxeeAPI.promptDialog('Sign Up!', 'Do you agree to our terms of service?', 'myPromptCallback');
	
	// Show a short notification in the top right corner of the screen
	//   Since the browser's console is not accessible, this is one way to get feedback while developing.
	//
	//   message: string to display (will be truncated if too long)
	//   seconds: integer length of time in seconds to show message (defaults to 2)
	boxeeAPI.notify(message, seconds = 2)

