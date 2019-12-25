# networkstuff
elasticsearch, zeek and whatnot...

I had some troubles with getting the zeek-module for filebeat to show a nice dashboard in kibana. So I googled and followed the not so many examples.

At elastic.co the help page was not really giving the help I needed:
https://www.elastic.co/guide/en/beats/filebeat/master/filebeat-module-zeek.html

First out you need to change the ascii-logger to log in json format:
