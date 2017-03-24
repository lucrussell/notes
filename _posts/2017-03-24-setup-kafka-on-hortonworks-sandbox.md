---
post_title: How to Set Up Kafka on Hortonworks Sandbox (Docker version)
layout: post
published: true
tags:
  - kafka
categories:
  - kafka
---

## How to Set Up Kafka in Hortonworks Sandbox (Docker version)
Assumes a container was previously set up following [these instructions](https://community.hortonworks.com/articles/58458/installing-docker-version-of-sandbox-on-mac.html) and you now want to enable the Kafka service.


1. Stop and delete existing an existing sandbox container if one was already created:

        docker stop sandbox
        docker rm sandbox

2. Add the default Hortonworks Kafka port to the `create_container.sh` script:

        -p 6667:6667

3. Recreate and start the container:

        ./create_container.sh

4. SSH to the new container and start services. The password for the newly created container will have been reset to the hortonworks default (`hadoop`), so you'll need to reset it at this point:

        ssh -p 2222 root@localhost
        The password for the newly created container will have been reset to the hortonworks default (`hadoop`), so you'll need to reset it at this point.

5. When started, go to http://localhost:8080/#/login login as `maria_dev`/ `maria_dev`.

6. Start the Kafka service from the menu.

7. Check it works (assumes a local Kafka installation on your development machine). 

    * In one terminal session:
    
            cd $KAFKA_HOME
            bin/kafka-console-producer.sh --topic test --broker-list sandbox.hortonworks.com:6667
            (Type a message)
    
    * In a second session:

            cd $KAFKA_HOME
            ./kafka-console-consumer.sh --bootstrap-server localhost:6667 --topic test --from-beginning --zookeeper localhost:2181
            (Check the message from the first session reaches the second session)
    
