boxee-api.js
---

a javascript library to control how the Boxee remote interacts with your html5 app and trigger special Boxee browser specific functionality.

Using boxee-api.js is intended as an easier alternative to using a boxee control script.

This library is specifically for use on apps for the Boxee Box's browser, not the desktop Boxee software.

TO USE IT
---
You must include it on your page after including the jQuery and Underscore libraries


Tips
---

Most of the time, better user experiences come while in keyboard mode, since it simplifies things for the user.  

To make an app in keyboard mode:

  * include the boxee-api.js file on your pages
  * call `boxeeAPI.keyboardMode()` when a page loads
  * design the app so it can be controlled without using the mouse, and by only pressing arrow keys and enter
  * the Boxee remote does have a keyboard on the back, but it should only be used for typing, not navigation
      * keyboard is ok when entering a search query, or entering login credentials
      * don't hook special modes to letter keys. for example having the user press 'f' to enter a full screen mode is a bad experience.  Make it possible to do things like this with only the arrow keys and enter.
      
Since the Boxee box's browser does not give a developer easy access to console info, I recommend doing as much of the development as possible in chrome or safari, and test occasionally on the box.


Example usage
---
The boxee-api.js library is used to put the example apps in the `html5-examples` project into keyboard mode.

https://github.com/Boxee/html5-examples


API
---

The library will create a global variable called `boxeeAPI`.

**Keyboard Modes**:

    // Set the remote to cursor mode.  
    //   -> The d-pad will move around the mouse cursor on the screen.  
    //   -> The center button will map to a mouse click
    // *note*:
    //   cursor mode is the default
    //   you *can* switch between cursor mode and keyboard mode anytime, not just when the page loads
    boxeeAPI.cursorMode();

    // Set the remote to keyboard mode.  
    //   -> The d-pad on the remote will map to the keyboard's arrow keys.  
    //   -> The center button will map to the Enter key.
    boxeeAPI.keyboardMode();


**Closing an App**

    // Exit the current App
    boxeeAPI.closeApp();
    
    // Close the boxee browser
    boxeeAPI.closeBrowser();


**feedback messages**

    // Show a short notification in the top right corner of the screen
    //   Since the browser's console is not accessible, this is one way to get feedback while developing.
    //
    //   message: string to display (will be truncated if too long)
    //   seconds (optional): integer length of time in seconds to show message (defaults to 2)
    boxeeAPI.notify(message, seconds = 2)



**prompt**

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

