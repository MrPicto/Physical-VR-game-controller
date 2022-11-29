
![HighresScreenshot00006](https://user-images.githubusercontent.com/92038037/204267343-8dc7fa2e-ec81-4e8c-876e-aee93d874e13.png)

# Unreal Engine Design 设计草图

根据前期Arduino的设定，为了设计一个VR拳击游戏。就要设置几个基础游戏框架：
- 将普通操控手柄变成手部模型
- 制作打击球
  - 制作球体材质+
  - 制作击打效果
    - 3D建模碎裂的球体
    - 制作球体破碎的蓝图逻辑
    - 破碎声音
- 制作炸弹&墙体
- 球体发射器（心率数据控制区）
- 计分系统
- 游戏结束判断系统
- 场景制作
- Arduino与Unreal 链接
  - 手柄的震动设计
  - 心率影响发球速度的蓝图
  - 震动蓝图

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

# Hand model replacement 手部模型更换
## Purpose 目的 
The presence of a controller in VR games affects the player's gaming experience. Replacing the grips with hand models while allowing the hands to have movement changes makes the game more realistic.
VR游戏出现手柄影响玩家的游戏体验。将手柄换成手部模型，同时让手部有动作变换让游戏更具真实性。

## Blueprint 
Bind the hand skeleton and attach the animation to the blueprint of the handle input.

绑定手部骨骼，将动画连接到手柄input的蓝图中。
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![221128-TheBoxingRoom-Layout-14](https://user-images.githubusercontent.com/92038037/204279929-c9410ff8-4800-4820-b1e8-ffd470a35af5.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)


## Effects 效果
In the process of changing the model, the orientation of the virtual world palm needs to be constantly adjusted to match the orientation of the real world palm, as follows.

在更换模型的过程中，需要不断调整虚拟世界手掌的方向要与现实世界的手掌方向一致，以下是正在调整的过程：
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![IMG_6516](https://user-images.githubusercontent.com/92038037/204267824-a56b0827-c282-4223-a915-a03575222797.jpg)

## Handle vibration effect 手柄震动效果
#### Hit Ball Haptic
![HitBall_Haptic](https://user-images.githubusercontent.com/92038037/204439451-a6a06926-2bfa-4538-89bb-799008fbd185.png)
#### Bomb Haptic
![Bomb_Haptic](https://user-images.githubusercontent.com/92038037/204439458-d544b32b-760b-4090-8ae0-b893e5cc676e.png)


### Copyright
- VR Hand： https://www.unrealengine.com/marketplace/en-US/product/handy-hands-pack-vr-hands-megapack
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
# Making a hitting ball 打击球制作
## Principle 原理
先要制作2个球体：
- 一个完整的球体（物体）
- 一个破碎的球体（动画）
这里的创作原理是当VR Hand 与完整球体的碰撞体交叠时，完整球体会消失，这时候开始播放破碎球体的动画
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![2A96D482-9BBF-4417-8EFC-F647BE51F23A](https://user-images.githubusercontent.com/92038037/204269564-dd829f71-24e9-491f-8b3b-e48b793f8620.png)
![221128-TheBoxingRoom-Layout-12](https://user-images.githubusercontent.com/92038037/204270611-66b04332-1418-4189-9bf8-c0c963e6e478.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
## Material 材质
The material is designed with a glassy texture. It is to make the visual effect more interesting.

材质设计的是玻璃质感。整体视觉效果趣味性更强。
![M_BBall_R 材质](https://user-images.githubusercontent.com/92038037/204271185-52093188-3d7d-41b9-be9b-1536d6e182cc.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

## Blueprint of the crushing effect 破碎效果蓝图
### Making the ball 制作球体
先设计球体的3个碰撞体
- front box(手部与这个部分交叠就加分)
- back box(手部与这个部分交叠不加分，但盒子会消失)
- vibration sphere（给Arduino传输振动信号的碰撞区）

![221128-TheBoxingRoom-Layout-13](https://user-images.githubusercontent.com/92038037/204273267-602286bb-bc14-4854-9aff-722f45b179dc.png)
### Setting up the VRhand blueprint 设置VRhand蓝图
Make the hand jump to the animation blueprint when interlocking the spheres

让手部在交叠球体的时候跳转至动画蓝图

![手部击球动画跳转](https://user-images.githubusercontent.com/92038037/204273798-f1117358-14a0-4763-b026-48a648d64f7a.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

# Bomb and wall making 炸弹与墙体的制作
The same principle is used to make bombs and walls as for hitting balls, the difference is that points are deducted when the VRHand touches the bombs and walls. The principle of the scoring system will be explained later.

与击打球同样的原理制作炸弹和墙体，不同的是在VRHand触碰炸弹与墙体的时候要扣分。后面会解释计分系统的原理。
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![BP_Bomb](https://user-images.githubusercontent.com/92038037/204274618-8211ccc2-3a8b-4e11-a945-bd3b84c47811.png)
![HighresScreenshot00002](https://user-images.githubusercontent.com/92038037/204276529-980f8191-3984-40bb-bec5-62aaebf3e6e7.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

# Launcher 发射器
## Principle 原理
In the UE I set up 6 launch points and the spheres/bombs/walls will be launched in these 6 channels.

在UE中我设置了6个发射点，球体/炸弹/墙体会在这6个通道中发射出来。
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![221128-TheBoxingRoom-Layout-15](https://user-images.githubusercontent.com/92038037/204280546-8218afdd-b786-43c8-b2b9-feb62ff7c402.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![09F7C8F6-1DF7-42FD-B7F5-05FA9D9C8009](https://user-images.githubusercontent.com/92038037/204280586-1de0c8d7-1a3b-4402-8966-30b2cc33cd9e.png)


## Blueprint
Once this system has been written, I will set up a list of launches in "Details" for each ball and its launch position. This blueprint will generate one sphere at a time, and this blueprint will keep cycling. The list of balls I have set up will be launched one by one.

这个系统写完之后，我会在“细节”设置每一个出球以及发射位置，组成一个发射列表。这个蓝图一次会生成一个球体，此蓝图会一直循环。将我设置的出球名单一个个发射出。
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![发射器1](https://user-images.githubusercontent.com/92038037/204280742-77b92d40-bda1-4ea0-a8a2-14da6d732480.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
Here is a blueprint of the sphere launch interval, the value affected by heart rate is the time interval between launches

这里是球体发射间隔的蓝图，心率影响的数值就是发球的时间间隔
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![发射器2](https://user-images.githubusercontent.com/92038037/204286025-9d5f1926-c873-4fae-bab0-e4ebe19fb462.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

## Launch list 发射列表
![VRGame_Orlando - Unreal Editor 2022_11_28 12_49_22](https://user-images.githubusercontent.com/92038037/204325191-2552de5a-2b34-4d37-851b-18584756268b.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

# Scoring system 计分系统
## Principle 原理

The game system will know how many spheres are to be played in total, for example if I set 200 spheres, then the total number of points is 2000. If a sphere is not hit 10 points will be deducted. So how does the game know that the player hasn't reached the spheres?
It is because I set up an invisible wall behind the player. If a sphere is detected, it means the player didn't hit that sphere, the combo will clear and 10 points will be deducted. This data is then sent to the blueprint in EndUI at the end of the game, presenting the final score.
Similarly when a hand comes into contact with a bomb, it is sent to the GameUI blueprint to count the points together.

游戏系统会知道总共要出多少球体，比如我设置了200个球体，那么总积分就是2000分。如果没有击中一个球就会扣10分。那么游戏是怎么知道玩家没有达到球体呢？
是因为我在玩家的背后设置一个隐形墙。如果检测到球体，就说明玩家没有击中这个球体，combo会清零，积分会扣10分。然后这个数据会在游戏结束后发送到EndUI的蓝图中，呈现最后的积分。
同样当手部接触到炸弹，也会发送到EndUI的蓝图中一起算分数。
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![221128-TheBoxingRoom-Layout-16](https://user-images.githubusercontent.com/92038037/204324665-02616413-fb0e-4cd1-b459-0cbe794a5b60.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

## Blueprint
GameUI's are responsible for scoring and sending scores to EndUI once they have been calculated

GameUI的负责计分，分数计算完毕发送到EndUI
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![计分BP1](https://user-images.githubusercontent.com/92038037/204290862-69d4bf54-b4bc-493d-a8db-a3de10b7107f.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)



# Scene 场景制作
## Start Level
The player will enter this screen first and will first see their heart rate values and get used to the virtual world. When ready to start, place your hand on the UI platform and the door will automatically open to enter the game interface

玩家会先进入这个界面，会先看到自己的心率数值，适应虚拟世界。准备开始时，将手放在UI平台上，门会自动打开进入到游戏界面
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![HighresScreenshot00002 (2)](https://user-images.githubusercontent.com/92038037/204285259-43079b2d-3f6c-404a-b02a-3fc40e030e8b.png)
![HighresScreenshot00004 (2)](https://user-images.githubusercontent.com/92038037/204285343-7e9bcc3f-f52d-41f8-8bdc-9d5715d1ad05.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

## Game Level
This is the game interface

此为正式的游戏界面
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![HighresScreenshot00008](https://user-images.githubusercontent.com/92038037/204288788-e8865aef-e858-48a7-ac67-d91f5cf73fd5.png)
![HighresScreenshot00006](https://user-images.githubusercontent.com/92038037/204288840-3d8818c7-80e9-490a-bc27-5baf67680eb7.png)
![HighresScreenshot00007 (2)](https://user-images.githubusercontent.com/92038037/204288862-d6d6a374-eb88-4820-a5c9-a4b3d2dfe72d.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)


---

# Unreal Engine Link to Arduino
## Plugins
The SerialCOM plugin correlates data from the Arduino's sensors with Unreal Engine blueprints to achieve real-world interaction. The principle is to pass the Arduino's serial data into the Unreal Engine and write the data to manipulate objects in the game. For example, real-life buttons can switch on and off lights or change colours in the game.

SerialCOM插件将Arduino所属传感器的数据与Unreal Engine蓝图进行关联，从而达到虚实交互。原理是将Arduino的串口数据传入到Unreal Engine中，对数据进行编写去操控游戏中的物件。比如现实中的按钮可以开关游戏中的灯光或者改变颜色。
- Link：https://forums.unrealengine.com/t/new-free-arduino-serial-communication-plugin-serial-com-v3-fork-from-ue4duino/265486
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![serial_com_fork_03](https://user-images.githubusercontent.com/92038037/204292841-7222aca1-94f2-4a16-9140-619eb0bf1043.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

## Link to Arduino BP 链接Arduino的BP
The Arduino data is first verified to be transferred to the UE, then the heart rate values are set into a Widget's text so that the BeginUI and GameUI can present the user heart rate data. The player can then see the heart rate values in both game screens (Start Level and Game Level).

首先先验证Arduino数据是否传输到UE中，然后将心率数值设置到一个Widget的text中，让BeginUI和GameUI能呈现用户心率数据。玩家这样可以在两个游戏界面（Start Level和Game Level）都能看到心率数值。
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![心率链接BP](https://user-images.githubusercontent.com/92038037/204293375-d14a8333-a644-4a1a-bf1b-6ef5649a48b6.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

## Heart rate affects ball speed BP 心率影响出球速率的BP
#### 原理
Set the time interval between balls coming out of the launcher by different heart rate intervals. I set the heart rate detectable range from 0-200BPM and the ball time interval from 2-0s (flashback) for different heart rate zones. This way the lower the heart rate the faster the launcher will be and the higher the heart rate the slower the launcher will be.

通过不同的心率区间设置发射器出球的时间间隔。我将心率可检测范围设置在0-200BPM，不同心率区间的球体时间间隔从2-0s（倒叙）。这样心率越低发球速度越快，心率越高发球速度越慢。
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)

![心率算法1](https://user-images.githubusercontent.com/92038037/204293471-236a51b4-0094-4a2f-aaa2-edb74276170a.png)
![心率算法2](https://user-images.githubusercontent.com/92038037/204293489-7699866b-41b3-4bd9-b3d2-8ad77348cfdb.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)


## UE transmits vibration data back to Arduino
The UE sends the string "0" to the Arduino when the VRHand overlaps the Vibration sphere of the ball, and the Arduino vibrates for 0.5 seconds when it receives the "0".
VRHand 在接触到球体的Vibration sphere时，UE会发送字符串“0”到Arduino，Arduino在收到“0”时会震动0.5秒。
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![0ACDF384-B652-46E3-8A6A-240706504085](https://user-images.githubusercontent.com/92038037/204323946-df5fc3d2-fdb3-4376-a96d-349902aa1186.png)
![221128-TheBoxingRoom-Layout-13](https://user-images.githubusercontent.com/92038037/204309217-e09654d1-b5de-469c-84dc-7519ddeb58ac.png)
![震动BP](https://user-images.githubusercontent.com/92038037/204293611-c7bd508f-cf59-4251-a825-da57d8bd5871.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)



