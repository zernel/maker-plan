# 💡 LED灯带 (NeoPixel/WS2812B)

## 🎯 一句话定义
LED灯带就像魔法灯串，每个灯都能变任何颜色，能创造出绚丽的灯光效果。

## 🧒 给孩子的解释
你见过圣诞节的彩灯吗？LED灯带比那更厉害！每个小灯都能独立变颜色，红的、绿的、蓝的、紫的，什么颜色都行。而且你可以控制每一个灯，让它们像彩虹一样流动，或者跟着音乐跳舞。就像有一串会变魔术的小灯泡！

## 🔬 工作原理

### WS2812B 结构
```
单个LED内部：
┌─────────────────────┐
│   ┌─────┐          │
│   │红LED│          │
│   └─────┘          │
│   ┌─────┐          │
│   │绿LED│          │
│   └─────┘          │
│   ┌─────┐          │
│   │蓝LED│          │
│   └─────┘          │
│   ┌─────────────┐  │
│   │ 控制芯片     │  │
│   └─────────────┘  │
└─────────────────────┘
```

### 数据传输协议
```
单线归零码协议：
  数据线空闲：低电平
  0码：高电平0.35μs + 低电平0.8μs
  1码：高电平0.7μs + 低电平0.6μs
  复位：低电平>50μs

数据格式：
  GRB顺序（绿-红-蓝），每色8位
  共24位/LED
```

### 串联连接
```
DIN ──> LED1 ──> LED2 ──> LED3 ──> ... ──> LEDn
      DOUT  DIN  DOUT  DIN       DOUT

数据从第一个LED开始，依次传递
每个LED读取24位数据后，将剩余数据传给下一个
```

### 颜色混合
```
RGB颜色混合：
  红(255,0,0)
  绿(0,255,0)
  蓝(0,0,255)
  黄(255,255,0) = 红+绿
  青(0,255,255) = 绿+蓝
  紫(255,0,255) = 红+蓝
  白(255,255,255) = 红+绿+蓝
```

## 📊 技术参数

| 参数 | 数值 | 说明 |
|------|------|------|
| 工作电压 | 5V DC | 必须5V供电 |
| 工作电流 | 约60mA/LED（全亮白色） | 最大值 |
| 数据接口 | 单线（DIN/DOUT） | 串联 |
| 颜色深度 | 24位（1677万色） | RGB各8位 |
| 刷新率 | 800kHz | 高速 |
| 工作温度 | -25°C到80°C | 宽温度范围 |
| 尺寸 | 5×5mm/LED | 小巧 |
| 防水等级 | IP30/IP65/IP67 | 可选 |

### 常见规格
```
30LED/m：每米30个LED
60LED/m：每米60个LED
144LED/m：每米144个LED
```

### 引脚说明
```
5V   ──── 电源正极（5V）
DIN  ──── 数据输入
GND  ──── 电源负极
DOUT ──── 数据输出（连接下一个LED）
```

## 🎮 项目创意

### 入门项目
- **单色点亮**：点亮一个颜色
- **颜色切换**：循环切换颜色

### 进阶项目
- **彩虹效果**：彩虹流动效果
- **呼吸灯**：亮度渐变效果
- **追逐效果**：光点追逐

### 创意项目
- **音乐可视化**：跟着音乐节奏变化
- **LED矩阵**：组成显示屏
- **氛围灯**：房间氛围灯光
- **游戏机**：LED矩阵游戏

## 🔌 兼容性

| 开发板 | 支持 | 说明 |
|--------|------|------|
| Micro:bit | ✅ | 使用P0，需要外接电源 |
| Arduino | ✅ | 使用NeoPixel库 |
| ESP32 | ✅ | 支持 |
| Raspberry Pi | ✅ | 使用rpi_ws281x库 |

### Arduino 接线示例
```
WS2812B        Arduino
5V         ──>  5V（外部电源）
DIN        ──>  D6
GND        ──>  GND
```

### Arduino 代码示例
```cpp
#include <Adafruit_NeoPixel.h>

#define PIN 6
#define NUM_LEDS 8

Adafruit_NeoPixel strip = Adafruit_NeoPixel(NUM_LEDS, PIN, NEO_GRB + NEO_KHZ800);

void setup() {
  strip.begin();
  strip.show();
}

void loop() {
  // 红色
  for (int i = 0; i < NUM_LEDS; i++) {
    strip.setPixelColor(i, strip.Color(255, 0, 0));
  }
  strip.show();
  delay(1000);
  
  // 绿色
  for (int i = 0; i < NUM_LEDS; i++) {
    strip.setPixelColor(i, strip.Color(0, 255, 0));
  }
  strip.show();
  delay(1000);
  
  // 蓝色
  for (int i = 0; i < NUM_LEDS; i++) {
    strip.setPixelColor(i, strip.Color(0, 0, 255));
  }
  strip.show();
  delay(1000);
}
```

### Micro:bit 接线示例
```
WS2812B        Micro:bit
5V         ──>  外部5V电源
DIN        ──>  P0
GND        ──>  GND（共地）
```

### MicroPython 代码示例
```python
from microbit import *
import neopixel

np = neopixel.NeoPixel(pin0, 8)

# 红色
for i in range(8):
    np[i] = (255, 0, 0)
np.show()
sleep(1000)

# 绿色
for i in range(8):
    np[i] = (0, 255, 0)
np.show()
sleep(1000)
```

## 💰 价格参考

| 类型 | 价格范围 | 说明 |
|------|----------|------|
| 8灯珠模块 | ¥3-8 | 入门推荐 |
| 1米30灯 | ¥10-20 | 基础款 |
| 1米60灯 | ¥15-30 | 推荐 |
| 1米144灯 | ¥30-60 | 高密度 |
| 灯环（16灯） | ¥5-12 | 圆形效果 |

## 🔗 相关链接

### 学习路径
- [[04-Learning-Paths/Track-B-7yo/Node-11-LED编程]] - LED编程入门
- [[04-Learning-Paths/Track-C-8yo-MicroPython/Node-20-灯光秀]] - 灯光秀项目

### 相关概念
- [[02-Concepts/RGB颜色模型]] - 颜色基础知识
- [[02-Concepts/数据通信协议]] - 单线通信协议
- [[02-Concepts/电流与功率]] - 电流计算

### 竞赛应用
- [[01-White-List-Competitions/全国青少年科技创新大赛]] - 创意灯光项目

### 相关组件
- [[蜂鸣器]] - 灯光+声音效果
- [[声音传感器]] - 音乐可视化
- [[触摸传感器]] - 触摸控制灯光

---

> 💡 **小贴士**：LED灯带功耗很大，全亮白色时每个LED约60mA，1米60灯就是3.6A。必须使用外部电源供电，不能用开发板供电。另外，长距离传输时要在灯带中间加电源注入点，否则末端LED会变暗。数据线要串联330-470Ω电阻保护。
