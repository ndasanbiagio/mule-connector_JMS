MuleSoft JMS Connector Example
This project demonstrates how to configure and use the JMS Connector in MuleSoft to send and receive messages from JMS queues.

Prerequisites
Anypoint Studio installed
Maven installed
JMS provider setup (e.g., ActiveMQ)
Project Structure
css
Copiar código
my-mulesoft-project/
├── src/
│   └── main/
│       ├── java/
│       └── mule/
│           └── my-config.xml
├── pom.xml
└── README.md
Step-by-Step Guide
Step 1: Add JMS Connector Dependency
Ensure the JMS connector dependency is included in the pom.xml file.

xml
Copiar código
<dependency>
    <groupId>org.mule.connectors</groupId>
    <artifactId>mule-jms-connector</artifactId>
    <version>1.7.1</version> <!-- Verify the latest version available -->
    <classifier>mule-plugin</classifier>
</dependency>
Step 2: Configure JMS Global Element
Open the Mule configuration file (my-config.xml).
Add the JMS configuration in the Global Elements tab.
xml
Copiar código
<jms:config name="JMS_Config" connectionFactoryJndiName="ConnectionFactory"
            jndiInitialFactory="com.sun.jndi.fscontext.RefFSContextFactory"
            jndiProviderUrl="file:///C:/JNDI-Directory"
            doc:name="JMS Config"/>
Step 3: Create Mule Flows
Example of a JMS Receiver Flow
xml
Copiar código
<flow name="jmsReceiverFlow">
    <jms:inbound-endpoint queue="myQueue" connector-ref="JMS_Config" doc:name="JMS"/>
    <logger message="Received JMS message: #[payload]" level="INFO" doc:name="Logger"/>
</flow>
Example of a JMS Sender Flow
xml
Copiar código
<flow name="jmsSenderFlow">
    <http:listener config-ref="HTTP_Listener_Configuration" path="/send" doc:name="HTTP"/>
    <set-payload value="Hello JMS" doc:name="Set Payload"/>
    <jms:outbound-endpoint queue="myQueue" connector-ref="JMS_Config" doc:name="JMS"/>
</flow>
Step 4: Deploy and Test
Deploy the Mule application in Anypoint Studio.
Use an HTTP client (e.g., Postman) to send a request to the HTTP endpoint configured in the jmsSenderFlow.
Verify that the message is received and logged by the jmsReceiverFlow.
