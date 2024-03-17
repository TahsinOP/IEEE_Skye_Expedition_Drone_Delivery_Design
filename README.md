# Design Philosophy

Our design philosophy emphasizes modularity and compatibility, ensuring seamless integration with various UAV systems. By prioritizing modularity, we aim to create a platform that can adapt to various UAV configurations, catering to the diverse needs of different applications and industries.

## Modularity

The modularity of our design allows for easy customization and adaptation to different UAV systems. By breaking down the platform into distinct components, such as the payload-holding layer and the electronics layer, we enable flexibility in assembly. The design is easily scalable to a bigger dimension keeping the core principle the same. The design can be further incorporated with more extensive electronic circuits and components for other complex applications.

## Compatibility

We understand the importance of compatibility when designing accessories for UAVs. Our platform is engineered to be compatible with a wide range of UAV models, whether it's a small quadcopter or a large fixed-wing UAV. Our design can seamlessly attach and function without requiring extensive modifications or adjustments. We will look further into what is so interesting and unique about our attachment method.

To summarize, the basic design philosophy is a sweet and simple design, user-friendly, hassle-free, compatible, modular, cost-efficient, and easy to manufacture. Our team has tried to make the best possible design under the given weight constraints.

Now let us have a deep dive into the specifics of our design, the mechanisms used, and the electronic components integrated.

# Design Components (*Carbon Fibre Reinforced Polymers)

## Electronic Components

- Raspberry Pi 4 Model B: The central processing unit responsible for managing communication protocols and executing high-level commands. (It is assumed the drone has a controller like PixHawk etc)
  
- Arduino Uno R3: Facilitates low-level control and coordination of various mechanisms involving payload release and platform attachment.

- 12V LiPo Battery: Provides power to both the Raspberry Pi and Arduino, ensuring continuous operation throughout the flight.

- Servo Motors (2x): Actuates the payload release mechanism, allowing for controlled and accurate deployment.

- Relay Electromagnet: Enables secure attachment of the platform to the UAV, ensuring stability during flight. The lifting capacity of the chosen electromagnet is 10 kg

## Mechanical Components (Components 1,2,3 are made of *CFRP)

- Movable Base (Bottom Layer): This base holds the payload in place and can be actuated to release the payload efficiently.

- Landing Gear Base: This is of a similar structure as the previous one but integrated directly with the deployment platform, the reasoning for this will be explained further in the document.

- Fixed Base (Middle layer): This layer is the main upper frame of the body which holds all the electronic components, supports the payload, and gives the overall structure to the platform.

- Metallic Covering (Top layer): This covers all the electronics from the top and is made of a metallic material for the magnet to attach on.

# Manufacturing

All the components involved in the design except Component 4 can be easily manufactured using the most versatile and popular additive manufacturing method which is 3-D printing. We have chosen the material as Carbon Fiber Reinforced Polymer (CFRP). CFRP has the perfect combination of durability, robustness, and strength. They are extremely lightweight and perfectly suitable for UAV applications.
CFRP is the most commonly used material for 3-D Printing, therefore resulting in easy, precise, and hassle-free manufacturing of the components.

For Component 4, we prefer to use Laser Cutting for high precision and tolerances. Alternatively, CNC machining can be adopted giving almost the same results, the choice depends on the availability, cost, and other economic factors. This component is made of a magnetic material mostly an iron alloy with a thin coating (1mm) of magnetic polymer matrix.

# Assembly

The assembly for the platform is pretty simple, all the components have all the necessary holes. 3-D print components (1,2,3), laser cut / CNC machine component - 4, acquire all the necessary screws, nuts, and fasteners (refer to CAD design for accurate dimensions), prepare all the electronics components. Now we are ready to assemble the deployment platform.

1. Attach the Movable base to the Landing gear base via the extruded shaft portions, no fasteners are required as it is a tight fit.
2. Now attach the Fixed base to the landing gear base using screws and nuts.
3. Finally, attach the magnetic covering after wiring and soldering all the electronic components. (Holes are provided)

# Mechanisms and Algorithms

## Remote Payload Deployment

The payload is released using a two-bar mechanism attached to the movable base platform. The links are actuated using two servo motors placed on diagonal ends (maintains the center of mass). When the links are activated, the platform goes down dropping the payload.


![photo_2024-03-17_15-59-21](https://github.com/TahsinOP/IEEE_Skye_Expedition_Drone_Delivery_Design/assets/117567813/23b6a486-ef4b-475d-bd9c-7aa2bad58813)


The motors are controlled by Arduino Uno, which is commanded by the onboard Raspberry Pi 4. Using Wi-Fi, we can headlessly connect to the Pi using our personal computer.For fast and seamless communication, we will use ROS2 middleware communication on the same Wi-Fi network. Services and nodes will be coded which will help trigger the servo motor whenever we want to release the payload from the required height. One needs to just call the ROS2 service a call to turn the motors on (the motor angle will be controlled by the basic Arduino servo motor code). To bring the platform back again, another ROS2 service will be called to turn the motors at the same angle but in the opposite direction.

In simple words:

![photo_2024-03-17_16-00-26](https://github.com/TahsinOP/IEEE_Skye_Expedition_Drone_Delivery_Design/assets/117567813/cf3194ce-45f6-4643-be6b-5d2b7ac8095a)

## Platform Attachment

This is one of the most unique solutions our team has developed. When we saw the rulebook now screws, fasteners, etc can be used. According to the given constraints we have come up with an efficient and compatible solution that can be integrated with most UAV applications.

### Method 1: (Rating of electromagnet - 10 kg)

We have used a relay electromagnet which can be controlled using the remote control(RC) used for the drone motion. The electromagnet is fixed to the drone underside and whenever the platform needs to be attached just turn on the magnet it will get attached to the top of the platform (as the top surface has a thin coating of magnetic alloys). In the model, we have used steel as the top material for convenience purposes.

The power supply of the electromagnet will come from the battery installed for the drone controller (mostly Pixhawx used in industry). The RC controller of the drone has extra buttons that can be customized for other purposes. We will use one of those switches to turn ON/OFF the electro-magnet whenever required. To attach the platform to any other UAV just fix the electromagnet to the drone underside (wire it with the controller) and turn the magnet ON.

### Method 2:

In this method also we are using the magnet, but it's now attached to the deployable platform using screws and fasteners. The magnet can be directly controlled by Arduino in this case to turn it ON/OFF, this method is much more compatible and scalable for any UAV. There is no need for any joints to the drone base, just turn the magnet on the magnet will attach to the drone base. The only condition required is that the drone base is made of steel/iron alloys or any metallic alloy.

![Payload_Platform_Attachment_mechanism_workflow](https://github.com/TahsinOP/IEEE_Skye_Expedition_Drone_Delivery_Design/assets/117567813/c4272025-436b-4ca0-8ea3-e518c833ee08)


## Landing Gear

We removed the original landing gear as it was interfering with our deployable platform. We mimicked the old landing gear design in a simple way and integrated it into the platform base. It serves the same functionality with a wide base to land safely on any terrain.

![photo_2024-03-17_16-02-10](https://github.com/TahsinOP/IEEE_Skye_Expedition_Drone_Delivery_Design/assets/117567813/4ff3c250-374c-429b-bd8e-f04a793e25c0)

## Multiple Payloads Case

For multiple payloads just extrude the green part, the landing gear base, and the movable layer to either side depending on the number of payloads, the release mechanism will be the same with two servo motor controls for each of the payloads respectively.

# CFD Analysis

The final weight of the platform (Theoretical): 2243.659 g = 2.4KG

The CFD analysis for both the drone and the deployable platform will be attached in a separate PDF file with all the figures, results, and parameters.

![photo_2024-03-17_16-03-14](https://github.com/TahsinOP/IEEE_Skye_Expedition_Drone_Delivery_Design/assets/117567813/24de8418-3578-4171-a244-29ac9d3b0a25)

![photo_2024-03-17_16-04-41](https://github.com/TahsinOP/IEEE_Skye_Expedition_Drone_Delivery_Design/assets/117567813/8474421f-058f-4494-b901-cfa030ab4601)




