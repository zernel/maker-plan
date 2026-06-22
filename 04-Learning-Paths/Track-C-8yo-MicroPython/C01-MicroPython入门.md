# 💻 C01 MicroPython入门

> **节点编号**: C01
> **适用Track**: Track C (8岁MicroPython进阶)
> **预计时长**: 3-4次活动，每次45分钟

---

## 📌 适用Track说明

本节点是 Track C 的起点，孩子将从图形化编程（MakeCode）过渡到文本编程（MicroPython）。这是编程能力的重要跃迁。

---

## 🔗 前置知识

- 有MakeCode图形化编程经验（建议完成 [[04-Learning-Paths/Track-B-7yo/B01-Hello-Micro-bit|Track B]])
- 会基本的电脑操作（打字、保存文件）
- 理解变量、循环、条件判断概念

---

## 🧠 核心原理简述（给家长）

**MicroPython** 是Python语言的精简版，专门为微控制器设计。它让孩子能够用真正的代码来控制硬件。

为什么从图形化过渡到文本：
- **代码可读性**: 文本代码更接近真实编程
- **灵活性**: 文本代码能实现更复杂的功能
- **职业基础**: Python是全球最流行的编程语言之一
- **调试能力**: 学会阅读错误信息，独立解决问题

MicroPython的优势：
- 语法简洁，适合初学者
- 即时反馈，代码运行快
- 丰富的库支持
- 社区活跃，资源丰富

---

## 🔬 趣味实验清单

### 实验1: 🌍 Hello World

**零件清单**:
- Micro:bit V2 一块
- USB数据线一根
- 电脑（安装Mu Editor或Thonny）

**玩法描述**:
1. 安装Mu Editor（推荐）或Thonny
2. 连接Micro:bit到电脑
3. 编写第一个程序：
```python
from microbit import *
display.scroll("Hello World!")
```
4. 点击"Flash"下载到Micro:bit
5. 观察LED显示"Hello World!"
6. 尝试修改文字，显示自己的名字

**观察与思考**:
- `from microbit import *` 是什么意思？
- `display.scroll()` 和 `display.show()` 有什么区别？
- 代码中的引号必须是英文引号吗？

---

### 实验2: 📊 变量与循环

**零件清单**:
- Micro:bit V2 一块
- USB数据线一根
- 电脑

**玩法描述**:
1. 编写计数器程序：
```python
from microbit import *

count = 0
while True:
    display.scroll(str(count))
    count = count + 1
    sleep(1000)
```
2. 下载程序，观察数字递增
3. 修改代码：
   - 让计数每次加2
   - 计数到10就清零
   - 按A按钮时计数，按B显示
4. 尝试用for循环：
```python
for i in range(10):
    display.scroll(str(i))
    sleep(500)
```

**观察与思考**:
- `while True` 和 `for` 循环有什么区别？
- 变量 `count` 是怎么变化的？
- `sleep(1000)` 的1000代表什么？

---

### 实验3: 💡 LED控制

**零件清单**:
- Micro:bit V2 一块
- USB数据线一根
- 电脑
- 外接LED（可选）
- 面包板和电阻（可选）

**玩法描述**:
1. 控制内置LED矩阵：
```python
from microbit import *

while True:
    display.set_pixel(2, 2, 9)  # 点亮中心LED
    sleep(500)
    display.set_pixel(2, 2, 0)  # 熄灭
    sleep(500)
```
2. 画一个闪烁的爱心：
```python
from microbit import *

heart = Image("09090:"
              "99999:"
              "99999:"
              "09990:"
              "00900")

while True:
    display.show(heart)
    sleep(500)
    display.clear()
    sleep(500)
```
3. 尝试控制外接LED：
```python
from microbit import *

pin0.write_digital(1)  # 点亮
sleep(1000)
pin0.write_digital(0)  # 熄灭
```

**观察与思考**:
- `set_pixel(x, y, brightness)` 的坐标怎么理解？
- 亮度值范围是多少？（0-9）
- `write_digital(1)` 和 `write_analog()` 有什么区别？

---

## 🚀 拓展挑战

### 挑战1: 按钮交互
按A显示数字，按B清空，同时按显示特殊图案。

### 挑战2: 随机数
生成随机数，显示骰子点数。

### 挑战3: 函数封装
把闪烁LED封装成函数，方便重复调用。

---

## 🔗 相关链接

- [[02-Concepts/计算思维]] - 计算思维基础
- [[02-Concepts/实体计算]] - 实体计算理念
- [[B01-Hello-Micro-bit]] - 前置参考：MakeCode入门
- [[C02-传感器读取]] - 下一个节点：传感器读取
- [[01-White-List-Competitions/]] - 白名单竞赛

---

## 🔧 常见问题排查

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| Mu Editor无法识别Micro:bit | USB驱动问题 | 安装Micro:bit USB驱动，或换USB口 |
| 程序下载后无反应 | 代码有语法错误 | 检查缩进、引号、拼写 |
| 出现"NameError" | 变量名拼写错误 | 检查变量名是否一致 |
| 出现"IndentationError" | 缩进不正确 | 使用4个空格缩进，不要用Tab |
| LED显示"None" | 函数没有返回值 | 检查函数是否有return语句 |

**调试技巧**：
1. 使用`print()`输出中间结果
2. 逐行运行代码，观察变量变化
3. 遇到错误时，先看错误信息的第一行
4. 使用REPL（交互式命令行）测试小段代码

**常见错误类型**：
- **SyntaxError**：语法错误（括号不匹配、引号不闭合）
- **NameError**：变量未定义
- **TypeError**：类型错误（如字符串和数字相加）
- **IndentationError**：缩进错误

---

## 🏆 竞赛应用

本节点技能直接应用于：
- **人工智能创新挑战赛** - Python编程赛项
- **全国青少年人工智能大赛** - MicroPython编程
- **WRC机器人设计大赛** - 机器人编程控制

---

## ✅ 完成标准

- [ ] 能独立安装和配置Mu Editor
- [ ] 理解`from microbit import *`的作用
- [ ] 能使用`display.scroll()`和`display.show()`显示内容
- [ ] 能使用变量和循环创建计数器
- [ ] 能控制内置LED和外接LED
- [ ] 完成至少2个拓展挑战

---

## 📝 家长小贴士

> 💡 **关键点**: 从图形化到文本的过渡需要时间。不要急，让孩子慢慢适应"打字编程"。初期可以先复制代码运行，再逐步理解。

> ⚠️ **常见误区**: Python对缩进敏感。告诉孩子：缩进不是为了好看，而是语法要求。缩进错误会导致程序无法运行。
