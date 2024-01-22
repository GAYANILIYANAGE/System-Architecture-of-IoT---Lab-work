# System Architecture of IoT - Lab 3 report

**Description:** _Establish a MQTT connection that is safe from (unintended) snooping and is private using a gateway._

**Group members:** Gayani Liyanage Sankalpa Neupane 
**Lab dates:**  16.03.2023

## Work description (3 p)

Provide a short description of the setup (hardware and software) and how the different components interact. Explain the steps you performed in the lab, e.g., using screenshots and photos including the received messages on the AWS dashboard.

Explain how the Thing connects to your gateway, including TLS mutual authentication. Use relevant diagrams. Check the folder groupCA in your directory. 

Using the given IP address we connected to the reaspberry pi device through VM and then check the Greengrass is installed or not, we realaised that greengrass is not installed and then we started the process.

After follwing given instruction in the lab we setup Greengrass core device as follows

1. setup the Greengrass software on the RPI
2. Setup the access key
3. Save the aceess key and secret access key 
4. Set up Greengrass software using AWS console 
5. set up greengarss core device
6. set up the credentials to communicate with AWS service
7. start script on the AWS console
8. Run the installer

![greengrsaa completed 2](https://user-images.githubusercontent.com/100039767/226163274-dee03233-e4a4-4c80-ab73-fc5c52ec7f9e.jpg)

Finally we got healthy greengrass core device.

Then we created Things according to the given instructions and connected it to the greengrass core device.

![deployment is completed](https://user-images.githubusercontent.com/100039767/226166836-f36ee938-0ae0-4023-a71f-6ff4bfa25337.jpg)

After suscribing to the topic we got 10 messages as follows

![image](https://user-images.githubusercontent.com/100039767/226171777-45a66090-75cb-4a5a-b818-c7ede1a66ddd.png)

Two-way authentication between the client and the server is necessary for mutual TLS authentication. While using mutual TLS, clients must display X.509 certificates as identification proof before they may use your API. Mutual TLS is a common requirement for Internet of Things (IoT).

![image](https://user-images.githubusercontent.com/100039767/226176111-71ef80ff-bc63-4116-9277-208e39e81b59.png)

The thing will contact the AWS IoT via HTTPS, at this time TLS authentication occured. After that the gateway connects to the AWS IoT service and in here agin TLS authentication happed to verify server and the gateway.After that AWS IoT server send thing group to the and then the thing will connect with group CA through MQTT.Once the connection is fine the data can be transferd through MQTT protocol.

## Measure the latency of establishing the connection to the gateway (7 p)

Modify `pubSub.py` to measure the latency of establishing the connection to the gateway. Use `time`
   module and use `perf_counter()` to measure the time. See
   [documentation](https://docs.python.org/3/library/time.html#time.perf_counter). Compare the measured time with the ping value optained from the VM to your gateway. 

changes in pubSub.py code commited in github spurce code folder and herwith attcahed a screenshot of the latency output

![image](https://user-images.githubusercontent.com/100039767/226171863-23477881-2a42-4459-ad54-e4c5167676ad.png)

Measured the latency as 10s

## Optional tasks

If you are doing the optional tasks, write your results here.
