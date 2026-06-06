# Java Swing 信息管理系统

一个基于 Java Swing 的学生信息管理系统示例项目。项目主要用于课程作业或 Java GUI 入门练习，界面使用 Swing 编写，数据持久化使用 MySQL。

系统按用户权限区分管理员、老师和学生，不同身份登录后进入对应的管理界面。项目中包含学生信息维护、用户管理、课程/成绩查询与修改等基础功能。

## 功能概览

- 登录验证：根据用户身份进入不同界面；
- 用户管理：管理员可以维护系统用户；
- 学生信息管理：支持学生资料的新增、查询、修改等操作；
- 课程信息管理：维护学生课程、任课老师和成绩信息；
- 权限区分：支持管理员、老师、学生三类角色；
- Swing 图形界面：所有主要操作通过桌面窗口完成。

## 技术栈

- Java 19
- Java Swing
- MySQL
- JDBC
- IntelliJ IDEA
- DataGrip

项目依赖的第三方 jar 放在 `lib/` 目录下，运行前需要在 IDE 中把 `lib` 设置为项目库。

当前 `lib/` 包含：

```text
JDateChooser.jar
jcommon-1.0.17.jar
jfreechart-1.0.14.jar
mysql-connector-java-8.0.18.jar
```

## 目录结构

```text
.
├── lib/                     # 第三方 jar 依赖
├── src/
│   ├── Main.java
│   ├── com/
│   │   ├── dao/             # 数据访问层
│   │   ├── db/              # 数据库连接管理
│   │   ├── entity/          # 实体类
│   │   └── gui/             # Swing 界面
│   └── comm/                # 另一组包名下的同类实现
└── README.md
```

主要包说明：

| 路径 | 说明 |
|---|---|
| `src/com/db/DBManager.java` | MySQL 连接和 SQL 执行封装 |
| `src/com/dao/` | 用户、学生、课程相关的数据访问逻辑 |
| `src/com/entity/` | `User`、`Student` 等实体类 |
| `src/com/gui/` | 登录、管理、查询、添加、成绩修改等 Swing 窗口 |
| `lib/` | JDBC、日期选择器、图表相关 jar 包 |

## 数据库配置

数据库连接配置在 `DBManager.java` 中：

```java
private String accountName = "root";
private String accountPass = "123456";
private String url = "jdbc:mysql://localhost:3306/StudentSys?serverTimezone=Asia/Shanghai";
private String driver = "com.mysql.cj.jdbc.Driver";
```

运行前需要根据本机 MySQL 环境修改：

- 数据库用户名；
- 数据库密码；
- 数据库名；
- MySQL 地址和端口。

默认数据库名为：

```text
StudentSys
```

## 数据表说明

项目使用三张主要数据表：

### `usertbl`

用户表，用于登录和权限判断。

| 字段 | 类型 | 说明 |
|---|---|---|
| `uid` | `int` | 用户 ID |
| `uname` | `varchar` | 用户名 |
| `upassword` | `varchar` | 密码 |
| `uright` | `varchar` | 用户权限，可取老师、学生、管理员 |

### `stutbl`

学生信息表。

| 字段 | 类型 | 说明 |
|---|---|---|
| `sid` | `int` | 学生 ID |
| `sname` | `varchar` | 学生姓名 |
| `sage` | `int` | 年龄 |
| `ssex` | `tinyint` | 性别标记，通常使用 0/1 |
| `susername` | `varchar` | 学生登录用户名 |
| `spassword` | `varchar` | 学生登录密码 |
| `semail` | `varchar` | 邮箱 |
| `sphone` | `varchar` | 手机号 |
| `sqqnumber` | `varchar` | QQ 号 |

### `curritbl`

课程与成绩表。

| 字段 | 类型 | 说明 |
|---|---|---|
| `cstudent` | `varchar` | 学生 |
| `cname` | `varchar` | 课程名称 |
| `cid` | `varchar` | 课程编号 |
| `cteacher` | `varchar` | 任课老师 |
| `cgrade` | `int` | 成绩 |

> 说明：仓库当前没有提供完整的建表 SQL 文件。运行前需要先在 MySQL 中创建数据库和上述数据表，并准备必要的初始用户数据。

## 运行方式

1. 使用 IntelliJ IDEA 打开项目。
2. 确认本机已安装 JDK 19 和 MySQL。
3. 在项目结构中把 `lib/` 下的 jar 文件添加为依赖库。
4. 创建 MySQL 数据库 `StudentSys`，并按上面的表结构创建数据表。
5. 修改 `DBManager.java` 中的数据库用户名、密码和连接地址。
6. 运行登录窗口类：

```text
src/com/gui/LoginForm.java
```

也可以根据实际包路径运行 `comm/gui/LoginForm.java` 下的版本。

## 注意事项

- 项目是 Swing 桌面程序，不是 Web 项目；
- MySQL 连接信息目前写在源码中，运行前需要手动修改；
- `lib/` 必须添加到项目依赖，否则 JDBC、日期选择器或图表相关类可能无法加载；
- 当前仓库没有包含数据库初始化 SQL，需要自行创建表和初始数据；
- `src/com` 和 `src/comm` 下存在两组相近实现，运行时建议先选择其中一组作为主路径。

## 适用场景

这个项目适合用于：

- Java Swing 入门练习；
- JDBC 与 MySQL 连接练习；
- 简单信息管理系统课程作业；
- 学生、课程、成绩管理逻辑参考。
