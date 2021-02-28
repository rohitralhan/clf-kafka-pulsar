<div>
<h1>OpenShift - Cluster Log Forwarding to Apache Pulsar</h1>
<div>
<div>Table of Contents</div>
<ul>
<li><a href="#_background">Background</a></li>
<li><a href="#_prerequisites">Prerequisites</a></li>
<li><a href="#_goals">Goals</a></li>
<li><a href="#_steps">Steps</a></li>
</ul>
</div>
</div>
<div>
<div>
<h2 id="_background">Background</h2>
<p>Red Hat OpenShift&nbsp;is an open-source container application platform based on the Kubernetes container orchestrator for enterprise application development and deployment. This article will be showing procedure on how to forward logs from&nbsp;<a href="https://www.openshift.com/products/container-platform" target="_blank" rel="noopener noreferrer">Openshift Container Platform</a>&nbsp; to Apache Pulsar via Kafka.&nbsp;</p>
</div>
<div>
<h2 id="_prerequisites">Prerequisites</h2>
<div>
<div>
<p><strong>Tools</strong></p>
</div>
<div>
<p>The tools you need locally:</p>
</div>
<div>
<ul>
<li>
<p>Access to Red Hat OpenShift platform 4.6+</p>
</li>
<li>oc - OpenShift Command Line Interface (CLI) - Available from&nbsp;OpenShift cluster (See image below)</li>
<li>
<p>Access to command line</p>
</li>
<li>
<p>A browser (Chrome, Firefox)</p>
</li>
</ul>
<p><strong>OpenShift command line tool download:</strong></p>
<div>
<p><img src="images/command-line-tools-download_1.png" alt="OCDownload" /></p>
</div>
</div>
<div>
<p><strong>Skills</strong></p>
</div>
<div>
<ul>
<li>
<p>Familiarity with Red Hat OpenShift Platform and Operators.</p>
</li>
<li>
<p>Familitrity with the OC Command</p>
</li>
</ul>
</div>
</div>
</div>
<div>
<h2 id="_goals">Goals</h2>
<div>
<div>
<ul>
<li>
<p>Install ElasticSearch operator</p>
</li>
<li>
<p>Install Cluster Logging operator</p>
</li>
<li>
<p>Create a ClusterLogging and ClustarLogForwarder instance</p>
</li>
<li>
<p>Deploy Kafka, Zookeeper and Pulsar instances running on the OpenShift Platform</p>
</li>
<li>Run the Pulsar client to receive the messages from Kafka topic</li>
</ul>
</div>
<div>&nbsp;</div>
</div>
</div>
<div>
<h2 id="_steps">Steps</h2>
<div>
<div>
<ul>
<li>
<p>Provision a Red Hat OpenShift platform</p>
</li>
<li>
<p>Install the Elasticsearch Operator (from the UI)</p>
</li>
</ul>
</div>
<div>
<p><img src="images/elasticoperator.png" alt="ElasticsearchOperator" /></p>
<p><img src="images/elasticoperatorInstall.png" alt="ElasticsearchOperatorInstall" /></p>
</div>
<ul>
<li>
<p>Install the ClusterLogging Operator</p>
</li>
</ul>
</div>
<div>
<p><img src="images/clusterloggingoperator.png" alt="ClusterLogging" /></p>
<p><img src="images/clusterloggingoperatorInstall.png" alt="ClusterLoggingInstall" /></p>
</div>
<div>
<ul>
<li>
<p>Download the scripts to a folder (all teh yml files)</p>
</li>
<li>
<p>Go to command line and login to your OpenShift cluster</p>
</li>
<li>
<p>Execute the following Commands in sequence from teh folder where you have downloaded the scripts</p>
<ul>
<li>oc apply -f kafka-pulsar-integration.yml</li>
<li>oc apply -f ClusterLogging.yml</li>
<li>oc apply -f ClusterLogForwarder.yml</li>
</ul>
</li>
</ul>
</div>
<div>
<ul>
<li>
<p>The Kafka, Zookeeper and the Pulsar Pod's are provisioned in the <strong>zkp-integ</strong> projec</p>
</li>
<li>Go to the <strong>zkp-integ project</strong> --&gt; <strong>pulsar-kafka-standalone pod</strong> --&gt; <strong>Terminal Tab&nbsp;</strong></li>
<li>
<p>Under the /pulsar folder run the python pulsar listener application to see the logs coming from OpenShift into pulsar via kafka</p>
</li>
<p><img src="images/openshiftlogs.png" alt="Logs" /></p>
<li>Below is the pulsar client code to display the message on the terminal</li>
</ul>
</div>
<div>
<p><img src="images/ccode.png" alt="CCode" /></p>
</div>
<div>&nbsp;</div>
</div>
</div>
