# ruby cheatsheats

https://github.com/ThibaultJanBeyer/cheatsheets/blob/master/Ruby-Cheatsheet.md

## besides

* 0, empty string and empty array are all evaluate to true!
* start website from folder: `ruby -run -e httpd . -p 5000`

## tcp server

```
require 'socket'
server = TCPServer.new 5678

while session = server.accept
    session.puts "Hello world! The time is #{Time.now}"
    session.close
end
```

## tcp client

```
require 'socket'
server = TCPSocket.new 'localhost', 5678

while line = server.gets
    puts line
end

server.close
```

## http server

```
require 'socket'
require 'net/http'

server = TCPServer.new 8080

while session = server.accept
    request = session.gets
    puts request

    #option 1
    #response = `curl http://quotes.rest/qod.json`

    #option 2    
    stack = Net::HTTP.new 'quotes.rest'
    page = '/qod.json'
    response = stack.get(page).body

    session.print "HTTP/1.1 200\r\n" # 1
    session.print "Content-Type: text/html\r\n" # 2
    session.print "\r\n" # 3
    session.print "Hello world! The time is #{Time.now}" #4
    session.print response

    session.close
end
```
