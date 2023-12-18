# 服务

1. 服务是 ROS 图中节点通信的另一种方法。 服务基于调用和响应模型，而不是主题的发布者-订阅者模型。 虽然主题允许节点订阅数据流并获取持续更新，但服务仅在客户端专门调用时才提供数据

2. 启动两个turtlesim节点`/turtlesim`和`/teleop_turtle`

   ```shell
   ros2 run turtlesim turtlesim_node
   ros2 run turtlesim turtle_teleop_key
   
   #新终端中运行命令将返回系统中当前活动的所有服务的列表
   ros2 service list
   
   #看到两个节点具有相同的六个服务，其名称中均带有 parameters。 ROS 2 中的几乎每个节点都有这些参数构建的基础设施服务
   ```

3. 服务具有描述服务的请求和响应数据的结构的类型。 服务类型的定义与主题类型类似，不同之处在于服务类型有两部分：一个用于请求的消息，另一个用于响应

   ```
   #找出服务的类型
   ros2 service type <service_name>
   ```

4. 同时查看所有活动服务的类型

   ```
   ros2 service list -t
   ```

5. 要查找特定类型的所有服务，可以使用以下命令

   ```shell
   ros2 service find <type_name>
   
   #可以找到所有Empty类型的服务
   ros2 service find std_srvs/srv/Empty
   
   '''
   -- 将请求结构（上方）与响应结构（下方）分开,Empty 类型不会发送或接收任何数据。 所以，它的结构是空白的
   '''
   
   ros2 interface show turtlesim/srv/Spawn
   ```

6. 调用服务

   ```shell
   ros2 service call <service_name> <service_type> <arguments>
   
   #eg:
   ros2 service call /clear std_srvs/srv/Empty
   
   #调用 /spawn 并输入参数来生成一只新海龟
   ros2 service call /spawn turtlesim/srv/Spawn "{x: 2, y: 2, theta: 0.2, name: ''}"
   ```

   