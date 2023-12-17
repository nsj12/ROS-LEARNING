# 节点

1. ROS 中的每个节点应负责单一模块用途（例如，一个节点用于控制车轮电机，一个节点用于控制激光测距仪等）。 每个节点都可以通过主题、服务、操作或参数向其他节点发送和接收数据，完整的机器人系统由许多协同工作的节点组成。 在 ROS 2 中，单个可执行文件（C++ 程序、Python 程序等）可以包含一个或多个节点

2. ros查看节点

   ```
   # 运行
   ros2 run turtlesim turtlesim_node
   #查询 另外一个终端
   ros2 node list
   ```

3. 重新映射

   - [重新映射](https://design.ros2.org/articles/ros_command_line_arguments.html#name-remapping-rules)允许您将默认节点属性（例如节点名称、主题名称、服务名称等）重新分配给自定义值

     ```shell
     ros2 run turtlesim turtlesim_node --ros-args --remap __node:=my_turtle
     
     '''
     ros2 run turtlesim turtlesim_node: 这部分运行turtlesim_node节点。这是一个ROS 2中的节点，用于在仿真环境中模拟海龟的运动。
     
     --ros-args: 这个选项表示后面的参数是ROS相关的参数，而不是turtlesim_node节点本身的参数。
     
     --remap __node:=my_turtle: 这个部分使用--remap选项对ROS节点的名称进行重新映射。在这里，__node 是一个特殊的ROS参数，表示节点的名称。通过--remap __node:=my_turtle，将节点的名称从默认值（可能是turtlesim）重命名为 my_turtle。
     '''
     ```

4. 节点信息

   ```shell
   ros2 node info <node_name>
   '''
   eg：
   ros2 node info /my_turtle
   ros2 node info返回与该节点交互的订阅者、发布者、服务和操作（ROS 图形连接）的列表
   '''
   ```

