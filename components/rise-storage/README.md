# Rise Storage Web Component

## Introduction

The Rise Storage Web Component uses Google’s Storage API to retrieve the URL of a file, or the URLs of all files within a folder, from Rise Storage. If the Rise Cache application is running, it will be utilized for local storage of the files, and the URLs returned by the web component will point to Rise Cache. Otherwise, if Rise Cache is not running, the browser's cache will be utilized.

Single files are only downloaded once and are not subsequently checked for changes. Folders are monitored for changes, but a minimum refresh time of 15 minutes is enforced.

Rise Storage Web Component works in conjunction with [Rise Vision](http://www.risevision.com), the [digital signage management application](http://rva.risevision.com/) that runs on [Google Cloud](https://cloud.google.com).

At this time Chrome is the only browser that this project and Rise Vision supports.

###Usage
To use the Rise Storage Web Component, you should first install `webcomponents.js`. The `webcomponents.js` polyfills enable Web Components in (evergreen) browsers that lack native support.

To install with Bower:
```
bower install webcomponentsjs
```

To install with npm:
```
npm install webcomponents.js
```

Next, install the Rise Storage Web Component with Bower:
```
bower install rise-storage
```

Finally, construct your HTML page. You should include `webcomponents.js` before any code that touches the DOM, and load the web component using an HTML Import. For example:
```
<!DOCTYPE html>
<html>
  <head>
    <script src="bower_components/webcomponentsjs/webcomponents.js"></script>
    <link rel="import" href="bower_components/web-component-rise-storage/rise-storage/rise-storage.html">
  </head>
  <body>
    <rise-storage
      companyId="my-company-id"
      folder="my-folder"
      fileName="my-image.png"
      folderRefresh="60"></rise-storage>

    <script>
      // Wait for 'polymer-ready'. Ensures the element is upgraded.
      window.addEventListener('polymer-ready', function(e) {
        var storage = document.querySelector('rise-storage');

        // Respond to events it fires.
        storage.addEventListener('rise-storage-response', function(e) {
          console.log(e.detail[0]); // URL to the file.
        });

        storage.go(); // Call its API methods.
      });
    </script>
  </body>
</html>
```

#### Attributes
| Attribute       | Type                                                                            | Default          |
| --------------- | ------------------------------------------------------------------------------- |:----------------:|
| `companyId`     | `<string>` The ID of the Company.                                               | `''`             |
| `folder`        | `<string>` The folder name.                                                     | `''`             |
| `fileName`      | `<string>` The file name within the folder.                                     | `''`             |
| `folderRefresh` | `<number>` The number of minutes before the folder will be checked for changes. The minimum refresh time is 15 minutes. | `0` (no refresh) |

#### Properties
| Property         | Type                                              | Default |
| ---------------- | ------------------------------------------------- |:-------:|
| `url`            | `<string>` The URL target of the request.         | `''`    |
| `isCacheRunning` | `<boolean>` Whether or not Rise Cache is running. | `false` |

#### Events
| Event                   | Description                        |
| ----------------------- | -----------------------------------|
| `rise-storage-response` | Fired when a response is received. |
| `rise-storage-error`    | Fired when an error is received.   |


#### Methods
| Method | Description                                    |
| ------ | ---------------------------------------------- |
| `go`   | Performs an Ajax request to the specified URL. |

## Built With
- [Polymer](https://www.polymer-project.org/)
- [npm](https://www.npmjs.org)
- [Bower](http://bower.io/)
- [Gulp](http://gulpjs.com/)
- [Mocha](http://mochajs.org/), [Chai](http://chaijs.com/) and [web-component-tester](https://github.com/Polymer/web-component-tester) for testing

## Development

### Dependencies
* [Git](http://git-scm.com/) - Git is a free and open source distributed version control system that is used to manage our source code on Github.
* [npm](https://www.npmjs.org/) & [Node.js](http://nodejs.org/) - npm is the default package manager for Node.js. npm runs through the command line and manages dependencies for an application. These dependencies are listed in the _package.json_ file.
* [Bower](http://bower.io/) - Bower is a package manager for Javascript libraries and frameworks. All third-party Javascript dependencies are listed in the _bower.json_ file.
* [Gulp](http://gulpjs.com/) - Gulp is a Javascript task runner. It lints, runs unit and E2E (end-to-end) tests, minimizes files, etc. Gulp tasks are defined in _gulpfile.js_.

### Local Development Environment Setup and Installation
To make changes to the web component, you'll first need to install the dependencies:

- [Git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Node.js and npm](http://blog.nodeknockout.com/post/65463770933/how-to-install-node-js-and-npm)
- [Bower](http://bower.io/#install-bower) - To install Bower, run the following command in Terminal: `npm install -g bower`. Should you encounter any errors, try running the following command instead: `sudo npm install -g bower`.
- [Gulp](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md) - To install Gulp, run the following command in Terminal: `npm install -g gulp`. Should you encounter any errors, try running the following command instead: `sudo npm install -g gulp`.

The web components can now be installed by executing the following commands in Terminal:
```
git clone https://github.com/Rise-Vision/web-component-rise-storage.git
cd web-component-rise-storage
npm install
bower install
```

### Run Locally
You can access the `demo.html` file via a local web server. On Mac, execute the following command from the root directory of the web component:
```
python -m SimpleHTTPServer
```

This starts a web server on port 8000, and you can access the Rise Storage web component by navigating to `localhost:8000/demo.html`.

### Testing
You can run the suite of tests via a local web server. On Mac, execute the following command from the root directory of the web component:
```
python -m SimpleHTTPServer
```

This starts a web server on port 8000, and you can run the tests by navigating to `http://localhost:8000/test/index.html`.

### Deployment
Once you are satisifed with your changes, deploy the `components` and `rise-storage` folders to your server. You can then use the web component by following the *Usage* instructions.

## Submitting Issues
If you encounter problems or find defects we really want to hear about them. If you could take the time to add them as issues to this Repository it would be most appreciated. When reporting issues, please use the following format where applicable:

**Reproduction Steps**

1. did this
2. then that
3. followed by this (screenshots / video captures always help)

**Expected Results**

What you expected to happen.

**Actual Results**

What actually happened. (screenshots / video captures always help)

## Contributing
All contributions are greatly appreciated and welcome! If you would first like to sound out your contribution ideas, please post your thoughts to our [community](http://community.risevision.com), otherwise submit a pull request and we will do our best to incorporate it.

## Resources
If you have any questions or problems, please don't hesitate to join our lively and responsive community at http://community.risevision.com.

If you are looking for user documentation on Rise Vision, please see http://www.risevision.com/help/users/

If you would like more information on developing applications for Rise Vision, please visit http://www.risevision.com/help/developers/.

**Facilitator**

[Donna Peplinskie](https://github.com/donnapep "Donna Peplinskie")
