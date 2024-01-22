# System Architecture of IoT - Lab 1 report

**Description:** _Get a working understanding of the MQTT protocol. Setup a rudimentary publisher and subscriber using a openly available broker._

**Group members:** Gayani Liyanage Sankalpa Neupane 

**Lab dates:** 06.03.2023

## Introduction (3 p)

_Provide a short description of the setup (hardware and software) and how the different components interact. Explain the steps you performed in the lab, e.g., using screenshots and photos._

According to the pre lab session we have downloaded virtual box to the local computers and clone the GitHub repository to it.

We connected the Arduino MKR Wifi 1010 to the computer and at the start we were able to run the sample blinky.But when we connect the Arduino board and tried to run the blinky sample from the VM, it couldn't identify the port of the Arduino board, so we decided to continue on the computer without using virtual machine and continue the lab session 1.

We have installed all the necessary libraries for the Arduino and connected the Thermistor to the arduino board according to the given instructions.
![image](https://user-images.githubusercontent.com/100039767/226019748-b4aa5c55-0290-4a00-a905-e52b3b3d2583.png)

And then we have installed mosquitto to the computer and directed the command propmt directory to the mosquitto.

After compiling and uploading the given arduino code to the Arduino board after changing the Group name we able to get the responce from the Arduino Serial monitor as follows.
![image](https://user-images.githubusercontent.com/100039767/226020122-90a06597-46ab-44e4-b71b-f8c3f4773bae.png)
![image](https://user-images.githubusercontent.com/100039767/226020345-2bb8370a-d077-4be2-aa81-d0aaf805cc79.png)

Then we able to executed the mosquitto_sub command on the command prompt and then we executed the mosquitto_pub command to get the response according to the On OFF and TEMP commands. 

ON command
![image](https://user-images.githubusercontent.com/100039767/226027283-1046f5d2-8903-42ff-bd54-aa54c01b9521.png)
![image](https://user-images.githubusercontent.com/100039767/226027920-bef3c393-a0f6-4a20-8028-35c0266ac311.png)
![image](https://user-images.githubusercontent.com/100039767/226028939-dbf5f33b-0e34-4de8-90f0-d94165b3ed8e.png)

OFF command
![image](https://user-images.githubusercontent.com/100039767/226027491-b45f2957-310c-443f-adee-c658170cfce2.png)
![image](https://user-images.githubusercontent.com/100039767/226027762-fb4e311a-72b1-4bc6-8dd8-9669a57de109.png)
![image](https://user-images.githubusercontent.com/100039767/226029055-276870d7-f3ea-446a-853e-3731999b63f6.png)

TEMP command 
![image](https://user-images.githubusercontent.com/100039767/226021134-0384b028-caa6-4d47-a01e-c72b2cd77f92.png)
![image](https://user-images.githubusercontent.com/100039767/226020586-1d81890b-d969-4bf2-9f37-f09e3d711a72.png)

Other commands
![image](https://user-images.githubusercontent.com/100039767/226020887-4173b75b-14fa-4975-9402-1459e2b02e55.png)


## How does the `getTemp` function work (1 p)

According to the data sheet of the sensor getTemp() function start with initializing the voltage at 0v and temperature coefficient. Then take 10 samples of surrounding temperature from the sensor and calculate the ambient temperature. 
Since the Arduino board is 3.3v one, we have to convert the analog reading to voltage after multiplying by 3.3 and then the float value can be get diving it by 1024, that is how ambient voltage can be calculated.
Then  the temperature is calculating from the equation and getting the average of 10 temperature values and return it.
After sending message to the response topic the getTemp() function is called and the temparature value will print on the command line or the terminal on the VM 

## What is the value returned by `mqttClient.messageQoS()`? What does it mean? (1 p)

MQTT QoS is a level of service that serves as a consensus between a publisher and a broker on one hand, and the broker and a subscriber – on the other regarding a guarantee to successfully dispatch an MQTT message. 
In message trannsmission process, the broker is the one who act as a middle point between the publisher and subscriber, it prform a role of both sending and receiving data.To complete this process MQTT broker completes number of steps.
When a MQTT client is trying to subscribe for a topic, it sends a SUB packet which is including QoS level. The broker will answer the request with a RESPONSE packet and confirm the subscription.
When MQTT client wants to publish a message on a topic , it sends PUBLISH packet with the QoS level.
There are three QoS levels, in this case QoS level is 0 that means Publisher will send a message only once and the subscriber recieve the message or not recieve the message.MQTT QoS 0 ensures that a message is sent only once but doesn’t guarantee delivery. 
In this program when we give the commands On OfFF and TEMP, according to the commands, MQTT publisher send the packet and then the broker will forward it to the subscriber.Then the publisher discards the command at once.

## What is the value returned by `mqttClient.messageRetain()`? What does it mean? (1 p)
Upon receiving a message with the Retain flag set, the MQTT broker must store the message for the topic to which the message was published, and it must store only the latest message. So the subscribers which are interested in this topic can go offline, and reconnect at any time to receive the latest message instead of having to wait for the next message from the publisher after the subscription.

Retained messages help newly-subscribed clients get a status update immediately after they subscribe to a topic. The retained message eliminates the wait for the publishing clients to send the next update.

## Command and response (8 p)

Implement the functionality required in the lab instructions and provide the code according to the instructions. Explain in your report how your code works and provide the block diagram requested.

According to the given instructions we added Group Name to the arduino code as follows 
![image](https://user-images.githubusercontent.com/100039767/226089924-2974cfdb-6161-4878-b2dc-3c009ea16de1.png)

Then for the functionality requiements we changed the program and all changes commited in Github source code
![image](https://user-images.githubusercontent.com/100039767/226090813-89323156-402f-438b-accc-26d018480c8a.png)


![image](https://user-images.githubusercontent.com/100039767/226160501-2cbcc27d-6bbd-4be6-b6ab-b125532444e6.png)
