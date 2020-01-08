# Python cheatsheets

https://github.com/ehmatthes/pcc/releases/download/v1.0.0/beginners_python_cheat_sheet_pcc_all.pdf

https://github.com/ThibaultJanBeyer/cheatsheets/blob/master/python-cheatsheed.md

## Besides
### Install module when multi python version are installed
`pythonx -m pip install <modulename>`

### Serve current folder
`python3 -m http.server`

`python -m SimpleHTTPServer`

### Simple web server
```
from http.server import HTTPServer, BaseHTTPRequestHandler
from datetime import datetime
import requests

class Server(BaseHTTPRequestHandler):
    def do_GET(self):
        self.send_response(200)
        self.end_headers()
        r = 'hello world @ {}\n{}\n{}\n{}'
        self.wfile.write(bytes(r.format(str(datetime.utcnow()), str(self.command), str(self.path), str(self.headers)), 'utf-8'))
        
        try:
            r = requests.get('http://worldclockapi.com/api/json/utc/now')
            self.wfile.write(bytes(r.text, 'utf-8'))
        except Exception as error:
            print ('Error when access web! -----------------------------------------')
            print (error)

        try:
            f = open("150.txt", "r")
            self.wfile.write(bytes(f.read(), 'utf-8'))
        except Exception as error:
            print ('Error when read file! -----------------------------------------')
            print (error)

httpd = HTTPServer(('localhost', 8080), Server)
httpd.serve_forever()

```
