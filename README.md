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
A big query table will be important in this project as it will act as a data storage for data streaming from IoT devices. On the console menu, click BigQuery. Click the down arrow icon next to the project name and select 'create new dataset'. In this project, we name it heartRateData. Also, specify the location where the data will be stored.  Click the '+' sign to create new table. For Source Data, select Create empty table. For Destination table name, enter heartRateDataTable. Under Schema, click the Add Field button until there are a total of 4 fields. Name them as follows: sensorID, uniqueID,timeCollected, and heartrate.

       Pub/Sub Topic
Cloud Pub/ Sub Topic is important in streaming the data collected and handling messages.  In the Google console, select Pub/Sub then topics.  In case prompted to enable API, enable it.  Click on create a button and enter heartrateData as topic name and click create. 
In order for other google cloud services to access the messages, create a subscription. Click on the three dots on the right and then click new subscription. Enter heartratedata as the subscription name and click create.  

      Dataflow Template
   A dataflow template creates a process which monitors a pub/sub topic for incoming messages and then moves them to the big query.On the cloud console, select storage and then browser. Click create Bucket and give it a name.  Select a region that is similar to that one of the other project's services.  Click the create button. 
Go to the cloud console and select Dataflow. Click on Create Job from Template. Give the job a name and select the Pub/Sub Subscription to Big/Query template. Make sure the Regional endpoint matches where the rest of your project resources are located. Fill in the remainder of the field making sure that they align with the name of your storage bucket, Pub/Sub subscription and BigQuery dataset and tablename. Click on Run Job.
      Create IoT Core Registry 
Cloud IoT core facilitates the connection, management, and ingestion of data from several devices all over the world. IoT core as a central service enables the visualization of IoT data in real time. From the Cloud Console, select Cloud IoT Core. If prompted to enable API, enable it. Click on Create a device registry.Enter heartrate as registry ID. select a Region close to you, disable the HTTP protocol (since we are only using the MQTT protocol, limiting access is a good security practice) and select the Pub/Sub topic that was created in a previous step. Click on the Create button.
     Set Up the IoT Hardware 
  
     ## Assemble the Raspberry Pi and heart rate receiver
If there are more than 3 pins, trim the header down to only 3 pins. Solder the header pins to the sensor board.
Format the SD card and install the NOOBS(New Out Of Box Software) installer. Follow the steps here. Insert the SD card into the Raspberry Pi and place the Raspberry Pi into its case. 
Use the breadboard wires to connect the heart rate receiver to the Raspberry Pi
Raspberry Pi pin

Receiver connection
|Raspberry Pi pin|Receiver Connection|
|-----------------|------------------|
|Pin 16 (GPIO23)  |<not labelled>    |
 -------------------------------------
|Pin 17 (3V3)     |<not labelled>    |
          
--------------------------------------
|Pin 20 (GND)     |GND               |

Connect the monitor (using the mini-HDMI connector), keyboard/mouse (with the USB hub) and finally, power adapter.

Configure the Raspberry Pi
After the Raspberry Pi finishes booting up, select Raspbian for the desired operating system, make certain your desired language is correct and then click on Install (hard drive icon on the upper left portion of the window).

Click on the Wifi icon (top right of the screen) and select a network. If it is a secured network, enter the password (pre shared key).

Click on the raspberry icon (top left of the screen), select Preferences and then Raspberry Pi Configuration. From the Interfaces tab, enable I2C and SSH. From the Localisation tab, set the Locale and the Timezone. After setting the Timezone, allow the Raspberry Pi to reboot.

After the reboot has completed, click on the Terminal icon to open a terminal window.
Install the necessary software
Make sure that all the software on the Raspberry Pi is up to date and that needed packages are installed
sudo apt-get update
sudo apt-get install git
Clone the project code for the heart rate receiver
  git clone https://github.com/googlecodelabs/iotcore-heartrate
  cd iotcore-heartrate
  Make sure the required core packages are all installed

chmod +x initialsoftware.sh
  ./initialsoftware.sh
  **Create a security certificate
  
In order to communicate with Google Cloud, a security certificate must be generated and then registered with IoT core.
  chmod +x generate_keys.sh
  ./generate_keys.sh
  To transfer the public key to your computer so that it can later be registered with IoT Core, use SFTP (secure file transfer protocol).

**Add the device to the IoT Core Registry 

From the Cloud Console, return to IoT Core
Click the heartrate registry
For the Device ID, enter raspberryHeartRate. For public key format, select ES256. For authentication, either choose manual and then copy/paste the value from the key file into the Public key value area or choose upload and then upload the key from your computer. Click Add.
.IoT Core is now ready to receive communication from the Raspberry Pi.

**Start the Data
































































