# 🐍 MicroPython 语法与日常用法参考

> 为青少年创客学习者提供的 MicroPython 语法速查手册

---

## 📖 这个模块是什么？

本模块是 MicroPython 编程语言的语法参考手册，专为使用 Micro:bit 和 ESP32 的青少年学习者设计。每个语法点都配有：
- 清晰的语法说明
- 实际可用的代码示例
- 与硬件相关的应用场景

---

## 🎯 快速导航

| 章节 | 内容 | 适用场景 |
|------|------|----------|
| [[#基础语法]] | 变量、运算、输出 | 入门必学 |
| [[#数据类型]] | 数字、字符串、列表、字典 | 数据处理 |
| [[#控制结构]] | 条件、循环、跳转 | 程序逻辑 |
| [[#函数]] | 定义、调用、参数 | 代码复用 |
| [[#类与对象]] | 面向对象编程 | 复杂项目 |
| [[#文件操作]] | 读写文件 | 数据存储 |
| [[#异常处理]] | 错误捕获与处理 | 健壮性 |
| [[#Micro:bit专属]] | Micro:bit API | Micro:bit项目 |
| [[#ESP32专属]] | ESP32 API | ESP32项目 |
| [[#常用库]] | 内置库使用 | 各种功能 |

---

## 基础语法

### 变量与赋值

```python
# 变量不需要声明类型，直接赋值
name = "小明"          # 字符串
age = 10               # 整数
height = 1.45          # 浮点数
is_student = True      # 布尔值

# 多重赋值
x, y, z = 1, 2, 3

# 交换变量
a, b = 10, 20
a, b = b, a  # 现在 a=20, b=10
```

### 运算符

```python
# 算术运算符
a = 10 + 3      # 加法: 13
b = 10 - 3      # 减法: 7
c = 10 * 3      # 乘法: 30
d = 10 / 3      # 除法: 3.333...
e = 10 // 3     # 整除: 3
f = 10 % 3      # 取余: 1
g = 10 ** 3     # 幂运算: 1000

# 比较运算符
x = 5
x == 5          # 等于: True
x != 3          # 不等于: True
x > 3           # 大于: True
x < 10          # 小于: True
x >= 5          # 大于等于: True
x <= 4          # 小于等于: False

# 逻辑运算符
True and True    # 与: True
True or False    # 或: True
not True         # 非: False
```

### 输出与输入

```python
# print() 输出
print("Hello World!")
print("年龄:", age)
print(f"我叫{name}，今年{age}岁")  # f-string格式化
print("数字:", 42, "字符串:", "hello")  # 多个参数

# input() 输入（MicroPython中可能需要特殊处理）
user_input = input("请输入你的名字: ")
```

---

## 数据类型

### 数字类型

```python
# 整数 (int)
count = 42
negative = -10
binary = 0b1010    # 二进制: 10
octal = 0o17       # 八进制: 15
hexadecimal = 0xFF # 十六进制: 255

# 浮点数 (float)
pi = 3.14159
temperature = -5.5
scientific = 1.5e-3  # 科学计数法: 0.0015

# 类型转换
int("42")       # 字符串转整数: 42
float("3.14")   # 字符串转浮点数: 3.14
str(42)         # 数字转字符串: "42"
```

### 字符串

```python
# 创建字符串
name = "MicroPython"
greeting = 'Hello'
multiline = """这是
多行
字符串"""

# 字符串操作
len(name)              # 长度: 11
name[0]                # 索引: 'M'
name[-1]               # 负索引: 'n'
name[0:5]              # 切片: 'Micro'
name.upper()           # 大写: 'MICROPYTHON'
name.lower()           # 小写: 'micropython'
name.replace('Micro', 'Micro:')  # 替换: 'Micro:Python'
name.split('o')        # 分割: ['Micr', 'Pyth', 'n']

# 字符串格式化
name = "小明"
age = 10
# 方法1: f-string（推荐）
print(f"我叫{name}，今年{age}岁")
# 方法2: format()
print("我叫{}，今年{}岁".format(name, age))
# 方法3: % 格式化
print("我叫%s，今年%d岁" % (name, age))
```

### 列表 (List)

```python
# 创建列表
fruits = ["苹果", "香蕉", "橙子"]
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", True, 3.14]

# 访问元素
fruits[0]       # 第一个: "苹果"
fruits[-1]      # 最后一个: "橙子"
fruits[1:3]     # 切片: ["香蕉", "橙子"]

# 修改元素
fruits[0] = "草莓"

# 添加元素
fruits.append("葡萄")        # 末尾添加
fruits.insert(1, "芒果")     # 指定位置添加

# 删除元素
fruits.remove("香蕉")        # 按值删除
del fruits[0]                # 按索引删除
popped = fruits.pop()        # 弹出最后一个

# 列表操作
len(fruits)                  # 长度
fruits.sort()                # 排序
fruits.reverse()             # 反转
fruits.extend(["西瓜", "桃子"])  # 扩展
"苹果" in fruits             # 包含检查: True
```

### 元组 (Tuple)

```python
# 元组是不可变的列表
point = (10, 20)
rgb = (255, 128, 0)

# 访问
x, y = point  # 解包: x=10, y=20
r, g, b = rgb
```

### 字典 (Dictionary)

```python
# 创建字典
student = {
    "name": "小明",
    "age": 10,
    "grades": [90, 85, 92]
}

# 访问元素
student["name"]           # "小明"
student.get("phone", "无")  # 不存在时返回默认值

# 修改元素
student["age"] = 11

# 添加元素
student["phone"] = "13800138000"

# 删除元素
del student["phone"]

# 字典操作
len(student)              # 键值对数量
"name" in student         # 键存在检查: True
student.keys()            # 所有键
student.values()          # 所有值
student.items()           # 所有键值对

# 遍历字典
for key, value in student.items():
    print(f"{key}: {value}")
```

### 集合 (Set)

```python
# 创建集合（无序，不重复）
colors = {"红", "绿", "蓝"}
numbers = set([1, 2, 2, 3, 3])  # {1, 2, 3}

# 集合操作
colors.add("黄")          # 添加
colors.remove("红")       # 删除
"绿" in colors            # 包含检查: True

# 集合运算
set1 = {1, 2, 3}
set2 = {2, 3, 4}
set1 & set2               # 交集: {2, 3}
set1 | set2               # 并集: {1, 2, 3, 4}
set1 - set2               # 差集: {1}
```

---

## 控制结构

### 条件语句

```python
# if 语句
temperature = 25

if temperature > 30:
    print("天气很热")
elif temperature > 20:
    print("天气舒适")
elif temperature > 10:
    print("天气凉爽")
else:
    print("天气寒冷")

# 三元表达式
status = "成年" if age >= 18 else "未成年"

# 多条件
if temperature > 20 and temperature < 30:
    print("温度适中")

if age < 6 or age > 60:
    print("免费")
```

### for 循环

```python
# 遍历列表
fruits = ["苹果", "香蕉", "橙子"]
for fruit in fruits:
    print(fruit)

# 遍历数字范围
for i in range(5):          # 0, 1, 2, 3, 4
    print(i)

for i in range(2, 10):      # 2, 3, ..., 9
    print(i)

for i in range(0, 10, 2):   # 0, 2, 4, 6, 8
    print(i)

# 遍历字典
student = {"name": "小明", "age": 10}
for key, value in student.items():
    print(f"{key}: {value}")

# 带索引遍历
for i, fruit in enumerate(fruits):
    print(f"{i}: {fruit}")
```

### while 循环

```python
# 基本while循环
count = 0
while count < 5:
    print(count)
    count += 1

# 无限循环（需要break退出）
while True:
    user_input = input("输入'quit'退出: ")
    if user_input == "quit":
        break
    print(f"你输入了: {user_input}")

# continue 跳过当前迭代
for i in range(10):
    if i % 2 == 0:  # 跳过偶数
        continue
    print(i)  # 只打印奇数
```

### 循环控制

```python
# break - 跳出循环
for i in range(100):
    if i == 10:
        break  # 当i=10时跳出循环
    print(i)

# continue - 跳过当前迭代
for i in range(10):
    if i == 5:
        continue  # 跳过i=5
    print(i)

# for...else - 循环正常结束时执行
for i in range(5):
    if i == 10:
        break
else:
    print("循环正常结束")  # 会执行，因为没有break
```

---

## 函数

### 定义与调用

```python
# 基本函数
def greet():
    print("Hello!")

greet()  # 调用函数

# 带参数的函数
def greet_name(name):
    print(f"Hello, {name}!")

greet_name("小明")

# 带返回值的函数
def add(a, b):
    return a + b

result = add(3, 5)  # result = 8

# 多返回值
def get_dimensions():
    return 1920, 1080

width, height = get_dimensions()
```

### 参数类型

```python
# 默认参数
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("小明")              # Hello, 小明!
greet("小明", "你好")       # 你好, 小明!

# 关键字参数
def create_student(name, age, grade):
    return {"name": name, "age": age, "grade": grade}

student = create_student(grade=3, name="小明", age=10)

# 可变参数 (*args)
def sum_all(*numbers):
    total = 0
    for n in numbers:
        total += n
    return total

result = sum_all(1, 2, 3, 4, 5)  # 15

# 关键字可变参数 (**kwargs)
def print_info(**info):
    for key, value in info.items():
        print(f"{key}: {value}")

print_info(name="小明", age=10, city="北京")
```

### Lambda 函数

```python
# Lambda - 匿名函数
square = lambda x: x ** 2
print(square(5))  # 25

add = lambda a, b: a + b
print(add(3, 5))  # 8

# 常用场景
numbers = [3, 1, 4, 1, 5, 9, 2, 6]
sorted_numbers = sorted(numbers, key=lambda x: -x)  # 降序排序
```

---

## 类与对象

### 基本类定义

```python
class Robot:
    # 类属性（所有对象共享）
    species = "机器人"
    
    # 构造方法
    def __init__(self, name, color):
        # 实例属性（每个对象独有）
        self.name = name
        self.color = color
        self.battery = 100
    
    # 实例方法
    def say_hello(self):
        print(f"我是{self.color}色的{self.name}！")
    
    def move(self, distance):
        if self.battery >= distance * 2:
            print(f"{self.name}移动了{distance}米")
            self.battery -= distance * 2
        else:
            print("电量不足！")
    
    # 特殊方法
    def __str__(self):
        return f"Robot({self.name}, {self.color})"

# 创建对象
robot1 = Robot("小智", "蓝")
robot2 = Robot("小勇", "红")

# 调用方法
robot1.say_hello()  # 我是蓝色的小智！
robot1.move(10)     # 小智移动了10米
print(robot1)       # Robot(小智, 蓝)
```

### 继承

```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return f"{self.name}: 汪汪！"

class Cat(Animal):
    def speak(self):
        return f"{self.name}: 喵喵！"

# 使用
dog = Dog("旺财")
cat = Cat("咪咪")
print(dog.speak())  # 旺财: 汪汪！
print(cat.speak())  # 咪咪: 喵喵！
```

### 封装

```python
class BankAccount:
    def __init__(self, balance=0):
        self.__balance = balance  # 私有属性
    
    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
            return True
        return False
    
    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount
            return True
        return False
    
    def get_balance(self):
        return self.__balance

# 使用
account = BankAccount(1000)
account.deposit(500)
print(account.get_balance())  # 1500
```

---

## 文件操作

### 读写文本文件

```python
# 写入文件
with open("data.txt", "w", encoding="utf-8") as f:
    f.write("Hello World!\n")
    f.write("这是第二行\n")

# 读取文件
with open("data.txt", "r", encoding="utf-8") as f:
    content = f.read()
    print(content)

# 逐行读取
with open("data.txt", "r", encoding="utf-8") as f:
    for line in f:
        print(line.strip())  # strip()去除换行符

# 追加内容
with open("data.txt", "a", encoding="utf-8") as f:
    f.write("追加的内容\n")
```

### CSV文件操作

```python
import csv

# 写入CSV
with open("students.csv", "w", newline="", encoding="utf-8") as f:
    writer = csv.writer(f)
    writer.writerow(["姓名", "年龄", "成绩"])
    writer.writerow(["小明", 10, 95])
    writer.writerow(["小红", 11, 88])

# 读取CSV
with open("students.csv", "r", encoding="utf-8") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)
```

### JSON文件操作

```python
import json

# 写入JSON
data = {
    "students": [
        {"name": "小明", "age": 10},
        {"name": "小红", "age": 11}
    ]
}

with open("data.json", "w", encoding="utf-8") as f:
    json.dump(data, f, ensure_ascii=False, indent=2)

# 读取JSON
with open("data.json", "r", encoding="utf-8") as f:
    loaded_data = json.load(f)
    print(loaded_data)
```

---

## 异常处理

### try...except

```python
# 基本异常处理
try:
    result = 10 / 0
except ZeroDivisionError:
    print("不能除以零！")

# 多种异常
try:
    num = int(input("输入数字: "))
    result = 100 / num
except ValueError:
    print("请输入有效数字！")
except ZeroDivisionError:
    print("不能除以零！")
except Exception as e:
    print(f"未知错误: {e}")

# try...except...else...finally
try:
    num = int(input("输入数字: "))
    result = 100 / num
except ValueError:
    print("输入错误")
except ZeroDivisionError:
    print("除零错误")
else:
    print(f"结果: {result}")  # 没有异常时执行
finally:
    print("程序结束")  # 总是执行
```

### 自定义异常

```python
class AgeError(Exception):
    def __init__(self, age, message="年龄必须在0-150之间"):
        self.age = age
        self.message = message
        super().__init__(self.message)

def set_age(age):
    if age < 0 or age > 150:
        raise AgeError(age)
    return age

try:
    set_age(200)
except AgeError as e:
    print(f"错误: {e.message}，你输入的年龄是{e.age}")
```

---

## Micro:bit 专属 API

### 显示控制

```python
from microbit import *

# 显示LED图案
display.show(Image.HAPPY)  # 内置图案
display.show(Image("09090:"  # 自定义图案
                   "99999:"
                   "99999:"
                   "09990:"
                   "00900"))

# 显示文字
display.scroll("Hello!")  # 滚动显示
display.show("Hi")        # 静态显示

# 控制单个LED
display.set_pixel(2, 2, 9)  # 点亮(2,2)位置，亮度9
display.set_pixel(2, 2, 0)  # 熄灭

# 清除显示
display.clear()

# 显示数字
display.show(42)
```

### 按钮控制

```python
from microbit import *

# 检测按钮状态
if button_a.is_pressed():
    print("A按钮被按下")

if button_b.was_pressed():
    print("B按钮被按下过")

# 计数
count = 0
while True:
    if button_a.was_pressed():
        count += 1
        display.show(str(count))
    if button_b.was_pressed():
        count = 0
        display.clear()
    sleep(100)
```

### 传感器读取

```python
from microbit import *

# 温度传感器
temp = temperature()
print(f"温度: {temp}°C")

# 光线传感器
light = display.read_light_level()
print(f"光线: {light}")

# 加速度计
x, y, z = accelerometer.get_values()
print(f"X:{x}, Y:{y}, Z:{z}")

# 磁力计
compass.calibrate()  # 首次使用需要校准
heading = compass.heading()
print(f"方向: {heading}°")

# 手势检测
gesture = accelerometer.current_gesture()
if gesture == "shake":
    display.show("摇晃了！")
```

### 引脚控制

```python
from microbit import *

# 数字输出
pin0.write_digital(1)  # 高电平
pin0.write_digital(0)  # 低电平

# 数字输入
value = pin1.read_digital()

# 模拟输出 (PWM)
pin2.write_analog(512)  # 0-1023

# 模拟输入
analog_value = pin3.read_analog()

# 触摸引脚
if pin4.is_touched():
    print("引脚4被触摸")
```

### 音乐播放

```python
from microbit import *
import music

# 播放音符
music.play(music.NAIVETE)  # 内置旋律

# 自定义旋律
melody = ["C4:4", "D4:4", "E4:4", "C4:4"]
music.play(melody)

# 音符格式: "音符:时值"
# C4 = 中央C, :4 = 四分音符
# R = 休止符
```

### 无线电通信

```python
from microbit import *
import radio

# 开启无线电
radio.on()

# 发送消息
radio.send("Hello!")

# 接收消息
message = radio.receive()
if message:
    print(f"收到: {message}")

# 设置频道
radio.config(channel=7)

# 发送数字
radio.send("42")
```

---

## ESP32 专属 API

### WiFi 连接

```python
import network
import time

# 连接WiFi
wlan = network.WLAN(network.STA_IF)
wlan.active(True)
wlan.connect("WiFi名称", "WiFi密码")

# 等待连接
while not wlan.isconnected():
    time.sleep(1)
    print("连接中...")

print("已连接!")
print("IP地址:", wlan.ifconfig()[0])

# 创建热点
ap = network.WLAN(network.AP_IF)
ap.config(essid="MyESP32", password="12345678")
ap.active(True)
```

### HTTP 请求

```python
import urequests

# GET请求
response = urequests.get("https://api.example.com/data")
print(response.text)
print(response.json())

# POST请求
data = {"name": "小明", "age": 10}
response = urequests.post("https://api.example.com/submit", json=data)
print(response.status_code)
```

### Web 服务器

```python
import socket
import machine

# 创建Web服务器
def create_web_page():
    return """<!DOCTYPE html>
<html>
<head><title>ESP32控制</title></head>
<body>
    <h1>ESP32 Web控制</h1>
    <button onclick="location.href='/on'">开灯</button>
    <button onclick="location.href='/off'">关灯</button>
</body>
</html>"""

# 创建socket服务器
addr = socket.getaddrinfo('0.0.0.0', 80)[0][-1]
s = socket.socket()
s.bind(addr)
s.listen(1)

print("服务器已启动，访问:", wlan.ifconfig()[0])

while True:
    cl, addr = s.accept()
    request = cl.recv(1024)
    request = str(request)
    
    if '/on' in request:
        machine.Pin(2).value(1)
    elif '/off' in request:
        machine.Pin(2).value(0)
    
    response = create_web_page()
    cl.send('HTTP/1.1 200 OK\r\n')
    cl.send('Content-Type: text/html\r\n')
    cl.send('Connection: close\r\n\r\n')
    cl.sendall(response)
    cl.close()
```

### 定时器

```python
import machine
import time

# 创建定时器
timer = machine.Timer(0)

# 定时器回调函数
def timer_callback(timer):
    print("定时器触发！")
    machine.Pin(2).value(not machine.Pin(2).value())

# 每1000ms触发一次
timer.init(period=1000, mode=machine.Timer.PERIODIC, callback=timer_callback)

# 停止定时器
timer.deinit()
```

### PWM 控制

```python
from machine import Pin, PWM

# 创建PWM对象
pwm = PWM(Pin(2))
pwm.freq(1000)  # 频率1000Hz

# 设置占空比 (0-1023)
pwm.duty(512)   # 50%占空比
pwm.duty(0)     # 0% (关闭)
pwm.duty(1023)  # 100% (全开)

# 用于LED调光
for duty in range(0, 1024, 10):
    pwm.duty(duty)
    time.sleep_ms(10)

# 用于舵机控制
servo = PWM(Pin(15), freq=50)
servo.duty(40)   # 0度
servo.duty(77)   # 90度
servo.duty(115)  # 180度
```

---

## 常用库

### time 库

```python
import time

# 延时
time.sleep(1)        # 延时1秒
time.sleep_ms(500)   # 延时500毫秒
time.sleep_us(100)   # 延时100微秒

# 获取时间
seconds = time.time()           # Unix时间戳
time_tuple = time.localtime()   # 本地时间元组
formatted = time.strftime("%Y-%m-%d %H:%M:%S", time_tuple)
```

### random 库

```python
import random

# 随机整数
num = random.randint(1, 10)  # 1到10的随机整数

# 随机浮点数
num = random.random()        # 0到1的随机浮点数
num = random.uniform(1, 10)  # 1到10的随机浮点数

# 随机选择
fruits = ["苹果", "香蕉", "橙子"]
fruit = random.choice(fruits)

# 打乱列表
random.shuffle(fruits)

# 设置随机种子（可重复的随机序列）
random.seed(42)
```

### math 库

```python
import math

# 基本数学函数
math.ceil(3.2)     # 向上取整: 4
math.floor(3.8)    # 向下取整: 3
math.sqrt(16)      # 平方根: 4.0
math.pow(2, 3)     # 幂运算: 8.0
math.log(100, 10)  # 对数: 2.0

# 三角函数
math.sin(math.pi / 2)  # 正弦: 1.0
math.cos(0)            # 余弦: 1.0
math.tan(math.pi / 4)  # 正切: 1.0

# 常量
math.pi    # 3.141592653589793
math.e     # 2.718281828459045
```

### json 库

```python
import json

# 序列化（Python对象 -> JSON字符串）
data = {"name": "小明", "age": 10, "scores": [90, 85, 92]}
json_str = json.dumps(data, ensure_ascii=False)
print(json_str)

# 反序列化（JSON字符串 -> Python对象）
loaded = json.loads(json_str)
print(loaded["name"])

# 文件操作
with open("data.json", "w") as f:
    json.dump(data, f, ensure_ascii=False, indent=2)

with open("data.json", "r") as f:
    loaded = json.load(f)
```

---

## 常用代码片段

### LED 呼吸灯效果

```python
from microbit import *

while True:
    # 逐渐变亮
    for brightness in range(0, 10):
        display.set_pixel(2, 2, brightness)
        sleep(50)
    
    # 逐渐变暗
    for brightness in range(9, -1, -1):
        display.set_pixel(2, 2, brightness)
        sleep(50)
```

### 计时器

```python
from microbit import *

start_time = running_time()

# 做一些操作...

elapsed = running_time() - start_time
print(f"耗时: {elapsed}ms")
```

### 温度报警器

```python
from microbit import *
import music

THRESHOLD = 30

while True:
    temp = temperature()
    display.scroll(str(temp) + "C")
    
    if temp > THRESHOLD:
        music.pitch(1000, 500)  # 蜂鸣报警
        display.show(Image.ANGRY)
    else:
        display.show(Image.HAPPY)
    
    sleep(1000)
```

### 超声波测距

```python
from microbit import *
import machine
import time

# 假设超声波传感器连接到P0和P1
trig = machine.Pin(0, machine.Pin.OUT)
echo = machine.Pin(1, machine.Pin.IN)

def get_distance():
    trig.value(0)
    time.sleep_us(2)
    trig.value(1)
    time.sleep_us(10)
    trig.value(0)
    
    while echo.value() == 0:
        start = time.ticks_us()
    
    while echo.value() == 1:
        end = time.ticks_us()
    
    duration = time.ticks_diff(end, start)
    distance = (duration * 0.0343) / 2
    return distance

while True:
    dist = get_distance()
    print(f"距离: {dist:.1f}cm")
    sleep(500)
```

---

## 📚 延伸阅读

- [MicroPython 官方文档](https://docs.micropython.org/)
- [Micro:bit MicroPython 文档](https://microbit-micropython.readthedocs.io/)
- [ESP32 MicroPython 文档](https://docs.espressif.com/projects/esp-idf/)

---

## 🔗 相关链接

- [[02-Concepts/计算思维]] - 计算思维基础
- [[04-Learning-Paths/Track-C-8yo-MicroPython/C01-MicroPython入门]] - MicroPython入门课程
- [[04-Learning-Paths/Track-D-10yo-Advanced/D01-Python进阶语法]] - Python进阶语法
- [[03-Hardware-Sensors/]] - 传感器参考

---

*最后更新：2026年6月22日*
