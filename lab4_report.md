# System Architecture of IoT - Lab 4 report

**Description:** _Setup an edge - a local computing platform on the gateway for your devices to offload its computation. Connect a device to the edge and perform some computations._

**Group members:** Sankalpa Neupane Gayani Liyanage
**Lab dates:** 17.03.2023

## Work description (5 p)

Provide a short description of the setup (hardware and software) and how the different components interact. Explain the steps you performed in the lab, e.g., using screenshots and photos including the received messages on the AWS dashboard.

In your report describe the achieved architecture and behavior of your application. Use figures to illustrate your description.

Before starting the lab4 we made sure that the greengrass core device is running and healthy by using the following command:
sudo systemctl status greengrass
sudo cat /greengrass/v2/logs/greengrass.log

The first command will show that whether gressgrass core device is active and running or not and the second command will show all the logs if there are any kind errors. If the greengrass was the working, we need to again create a green grass core device like in lab 3 but our one was working.

As I found our greengrass core device is working we started creating a lambda function. From search bar we searched for the lambda and we opened it. As in the instruction we clicked create lambda function and selected author from scratch. we gave a name called HelloWorld_GayaSankalpa and chose python3.7 as runtime. From the existing role I selected service-role/DefaultLambdaRole and I selected create function. The lambda function was created. And from there I uploaded a zip file which was provided in the source code of lab 4. Again, we made sure that the runtime was python 3.7 and then we changed the handler to greengrassHelloWorld.function_handler
We did it because it will only execute in the zip file we uploaded in the previous step. In the file called greengrassHelloWorld.py we changed the topic to saiot/GayaSanakalpa/localtocloud to give the group an unique name. After all the changes were made we selected the deploy button. From the test tab we tested the py file whether it is successfully working or not. The test was running. For the test we also edited the json file :
{
  Message: “message”
}

As the test was running successfully, we started to create a new version of it by clicking to action and from the dropdown we selected publish new version.

Then it was time to create the component from the green grass then we followed all the instruction and created the component. Now it was time to select the deployed greengrass core device. We clicked in the deployed core device and on the top right corner we selected revise. Now it was time to go to component again we created and select lambda function under the component. Now from the public component we add aws.greengrass.LegacySubscriptionRouter and we press next. And from the next page we select aws.greengrass.clientdevices.mqtt.Bridge and select configure component and add the file in the configuration merge provided in the instruction. Then now we do the same for aws.greengrass.LegacySubscriptionRouter Now after 5 minutes we check there is log of the greengrass whether there is file called lambdaname.log or not. If there is not we need to redo the whole process again. After that we did the test using MQTT test client. But the pubsub file was not working so we could not test it. But we were able to publish and subscribe the messages.  

## Difference between long-lived Lambda function and an on-demand Lambda function (5 p)

In your report describe the behavior differences between a long-lived Lambda function and an on-demand Lambda function deployed on a gateway. Illustrate your response taking a simple application example and provide the corresponding sequence (UML) diagrams for each.

Using Amazon Lambda's computing service, programmers can run code without setting up or managing servers. On-demand and long-lived Amazon Lambda functions are available. In contrast to on-demand functions, long-lived Lambda functions are active for a long period. Lambda functions begin when necessary and cease when they are done.

behavioural differences
Execution time: While long-lived Lambda functions can run for up to 15 minutes, on-demand Lambda functions are typically only expected to run for a few seconds.

Use of resources: Short-lived Lambda functions use resources for the duration of their operation, but on-demand Lambda functions start, execute, and shut down quickly. On-demand services are more efficient and consume less resources, according to this.

Scaling: Long-lived Lambda functions can be used to provide continuous processing of data or requests, whilst on-demand functions are frequently used to handle data as it comes in.

Cost: As on-demand Lambda functions only have operating costs when they are invoked, running long-lived Lambda functions may be more expensive.

Example scenario
Imagine you want to build an image processing application using Amazon Lambda. The application takes a photo, applies a filter, and then outputs the filtered image. For the sake of simplicity, we'll suppose that the filter is a grayscale conversion filter.

Sequence diagram of long-lived lambda function:
![image](https://user-images.githubusercontent.com/100039767/226172913-074514b0-d4c7-44fb-9b57-c9ed57694925.png)

Sequence diagram for on-demand Lambda function:
![image](https://user-images.githubusercontent.com/100039767/226172927-c1e85331-e06d-436f-bcee-63ddc86361eb.png)

In this scenario, an API Gateway acts as the application and invokes an on-demand Lambda function each time a new photo is received. The Lambda function applies the grayscale filter on the image and also returns the filtered version. Just while the photo is being processed is the function active before it is turned down. The API Gateway, the application's entry point, is in charge of routing requests to the appropriate Lambda function.

In conclusion, there are considerable differences between long-lived and on-demand Lambda functions in terms of execution time, resource utilization, scale, and cost. While long-lived Lambda functions are suitable for ongoing data processing, on-demand Lambda functions are used to process data as it is received. Understanding the behavioural changes is vital for picking the proper type of Lambda function, which relies on the needs of the application.


## Optional tasks

If you are doing the optional tasks, write your results here.
