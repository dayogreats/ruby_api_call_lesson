# MAKING AN API CALL USING RUBY

[layout	title	     length	tags
page    Flow Control 60     fundamentals, computer science]

# Learning Goals
-	Whet your appetite on how web API works 
-	Know possible ways of making API calls
-	Using ruby standard libraries: Net/HTTP, URI, OpenURI, JSON
-	Show you how to find a third-party a rubygem that makes API call a breeze
 
# Introduction 
It is a known fact that our world today is now a global village where we are connected to the world like never before. Connectivity is amazing! We can now purchase, post, pin and pick almost anything - anywhere because we are connected together.

# Ever wondered how data move from place to place?
How different devices and applications are connected to each other making it possible for us to book flight / hotel reservations, buy goods on amazon, call Uber’s driver for ride or perhaps enroll for Turing School of Software?

# API, unsung hero of our connected world
Well `HTTP` is the king of the web services while the unsung hero of our connected world is API today. API is the engine that inspire innovation in our today’s world.  It’s behind scene and we take it for granted. It’s the engine under the hood that makes all the interactivities we all expect and rely upon online every day. 

# TAKE FOR EXAMPLE
We are all used to making Direct Flight Reservation online where we choose departure, destination and dates etc. Then that information is used to search the server the airline database directly for seat availability and cost based on some variables.  

But imagine a third-part travel service (like [Google Flight](https://www.google.com/flights/) ) that aggregates information from many airline servers for booking seat availability, date, cost and then display the response back to user.  It’s API that makes services like travel services possible to exist today. 

# Waht is API?
In plain word, API (Application Programming Interface) is a messenger that takes a request and tells the system what you want to do and return a response back to you.  In other words, an access given to interact with program / services remotely over the web. 

HTTP makes connectivity between web servers possible. Without Http Interaction with web services in a distance world will be impossible.


** [ CLIENT --->>--- Http Req --->>--- SERVER ] 

** [ CLIENT ---<<--- Http Res ---<<--- SERVER ]

# MATERIALS
At the end of this lesson we will use our ruby knowledge as listed above to build a command line ruby application:
- That prompts users to enter a url
- checks if the uri entered by the user is a valid uri
- Makes a remote request to an endpoint 
- Then display a returned json data


### [Demo](http://www.github.com/dayogreats/ruby_api_call)
I will walk you through the demo codes. 

# Ruby standard kibraries
+ [Open-uri](https://ruby-doc.org/stdlib-2.3.0/libdoc/open-uri/rdoc/OpenURI.html) is an easy-to-use wrapper for Net::HTTP, Net::HTTPS and Net::FTP
+ [Net::HTTP](https://ruby-doc.org/stdlib-2.3.0/libdoc/net/http/rdoc/Net/HTTP.html) provides a rich library which can be used to build HTTP user-agents
+ [URI](https://ruby-doc.org/stdlib-2.3.0/libdoc/uri/rdoc/URI.html) requiring `net/http` will also require ‘uri’ so you don’t need to require it separately


In this lesson we will focus on `open-uri` because it makes it possible to open an http, https or ftp URL as though it were a file:

#Introduction to New Material (I do)

** SCRAPING THE WEB WITH OPENURI
```
open("http://www.ruby-lang.org/") {|f|
  f.each_line {|line| p line}
}
```

Or 

```
open("http://www.ruby-lang.org/en") {|f|
  f.each_line {|line| p line}
  p f.base_uri         # <URI::HTTP:0x40e6ef2 URL:http://www.ruby-lang.org/en/>
  p f.content_type     # "text/html"
  p f.charset          # "iso-8859-1"
  p f.content_encoding # []
  p f.last_modified    # Thu Dec 05 02:45:02 UTC 2002
}
```

# Guided Practice (We do)
- Lets open and run the `you_do.rb` file in this excercise folder 
- Then change the uri from `http://www.ruby-lang.org/en` to `http://www.turing.io` in file and run the code 

# Third-Party Gem
- Rubygems [http://www.rubygems.org] is a place to find ruby gems.

# Httparty
Makes http fun again! 

** Example 
```
# Use the class methods to get down to business quickly
response = HTTParty.get('http://api.stackexchange.com/2.2/questions?site=stackoverflow')

puts response.body, response.code, response.message, response.headers.inspect

# Or wrap things up in your own class
class StackExchange
  include HTTParty
  base_uri 'api.stackexchange.com'

  def initialize(service, page)
    @options = { query: { site: service, page: page } }
  end

  def questions
    self.class.get("/2.2/questions", @options)
  end

  def users
    self.class.get("/2.2/users", @options)
  end
end

stack_exchange = StackExchange.new("stackoverflow", 1)
puts stack_exchange.questions
puts stack_exchange.users
```

Lets open and run the `example_httparty.rb` file in this excercise folder 

# Assignments
- Find another third-party ruby gem that will serve as alternative to httparty  [here](https://rubygems.org) 

# Links
- [Stackoverflow](https://stackoverflow.com/questions/16764030/what-is-the-difference-between-rubys-open-uri-and-nethttp-gems)
- [Net/Http](https://ruby-doc.org/stdlib-2.3.0/libdoc/net/http/rdoc/Net/HTTP.html)
- [Open-uri](https://ruby-doc.org/stdlib-2.3.0/libdoc/open-uri/rdoc/OpenURI.html)
- [Uri](https://ruby-doc.org/stdlib-2.3.0/libdoc/uri/rdoc/URI.html)
- [HttParty](http://jnunemaker.github.com/httparty)

