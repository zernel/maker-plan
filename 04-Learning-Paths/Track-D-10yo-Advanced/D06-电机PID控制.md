# 🎯 D06 电机PID控制

> **节点编号**: D06
> **适用Track**: Track D (10-12岁竞赛冲刺)
> **预计时长**: 4-5次活动，每次60分钟

---

## 📌 适用Track说明

本节点是 Track D 的核心技术节点，孩子将学习 PID 控制算法，让电机实现精准、稳定的运动控制。这是机器人竞赛中让小车"听话"的关键技术，也是 WRC 机器人大赛的核心考核点。

---

## 🔗 前置知识

- 完成 [[04-Learning-Paths/Track-D-10yo-Advanced/D05-传感器融合|D05 传感器融合]]
- 了解 PWM 调速原理
- 能使用 MicroPython 控制电机和读取传感器

---

## 🧠 核心原理简述（给家长）

**PID 控制**是工业界最常用的控制算法，它的核心思想是"根据偏差调整动作"。

想象你开车时想保持在车道中间：
- **P（比例）**：车偏左了，你就向右打方向盘。偏得越多，打得越多。
- **I（积分）**：如果车一直稍微偏左，说明你的方向盘打得不够，需要慢慢加大修正力度。
- **D（微分）**：如果车突然快速偏移，说明需要紧急修正；如果偏移很慢，就温和修正。

三个参数配合使用：
- **Kp（比例系数）**：决定反应速度。太大会震荡，太小会反应慢。
- **Ki（积分系数）**：消除稳态误差。太大会过冲，太小误差消除慢。
- **Kd（微分系数）**：抑制震荡。太大会抖动，太小会不稳。

为什么学 PID：
- **竞赛必备**：循迹小车、平衡车、机械臂都需要 PID
- **工程思维**：理解反馈控制系统的底层逻辑
- **现实应用**：空调温控、汽车定速巡航、无人机悬停都用 PID

---

## 🔬 趣味实验清单

### 实验1: 🌡️ 温度控制器（理解 P 控制）

**零件清单**:
- ESP32 开发板 × 1
- DS18B20 温度传感器 × 1
- 加热模块（或小风扇）× 1
- OLED 显示屏 × 1
- 面包板和杜邦线

**玩法描述**:
1. 设定目标温度为 30°C，用 P 控制调节加热功率：
```python
from machine import Pin, PWM
import time

# PID 参数
Kp = 10.0
Ki = 0.0
Kd = 0.0

# 目标温度
target_temp = 30.0

# 误差累计
integral = 0
last_error = 0

def read_temperature():
    # 读取温度传感器（模拟值）
    # 实际使用时替换为真实传感器读取
    return 25.0  # 示例值

def set_heater_power(power):
    # power: 0-100
    # 控制加热模块
    pwm = PWM(Pin(25), freq=1000)
    pwm.duty(int(power * 10.23))  # 0-1023
    print(f"加热功率: {power}%")

def pid_control(current_temp):
    global integral, last_error
    
    # 计算误差
    error = target_temp - current_temp
    
    # P 项
    p_term = Kp * error
    
    # I 项（累计误差）
    integral += error
    i_term = Ki * integral
    
    # D 项（误差变化率）
    d_term = Kd * (error - last_error)
    last_error = error
    
    # 计算输出
    output = p_term + i_term + d_term
    
    # 限制输出范围
    output = max(0, min(100, output))
    
    return output

# 主循环
while True:
    temp = read_temperature()
    power = pid_control(temp)
    set_heater_power(power)
    print(f"当前温度: {temp}°C, 目标: {target_temp}°C")
    time.sleep(1)
```

2. 观察不同 Kp 值的效果：
   - Kp = 5：反应慢，但稳定
   - Kp = 20：反应快，但可能震荡
   - Kp = 50：剧烈震荡

**观察与思考**:
- Kp 太小时，温度能达到目标吗？
- Kp 太大时，温度会怎样变化？
- 为什么只有 P 控制会有"稳态误差"？

---

### 实验2: 🚗 循迹小车（PID 完整应用）

**零件清单**:
- ESP32 开发板 × 1
- TB6612 电机驱动板 × 1
- TT 电机 × 2（带编码器更佳）
- 5 路循迹传感器 × 1
- 小车底盘 × 1
- 锂电池组 × 1
- 万向轮 × 1

**玩法描述**:
1. 搭建循迹小车，用 PID 控制方向：
```python
from machine import Pin, PWM
import time

# 电机引脚
motor_left_pwm = PWM(Pin(25), freq=1000)
motor_left_dir = Pin(26, Pin.OUT)
motor_right_pwm = PWM(Pin(27), freq=1000)
motor_right_dir = Pin(14, Pin.OUT)

# 循迹传感器引脚
sensor_pins = [Pin(i, Pin.IN) for i in [32, 33, 34, 35, 36]]

# PID 参数
Kp = 0.5
Ki = 0.01
Kd = 0.1

# 误差累计
integral = 0
last_error = 0

def read_sensors():
    """读取5路传感器，返回加权误差"""
    values = [s.value() for s in sensor_pins]
    # 权重: -2, -1, 0, 1, 2
    weights = [-2, -1, 0, 1, 2]
    error = sum(v * w for v, w in zip(values, weights))
    return error

def set_motors(left_speed, right_speed):
    """设置左右电机速度 (-100 到 100)"""
    # 左电机
    if left_speed >= 0:
        motor_left_dir.value(0)
        motor_left_pwm.duty(int(left_speed * 10.23))
    else:
        motor_left_dir.value(1)
        motor_left_pwm.duty(int(-left_speed * 10.23))
    
    # 右电机
    if right_speed >= 0:
        motor_right_dir.value(0)
        motor_right_pwm.duty(int(right_speed * 10.23))
    else:
        motor_right_dir.value(1)
        motor_right_pwm.duty(int(-right_speed * 10.23))

def pid_control(error):
    global integral, last_error
    
    # P 项
    p_term = Kp * error
    
    # I 项
    integral += error
    i_term = Ki * integral
    
    # D 项
    d_term = Kd * (error - last_error)
    last_error = error
    
    # 计算修正量
    correction = p_term + i_term + d_term
    
    return correction

# 基础速度
base_speed = 50

# 主循环
while True:
    error = read_sensors()
    correction = pid_control(error)
    
    # 调整左右电机速度
    left_speed = base_speed + correction
    right_speed = base_speed - correction
    
    # 限制速度范围
    left_speed = max(-100, min(100, left_speed))
    right_speed = max(-100, min(100, right_speed))
    
    set_motors(left_speed, right_speed)
    time.sleep(0.01)  # 10ms 控制周期
```

2. 调参步骤：
   - 先只用 Kp，从小到大调，找到能跟线但不震荡的值
   - 加入 Kd，抑制震荡
   - 最后加 Ki，消除稳态误差

**观察与思考**:
- 小车走直线时，PID 输出是多少？
- 小车过弯时，哪个参数最重要？
- 为什么控制周期要短（10ms）？

---

### 实验3: ⚖️ 电机速度闭环控制（编码器反馈）

**零件清单**:
- ESP32 开发板 × 1
- TB6612 电机驱动板 × 1
- 带编码器的 TT 电机 × 2
- 小车底盘 × 1
- 锂电池组 × 1

**玩法描述**:
1. 使用编码器实现精确速度控制：
```python
from machine import Pin, PWM
import time

# 编码器计数
encoder_count_left = 0
encoder_count_right = 0

# 编码器中断处理
def encoder_left_isr(pin):
    global encoder_count_left
    encoder_count_left += 1

def encoder_right_isr(pin):
    global encoder_count_right
    encoder_count_right += 1

# 编码器引脚（中断模式）
encoder_left = Pin(34, Pin.IN)
encoder_left.irq(trigger=Pin.IRQ_RISING, handler=encoder_left_isr)

encoder_right = Pin(35, Pin.IN)
encoder_right.irq(trigger=Pin.IRQ_RISING, handler=encoder_right_isr)

# 电机引脚
motor_left_pwm = PWM(Pin(25), freq=1000)
motor_left_dir = Pin(26, Pin.OUT)
motor_right_pwm = PWM(Pin(27), freq=1000)
motor_right_dir = Pin(14, Pin.OUT)

# PID 参数
Kp = 0.8
Ki = 0.02
Kd = 0.05

# 目标速度（编码器脉冲/秒）
target_speed = 100

# 误差累计
integral_left = 0
integral_right = 0
last_error_left = 0
last_error_right = 0

def read_speed(interval_ms=100):
    """读取电机速度（脉冲/秒）"""
    global encoder_count_left, encoder_count_right
    
    # 保存当前计数
    count_left = encoder_count_left
    count_right = encoder_count_right
    
    # 等待采样间隔
    time.sleep_ms(interval_ms)
    
    # 计算速度
    speed_left = (encoder_count_left - count_left) * (1000 / interval_ms)
    speed_right = (encoder_count_right - count_right) * (1000 / interval_ms)
    
    return speed_left, speed_right

def pid_speed_control(current_speed, target, integral, last_error):
    """PID 速度控制"""
    # 计算误差
    error = target - current_speed
    
    # P 项
    p_term = Kp * error
    
    # I 项
    integral += error
    i_term = Ki * integral
    
    # D 项
    d_term = Kd * (error - last_error)
    last_error = error
    
    # 计算输出
    output = p_term + i_term + d_term
    
    # 限制输出范围
    output = max(-100, min(100, output))
    
    return output, integral, last_error

def set_motor(speed, pwm_pin, dir_pin):
    """设置单个电机速度"""
    if speed >= 0:
        dir_pin.value(0)
        pwm_pin.duty(int(speed * 10.23))
    else:
        dir_pin.value(1)
        pwm_pin.duty(int(-speed * 10.23))

# 主循环
while True:
    # 读取当前速度
    speed_left, speed_right = read_speed(100)
    
    # PID 控制
    output_left, integral_left, last_error_left = pid_speed_control(
        speed_left, target_speed, integral_left, last_error_left
    )
    output_right, integral_right, last_error_right = pid_speed_control(
        speed_right, target_speed, integral_right, last_error_right
    )
    
    # 设置电机
    set_motor(output_left, motor_left_pwm, motor_left_dir)
    set_motor(output_right, motor_right_pwm, motor_right_dir)
    
    print(f"左轮: {speed_left:.0f} -> {output_left:.1f}")
    print(f"右轮: {speed_right:.0f} -> {output_right:.1f}")
```

2. 实验对比：
   - 不用 PID，直接给固定 PWM，观察速度是否稳定
   - 用 PID，观察速度是否能稳定在目标值
   - 负载变化时（上坡），PID 如何自动调整

**观察与思考**:
- 编码器脉冲数和实际速度是什么关系？
- 为什么两个轮子的 PID 参数可能不同？
- 如何让两个轮子速度完全一致？

---

## 🚀 拓展挑战

### 挑战1: 平衡车 PID
用 MPU6050 陀螺仪实现两轮平衡车，需要同时控制角度和速度两个 PID。

### 挑战2: 机械臂位置控制
用舵机 + 电位器实现机械臂的精确位置控制，让机械臂能准确到达指定角度。

### 挑战3: 自适应 PID
根据小车负载（电池电量、路面摩擦）自动调整 PID 参数，实现"智能调参"。

---

## 🔗 相关链接

- [[04-Learning-Paths/Track-D-10yo-Advanced/D05-传感器融合]] - 前置：传感器融合
- [[04-Learning-Paths/Track-D-10yo-Advanced/D07-状态机设计]] - 下一个：状态机设计
- [[04-Learning-Paths/Track-D-10yo-Advanced/D08-竞赛项目实战]] - PID 在竞赛项目中的应用
- [[03-Hardware-Sensors/电机驱动模块]] - 电机驱动硬件参考
- [[03-Hardware-Sensors/编码器]] - 编码器原理详解
- [[01-White-List-Competitions/02-WRC-Robot-Design|WRC机器人设计大赛]] - 机器人竞赛应用

---

## 📝 家长小贴士

> 💡 **关键点**: PID 调参是个"试错"过程，不要追求一步到位。先只用 P 参数让小车动起来，再慢慢加入 I 和 D。每次只调一个参数，观察效果后再调下一个。

> ⚠️ **常见误区**: 很多家长和孩子一开始就想把三个参数都调好，结果越调越乱。记住：P 是基础，D 是稳定器，I 是微调器。先把 P 调到"能用但有点抖"，再用 D 去抖，最后用 I 消除误差。

---

## ✅ 完成标准

- [ ] 能解释 P、I、D 三个参数的作用
- [ ] 能用 P 控制实现基本的循迹小车
- [ ] 能用 PID 控制实现稳定的循迹小车
- [ ] 能使用编码器实现电机速度闭环控制
- [ ] 理解调参的基本步骤和方法
- [ ] 完成至少1个拓展挑战

---

## 🏆 竞赛应用

本节点技能直接应用于：
- **WRC 机器人设计大赛** - 电机控制是机器人运动的核心
- **全国青少年人工智能大赛** - 智能小车项目需要精确控制
- **人工智能创新挑战赛** - AI+硬件项目需要稳定的执行机构
- **全球发明大会** - 发明作品中的运动控制部分