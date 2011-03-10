= Ruby HTTP Client

== SYNOPSIS

Patron is a Ruby HTTP client library based on libcurl. It does not try to expose
the full "power" (read complexity) of libcurl but instead tries to provide a
sane API while taking advantage of libcurl under the hood.


== USAGE

Usage is very simple. First, you instantiate a Session object. You can set a few
default options on the Session instance that will be used by all subsequent
requests:

    sess = Patron::Session.new
    sess.timeout = 10
    sess.base_url = "http://myserver.com:9900"
    sess.headers['User-Agent'] = 'myapp/1.0'
    sess.enable_debug "/tmp/patron.debug"

The Session is used to make HTTP requests.

    resp = sess.get("/foo/bar")

Requests return a Response object:

    if resp.status < 400
      puts resp.body
    end

The GET, HEAD, PUT, POST and DELETE operations are all supported.

    sess.put("/foo/baz", "some data")
    sess.delete("/foo/baz")

You can ship custom headers with a single request:

    sess.post("/foo/stuff", "some data", {"Content-Type" => "text/plain"})

That is pretty much all there is to it.


== REQUIREMENTS

You need a recent version of libcurl in order to install this gem. On MacOS X
the provided libcurl is sufficient. You will have to install the libcurl
development packages on Debian or Ubuntu. Other Linux systems are probably
similar. Windows users are on your own (not any more => see below). Good luck with that.


== INSTALL

  sudo gem install patron

== WINDOWS INSTALL

= Download and Install curl for win32
  - Download the last version of win32 curl (http://www.gknw.net/mirror/curl/win32/curl-7.21.4-devel-mingw32.zip)
  - Extract curl-7.21.4-devel-mingw32.zip to a folder (path should not include spaces). In my case, I put it in : c\curl-7.21.4-devel-mingw32
  - Add the path to curl bin dir (C:\curl-7.21.4-devel-mingw32\bin) to your Path environment variable.
  - Test curl: 
       Open a console and try the command : curl -V

= INSALL patron
   - Download the source of this gem
   - Build the gem: 
     gem build patron.gemspec
  - Install the gem: 
    gem install patron-0.4.12.gem -- --with-curl-lib="C:/curl-7.21.4-devel-mingw32/lib" --with-curl-include="C:/curl-7.21.4-devel-mingw32/include"  

Copyright (c) 2008 The Hive
