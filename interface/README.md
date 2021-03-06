<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

### Communicate Through Interface

<sub>[previous](../multiple-actors-ii/README.md#user-content-dynamically-alter-multiple-classes-ii) • [home](../README.md#user-content-ue4-blueprints) • [next](../interface-ii/README.md#user-content-communicate-through-interface-ii)</sub>

<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

What if we wanted a single event in the game interact with different objects differently (run different functions)? We can use an interface to implement as we like in each blueprint class. Interfaces (or abstract classes in C++) are very useful in game development. It enforces a structure on multiple objects so that we can call events and functions in all of them. I will show you a very simple use of an interface in this example. This is another way we can interface between actors. This allows us to communicate to multiple actor classes with one paradigm.

<br>

---


##### `Step 1.`\|`ITB`|:small_blue_diamond:

Scooch the camera over to **Room 10**. Add a `Blueprints | Room10` folder to the **Content Browser**.

![add room 10 folder](images/CreateRoom10Folder.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 2.`\|`FHIU`|:small_blue_diamond: :small_blue_diamond: 

*Right click* on **Room 9 | BP_LightbulbMulti** and *duplicate* it.

![duplicate bp_lightbulbmulti](images/DupeBPLightbulbRm12.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 3.`\|`ITB`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

*Call* the new blueprint `BP_LightbulbMultiInterface`. Move to **Room10**.

![rename bp and move to room 10](images/Add5LightsToRm12.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 4.`\|`ITB`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

*Drag and drop* several **BP_LightbulbMultiInterface** into room 10.

![add multiple copies of bp_lightbulginterface into room 10](images/AddRoom12SwitchToRoom.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 5.`\|`ITB`| :small_orange_diamond:

Drag a **Trigger Volume** to the level. Scale it to be in front where you can walk in and out of it in the room. *Clean* up the **World Outliner** by dragging all blueprints and the trigger volume into **Room 10**. Adjust the **Brush Settings** so that the volume takes up the front part of the room that the player can walk in and out of.

![add and scale trigger volume in room 10](images/DupeRoom9SwitchRm12.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 6.`\|`ITB`| :small_orange_diamond: :small_blue_diamond:

We are going to now create a special blueprint that will bridge multiple object. Go to **Blueprints | Room 10** and *press* **Add/Immport** and *select* **Blueprints | Blueprint Interface**. This is not like a regular blueprint class but creates an interface that multiple blueprints can share common functions.

> A [Blueprint Interface](https://docs.unrealengine.com/4.26/en-US/ProgrammingAndScripting/Blueprints/UserGuide/Types/Interface/) is a collection of one or more functions - name only, no implementation - that can be added to other Blueprints. Any Blueprint that has the Interface added is guaranteed to have those functions. The functions of the Interface can be given functionality in each of the Blueprints that added it. This is essentially like the concept of an interface in general programming, which allows multiple different types of Objects to all share and be accessed through a common interface. Put simply, Blueprint Interfaces allow different Blueprints to share with and send data to one another. - UE4 manual

![add blueprint interface](images/CreateBPInterfaceRm12.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 7.`\|`ITB`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

*Name* it `BP_RoomSwitchInterface`.

![BP_RoomSwitchInterface](images/ActorReferencesActorRm12.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 8.`\|`ITB`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Open this new blueprint. Notice it is read only. It is a virtual interface so you will define it in the actors. This is completely blank. But we can add parameters. *Select* **NewFunction_0** on the graph and *press* the **+** button next to **Inputs** and call this variable `bIsOn` and make it type **Boolean**. Leave its default value at `false`.

All other blueprints that subscribe to this interface will be able to access this boolean.

![add bIsOn boolean to interface](images/image_10.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 9.`\|`ITB`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Lets call the function something more meaningful. Rename it to `Turn Room 10 Switches On and Off`. *Press* the <kbd>Compile</kbd> button.

![add function Turn Room 10 Switches On and Off](images/RenameFunctionAddDescriptRm12.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 10.`\|`ITB`| :large_blue_diamond:

Open up **BP_LightbulbMultiInterface** as we are going to subcribe to the **Interface**. This is a commitment that we will implement the one interface function with a parameter that we have created. Press the **Class Settings** button and in the **Details** panel press the **Interfaces | Add** dropdown menu and select the **BP_RoomSwitchInterface** we just created. Then most importantly,finish by pressing the <kbd>Compile</kbd> button:

![subscribe to interface](images/SubscribeToInterface.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 11.`\|`ITB`| :large_blue_diamond: :small_blue_diamond: 

Now lets add an event to this blueprint that will run when this event is triggered. Go to the **Event Graph** tab and add a **Event Turns Room 10 Switches on Off** node:

![call interface's method](images/CallInterfaceEvent.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>


##### `Step 12.`\|`ITB`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 

Each actor that subscribes to it can create its own definition. This means that the behavior can be customized PER actor class. This is an event so there is an execution pin.

![interface method node](images/PrivateTooltipRm12.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 13.`\|`ITB`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Now add a **Switch Light** node and *attach* the execution pins and the boolean pins between **Is On** to **Turn On**. This will run the function we previously wrote to turn the light on and off. *Press* the <kbd>Compile</kbd> button.

![trigger switch light](images/SwitchLightOnOff2.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 14.`\|`ITB`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Select **TriggerVolume2** that is in room 10. Then press the **Blueprints** button then select **Open Level Blueprint**.

![open level blueprint](images/NameItBPSwitchInterface.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 15.`\|`ITB`| :large_blue_diamond: :small_orange_diamond: 

Press the **+** button next to **Variables** and add a new variable called `RefToLightbulbsInterface`. Make it type **BP_LightbulbMultiInterface | Object Reference**.

![add rerefece to lightbulbmultiinterface](images/SelectFunctionAddInput.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 16.`\|`ITB`| :large_blue_diamond: :small_orange_diamond:   :small_blue_diamond: 

*Press* the sphere icon next to the **Variable Type** and select an **Array**.

An [array](https://en.wikipedia.org/wiki/Array_programming) is a list of variables.  They can only be of a single type.  So this is creating an array of a reference to all the instances of the lightbulb in the room.

![change variable to array](images/ImplementInterfaceBPEventGraph.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 17.`\|`ITB`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Add a **Tooltip** with `Keeps array of all room 10 lightbulbs`. Set **Private** to `true` and add it to category `Room 10-Lightbulb`.

![variable settings](images/HookUpExecutionAndBoolRm12.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 18.`\|`ITB`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

In the **Event Graph** *add* to the nodes that are attached to **Begin Play**. Add a **Get All Actors of Class** node and select a **BP_LightbulbMultiInterface** class.

![get a reference to all actors that subscribe to the interface](images/CompileImplementedInterface.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 19.`\|`ITB`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Drag a copy of **RefToLightbulbsInterface** and add a **Set** node. Connect the execution pins and the **Out Actors** array node to the **RefToLightbulbsInterface** node.

![set the array with all subscribers](images/CallInterfaceFromSwitchRm12.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 20.`\|`ITB`| :large_blue_diamond: :large_blue_diamond:

Make sure you still have the Trigger Volume selected in game. *Right click* on the event graph and select **Add Event for Trigger Volume 2 | Collision | Add On Actor Begin Overlap** AND **Add On Actor End Overlap**.

![add begin and end overlap message](images/SendMessageToArrayRm12.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 21.`\|`ITB`| :large_blue_diamond: :large_blue_diamond: :small_blue_diamond:

*Right click* on the graph and add a **Get Ref to Ligthbulbs Interface** node. Pull off the *array* pin and select a **For Each Loop** node to go into each lightbulb to turn it on and off.

![add a lightbulb ref and for each loop](images/SameForTurningOffMessageRm12.jpg)

___


<img src="https://via.placeholder.com/1000x4/dba81a/dba81a" alt="drawing" height="4px" alt = ""/>

<img src="https://via.placeholder.com/1000x100/45D7CA/000000/?text=Next Up - Communicate Through Interface II">

<img src="https://via.placeholder.com/1000x4/dba81a/dba81a" alt="drawing" height="4px" alt = ""/>

| [previous](../multiple-actors-ii/README.md#user-content-dynamically-alter-multiple-classes-ii)| [home](../README.md#user-content-ue4-blueprints) | [next](../interface-ii/README.md#user-content-communicate-through-interface-ii)|
|---|---|---|
