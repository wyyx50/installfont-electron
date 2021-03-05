installfont-electron
===========

Update method to electron apps to execute from an ASAR file which doesn't allow temp files inside it.

Added options.overrideLocalFileDir

This property is to a temp folder to extract and install fonts from.  It must be from outside be a folder outside the application's runtime directory.

Example:

```
  let osTemp = require('os').tmpdir();
  installFont(fullPath, function(err) {
      if (err) {
          console.error('unable to install font', err);
          reject(err);
      } else {
          console.log('installed font', fullPath);
          resolve();
      }
  }, {overrideLocalFileDir: osTemp});
```

Must be unpacked from asar add to your config:

```{
"build": {
    "appId": "YOURID",
    "win": {
    "target": "NSIS",
    "asar": true,
    "asarUnpack": [
    " ./node_reports",
    "./assets/fonts",
    "./node_modules/installfont-electron",
    ""
    ]
},
"publish": {
    "provider": "generic",
    "url": "http://127.0.0.1"
    }
}
}
```

Nodejs module for installing system fonts.
This module is not tightly coupled to any specific font libraries or apis.
It also is not opinionated about how you get the fonts on your machine.

### Compatible OS:
* Mac OS
* Windows
* Ubuntu 14.0.4.1 LTS

*Run as Admin on linux or OSX*

###Assumptions

* Assumes font file(s) are downloaded to your machine, but not yet installed.

### Installation

Open your command line and run `npm install installfont-electron`

### Usage
*Installing a single font file*
```javascript
var installfont = require('installfont-electron');

installfont('path/to/your/font.ttf', function(err) {
  if(err) console.log(err, err.stack);
  //handle callback tasks here
});


```

*Installing all font files within a specified directory*

```javascript
var installfont = require('installfont-electron');

installfont('path/to/dir/containing/fonts', function(err) {
  if(err) console.log(err, err.stack);
  //handle callback tasks here
});
```


### Options
*Pass installfont an options parameter as a third argument*


```javascript
var installfont = require('installfont-electron');

var options = {
  removeFonts: true
};

installfont('path/to/dir/containing/fonts', function(err) {
  if(err) console.log(err, err.stack);
  //handle callback tasks here
}, options);
```
`removeFonts` - Pass true or false to specify if you want your font file(s) to be deleted after they are installed. Defaults to false;
