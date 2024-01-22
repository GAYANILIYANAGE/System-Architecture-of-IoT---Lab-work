# System-Architecture-of-IoT-Lab-work

The emerging and existing IoT frameworks share some central IoT architectural features. A central pattern seems to be about discovering, connecting, monitoring, controlling and/or interacting with a system of smart things or Things (with capital T), where a Thing is an abstract notion of a digitally augmented physical object. Digital augmentation is one or more combination of sensors, actuators, computation element or communication interfaces attached to the physical object. So, a Thing can be a circuit package with one sensor, or multiple sensors and actuator, or even a group of devices mimicking a physical object.

Three patterns emerge when it comes to binding the Things together. Direct Connectivity refers to a pattern where each Thing is directly connected to another Thing. Each Thing has its own application program interface (API) and they communicate with each other using a standardised API. However, this is indeed the most difficult approach due to diverse communication standards, lack of processing and operational power on the devices to support full-fledged networking stack, and lack of standardisation of the API. W3C is coming up with one such standard and is yet to be ratified.

Gateway-based connectivity is the second pattern, where a Thing cannot offer an API directly and sits behind an intermediary. The gateway mimics the Thing and provides an API on behalf of the Thing. The last common pattern is the cloud-based connectivity. This is similar to a gateway approach, the cloud service provides the API for the Things. The difference lies in the fact that the gateway can be physically closer to the Things. The interaction between gateway/cloud and the Things themselves could be orchestrated through a tightly coupled, proprietary communication protocols, that is lighter on power and computational load when compared to full internet stack.

In the lab, we will focus on the cloud and gateway pattern. We will use MQTT protocol to directly interact with the devices first and then subsequently conduct the interactions through a gateway. In process, the goal is to recognise some good practices when it comes to deploying a Thing network and this is demonstrated using Amazon's IoT and Greengrass product. We will cover common security practices that involve authorisation and authentication issues. We will also touch upon elastic edge computing, if time permits.

Concretely, the lab exercises are designed to achieve the following learning goals:

Lab 1: Get a working understanding of the MQTT protocol. Setup a rudimentary publisher and subscriber using a openly available broker.
Lab 2: Establish a secure MQTT connection and understand various parts of the setup
Lab 3: Establish a MQTT connection that is safe from (unintended) snooping and is private using a gateway.
Lab 4: Setup an edge - a local computing platform on the gateway for your devices to offload its computation. Connect a device to the edge and perform some computations.
