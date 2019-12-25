# networkstuff
elasticsearch, zeek and whatnot...

I had some troubles with getting the zeek-module for filebeat to show a nice dashboard in kibana. So I googled and followed the not so many examples.

I did the installation on Kali linux on a computer with celeron CPU and four TP-interfaces. 
*Intel(R) Celeron(R) 29xxu @ 1.40GHz*

Zeek takes up most of the CPU but Kibana and elastic is still running fine with 8 GB RAM. This is on a small home network..

At elastic.co the help page was not really giving the help I needed:
https://www.elastic.co/guide/en/beats/filebeat/master/filebeat-module-zeek.html

First out you need to change the ascii-logger to log in json format:

I did that by changing "use_json" to "T" in /usr/local/zeek/share/zeek/base/frameworks/logging/writers/ascii.zeek
const use_json = T &redef;

Then, in /etc/filebeat/modules.d/zeek.yml added var.paths to all logging options:
```
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
```

Everything else was pretty standard and easy to find solutions for or had very informative error messages.
