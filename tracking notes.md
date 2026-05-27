# Building an Elastic Interface Using Docker Containers

Docker is a lightweight build engine that leverages the Linux CLI. It processes builds quickly and provides built-in protection against shutdowns, maximizing availability through the use of nodes for redundant support across multiple containers.

The docker-compose file references an Elasticsearch image. The image holds a read-only version of the application for Docker to use. So in the first couple lines of the docker-compose file you can find `image: docker.elastic.co/elasticsearch/elasticsearch:${ES_VERSION}` — this references that image to run in the node specified in that code. I downloaded the image from elastic.co using git commands provided there.

I built the first 3-node cluster for operation using Claude AI to assist; it did not build correctly at first. From there I used Gordon, the built-in Docker AI, to correct the files and the build succeeded.

I studied the docker-compose file line by line so I could understand what had been built, then tested the website. Found that Elastic was not running. Containers all showed healthy.

Checked the logs for build output: authentication error — the setup container was attempting to log in before the application nodes were ready.

Used Gordon to correct the authentication. It created another container called "setup-users." From what I can tell, that should not be needed; I should be able to write in a stop-and-retry on a timer for the original setup container.

learned ElasticSearch is more the for the storage and indexing of data. You require other tools in the ecosystem to make the process work. one tool to log and ship the data (filebeat) 
Installed filebeat using git pull request from 'https://www.elastic.co/docs/reference/logstash/docker'

Found fleet is simpler than filebeat and a better begining stage, need to learn to add fleet to feed data into Elastic. 


Current targets being researched:
1. Integration to use in Elastic for home lab testing
2. Review how to have setup complete authentication instead of needing a separate container for that action.
3. look into fleet policies and agents, fleet controller, 
4. Set up VM for elastic data lake and fleet testing
