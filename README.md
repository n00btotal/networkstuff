# networkstuff
elasticsearch, zeek and whatnot...

I had some troubles with getting the zeek-module for filebeat to show a nice dashboard in kibana. So I googled and followed the not so many examples.

At elastic.co the help page was not really giving the help I needed:
https://www.elastic.co/guide/en/beats/filebeat/master/filebeat-module-zeek.html

First out you need to change the ascii-logger to log in json format:

I did that by changing "use_json" to "T" in /usr/local/zeek/share/zeek/base/frameworks/logging/writers/ascii.zeek
const use_json = T &redef;

Then, in /etc/filebeat/modules.d/zeek.yml added var.paths to all logging options:
[code]
- module: zeek
  # All logs
  connection:
    enabled: true
    var.paths: ["/usr/local/zeek/logs/current/conn.log*"]
  dns: 
    enabled: true
    var.paths: ["/usr/local/zeek/logs/current/dns.log*"]
  http:
    enabled: true
    var.paths: ["/usr/local/zeek/logs/current/http.log*"]
  files:
    enabled: true
    var.paths: ["/usr/local/zeek/logs/current/files.log*"]
  ssl:
    enabled: true
    var.paths: ["/usr/local/zeek/logs/current/ssl.log*"]
  notice:
    enabled: true
    var.paths: ["/usr/local/zeek/logs/current/notice.log*"]
[/code]
