# Education_Student_System（高校学生管理系统）
## 项目概述
本项目为基于Qt的教育学生系统，旨在为学校、培训机构及在线教育平台提供一站式的信息管理解决方案。该系统覆盖学生信息管理、课程安排、成绩评估、教师管理及通知沟通等全流程功能，实现高效、稳定且安全的数据管理与业务处理。通过模块化、分层设计架构，本系统兼具高度可配置性与维护性，为不同规模的教育机构提供定制化服务。
## 后续规划与展望
部分功能模块未实现，后面会持续更新！
## 安装、配置与部署步骤
### 环境要求
- Qt（5.14.2）
- SQLite3（建议预先配置好数据库实例）
- MySQL（可选）
- Redis（可选，用于缓存加速）
- Docker（用于容器化部署，可选）
## 代码结构
```
├── main.cpp  # 主程序入口
├── login.h / login.cpp  # 用户登录界面
├── mainwidget.h / mainwidget.cpp  # 信息管理界面
├── images/  # 图片资源
├── driver.cpp/driver.h  # 数据库驱动
├── addstudent.cpp/addstudent.h  # 添加学生界面
├── modifyingstudent.cpp/modifyingstudent.h  # 修改学生界面
├── DATA.db  # 数据库文件 
├── README.md  # 本项目文档
```
## 功能演示与用户指南
### 登录界面
![login](https://github.com/kawa1909/Qt_Education_Student_System/blob/master/Icon/login.png)
## 信息管理界面实现
![mainwidget](https://github.com/kawa1909/Qt_Education_Student_System/blob/master/Icon/mainwindow.png)
## 增加学生界面实现
![mainwidget](https://github.com/kawa1909/Qt_Education_Student_System/blob/master/Icon/addStudent.png)
## 修改学生界面实现
![mainwidget](https://github.com/kawa1909/Qt_Education_Student_System/blob/master/Icon/modifingStudent.png)
## 登录界面功能实现
1. **输入框的校验：**
   - 用户需要输入学号和密码（学号作为默认的登录标识）。
2. **检查输入框是否为空：**
   - 当用户点击登录按钮时，首先检查学号和密码输入框是否为空。
   - 如果任一输入框为空，弹出提示框提醒用户填入必要的字段，提示信息如下：
     ```
     "请输入学号和密码！"
     ```
3. **学号格式验证：**
   - 校验输入的学号是否符合格式要求（如：学号必须是数字，且位数固定）。
   - 如果学号格式不正确，弹出提示框，提示信息如下：
     ```
     "学号格式不正确！"
     ```
4. **密码格式验证：**
   - 检查输入的密码是否符合规定的格式（如：长度要求、字符要求等）。
   - 如果密码格式不符合要求，弹出提示框，提示信息如下：
     ```
     "密码格式不正确！"
     ```
5. **查询数据库中的学生信息：**
   - 使用学号查询数据库，获取该学生的密码。
   - 如果数据库中没有找到对应的学生记录，弹出提示框，提示信息如下：
     ```
     "学号不存在！"
     ```
6. **学生是否存在：**
   - 如果数据库中找到了学生信息，进一步验证密码。
7. **密码校验：**
   - 比较输入的密码与数据库中存储的密码。
   - 如果密码正确，表示登录成功，跳转到主界面或其他页面，或者显示欢迎信息。
   - 如果密码错误，弹出提示框，提示信息如下：
     ```
     "密码错误，请重新输入！"
     ```
8. **登录成功后的操作：**
   - 成功登录后，可以进行以下操作：
     - 跳转到学生个人信息页面，或者系统主界面。
     - 更新系统的登录状态。
## 信息管理界面功能实现
1. **学生信息管理**：
   - 主界面包含一个 `QTreeWidget` 控件，显示学生信息管理相关选项（如：学生管理、管理员管理）。
   - **学生管理**：可以通过表格查看所有学生信息。
   - **管理员管理**：此部分暂未实现。
2. **学生信息显示**：
   - 使用 `QTableWidget` 显示学生信息，包含学号、姓名、年龄、年级、班级等字段。
   - 初始数据通过数据库加载。
   - 支持点击表格行查看学生详细信息。
3. **学生人数显示**：
   - 在主界面上方显示学生总人数，调用数据库中的函数获取学生数量并更新显示。
4. **删除学生**：
   - 可以在表格中选择一个或多个学生进行删除。
   - 删除操作会弹出确认提示框，确认后删除选中的学生数据。
   - 删除成功后，会刷新表格，显示更新后的数据。
5. **搜索学生**：
   - 在主界面提供一个搜索框，用户可以根据学号或姓名搜索学生信息。
   - 搜索时，如果未找到匹配记录，会弹出提示框告知用户。
6. **全选功能**：
   - 提供一个全选复选框，用户可以选择全选或取消选择所有学生。
   - 全选时，表格中所有学生都会被选中，取消选择时则清空选中的状态。
7. **增加学生**：
   - 用户点击“增加学生”按钮，弹出新增学生窗口，填写学生信息后提交。
   - 新增学生后，会更新主界面的学生数据。
8. **修改学生信息**：
   - 用户可以在表格中选择需要修改的学生，点击修改按钮弹出修改窗口。
   - 在修改窗口中显示学生的详细信息，用户可以修改信息并保存。
   - 保存后，会更新主界面显示的数据。
9. **退出功能**：
   - 用户点击主界面的“退出”按钮，系统关闭。
## 添加学生界面功能实现
### 界面布局
- 添加学生界面包含多个输入框，用于填写学生的基本信息：
  - 姓名：`lineEdit_name`
  - 年龄：`lineEdit_age`
  - 班级：`lineEdit_class`
  - 年级：`lineEdit_grade`
  - 学号：`lineEdit_studentID`
  - 电话：`lineEdit_phone`
  - 微信：`lineEdit_wechat`
- 用户需要填写所有字段才能提交，输入框的值会被传递到数据库中。
### 更新学生信息
1. **验证输入框是否为空**：  
   当用户点击“更新”按钮时，系统会检查所有输入框的内容。如果任一字段为空，则弹出提示框，提醒用户补充完整学生信息：
   - 提示信息：`请将学生信息补充完整！`
2. **检查学生是否已存在**：  
   在提交学生信息之前，系统会通过学号查询数据库，检查该学生是否已存在。如果学生已存在，则弹出提示框，阻止重复添加：
   - 提示信息：`该学生已存在！`
3. **添加学生信息到数据库**：  
   如果所有字段填写完整且学生不存在，系统会将学生信息存入数据库，并刷新表格显示所有学生数据。
4. **发出刷新信号**：  
   添加成功后，系统通过发送信号 `addStudent_update` 通知主界面刷新数据。
### 退出界面
- 用户可以通过点击“退出”按钮退出当前界面，系统会关闭添加学生信息的窗口并发送 `addStudent_closed` 信号，通知主界面关闭该窗口。
## 修改学生界面功能实现
### 界面布局
- **表格（QTableWidget）**：显示所有学生的信息，包含以下列：
  - 学生ID
  - 姓名
  - 年龄
  - 年级
  - 班级
  - 学号
  - 电话
  - 微信
- **输入框（QLineEdit）**：显示当前选中学生的信息，用户可以编辑这些字段。
### 修改学生信息界面功能实现
1. **选中学生**：  
   用户可以通过点击表格中的某一行来选择需要修改的学生，选中的学生信息会自动填充到右侧的输入框中。
2. **填写修改信息**：  
   用户可以在右侧的输入框中修改学生的信息，包括姓名、年龄、年级、班级、学号、电话和微信等字段。
3. **提交修改**：  
   当用户点击“修改”按钮时，系统会检查输入的学生信息是否完整，如果有字段为空，会提示用户补充完整信息。如果所有信息填写完整且合法，系统会更新数据库中的学生信息，并提示修改成功。
   - 提示信息：
     - **成功**：`学生信息修改成功！`
     - **失败**：`学生信息修改失败，请检查输入！`
4. **退出界面**：  
   用户可以通过点击“完成”按钮退出修改界面。
### 表格数据显示与更新
- 当用户选择表格中的某一行时，表格的数据显示会被更新到输入框（`LineEdit`）中。  
- 表格数据在修改后会进行刷新，确保主界面显示的是最新的学生数据。
### 学生端演示
学生用户：登录后可查看个人信息、课程表、成绩单与在线资源，并支持实时提交作业及反馈问题。
### 教师端演示
教师用户：管理班级学生、录入成绩、发布通知与在线批改作业，同时支持成绩分析图表展示。
### 管理员端功能介绍
管理员拥有系统内所有权限，包括用户管理、数据导入导出、系统配置及安全监控。
内置的报表管理工具支持生成学科、班级、教师绩效等多维报表，便于决策分析。
### 常见操作步骤
用户注册和登录：详细的交互步骤引导用户完成账号注册、邮箱验证及密码找回。
数据录入与更新：系统内支持数据批量导入（CSV、Excel 格式）及手动录入，确保信息录入无缝衔接。
消息通知与审批流程：支持定制化审批流程，如请假申请、成绩申诉、课程调整申请等，均通过系统内消息动态进行处理。
# 主要功能模块
## 学生管理模块
### 1. 信息登记与更新
- 支持批量录入和单个录入，涵盖基本信息（姓名、年级、班级、学号、联系方式）。
- 提供数据校验机制，保证数据信息的真实性和完整性。
### 2. 学籍管理与档案维护
- 建立数字化学生档案，支持包括奖惩记录、学术成绩和心理辅导记录等多维数据跟踪。
- 借助权限控制，实现档案数据的细粒度管理，确保数据隐私和安全访问。
### 3. 出勤与行为追踪
- 集成出勤管理功能，实时记录每日到课情况及迟到、早退等异常记录。
- 行为追踪模块支持自定义考勤规则、请假审批流程和统计分析。
## 课程与排课管理模块
### 1. 课程资源管理
- 允许管理员创建、编辑和删除课程信息，设定课程编号、课程简介、考试大纲等详细信息。
- 支持课程分类、学分设置与先修课程设定，实现课程体系的逻辑关联。
### 2. 智能排课系统
- 自动化生成课程表，依据教师专业、教室资源及学生选课意愿进行智能排布。
- 提供冲突检测功能，确保单一时间段内无重复调度，优化资源利用率。
### 3. 教师分配与课酬管理
- 根据课程设置与教师资质，智能推荐最优课程分配方案。
- 提供教师课酬计算模块，支持基于课时及绩效的智能统计核算。
## 成绩评估与反馈模块
### 1. 多维度成绩录入
- 支持期中、期末考试、平时作业、项目考核等多种成绩指标录入。
- 带有成绩预警功能，自动标记低分及异常数据，供后续跟进处理。
### 2. 自动生成成绩单与分析报告
- 系统自动汇总各项分数并计算总成绩，按学期生成完整的成绩单。
- 数据图表展示学生成绩走势、班级整体表现及学科分布，便于教师进行针对性辅导。
### 3. 在线考试与成绩校验
- 集成在线考试平台，支持考务管理、试卷随机抽题与阅卷功能。
- 提供成绩复核及申诉机制，增强数据的透明性与公正性。
## 用户角色与权限管理模块
### 1. 多角色支持
- 系统内部预定义多种角色：管理员、教师、学生、家长、辅导员等。
- 每个角色拥有独立的仪表盘、操作界面与权限体系，确保职责分明。
### 2. 细粒度权限控制
- 系统采用基于角色和权限的访问控制（RBAC）模型，对敏感数据和核心功能进行严格管控。
- 动态权限调整功能，允许在运行中根据实际需求快速调整角色权限。
## 通知与沟通模块
### 1. 实时消息通知
- 内置消息系统支持系统公告、课程变动、考试提醒及个性化通知等多种应用场景。
- 提供邮件、短信以及应用内推送多渠道通知，确保信息的高效传递。
### 2. 教师与学生互动
- 集成在线讨论、作业提交及反馈机制，促进教师与学生间的实时交流。
- 支持家长端接口，实现家校互动、家庭作业查看和成绩反馈。
## 数据统计与报表生成
### 1. 定制化报表设计
- 系统提供灵活的报表设计工具，支持对学生成绩、出勤记录、教师评价等多维度数据生成统计报表。
- 报表支持导出为 Excel、PDF 等格式，方便后续数据归档和业务决策。
### 2. 数据分析与大屏展示
- 内置数据分析模块，利用图表、饼图、折线图等直观展示数据趋势。
- 支持数据大屏展示，适用于学校管理层会议及成果展示。
## 联系方式与支持
如果在使用过程中有任何疑问、建议或发现漏洞，请通过以下方式联系我们：
电子邮箱：1265865927@qq.com
GitHub Issues：https://github.com/kawa1909/education-student-system/issues
