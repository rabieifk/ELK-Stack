# ELK-Stack

**Objective:** Using ELK and Docker to design a scalable system to manage large volume of unstructed data.


"ELK" is the acronym for three open source projects: Elasticsearch, Logstash, and Kibana. Elasticsearch is a search and analytics engine. Logstash is a server‑side data processing pipeline that ingests data from multiple sources simultaneously, transforms it, and then sends it to a "stash" like Elasticsearch. Kibana lets users visualize data with charts and graphs in Elasticsearch. The Elastic Stack is the next evolution of the ELK Stack. [reference](https://www.elastic.co/elk-stack)

First, the [Apache logs](https://github.com/rabieifk/ELK-Stack/blob/master/apache_logs) file should be indexed by using filebeat, the file of apache_logs contains the date of the logs which is between 00:00:00 17-05-2015 and 12:00:00 21-05-2015. We can erase the indexes by REST API.

Secondly, I read the log file with logstash and the the result is stored in Elasticsearch, to do so I should set a filter to index the date and time in the Z ss:mm:HH:YYYY/MMM/dd format. Also the geoip should be used to store spatial information of logs.

Given the settings made in the filebeat.yml file in the filebeat prospectors section, the path of both files is given. Then in the Elasticsearch output field it is specified where the Elasticsearch address is located and the output will go to this address.
The following commands can be used to enable the apache2 module:

./filebear modules enable apache2

./filebear setup -e

./filebeat -e

The first setting is only for the apache log. Which is called apache_2.conf

The apache_multi.conf file is used to index both files whose filtering is restricted by type to be distinguished between two distinct files. For this purpose, the apache file is named apache with type and vhost file with type called vhost. Then,with use of "if else", these two are distinct and each has its own grok.

In elastic search 5, the number of shards and replicas for each index is made online by the API. (Unlike previous versions that were made in the elasticsearch.yml settings file this change).

For logstash scalability, you can use apache kafka. This distributed system plays the role of a broker for messages and buffs logstash messages. Logstash can boost CPU utilization. By default, logstash buffers messages that can not be reached for any reason, which may cause buffering in the source. This may involve consuming other resources, such as storage media. To solve this problem, kafka, which is separate from the data provider, completely buffs the data. If you increase the data, you can increase the number of kafka brokers and add the buffer size.
