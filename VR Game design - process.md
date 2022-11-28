
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

# 手部模型更换
## Purpose 目的 
The presence of a controller in VR games affects the player's gaming experience. Replacing the grips with hand models while allowing the hands to have movement changes makes the game more realistic.
VR游戏出现手柄影响玩家的游戏体验。将手柄换成手部模型，同时让手部有动作变换让游戏更具真实性。

## Effects 效果
In the process of changing the model, the orientation of the virtual world palm needs to be constantly adjusted to match the orientation of the real world palm, as follows.

在更换模型的过程中，需要不断调整虚拟世界手掌的方向要与现实世界的手掌方向一致，以下是正在调整的过程：
![IMG_6516](https://user-images.githubusercontent.com/92038037/204267824-a56b0827-c282-4223-a915-a03575222797.jpg)

### Copyright



