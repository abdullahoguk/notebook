##Node JS
* Apache is multithreaded but has blocking
* Node is one threaded and non blocking event driven io
* installation
```
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install -y build-essential
```
* update 
```
sudo npm cache clean -f
sudo npm install -g n
sudo n v4.4.5  // version
```
* switch versions with nvm
```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.1/install.sh | bash
nvm install <version>       //Download and install a <version>
nvm use <version>           //Modify PATH to use <version>
nvm ls                      //List versions (installed versions are blue)
```
* run file with `node <filename.js`
* `global` is main object (like `window` object in js)
* Global objects are `__dirname` `__filename` `console` `require()` `process` etc.
* STD Input and output(process object)
```
process.stdout.write("bla"); //outputs to console

process.stdin.on("data",function(data){
    process.stdout.write("\n"+data.toString().trim() + "\n")
    process.exit();
})
```
* Timeout and interval is the same with JS
* Readline
```
var readline = require('readline');
var rl = readline.createInterface(process.stdin,process.stdout)
rl.question("Question text", function(answer){//callback funct.
    console.log(answer)
})
```
* Event Emitter lets you create custom events.
```
var events = require("events");
var emitter = new events.EventEmitter();
//create event
emitter.on("myEvent", function(message,status){
    console.log(`${status}: ${message}`)
})

emitter.emit('myEvent',"hello","200 OK");//use that event
```
* Inheritence
```
var util = require("util");
var emitter = require("events").EventEmitter();

var Person = function(name){
    this.name = name;
}

util.inherits(Person,EventEmitter);

```
* Make a js file a module to reuse in other js files, `module.exports = object_name;` 
* Execute terminal commands
```
var exec = require("child_process").exec;
exec("xfce4-terminal");
exec("ls", function(err, stdout){
    if (err){throw err;}
    else{console.log(stdout)}
    
});
```
* **FILESYSTEM** `var fs = require("fs");`
     * Listing
```
var files = fs.readdirSync("./lib");
console.log(files);
```
    * ReadFile
```
var contents = fs.readFileSync("d3.md","UTF-8")
```
    * Write to file
```
//Creates file
fs.writeFile("filename.md", content_string, function(err){
    console.log("ddfd");
})

//Appends content to a file
fs.appendFile("filename.md", content_string,function(){  })
```
    * Create and remove directory
```
control existence of folder
if(fs.existSync("folderName")){
    ...
}
else{
    //Creates directory
    fs.mkdir("folderName", function(err){
    console.log("Folder created");
    });    
}

//remove dir(dir shoud be empty)
fs.rmdir("folderName", function(err){
    console.log("Folder removed");
    });

```
    * Move,rename,remove a file
```
//rename file or folder
fs.renameSync("fileName_with_dir","NEWfileName_with_dir");

//for move, use rename and change dir in second argument

//remove
fs.unlinkSync("fileName_with_dir");
```
    * Readable streams
```
var stream = fs.createReadStream("fileName","UTF-8");
var data = "";

//runs once when the first data event happen
stream.once("data",function(){
  ...
});


stream.on("data",function(chunk){
   process.stdout.write("chunksize "+ chunk.length);
   data += chunk;
});

//runs when the stream ends
stream.on("end",function(){
   ...
});
```
    * Writable streams
```
var stream = fs.createWriteStream("fileName");
stream.write("Content string");
stream.close();
```
* **HTTP**
    * create basic http server
```
var http=require("http");

var server = http.createServer(function(request,response){
    response.writeHead(200,{"Content-Type":"text/html"});
    response.write("<h1>WELCOME TO HTTP SERVER<h1>");
    response.end();
});

server.listen(8888);
```
    * create basic https request
```
var http=require("https");
var fs = require("fs");

var options = {
    hostname: "en.wikipedia.org",
    port: 443,
    path: "wiki/George_Washington",
    method: "GET"
};

//Response is a stream
var req = https.request(options, function(response){
    var responseBody = "";
    console.log("Status: " + response.statusCode + "\nResponse Headers: " + response.headers);

    response.setEncoding("UTF-8");
});
req.end();
```
    * create basic file server
```
var http = require("http");
var fs = require("fs");
var path = require("path");

//create server
http.createServer(function(request,response){
    console.log(`${request.method} requests for ${request.url}`)

    if(request.url === "/"){
        //homepage file is in public folder
        fs.readFile("./public/index.html","UTF-8",function(err,content){
            response.writeHead(200,{"Content-Type":"text/html"});
            response.end(content);   
        });
    else if (request.url.match(/.css$/)) {
        var cssPath = path.join(__dirname, 'public', request.url);
        var fileStream = fs.createReadStream(cssPath, "UTF-8");

        response.writeHead(200, {"Content-Type": "text/css"});
        fileStream.pipe(response);

    } else if (request.url.match(/.jpg$/)) {
        var imgPath = path.join(__dirname, 'public', request.url);
        var imgStream = fs.createReadStream(imgPath);

        response.writeHead(200, {"Content-Type": "image/jpeg"});
        imgStream.pipe(response);
    }else{
        response.writeHead(404,{"Content-Type":"text/html"});
        response.end("404 file not found")
    }

}).listen(8888);
```
    * create api server
```
var http = require("http");
var data = require("pathto/file");

http.createServer(function(request,response){
    response.writeHead(200,{"Content-Type": "text/json"});
    response.end(JSON.stringify(data));
}).listen(3000);
```
    * create form server
```
var http = require("http");
var fs = require("fs");

http.createServer(function(req, res) {
    if (req.method === "GET") {
        res.writeHead(200, {"Content-Type": "text/html"});
        fs.createReadStream("./public/form.html", "UTF-8").pipe(res);
    } else if (req.method === "POST") {
        var body = "";

        req.on("data", function(chunk) {
            body += chunk;
        });

        req.on("end", function() {
            res.writeHead(200, {"Content-Type": "text/html"});
            res.end(`
                <!DOCTYPE html>
                <html>
                    <head>
                        <title>Form Results</title>
                    </head>
                    <body>
                        <h1>Your Form Results</h1>
                        <p>${body}</p>
                    </body>
                </html>
            `);
        });
    } 
}).listen(3000);
console.log("Form server listening on port 3000");
```
* Packages 
    * `httpster`
    * `express` framework 
    * 