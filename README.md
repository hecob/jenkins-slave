# Jenkins slave
```
[link](https://hub.docker.com/r/jenkins/jnlp-slave/)
```
## Jenkins master configuration
```
* create a node
1. name - 'agent'
2. # of executor - '3'
3. home - '/home/jenkins/agent'
4. label - 'docker-agent'
5. others - default

* disable ssl handshake
1. http://<host>:9080/script
2. run -> jenkins.slaves.DefaultJnlpSlaveReceiver.disableStrictVerification=true
```

## To run a Docker container with Work Directory:
```
docker run jenkins/jnlp-slave:latest -url http://192.168.0.18:9080 -tunnel 192.168.0.18:51000 -workDir=/home/jenkins/agent 402bf959f442645388bf60b4ab2537f9d7838a12235651377d495d3597ac79fa  agent
```
## Optional environment variables:
```
JENKINS_URL: url for the Jenkins server, can be used as a replacement to -url option, or to set alternate jenkins URL
JENKINS_TUNNEL: (HOST:PORT) connect to this agent host and port instead of Jenkins server, assuming this one do route TCP traffic to Jenkins master. Useful when when Jenkins runs behind a load balancer, reverse proxy, etc.
JENKINS_SECRET: agent secret, if not set as an argument
JENKINS_AGENT_NAME: agent name, if not set as an argument
JENKINS_AGENT_WORKDIR: agent work directory, if not set by optional parameter -workDir
Configuration specifics
Enabled JNLP protocols
By default, the JNLP3-connect is disabled due to the known stability and scalability issues.
You can enable this protocol on your own risk using the
JNLP_PROTOCOL_OPTS=-Dorg.jenkinsci.remoting.engine.JnlpProtocol3.disabled=false property (the protocol should be enabled on the master side as well).

In Jenkins versions starting from 2.27 there is a JNLP4-connect protocol.
If you use Jenkins 2.32.x LTS, it is recommended to enable the protocol on your instance.
```
