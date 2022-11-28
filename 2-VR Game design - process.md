
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

# 手部模型更换
## Purpose 目的 
The presence of a controller in VR games affects the player's gaming experience. Replacing the grips with hand models while allowing the hands to have movement changes makes the game more realistic.
VR游戏出现手柄影响玩家的游戏体验。将手柄换成手部模型，同时让手部有动作变换让游戏更具真实性。

## Effects 效果
In the process of changing the model, the orientation of the virtual world palm needs to be constantly adjusted to match the orientation of the real world palm, as follows.

在更换模型的过程中，需要不断调整虚拟世界手掌的方向要与现实世界的手掌方向一致，以下是正在调整的过程：
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
![IMG_6516](https://user-images.githubusercontent.com/92038037/204267824-a56b0827-c282-4223-a915-a03575222797.jpg)

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
![BP_Bomb](https://user-images.githubusercontent.com/92038037/204274618-8211ccc2-3a8b-4e11-a945-bd3b84c47811.png)
![space](https://user-images.githubusercontent.com/92038037/204270709-a69fe2d9-c077-492d-9d18-c3c3fbbc4617.png)
