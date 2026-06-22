# 🚗 C04 Maqueen小车入门

> **节点编号**: C04
> **适用Track**: Track C (8岁MicroPython进阶)
> **预计时长**: 3-4次活动，每次45分钟

---

## 📌 适用Track说明

本节点使用专为Micro:bit设计的Maqueen小车，它简化了电路连接，让孩子专注于编程和算法。

---

## 🔗 前置知识

- [[C01-MicroPython入门]] - MicroPython基础
- [[C02-传感器读取]] - 传感器读取
- [[C03-电机控制基础]] - 电机控制原理

---

## 🧠 核心原理简述（给家长）

**Maqueen** 是DFRobot出品的Micro:bit编程小车，特点：

- **即插即用**: Micro:bit直接插上就能用
- **集成电机**: 两个TT电机，带编码器
- **集成传感器**: 超声波接口、循迹传感器、LED灯
- **扩展接口**: 丰富的Grove接口

优势：
- 无需面包板和杜邦线
- 电机驱动已集成
- 适合快速原型开发

---

## 🔬 趣味实验清单

### 实验1: 🚙 前进后退

**零件清单**:
- Maqueen小车套件
- Micro:bit V2 一块
- 3节AAA电池
- 电脑

**玩法描述**:
1. 组装Maqueen：
   - 安装电池盒
   - 插入Micro:bit
2. 编写前进程序：
```python
from microbit import *
import maqueen

# 前进
maqueen.motor_run(maqueen.Motors.ALL, maqueen.Dir.CW, 100)
sleep(2000)

# 停止
maqueen.motor_stop(maqueen.Motors.ALL)
```
3. 编写后退程序：
```python
from microbit import *
import maqueen

# 后退
maqueen.motor_run(maqueen.Motors.ALL, maqueen.Dir.CCW, 100)
sleep(2000)

# 停止
maqueen.motor_stop(maqueen.Motors.ALL)
```
4. 测试前进后退

**观察与思考**:
- 两个电机速度一样吗？小车走直线吗？
- 如何调整两侧电机速度？
- `maqueen.Dir.CW` 和 `maqueen.Dir.CCW` 代表什么？

---

### 实验2: 🔁 转弯控制

**零件清单**:
- Maqueen小车套件
- Micro:bit V2 一块
- 电池
- 电脑

**玩法描述**:
1. 左转：
```python
from microbit import *
import maqueen

# 左转：右轮前进，左轮停止
maqueen.motor_run(maqueen.Motors.M1, maqueen.Dir.CW, 100)
maqueen.motor_run(maqueen.Motors.M2, maqueen.Dir.CW, 0)
sleep(1000)
maqueen.motor_stop(maqueen.Motors.ALL)
```
2. 右转：
```python
from microbit import *
import maqueen

# 右转：左轮前进，右轮停止
maqueen.motor_run(maqueen.Motors.M1, maqueen.Dir.CW, 0)
maqueen.motor_run(maqueen.Motors.M2, maqueen.Dir.CW, 100)
sleep(1000)
maqueen.motor_stop(maqueen.Motors.ALL)
```
3. 原地旋转：
```python
from microbit import *
import maqueen

# 原地左转
maqueen.motor_run(maqueen.Motors.M1, maqueen.Dir.CCW, 80)
maqueen.motor_run(maqueen.Motors.M2, maqueen.Dir.CW, 80)
sleep(1000)
maqueen.motor_stop(maqueen.Motors.ALL)
```
4. 画正方形：
```python
from microbit import *
import maqueen

for _ in range(4):
    # 前进
    maqueen.motor_run(maqueen.Motors.ALL, maqueen.Dir.CW, 80)
    sleep(800)
    # 左转
    maqueen.motor_run(maqueen.Motors.M1, maqueen.Dir.CW, 0)
    maqueen.motor_run(maqueen.Motors.M2, maqueen.Dir.CW, 80)
    sleep(500)

maqueen.motor_stop(maqueen.Motors.ALL)
```

**观察与思考**:
- 前进转弯和原地转弯有什么区别？
- 如何让转弯角度更精确？
- 画正方形时，每边长度一样吗？

---

### 实验3: 💡 灯光控制

**零件清单**:
- Maqueen小车套件
- Micro:bit V2 一块
- 电池
- 电脑

**玩法描述**:
1. 控制车头灯：
```python
from microbit import *
import maqueen

# 开灯
maqueen.write_led(maqueen.LED.LEDLeft, maqueen.LEDswitch.turnOn, 100)
maqueen.write_led(maqueen.LED.LEDRight, maqueen.LEDswitch.turnOn, 100)
sleep(2000)

# 关灯
maqueen.write_led(maqueen.LED.LEDLeft, maqueen.LEDswitch.turnOff, 0)
maqueen.write_led(maqueen.LED.LEDRight, maqueen.LEDswitch.turnOff, 0)
```
2. 转向灯效果：
```python
from microbit import *
import maqueen

while True:
    # 左转向灯
    maqueen.write_led(maqueen.LED.LEDLeft, maqueen.LEDswitch.turnOn, 100)
    sleep(500)
    maqueen.write_led(maqueen.LED.LEDLeft, maqueen.LEDswitch.turnOff, 0)
    sleep(500)
```
3. 呼吸灯效果：
```python
from microbit import *
import maqueen

while True:
    for brightness in range(0, 255, 5):
        maqueen.write_led(maqueen.LED.LEDLeft, maqueen.LEDswitch.turnOn, brightness)
        sleep(50)
    for brightness in range(255, 0, -5):
        maqueen.write_led(maqueen.LED.LEDLeft, maqueen.LEDswitch.turnOn, brightness)
        sleep(50)
```

**观察与思考**:
- Maqueen有几个LED？
- 如何用灯光表达小车状态？
- PWM控制亮度的原理是什么？

---

## 🚀 拓展挑战

### 挑战1: 按钮遥控
用Micro:bit的A/B按钮控制小车运动。

### 挑战2: 倾斜控制
用Micro:bit的加速度计，倾斜控制小车方向。

### 挑战3: 编码器测速
读取编码器数据，测量小车实际速度。

---

## 🔗 相关链接

- [[03-Hardware-Sensors/]] - 硬件传感器参考
- [[02-Concepts/实体计算]] - 实体计算理念
- [[C03-电机控制基础]] - 前置节点：电机控制
- [[C05-避障小车]] - 下一个节点：避障小车
- [[02-Concepts/机器人教育]] - 机器人教育概述

---

## 📝 家长小贴士

> 💡 **关键点**: Maqueen的设计理念是"让编程更简单"。它把复杂的电路集成化，让孩子能快速看到编程效果。

> ⚠️ **常见误区**: Maqueen的电机速度不是线性的。速度值50可能不动，需要从70-80开始测试。
