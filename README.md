# curl2tsung
A simple utility to convert a curl request to tsung's xml request. Useful for
quickly generating tsung's xml conf rather than typing xml yourself.

[Firefox](https://developer.mozilla.org/en-US/docs/Tools/Network_Monitor#Copy_as_cURL) and
[Chrome](https://developers.google.com/web/tools/chrome-devtools/network-performance/resource-loading#curl) support
copying an http request as curl command from the web developer tools. You can
use that feature to copy a request as curl and then replace curl with curl2tsung
script. It currently supports only the most common curl options I encountered
while dealing curl commands generated with firefox and chrome developer tools.

## Usage

A request to github.com, 'copied as curl' from chrome developer tools looks like this

``` shell
curl 'https://github.com/' -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8' -H 'Connection: keep-alive' -H 'Accept-Encoding: gzip, deflate, sdch, br' -H 'Accept-Language: en-US,en;q=0.8' -H 'Upgrade-Insecure-Requests: 1' -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.71 Safari/537.36' --compressed
```

Replacing curl with curl2tsung utility generates following output:

``` xml
<request>
  <http method="GET" url="https://github.com/" version="1.1">
    <http_header name="Accept-Language" value="en-US,en;q=0.8"/>
    <http_header name="Accept-Encoding" value="gzip, deflate, sdch, br"/>
    <http_header name="Accept" value="text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8"/>
    <http_header name="User-Agent" value="Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.71 Safari/537.36"/>
    <http_header name="Connection" value="keep-alive"/>
    <http_header name="Upgrade-Insecure-Requests" value="1"/>
  </http>
</request>
```
