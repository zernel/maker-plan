# 🐍 D01 Python进阶语法

> **节点编号**: D01
> **适用Track**: Track D (10-12岁竞赛冲刺)
> **预计时长**: 4-5次活动，每次60分钟

---

## 📌 适用Track说明

本节点是 Track D 的起点，孩子将从 MicroPython 基础过渡到 Python 进阶语法。这是参加 AI 类竞赛的必备基础。

---

## 🔗 前置知识

- 完成 [[04-Learning-Paths/Track-C-8yo-MicroPython/C01-MicroPython入门|Track C MicroPython入门]]
- 熟练掌握变量、循环、条件判断、函数
- 有基本的文件操作经验

---

## 🧠 核心原理简述（给家长）

**面向对象编程 (OOP)** 是现代编程的核心范式。它让孩子学会用"对象"的方式思考问题：

- **类 (Class)**：对象的模板，定义属性和方法
- **对象 (Object)**：类的实例，拥有具体的属性值
- **继承 (Inheritance)**：代码复用的重要机制
- **封装 (Encapsulation)**：隐藏内部细节，只暴露必要接口

为什么学 OOP：
- **代码组织**：复杂项目的代码管理
- **竞赛必备**：AI竞赛项目通常需要OOP设计
- **职业基础**：工业界主流编程范式

---

## 🔬 趣味实验清单

### 实验1: 🤖 创建你的第一个类

**零件清单**:
- 电脑（安装 Python 3.8+ 或 Mu Editor）
- Micro:bit V2（可选，用于硬件实验）

**玩法描述**:
1. 创建一个"机器人"类：
```python
class Robot:
    def __init__(self, name, color):
        self.name = name
        self.color = color
        self.battery = 100
    
    def say_hello(self):
        print(f"我是{self.name}，{self.color}色的机器人！")
    
    def move(self, distance):
        if self.battery > 0:
            print(f"{self.name}移动了{distance}米")
            self.battery -= distance * 2
        else:
            print("电量不足，请充电！")
    
    def charge(self):
        self.battery = 100
        print(f"{self.name}已充满电！")

# 创建对象
my_robot = Robot("小智", "蓝")
my_robot.say_hello()
my_robot.move(10)
print(f"剩余电量：{my_robot.battery}%")
```

2. 修改代码，添加新功能：
   - 添加 `dance()` 方法
   - 添加 `battery_level` 属性显示
   - 创建多个机器人对象

**观察与思考**:
- `__init__` 方法什么时候被调用？
- `self` 代表什么？
- 类和对象有什么区别？

---

### 实验2: 📦 文件操作与数据持久化

**零件清单**:
- 电脑
- Micro:bit V2（可选）

**玩法描述**:
1. 创建一个成绩管理系统：
```python
class Student:
    def __init__(self, name):
        self.name = name
        self.scores = {}
    
    def add_score(self, subject, score):
        self.scores[subject] = score
    
    def get_average(self):
        if not self.scores:
            return 0
        return sum(self.scores.values()) / len(self.scores)
    
    def save_to_file(self, filename):
        with open(filename, 'w', encoding='utf-8') as f:
            f.write(f"学生姓名：{self.name}\n")
            for subject, score in self.scores.items():
                f.write(f"{subject}：{score}\n")
            f.write(f"平均分：{self.get_average():.1f}\n")
        print(f"成绩已保存到 {filename}")

# 使用
student = Student("小明")
student.add_score("数学", 95)
student.add_score("语文", 88)
student.add_score("英语", 92)
student.save_to_file("成绩.txt")
```

2. 扩展功能：
   - 添加 `load_from_file()` 方法读取文件
   - 添加异常处理（文件不存在怎么办）
   - 支持多个学生数据

**观察与思考**:
- `with open()` 和 `open()` 有什么区别？
- `encoding='utf-8'` 为什么重要？
- 文件操作出错时程序会怎样？

---

### 实验3: 🎮 异常处理与健壮性

**零件清单**:
- 电脑

**玩法描述**:
1. 创建一个安全的计算器：
```python
class Calculator:
    def divide(self, a, b):
        try:
            result = a / b
            return result
        except ZeroDivisionError:
            print("错误：除数不能为零！")
            return None
        except TypeError:
            print("错误：请输入数字！")
            return None
    
    def safe_input(self, prompt):
        while True:
            try:
                return float(input(prompt))
            except ValueError:
                print("请输入有效的数字！")

# 使用
calc = Calculator()
num1 = calc.safe_input("请输入第一个数：")
num2 = calc.safe_input("请输入第二个数：")
result = calc.divide(num1, num2)
if result is not None:
    print(f"结果：{result}")
```

2. 扩展功能：
   - 添加更多运算（开方、幂运算）
   - 添加输入历史记录
   - 添加错误日志文件

**观察与思考**:
- `try...except` 的执行流程是怎样的？
- 为什么要捕获特定异常而不是所有异常？
- 异常处理如何提高程序的健壮性？

---

## 🚀 拓展挑战

### 挑战1: 继承与多态
创建 `SmartRobot` 继承 `Robot`，添加语音识别功能。

### 挑战2: 文件加密器
用类实现一个简单的文件加密/解密工具。

### 挑战3: 学生成绩管理系统
支持增删改查、文件存储、统计分析的完整系统。

---

## 🔗 相关链接

- [[02-Concepts/计算思维]] - 计算思维进阶
- [[04-Learning-Paths/Track-C-8yo-MicroPython/C01-MicroPython入门]] - MicroPython基础
- [[D02-数据结构基础]] - 下一个节点：数据结构
- [[01-White-List-Competitions/08-Youth-AI-Competition|全国青少年人工智能大赛]] - AI竞赛应用
- [[01-White-List-Competitions/01-AI-Innovation-Challenge|人工智能创新挑战赛]] - 创新项目应用

---

## 📝 家长小贴士

> 💡 **关键点**: 面向对象编程是现代编程的核心。不要急于求成，让孩子通过创建"有趣的对象"（如机器人、游戏角色）来理解类的概念。

> ⚠️ **常见误区**: Python的缩进不是装饰，而是语法。告诉孩子：缩进错误会导致程序无法运行，就像写文章必须分段一样。

---

## ✅ 完成标准

- [ ] 能独立创建类，定义属性和方法
- [ ] 理解 `__init__` 和 `self` 的作用
- [ ] 能使用 `try...except` 处理异常
- [ ] 能进行基本的文件读写操作
- [ ] 完成至少2个拓展挑战

---

## 🏆 竞赛应用

本节点技能直接应用于：
- **人工智能创新挑战赛** - AI项目通常需要OOP设计
- **全国青少年人工智能大赛** - Python编程是核心考核点
- **NOI信息学奥赛** - 数据结构和算法需要扎实的编程基础
