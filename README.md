# elk-stack-logging-example
How to perform centralize logging in microservice architecture using ELK Stack

###### Download ELK Binary Distrubution

###### 1.Elastic Search [Download](https://www.elastic.co/downloads/elasticsearch).
###### 2.Logstash [Download](https://www.elastic.co/downloads/kibana).
###### 3.Kibana [Download](https://artifacts.elastic.co/downloads/logstash/logstash-7.6.2.zip).

# https://www.youtube.com/watch?v=5s9pR9UUtAU&ab_channel=JavaTechie
After configuration of elasticsearch and kibana from "Tips and trick ELK.docx" file below are the step need to flow.

1) Goto logstash >> config folder >> create a file named as logstash.conf below are the configuration need to do in logstash.conf file.

input {
	file {
		path => "D:/Configure-Stuff/Git/OWN_REPO/elk-stack-logging-example/elk-stack.log"
		start_position => "beginning"
	}
}

output {
	
	stdout {
		codec => rubydebug
	}
  elasticsearch {
    hosts => ["http://localhost:9200"]
	index => "elk.logstash.test"
	user => "elastic"
    password => "<password generated from elastisearch cmd = elasticsearch-reset-password -u elastic>"
  }
}

2) Go to Kibana http://localhost:5601/  and  create indices in kibana >> Management >> Dev Tool >> Console >> run the below command 
	a) PUT elk.logstash.test
	b) GET elk.logstash.test/_searc
3) make sure the elasticsearch and kibana is up
4) now run the logstash server by cmd = logstash -f .\..\config\logstash.conf --config.reload.automatic
5) hit the restapi and test the log

	http://localhost:9200/_cat
	http://localhost:9200/_cat/indices
	http://localhost:9200/elk.logstash.test/_search




