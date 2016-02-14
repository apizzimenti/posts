**February 13, 2016**

I had a few prerequisites for building this site, so before I started, I needed a few things:

* purchase a VPC (virtual private cloud) server from Amazon Web Services
* purchase the domain name (very lucky)
* create an (extremely) small express server
* write the site
* make a posts repo

These things were reasonably time-consuming. So, let's go through each.

1 - purchase a VPC server from Amazon Web Services

This was the easy-ish part. There are easy-to-follow instructions from Amazon, and I set up a VPC instance running 
Ubuntu (for easy Node integration). I installed Node.js, ran into a few troubles, but worked everything out and created
two directories, one for the server and one for the `dist` folder of my website.

I set up an Elastic IP address so when I purchased the domain name, I'd be able to route directly to the server, and set
the security rules to open up port 80 for HTTP traffic. Nice way to start my evening last night.

2 - purchase the domain name

I just used GoDaddy to buy apizzimenti.com, no problem. Took 5 minutes. Done and done.

3 - write an `express` server

here's the whole thing:

```
var express = require('express'),
    app = express();

app.use(express.static('/home/ubuntu/dist/'));

app.get('/', function (req, res) {
    res.sendFile('/home/ubuntu/dist/index.html');
}).listen(8080, function () {
    console.log('listening!');
});
```

That's it. Everything is stored in `/dist`, so `express` serves all the files statically.

4 - write the site

I used `yeoman` and its `angular-generator` to get a basic app layout. My original idea was to have a database where all
my posts were stored, but I tossed that out the window because it'd be too much server work. I decided to use a GitHub repo
and just grab my posts from the repo all at once using the GitHub api. I also wanted to be able to handle mathtyping (LaTeX),
so I used what I call grease functions to integrate it.

Grease functions are self-invoking functions that, when the dependency can't be installed with `npm` or `bower` and work
out of the box, I use to make my life a little easier. They allow for the smooth (*greasy*) transition between libraries
and their uses in my apps. They're usually quite small, performing a regex or config task that is crucial to the integration
of the library or dependency.

Anyway, angular goes out and grabs the posts and data from GitHub, transpiles the markdown to html, and slams it onto the
correct page. That's what happens for essentially everything.

5 - make a posts repo

I wanted to store my posts and information in a logical, organized place that was easy to reach. GitHub was the first choice,
and I can do essentially whatever I want here. It's a great time.