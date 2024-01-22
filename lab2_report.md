# System Architecture of IoT - Lab 2 report

**Description:** _Establish a secure MQTT connection and understand various parts of
   the setup._

**Group members:** Sankalpa Neupana , Gayani Liyanage
**Lab dates:** 06.03.2023

## Work description (4 p)

Provide a short description of the setup (hardware and software) and how the different components interact. Explain the steps you performed in the lab, e.g., using screenshots and photos including the received messages on the AWS dashboard.

First as in the description we started with generating the key pair and Certificate Signing Request (CSR). For generating the certificated from the source of lab2 we opened the sketch ECC08CSR. Then we opened the serial monitor and from the serial monitor on the right there is a button with the drop-down menu where we selected both NL & CR. We set the baud rate to 9600, mostly the baud rate is 9600 by default. From there we uploaded the ECC08CSR sketch and verified it. We followed the instruction provided and put all the details given then we got the CSR. We copied the CPR in the plain text and saved in the folder.  We logged into the amazon using the credentials provided. We need to add the number, username and password while logging in. Then after logged in we made sure that the region is Frankfurt. As we was familiar with AWS instead of going through the instruction, I directly searched for the IoT core and from there I again started following the instruction. I created the single thing and as in the instruction we wrote our group name. After that there was a place where we need to upload our CSR which we created earlier we uploaded that. We did not add policies as said in the instruction. 
After the thing is created, we started creating policies and as in instruction we followed them. Now it was time to attach the policy to the thing we created previously. We selected the thing we created and added the policy we just created. After attaching the policy, we can get the certificate and we downloaded that for further use. Then we started to create the secure connection to MQTT for testing. We opened the source code of lab 2 then in the secrets we modified the SSID, PASS and GROUP and for the broker that we need to modify we got it form AWS. The broker can be found from the setting of IoT core. Then we filled the client certificate with the text of certificate we created in previous step. We load the program and check that it is connected with the AWS IoT broker. 

![image](https://user-images.githubusercontent.com/100039767/226089574-7c003eef-661c-4cf9-b387-9f8c43883cd6.png)

Then from the MQTT test client we typed our topic to subscribe (it was the one in the Arduino program where we need to change it to our group name in the format of “saiot/Groupname/publish”. We need to select payload as string in the setting so that we can see the full message rather than only characters. 

![image](https://user-images.githubusercontent.com/100039767/226089593-0b220059-c2cc-414f-8915-da00e13f36cd.png)

![image](https://user-images.githubusercontent.com/100039767/226089596-88485496-410b-4278-ba9a-5606e5c2c248.png)

![image](https://user-images.githubusercontent.com/100039767/226089607-20e9ce38-99ff-433f-b27c-23becd5689d7.png)

This code establishes a MQTT client connection to a broker with the aid of SSL/TLS. The code also includes essential libraries like ArduinoBearSSL, ArduinoECCX08, and ArduinoMqttClient, as well as the Wi-Fi network and broker credentials that are stored in a separate arduino secrets.h file.
The setup function initiates a call back to obtain the current time, initializes the serial communication, determines a string for the client certificate, and determines whether an ECCX08 chip is present. The ECCX08 slot is set up to use both the private key and the accompanying public certificate. Although the client ID is optional, it is recommended that it be distinct for each device connected to the broker.
The loop function can subscribe to arriving topics and post messages to outgoing topics by connecting to the Wi-Fi network and broker. If there is a serial monitor, it prints a message from the inbound topic. The MQTT client disconnects from the broker every 30 seconds to avoid timing out.

## TLS/SSL mutual autentication (2 p)

Explain your understanding of TLS/SSL mutual authentication mechanism with respect to the Arduino and AWS IoT core. Make use of diagrams. Check the references for some useful references on this topic.

TLS/SSL mutual authentication is a security method used to authenticate both the client and the server in a communication. By setting up the client (Arduino) and the server (Amazon IoT core) to exchange digital certificates with one another during the SSL/TLS interaction phase, mutual authentication between Arduino and AWS IoT core may be done. By doing this, it is ensured that both parties may verify each other's identification before a communication session begins. The reciprocal authentication technique, which also serves to prevent unauthorized access and data breaches, adds another layer of protection for IoT devices.

## Pros and cons of using TLS/SSL mutual authentication (2 p)

Check references.

Pros:-
One of the main advantages of using TLS/SSL mutual authentication is that it adds an additional layer of security to communications between clients and servers. It ensures that the connection is safe and that data transmitted over the connection is encrypted, protecting against unauthorized access and man-in-the-middle attacks. Mutual authentication aids in establishing the reliability of the client and server as well as the veracity of the individuals taking part in the connection. This may be especially important in places like financial institutions and healthcare facilities where security is a major priority.
Cons:-
The main disadvantage of TLS/SSL mutual authentication is the potential for increased complexity throughout the authentication process, which might be challenging for some users. Mutual authentication requires the use of valid digital certificates but obtaining and maintaining them can be difficult. But, handling digital certificates may be time-consuming and, if done improperly, might expose security holes. Last but not least, the implementation of mutual authentication can be a resource-intensive process that boosts the cost of establishing and maintaining asecure communication infrastructure.

## Role of the crypto processor (2 p)

Assuming that the symmetric encryption was carried out by the WiFi module, what was the role of the crypto processor during the TLS/SSL handshake.

During the TLS/SSL handshake, the crypto processor generates and signs a digital certificate to verify the device.  Furthermore, it takes part in key exchange to provide a unique session key that is used for symmetric encryption during the connection. The WiFi module then uses this session key to encrypt and decode the data being sent. As a result, the WiFi module handles symmetric encryption, while the crypto processor is responsible for device authentication and key exchange during the TLS/SSL handshake.

## Optional tasks

If you are doing the optional tasks, write your results here.
