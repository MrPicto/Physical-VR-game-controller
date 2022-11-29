
![HighresScreenshot00006](https://user-images.githubusercontent.com/92038037/204267343-8dc7fa2e-ec81-4e8c-876e-aee93d874e13.png)

# Unreal Engine Design 

Based on the Arduino design and research. In order to design a VR boxing game, the following game framework has to be designed.
- Turning a normal control handle into a hand model
- Making a striking ball
  - Making the ball material+
  - Creating the striking effects
    - 3D modelling the shattered sphere
    - Creating blueprint logic for sphere shattering
    - Shattering sounds
- Making bombs & walls
- Sphere launcher (heart rate data control area)
- Scoring system
- End of game judging system
- Scene making
- Arduino and Unreal linking
  - Handle vibration design
  - Blueprint for heart rate influencing serve speed
  - Vibration blueprint
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

# Hand model replacement 
## Purpose 
The presence of a controller in VR games affects the player's gaming experience. Replacing the grips with hand models while allowing the hands to have movement changes makes the game more realistic.


## Blueprint 
Bind the hand skeleton and attach the animation to the blueprint of the handle input.


![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![221128-TheBoxingRoom-Layout-14](https://user-images.githubusercontent.com/92038037/204279929-c9410ff8-4800-4820-b1e8-ffd470a35af5.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)


## Effects 
In the process of changing the model, the orientation of the virtual world palm needs to be constantly adjusted to match the orientation of the real world palm, as follows.

![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![IMG_6516](https://user-images.githubusercontent.com/92038037/204267824-a56b0827-c282-4223-a915-a03575222797.jpg)

## Handle vibration effect 
#### Hit Ball Haptic
![HitBall_Haptic](https://user-images.githubusercontent.com/92038037/204439451-a6a06926-2bfa-4538-89bb-799008fbd185.png)
#### Bomb Haptic
![Bomb_Haptic](https://user-images.githubusercontent.com/92038037/204439458-d544b32b-760b-4090-8ae0-b893e5cc676e.png)


### Copyright
- VR Hand： https://www.unrealengine.com/marketplace/en-US/product/handy-hands-pack-vr-hands-megapack
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
# Making a hitting ball 
## Principle 
To start with 2 spheres are to be made.
- A complete sphere (object)
- A broken sphere (animation)
The creation principle here is that when the VR Hand overlaps the collision body of the full sphere, the full sphere disappears and the animation of the broken sphere starts at this point
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![2A96D482-9BBF-4417-8EFC-F647BE51F23A](https://user-images.githubusercontent.com/92038037/204269564-dd829f71-24e9-491f-8b3b-e48b793f8620.png)
![221128-TheBoxingRoom-Layout-12](https://user-images.githubusercontent.com/92038037/204270611-66b04332-1418-4189-9bf8-c0c963e6e478.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
## Material 
The material is designed with a glassy texture. It is to make the visual effect more interesting.

![M_BBall_R 材质](https://user-images.githubusercontent.com/92038037/204271185-52093188-3d7d-41b9-be9b-1536d6e182cc.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

## Blueprint of the crushing effect 
### Making the ball 
Start by designing the 3 colliding bodies of the sphere
- front box (points are added when the hand overlaps this part)
- back box (no points for the hand overlapping this part, but the box will disappear)
- vibration sphere (a collision zone that transmits vibration signals to the Arduino)

![221128-TheBoxingRoom-Layout-13](https://user-images.githubusercontent.com/92038037/204273267-602286bb-bc14-4854-9aff-722f45b179dc.png)
### Setting up the VRhand blueprint
Make the hand jump to the animation blueprint when interlocking the spheres

![手部击球动画跳转](https://user-images.githubusercontent.com/92038037/204273798-f1117358-14a0-4763-b026-48a648d64f7a.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

# Bomb and wall making 
The same principle is used to make bombs and walls as for hitting balls, the difference is that points are deducted when the VRHand touches the bombs and walls. The principle of the scoring system will be explained later.


![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![BP_Bomb](https://user-images.githubusercontent.com/92038037/204274618-8211ccc2-3a8b-4e11-a945-bd3b84c47811.png)
![HighresScreenshot00002](https://user-images.githubusercontent.com/92038037/204276529-980f8191-3984-40bb-bec5-62aaebf3e6e7.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

# Launcher 
## Principle 
In the UE I set up 6 launch points and the spheres/bombs/walls will be launched in these 6 channels.

![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![221128-TheBoxingRoom-Layout-15](https://user-images.githubusercontent.com/92038037/204280546-8218afdd-b786-43c8-b2b9-feb62ff7c402.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![09F7C8F6-1DF7-42FD-B7F5-05FA9D9C8009](https://user-images.githubusercontent.com/92038037/204280586-1de0c8d7-1a3b-4402-8966-30b2cc33cd9e.png)


## Blueprint
Once this system has been written, I will set up a list of launches in "Details" for each ball and its launch position. This blueprint will generate one sphere at a time, and this blueprint will keep cycling. The list of balls I have set up will be launched one by one.


![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![发射器1](https://user-images.githubusercontent.com/92038037/204280742-77b92d40-bda1-4ea0-a8a2-14da6d732480.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
Here is a blueprint of the sphere launch interval, the value affected by heart rate is the time interval between launches

![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![发射器2](https://user-images.githubusercontent.com/92038037/204286025-9d5f1926-c873-4fae-bab0-e4ebe19fb462.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

## Launch list 
![VRGame_Orlando - Unreal Editor 2022_11_28 12_49_22](https://user-images.githubusercontent.com/92038037/204325191-2552de5a-2b34-4d37-851b-18584756268b.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

# Scoring system 
## Principle 

The game system will know how many spheres are to be played in total, for example if I set 200 spheres, then the total number of points is 2000. If a sphere is not hit 10 points will be deducted. So how does the game know that the player hasn't reached the spheres?
It is because I set up an invisible wall behind the player. If a sphere is detected, it means the player didn't hit that sphere, the combo will clear and 10 points will be deducted. This data is then sent to the blueprint in EndUI at the end of the game, presenting the final score.
Similarly when a hand comes into contact with a bomb, it is sent to the GameUI blueprint to count the points together.

![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![221128-TheBoxingRoom-Layout-16](https://user-images.githubusercontent.com/92038037/204324665-02616413-fb0e-4cd1-b459-0cbe794a5b60.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

## Blueprint
GameUI's are responsible for scoring and sending scores to EndUI once they have been calculated

![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![计分BP1](https://user-images.githubusercontent.com/92038037/204290862-69d4bf54-b4bc-493d-a8db-a3de10b7107f.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)



# Scene 
## Start Level
The player will enter this screen first and will first see their heart rate values and get used to the virtual world. When ready to start, place your hand on the UI platform and the door will automatically open to enter the game interface

![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![HighresScreenshot00002 (2)](https://user-images.githubusercontent.com/92038037/204285259-43079b2d-3f6c-404a-b02a-3fc40e030e8b.png)
![HighresScreenshot00004 (2)](https://user-images.githubusercontent.com/92038037/204285343-7e9bcc3f-f52d-41f8-8bdc-9d5715d1ad05.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

## Game Level
This is the game interface

![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![HighresScreenshot00008](https://user-images.githubusercontent.com/92038037/204288788-e8865aef-e858-48a7-ac67-d91f5cf73fd5.png)
![HighresScreenshot00006](https://user-images.githubusercontent.com/92038037/204288840-3d8818c7-80e9-490a-bc27-5baf67680eb7.png)
![HighresScreenshot00007 (2)](https://user-images.githubusercontent.com/92038037/204288862-d6d6a374-eb88-4820-a5c9-a4b3d2dfe72d.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)


---

# Unreal Engine Link to Arduino
## Plugins
The SerialCOM plugin correlates data from the Arduino's sensors with Unreal Engine blueprints to achieve real-world interaction. The principle is to pass the Arduino's serial data into the Unreal Engine and write the data to manipulate objects in the game. For example, real-life buttons can switch on and off lights or change colours in the game.

- Link：https://forums.unrealengine.com/t/new-free-arduino-serial-communication-plugin-serial-com-v3-fork-from-ue4duino/265486
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![serial_com_fork_03](https://user-images.githubusercontent.com/92038037/204292841-7222aca1-94f2-4a16-9140-619eb0bf1043.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

## Link to Arduino BP 
The Arduino data is first verified to be transferred to the UE, then the heart rate values are set into a Widget's text so that the BeginUI and GameUI can present the user heart rate data. The player can then see the heart rate values in both game screens (Start Level and Game Level).

![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![心率链接BP](https://user-images.githubusercontent.com/92038037/204293375-d14a8333-a644-4a1a-bf1b-6ef5649a48b6.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

## Heart rate affects ball speed BP 
#### principle
Set the time interval between balls coming out of the launcher by different heart rate intervals. I set the heart rate detectable range from 0-200BPM and the ball time interval from 2-0s (flashback) for different heart rate zones. This way the lower the heart rate the faster the launcher will be and the higher the heart rate the slower the launcher will be.

![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

![心率算法1](https://user-images.githubusercontent.com/92038037/204293471-236a51b4-0094-4a2f-aaa2-edb74276170a.png)
![心率算法2](https://user-images.githubusercontent.com/92038037/204293489-7699866b-41b3-4bd9-b3d2-8ad77348cfdb.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)


## UE transmits vibration data back to Arduino
The UE sends the string "0" to the Arduino when the VRHand overlaps the Vibration sphere of the ball, and the Arduino vibrates for 0.5 seconds when it receives the "0".
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![0ACDF384-B652-46E3-8A6A-240706504085](https://user-images.githubusercontent.com/92038037/204323946-df5fc3d2-fdb3-4376-a96d-349902aa1186.png)
![221128-TheBoxingRoom-Layout-13](https://user-images.githubusercontent.com/92038037/204309217-e09654d1-b5de-469c-84dc-7519ddeb58ac.png)
![震动BP](https://user-images.githubusercontent.com/92038037/204293611-c7bd508f-cf59-4251-a825-da57d8bd5871.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)



