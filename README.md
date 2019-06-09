# ELK-Stack
how to use ELK, docker and designing scalable systems big data
In this section, logs are indexed by filebeat. At first, the log file is logged as apache_logs and in kibana several graphs are drawn in visual form.
Then, at the end, both the log files are indexed.
For settings, the address of the log files should be in the filebe file config file.

Given the settings made in the filebeat.yml file in the filebeat prospectors section, the path of both files is given. Then in the Elasticsearch output field it is specified where the elasticsearch address is located and the output will go to this address.
The following commands can be used to enable the apache2 module:

./filebear modules enable apache2

./filebear setup -e

./filebeat -e

The first setting is only for the apache log. Which is called apache_2.conf

The apache_multi.conf file is used to index both files whose filtering is restricted by type to be distinguished between two distinct files. For this purpose, the apache file is named apache with type and vhost file with type called vhost. Then,with use of "if else", these two are distinct and each has its own grok.

In elastic search 5, the number of shards and replicas for each index is made online by the API. (Unlike previous versions that were made in the elasticsearch.yml settings file this change).

For logstash scalability, you can use apache kafka. This distributed system plays the role of a broker for messages and buffs logstash messages. Logstash can boost CPU utilization. By default, logstash buffers messages that can not be reached for any reason, which may cause buffering in the source. This may involve consuming other resources, such as storage media. To solve this problem, kafka, which is separate from the data provider, completely buffs the data. If you increase the data, you can increase the number of kafka brokers and add the buffer size.
