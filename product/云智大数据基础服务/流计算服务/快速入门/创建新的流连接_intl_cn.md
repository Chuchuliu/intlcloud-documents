##1. 登录控制台
登录【流计算服务】控制台，单击左侧导航【流连接】，进入流连接系统。


##2. 新建工程
单击【新建工程】按钮，在弹窗中填写对应的工程信息，完成后单击【创建】。

> 注意： “流连接”与“流创建”的地域须相同；同时，流连接也只能与同地域的 Ckafka、CDB 等产品进行协作，尝试跨地域访问将失败。


##3.新建 Topic
**创建流计算数据源的 Topic**
单击先前创建的工程名称，进入该工程。单击【新建 Topic】按钮，在弹出的页面中填写 Topic 的信息。
![image](https://main.qcloudimg.com/raw/1885e35ba189a46e0cd7d14176a16ccd.png)
所需输入项中，类型有三种，这里选择 tuple 类型。

**tuple**：最常用的类型，表明数据为文本格式。
**blob**：用于数据为二进制类型的 （暂不能与流计算配合使用）。
**upsert**：流连接导出数据到 CDB 中，并希望对已有记录根据主键聚合运算结果做更新时，选择该项。
**分区数**：选择默认的 1。

**创建用于流计算结果输出的流连接 Topic**
![image](https://main.qcloudimg.com/raw/bc9513af3090213149715ee662c8729f.png)
可以看到与作为数据源的 Topic 很相似，只是表结构略有变化，如果是聚合运算等需要对结果进行更新操作的请选择 upsert 类型，并指定主键字段。


##4.新建 Integrator
流连接能够与腾讯云上已有的产品通过配置打通数据传输。 对于作为流计算结果输出作用的 Topic，可以配置其 Integrator 实现数据自动输出到 CDB。

###4.1 申请 CDB 实例并创建数据库、表，表 schema 与 topic 保持一致：

    CREATE TABLE `demo_sink` (
      `record_time` varchar(32) NOT NULL,
      `pv` bigint(20) NOT NULL,
      `uv` bigint(20) NOT NULL,
      PRIMARY KEY (`record_time`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8

###4.2 单击 Topic 列表中的【新建Integrator】。
![image](https://main.qcloudimg.com/raw/d698554a92e8c48acdcd20e8490dab30.png)
类型固定选择“CDB For MySQL”，输入目的 CDB 数据库的实例 ID、用户名、密码。

###4.3 单击【验证】按钮，将会使用该用户名、密码连接 CDB 数据库，验证通过后会有提示信息。
![image](https://main.qcloudimg.com/raw/355b7a4e535f3f25e6ab02f9762c79fd.png)
选择之前申请并创建的库、表后，单击【创建】按钮完成 Integrator。


##5. 启动 Integrator
单击操作列的【启动】，将刚刚创建的 Integrator 启动起来。
![image](https://main.qcloudimg.com/raw/b02e3579600bc1f674d285674c162edf.png)

至此，流连接部分的准备工作完成。 我们创建了一个用于流计算数据输入的流连接 Topic；创建了一个用于流计算数据结果输出的流连接 Topic，同时该 Topic 还会自动将数据传送至指定的 CDB 数据库中。
