---
layout: post
title:  代码大全笔记03~05
categories: coding
---
## 第3章 三思而后行：前期准备

不同规模的构建，需要不同程度的准备工作，项目的成败，早已埋下伏笔。构建一般占项目时间的65%，而糟糕的准备工作会让构建时间增加两三倍。

### 3.1 前期准备的重要性

高质量的软件来自高质量的实践，如何保证质量？

- 前期：关注需求、设计。
- 中期：关注构建。
- 后期：关注测试。

本书重点关注中期，但是在开始构建之前，需要弄清前期准备做到了什么程度，贸然开场容易悲剧。

#### 现代软件开发是否需要前期准备？

需要。前期准备可以降低风险，不同的项目可能需要不同的前期准备实践，但不能没有。

#### 不完整的前期准备的理由

- 开发者没有经验——那就去学啊。
- 按捺不住写代码的心——多碰几次壁。
- 上级让你赶紧写代码！——拒绝上级；假装在编程；教育上级；跳槽。

#### 构建之前做好前期准备的理由

你可以拿它来教育别人。

##### 诉诸逻辑

- 需要弄清楚到底想构建个啥。
- 需要弄清楚怎么去构建系统。

##### 诉诸类比

- 造房子
- 软件开发食物链：程序员在食物链尽头。

##### 诉诸数据

- 最后阶段更改的代价是10~100倍。

##### 老板敏捷测试

自我实现预言：

- 我们必须立即开始编码因为还有很多调试工作要做。
- 我们没有计划多少时间去测试因为不会找到太多的缺陷。
- 我们充分研究了需求和设计，在编码和调试的时候不会遇到大的问题。

### 3.2 确定你开发的软件类型

针对不同的软件类型，需要不同的生命周期模型:

- 商业系统
- 关键任务系统
- 嵌入式性命攸关系统

#### 迭代方法在前期准备中的作用

- 先做80%的需求分析，则类似串行
- 先做20%的需求分析，则类似迭代

#### 在迭代方法与串行方法间的选择

- 需求是否明确？
- 设计是否复杂？
- 团队对领域是否熟悉？
- 项目风险大不大？
- 更改需求、设计的代价如何？

### 3.3 问题定义

- 好的问题定义弄清楚问题是什么，而不要考虑实现。
- 问题定义在需求分析之前，使用用户语言描述。
- 最好的解决方案可能不需要写软件。
- 除非是为了解决计算机系统问题，否则不使用计算机语言。
- 问题定义出错的代价：浪费了时间，没有解决真正的问题。

### 3.4 需求分析

需求分析讨论软件怎么解决问题，是解决方案的第一步。

#### 为什么需要正式的需求？

- 确保用户而非程序员决定系统功能，程序员明确知道用户需要什么。
- 避免争吵，以需求为准。
- 好的需求会减少开始构建后的变更。

#### 稳定需求的神话

稳定的需求是软件开发的圣杯。

- 用户往往不能准备描述需求。
- 只有充分使用系统，才能深入理解系统。
- 开发过程会使用户更好的理解系统，这也是需求变更的主要来源。
- 典型的系统会有25%的需求变更，花费70%~85时间重做。

#### 在构建时应对需求变化

- 检查需求分析的质量，如有问题，尽早返工。
- 确保每个人明白需求变更的代价，正确应对“特性中毒者”。
- 建立变更控制过程，做到程序员顾客都满意。
- 使用能适应需求变更的开发方法：原型进化、渐进交付、小开发周期。
- 放弃项目。
- 始终关注项目的商业价值。

### 3.5 架构设计

架构设计，一般对应“概要设计文档”，架构决定了系统的“概念完整”。架构设计进行工作分解，直至程序员可以上手工作。

#### 典型的架构要素

##### 程序组织结构

- 系统鸟瞰。
- 考虑了备选方案，综合考虑使用目前的方案。
- 设计主要模块，追溯相应的需求。
- 模块职责分明，对其它模块依赖越少越好。
- 模块间的通信方式有良好定义，明确调用关系。

##### 主要的类

- 描述主要的类，职责以及和其他类的关系，继承体系、状态转换图、对象持久化方法，如何组织成子系统。
- 考虑备选方案，以及使用本方案的理由，不必要描述所有的类。

##### 数据设计

- 文件、表格设计，数据结构选择的理由。
- 数据通常只由一个类或子系统获取。
- 数据库使用的高层组织和内容，选择数据库还是平面文件，单数据库还是多数据库。

##### 用户接口设计

- 需求阶段设计亦可。
- 用户界面可替代原则。
- 命令行用户接口在测试中很有用。

##### 资源管理

- 关键资源如：数据库连接、进程、句柄。
- 内存管理：一般情况和极端情况。
- 由开发环境管理还是自行管理。

##### 安全

- 设计级别的安全与代码级别的安全。
- 建立威胁模型。
- 编程规范要考虑缓存、输入数据过滤、加密、错误信息的详细程度、内存关键数据的保护等。

##### 性能

- 如果关心性能，则需求中要明确。权衡速度、内存、花销。
- 架构要说明为何能达到性能目标，阐明风险，说明是否需要特殊的算法，权衡时间和空间。

##### 扩展性

架构如何应对用户数、服务数、网络节点数、数据库记录的增加。

##### 互操作性

如何为其他软硬件提供数据或资源。

##### 国际化/本地化

i18n问题，如何存储使用字符串。

##### 输入输出

- 描述前向、后向、即时的输入输出。
- 在什么层面检测错误：字段、记录、数据流、文件。

##### 错误处理

90%的代码在处理异常情况。

- 检错还是纠错，忽略还是终止，是否通知用户。
- 主动检测还是被动检测。
- 错误如何传播？策略要一致，不使用户费解。
- 异常如何处理, 捕捉、记录、存档。
- 在什么层面处理错误。
- 每个类输入数据如何验证，分散还是集中，输入是否干净。
- 使用开发环境的错误处理系统还是自定义错误系统。

##### 容错

- 重试与回退。
- 用备用方法。
- 用选举法。
- 用假值替代。

总体策略：退化、转入特定状态、关闭或重启。

##### 可行性

如可能有不可行处，要充分说明，考虑原型概念验证或研究。

##### 过度设计

通过过度设计提高鲁棒性，应对缺陷的乘法原理。

##### 买或是开发

弄清为什么要自己开发。

##### 重用决策

重用是如何满足需求的。

##### 变更策略

- 可能的变更已纳入考虑，最可能的变更易于实现，单一变更影响的类较少。
- 一些方法：版本号、保留字段、设计文件、代码生成器。
- 延迟决策：使用表驱动代替硬编码的条件判断、使用配置文件。

#### 架构质量

- 好的架构指出类之后的隐含信息，包含或不包含某些设计的理由。
- 好的架构是自然的，一个优美的概念结合一些自组织的附属概念。
- 架构更改时应当与整体概念保持一致。
- 架构应当阐明目标，比如功能相同的软件性能要求可能不同。
- 架构应当阐明主要决策的理由。
- 好的架构应当尽量独立于机器及语言。
- 架构应当阐明风险及解决方法。
- 架构应当包含多种视角。
- 你应当能理解架构的全部内容。

### 3.6 前期准备需要的时间

取决于软件类型：

- 需求不确定的正式项目：可能需要时间和分析师一起把需求理清。
- 需求不确定的非正式项目：自己理清需求，直到需求的易变部分对构建的影响最小。

只要需求不明确，需求本身就要作为一个项目来做，只有明确了需求，才能估计开发的时间。

## 第4章 关键构建决策

### 4.1 选择编程语言

语言选择事关效率，语言熟悉——效率高30%，熟练工——3倍效率。一定程度上，思想表达能力取决于词汇量。
表达能力：C,1;C++,2.5;Python,6.
不要使用了一门新的语言，确不使用它好的机制，还是完全用旧语言的模式编程。
语言描述：

- Ada 数据抽象，信息隐藏，用于军队、航空航天。
- 汇编 处理器相关，代码体积或速度有严格限制时应用。
- C 普适，中等语言，可移植的汇编（指针、地址、位运算、弱类型），高级特性：结构体，控制流，机器独立，丰富的运算符。
- C++ C基础上的面向对象语言，类、多态、异常处理、模板、类型控制、标准库
- C# 类似C、C++、Java（个人认为C#语言本身是很优秀的，融合了部分函数式编程的思想，但是社区支持比Java略差）
- Cobol 通用商业语言（银行还在用）。
- Fortran 最早的高级语言之一，过去科学计算和教学比较多使用（先做Python用得更多吧）。
- Java （最早的虚拟机语言？，社区庞大。）
- JavaScript （无处不在了）
- Perl 擅长字符处理（跟Python不同的哲学）
- PHP （世界上最好的语言）
- Python （万能胶水）
- SQL 结构化查询语言，主要用于数据库。
- Visual Basic （拉控件编程的经典）

### 4.2 编程约定

高层的架构与底层实现要保持一致，统一的规范不单利于团队合作，还可以解放脑力。

### 4.3 你在技术浪潮中的位置

处在一个技术的早期，风险与额外的收益并存，技术成熟期则风险小，中规中矩。
注意Program in a language 和  Program **into** a language的区别，语言提供了工具箱，但是不要局限于语言的工具箱。

### 4.4 选择你主要的构建实践

检查表 主要构建实践

#### 编码

- 你是否想好多少设计留到写代码时在键盘前完成？
- 是否定义了编程规范，如命名、注释、布局？
- 是否定义了体系架构暗示的编程实践，如错误如何处理？安全问题如何处理？类接口如何约定？复用代码的标准？考虑多少性能问题？
- 你是否找准在技术浪潮中位置，适应调整了自己的方法？如有必要，你是否考虑了Program **into** a language？

#### 团队合作

- 是否规定了集成的规范，即是否规定了程序员在代码签入主分支前的特定步骤？
- 结对编程？

#### 质量保存

- 是否写代码前先写测试用例？
- 是否写单元测试？
- 签入代码前在调试器中逐步执行？
- 签入代码前集成测试？
- 相互复审或检查？

#### 工具

- 版本控制工具？
- 语言、语言版本、编译器版本
- 框架选择，如J2EE，.Net
- 是否允许使用非标准的语言特性
- 编辑器、反编译器、调试器、测试框架、语法检查器等。

## 第五章 构建中的设计

设计不太可能在构建之前完成。

### 5.1 设计挑战

- 设计是一个邪恶的(wicked)问题：只能通过解决这个问题或部分解决问题才能清楚的定义这个问题。
  真正的程序和学生作业的区别。
- 设计是一个草率的过程
  会犯错；好的方案很精妙；“足够好”很难定义。
- 设计关乎权衡和优先级
- 设计牵涉约束
- 设计是非决定性的
- 设计是一个启发式的过程：没有银弹
- 设计是自然发生的

### 5.2 关键设计概念

#### 软件的首要技术法则：管理复杂性

##### 偶然的和本质的困难

此划分来自亚里士多德的哲学。
偶然的：笨拙的语法、非交互式的计算机、难以一起工作的工具；
本质的：与真实世界复杂、无序的接口，异常情况，精确性，准确定义真实世界如何运行。

##### 管理复杂性的重要性

失败的原因：糟糕的需求/计划/管理，失控的复杂性管理。
程序太大，人类无法一次性理解。问题分级后易于理解（如包管理），保持从程序短小，写代码时考虑人类的极限。

##### 如何消灭复杂性

- 减少每个人脑中需要一次性处理的固有复杂性。
- 防止不必要复杂性的增殖。

#### 描述设计的特征

- 最小复杂度：聪明的 vs 简单易维护的。
- 易维护：为代码维护者编程，自解释的设计。
- 松耦合：不同部分之间的联系尽量少。
- 可扩展性：更改时减少创伤。
- 可复用性
- 高扇入：充分复用底层模块
- 中低扇出：不过度依赖其他部分
- 可移植性
- 精简：没有多余部分
- 分层化：隔离变化
- 标准技术

#### 设计的层次

##### 第1层：软件系统

##### 第2层：划分子系统或包

子系统间的通信必须加以限制，否则会不断熵增，一篇混乱，可以先紧后松。常见的子系统：

- 商业规则
- 用户接口
- 数据存取
- 系统依赖

##### 第3层：划分类

包括接口。大项目由子系统划分，定义一些外部函数；小项目由系统直接划分。

##### 第4层：划分例程

可能会引起第3层的修改。

##### 第5层：例程内设计

### 5.3 设计建造的砖块：启发式

一个不断试错的过程。

#### 找到现实世界的对象

- 标识对象和其属性
- 决定改对象能干啥
- 决定每个对象能对其他对象干啥
- 决定对象各部分的可见性
- 决定对象的公开接口

一个迭代过程：重新组织，类的细节修改。

#### 组织一致的抽象

在不同的层次忽略细节。集合=>抽象。基类、接口。

- 函数层次
- 类层次
- 包或子系统层次

#### 封装实现细节

#### 继承——当继承简化设计时使用

#### 信息隐藏

- 结构化设计：黑盒
- 面向对象设计：封装、模块化、抽象

##### 秘密和隐私权

##### 两种策略

- 隐藏复杂性使你的大脑不需要考虑它，除非特别关注时
- 隐藏更改源，隔离变化

##### 信息隐藏的障碍

- 分布过广的信息
- 环形依赖
- 不当的全局数据
- 担心性能损失

##### 信息隐藏的价值

启发性的力量，设计好的公共接口。问正确的问题：这个类需要隐藏什么？

#### 标示易变区域

标示=>分割=>隔离

- 商业规则
- 硬件依赖
- 输入输出
- 非标准语言特性
- 设计和构建困难的区域
- 状态变量：使用枚举代替bool值；使用存取函数代替直接访问。
- 数据大小限制

##### 预期不同程度的变化

先找出最小子集，再做功能性、质量性改进。

#### 保持松耦合

##### 耦合标准

- 大小：模块间联系的数量，如函数的参数个数，类的公开方法数量；
- 可见性：明确引用，胜过更改全局变量。
- 可变性：容易改变连接，被不同的模块调用。

##### 耦合的种类

- 简单数据参数耦合：模块间传递了简单数据类型。常见、可接受。
- 简单对象耦合： 一个对象初始化了另一个对象。合理。
- 对象参数耦合：对象1需要对象2向其传递对象3。耦合较紧密。
- 语义耦合
  - 模块1传递了一个标志给模块2，告诉模块2应该去干啥。如果模块2定义了一个数据类型来表示该标志，则合理。
  - 模块2使用模块1更改过的全局变量。有时序假设，不好。
  - 模块1在调用某函数前必须先调用初始化函数。
  - 模块1传递对象给模块2，知道模块2将使用对象的部分方法，只对对象进行部分初始化。
  - 模块1传递基类给模块2，模块2知道模块1实际传递的是派生类，强制转化后使用。

危险:使用了编译器无法检测的方法使用别的类。
一旦使用了，你就得自己负责正确性。

#### 寻找一般的设计模式

- 模式通过已经准备好的抽象来降低复杂性
- 模式使一般解决方案制度化以减少错误
- 模式通过建议设计选择提供启发性价值
- 模式通过提升设计语言测层次使沟通更流畅

#### 其他的启发式方法

- 高内聚
- 构建继承体系
- 正式化类协议
- 职责分配
- 为测试设计
- 避免失败
- 有意识的选择绑定时间
- 使控制点集中
- 使用暴力方法
- 画图示
- 保持设计模块化

#### 启发性方法指导

```
Polya's How to Solve It
```

不要卡在一个小问题上，你不需要一次性解决所有的设计问题。

### 5.4 设计实践

#### 迭代

发现不顶用的设计。

#### 分治

#### 自顶向下与自底向上

两种方法论应当结合使用。自顶向下容易入手，但是有时底层的复杂性会影响到上层；自底向下难入手，但是能及早的管理复杂性，使得上层设计更容易。

#### 试验原型

#### 协作设计

- 起身去问协作者
- 和协作者坐在一起用白板讨论草图
- 结对编程
- 开会向其他协作者讲解设计
- 正式的审查
- 冷处理自己的设计，再回头看
- 求助公司外的人，在论坛上提问

#### 多少设计才足够？

一般来说，越细越好；设计文档不是越多越好。

#### 记录你的设计工作

- 在代码中插入设计文档
- 在Wiki中记录设计的讨论和决定
- 写e-mail总结
- 拍照
- 保存设计海报
- 使用“类-职责-协作”卡片
- 在适当的细节层次使用UML图

### 5.5 对流行方法学的评论

不要过多关注设计方法学，关注设计本身，不设计或事无巨细的设计都不可取，还是要具体情况具体分析。