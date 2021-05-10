Background 

The idea of connecting 'things' or physical objects has gained traction in recent years.  Under the Internet of Things(IoT) concept, objects with sensors are connected to the internet so as to share data and information with other objects over the internet.  One of the many areas that IoT is being applied is in healthcare.  For instance, doctors can use IoT devices to know whether patients are adhering to the medication provided. It is on this premise that this project is based; having the heart rate of a person recorded and the data streamed to Google cloud. A doctor or a health care provider can be able to monitor the heart rate of the person and give personalized attention. This is important especially when the person lives alone


Hardware Requirements

1.Heart Rate pulse sensor 
2.Raspberry pi 
3.Power Supply 
4.Monitor
5.USB card 
6.Monitor for display 
7.Mouse 
8.Keyboard 

Software Requirements 
1. Gmail account
2. Google cloud- New users are given a free trial of $300. Do not click upgrade if you do not want to be charged. 
3. Internet

Google cloud Set up 

Sign in to google console and create a new project. Give a project ID that is unique
In this project, the project ID is iot-heartrateit432. You can always view your project id in the home area of the cloud console. 
API's 
Since the project uses pub/sub, dataflow,compute engine, and IoT core, their APIs have to be enabled. This is done by selecting APIs & services in the console menu. Then, click enable API and services.  Specify the type of API to enable, ie PubSub.  Click on the result that appears'Cloud Pub/Sub API' and click 'Enable API' on the following page. 
          BigQuery Table 
A big query table will be important in this project as it will act as a data storage for data streaming from IoT devices. On the console menu, c 










