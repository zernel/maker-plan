# 📱 OLED显示屏 (SSD1306)

## 🎯 一句话定义
OLED显示屏就像机器人的小电视，能显示文字和图案，让机器人有了"脸"。

## 🧒 给孩子的解释
你想让机器人显示表情吗？OLED显示屏就是机器人的"脸"！它小小的，但是能显示很多东西。可以显示文字、数字、图案，甚至简单的动画。就像你手表上的屏幕一样，但是更酷！你可以让机器人显示笑脸、哭脸，或者显示温度、湿度等信息。

## 🔬 工作原理

### OLED技术
```
OLED = Organic Light-Emitting Diode（有机发光二极管）

特点：
  自发光：不需要背光
  高对比度：黑色更黑
  广视角：各个方向都能看清
  低功耗：显示黑色时不耗电
  响应快：动画流畅
```

### SSD1306 驱动芯片
```
┌─────────────────────────────┐
│        OLED面板              │
│   ┌───────────────────┐    │
│   │  128×64 像素       │    │
│   │  ┌──┬──┬──┬──┐    │    │
│   │  │  │  │  │  │    │    │
│   │  ├──┼──┼──┼──┤    │    │
│   │  │  │  │  │  │    │    │
│   │  └──┴──┴──┴──┘    │    │
│   └───────────────────┘    │
│   ┌───────────────────┐    │
│   │    SSD1306芯片     │    │
│   └───────────────────┘    │
└─────────────────────────────┘
```

### 通信接口
```
I2C接口（最常用）：
  SCL：时钟线
  SDA：数据线
  地址：0x3C 或 0x3D

SPI接口（速度更快）：
  SCLK：时钟
  MOSI：数据
  CS：片选
  DC：数据/命令
  RES：复位
```

## 📊 技术参数

| 参数 | 数值 | 说明 |
|------|------|------|
| 分辨率 | 128×64 像素 | 常见尺寸 |
| 颜色 | 单色（白/蓝/黄） | 可选 |
| 工作电压 | 3.3V-5V | 兼容多种开发板 |
| 通信接口 | I2C/SPI | I2C最常用 |
| I2C地址 | 0x3C/0x3D | 可配置 |
| 工作电流 | 约20mA | 低功耗 |
| 响应时间 | <10μs | 快速 |
| 工作温度 | -40°C到85°C | 宽温度范围 |
| 尺寸 | 0.96英寸 | 常见尺寸 |

### 引脚说明（I2C）
```
VCC  ──── 3.3V或5V电源
GND  ──── 电源负极
SCL  ──── I2C时钟线
SDA  ──── I2C数据线
```

### 显示内容
```
文字：ASCII字符、中文（需要字库）
数字：整数、小数
图案：位图、图标
动画：帧动画
```

## 🎮 项目创意

### 入门项目
- **文字显示**：显示"Hello World"
- **数字显示**：显示计数器

### 进阶项目
- **表情显示**：显示笑脸、哭脸
- **数据监控**：显示温湿度数据
- **游戏机**：简单像素游戏

### 创意项目
- **机器人表情**：各种表情动画
- **天气显示**：显示天气信息
- **音乐播放器**：显示歌曲信息
- **电子宠物**：养一个像素宠物

## 🔌 兼容性

| 开发板 | 支持 | 说明 |
|--------|------|------|
| Micro:bit | ✅ | 使用P19/P20 |
| Arduino | ✅ | 使用Adafruit库 |
| ESP32 | ✅ | 支持 |
| Raspberry Pi | ✅ | 使用I2C |

### Arduino 接线示例
```
SSD1306        Arduino
VCC        ──>  3.3V
GND        ──>  GND
SCL        ──>  A5
SDA        ──>  A4
```

### Arduino 代码示例
```cpp
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64

Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, -1);

void setup() {
  display.begin(SSD1306_SWITCHCAPVCC, 0x3C);
  display.clearDisplay();
  
  // 显示文字
  display.setTextSize(1);
  display.setTextColor(WHITE);
  display.setCursor(0, 0);
  display.println("Hello, World!");
  display.display();
}

void loop() {
  // 更新显示
}
```

### Micro:bit 接线示例
```
SSD1306        Micro:bit
VCC        ──>  3V
GND        ──>  GND
SCL        ──>  P19
SDA        ──>  P20
```

### MicroPython 代码示例
```python
from microbit import *
import ssd1306

i2c.init(freq=400000, sda=pin20, scl=pin19)
oled = ssd1306.SSD1306_I2C(128, 64, i2c)

# 显示文字
oled.text("Hello, World!", 0, 0)
oled.show()
sleep(2000)

# 显示数字
oled.fill(0)
oled.text("Count: 42", 0, 0)
oled.show()
```

## 💰 价格参考

| 尺寸 | 价格范围 | 说明 |
|------|----------|------|
| 0.96寸 | ¥8-15 | 最常用 |
| 1.3寸 | ¥12-20 | 稍大 |
| 0.91寸 | ¥6-12 | 小巧 |
| 带外壳 | ¥15-25 | 即插即用 |

## 🔗 相关链接

### 学习路径
- [[04-Learning-Paths/Track-B-7yo/Node-12-显示与输出]] - 显示与输出课程
- [[04-Learning-Paths/Track-C-8yo-MicroPython/Node-21-机器人表情]] - 机器人表情项目

### 竞赛应用
- [[01-White-List-Competitions/全国青少年科技创新大赛]] - 创意显示项目

### 相关组件
- [[温湿度传感器]] - 显示温湿度数据
- [[陀螺仪传感器]] - 显示姿态数据
- [[蜂鸣器]] - 显示+声音效果

---

> 💡 **小贴士**：OLED显示屏的I2C地址可能是0x3C或0x3D，如果通信失败可以试试另一个地址。另外，显示中文需要加载中文字库，会占用较多内存。频繁刷新显示会增加功耗，不需要时可以关闭显示。
