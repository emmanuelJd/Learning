**A web worker is a JavaScript that runs in the background, independently of other scripts, without affecting the performance of the page. You can continue to do whatever you want: clicking, selecting things, etc., while the web worker runs in the background.**

You can use it, with this synthax :<br>
                `var worker = new Worker("script_workers.js");`<br>
_The code that a web worker execute needs to be contained in a separate file because it is run in an isolated thread "script_worker.js"_<br>

**Why should I use it ?**<br>
One thing that's remained a hindrance for JavaScript is actually the language itself. JavaScript is a single-threaded environment, meaning multiple scripts cannot run at the same time. As an example, imagine a site that needs to handle UI events, query and process large amounts of API data, and manipulate the DOM. Pretty common, right? Unfortunately all of that can't be simultaneous due to limitations in browsers' JavaScript runtime. Script execution happens within a single thread.

The Web Workers specification defines an API for spawning background scripts in your web application. Web Workers allow you to do things like fire up long-running scripts to handle computationally intensive tasks, but without blocking the UI or other scripts to handle user interactions

**An example**<br>

At first check if the user's browser support web worker.
                if (typeof(Worker) !== "undefined") {
                    // Web worker support!
                } else {
                    // No Web Worker support.
                }

Then, this is a script that take a long time to be fully execute, result is a freezing web page for some second :
_These code has been implemented by a senior developer don't try this at home_

script JavaScript : _main.js_ <br>
                var res = 0;
                for(var i = 0; i < 5000000000 ;i++){
                   res += i;
                };
Adding this script to a Html page can cause some freeze.

To prevent html page to be in the state, you can use a web worker to do a long process script ( long calcul, read / parse a file, etc ).
Usually another file is using to implement the script of the worker but you can use a blob :<br>

                var blob = new Blob([
                    "onmessage = function(e) { var res = 0;for(var i = 0; i < 5000000000 ;i++){res += i;};postMessage(res); }"]);
                
                // Obtain a blob URL reference to our worker 'file'.
                var blobURL = window.URL.createObjectURL(blob);
                
                var worker = new Worker(blobURL);
                worker.onmessage = function(e) {
                    console.log(e.data);
                };
                worker.postMessage(""); //Start the worker.

**Source for more details**<br>
[The Basics of Web Workers](http://www.html5rocks.com/en/tutorials/workers/basics/)<br>
[Mozilla Developer Network](https://developer.mozilla.org/fr/docs/Utilisation_des_web_workers)<br>
[w3schools.com](http://www.w3schools.com/html/html5_webworkers.asp)<br>
