# qu

[![Build Status](https://travis-ci.org/cfpb/qu.png)](https://travis-ci.org/cfpb/qu)

_qu_ is an **in-progress** data platform created by the [CFPB][] to
serve their public data sets.

The goals of this platform are to:
* Import data in our
  [Google-Dataset-inspired format][dataset-inspired]
* Query data using our
  [Socrata-Open-Data-API][soda]-inspired API
* Export data in JSON or CSV format

[CFPB]: http://www.consumerfinance.gov/
[dataset-inspired]: https://github.com/cfpb/qu/wiki/Dataset-publishing-format
[soda]: http://dev.socrata.com/consumers/getting-started/

## Getting Started

### Prerequisites

In order to work on _qu_, you need the following languages and tools
installed:

* [Java][]
* [Node.js][]
* [Leiningen][]
* [Grunt][]
* [Bower][]
* [MongoDB][]

[Java]: http://www.java.com/en/
[Node.js]: http://nodejs.org/
[Leiningen]: http://leiningen.org/
[Grunt]: http://gruntjs.com/
[Bower]: http://twitter.github.com/bower/
[MongoDB]: http://www.mongodb.org/

### Setup

Once you have the prerequisites installed and the code downloaded and
expanded into a directory (which we will call "qu"), run the following
commands:

```sh
cd qu
lein deps
npm install -g grunt-cli bower
npm install && bower install
grunt
```

If editing the JavaScript or CSS, run the following to watch the JS
and CSS and make sure your changes are compiled:

```sh
grunt watch
```

You can run `grunt` to compile the files once.

To start a Clojure REPL to work with the software, run:

```sh
lein repl
```

In order to run the API as a web server, run:

```sh
lein ring server
```

Go to http://localhost:3000 and you should see the app running.

Before starting the API, you will want to start MongoDB and load some
data into it. Currently, _qu_ only supports connecting to a local
MongoDB connection.

### Loading data

Make sure you have MongoDB started. To load some sample data, run
`lein repl` and enter the following:

```clojure
(require 'cfpb.qu.loader)
(in-ns 'cfpb.qu.loader)
(mongo/connect!)
(load-dataset "county_taxes")
(load-dataset "census") ; Takes quite a while to run; can skip.
(mongo/disconnect!)
```

