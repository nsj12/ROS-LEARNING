# 主题

1. ROS 2 将复杂的系统分解为许多模块化节点。 主题是 ROS 图的重要元素，充当节点交换消息的总线。节点可以将数据发布到任意数量的主题，并同时订阅任意数量的主题

2.  使用`rqt_graph`可视化不断变化的节点和主题，以及它们之间的联系

   ```
   rqt_graph
   ```

   ![topic1](/home/nsj/Desktop/Ros_Learning/ROS2/img/topic1.png)

​		描绘了 `/turtlesim` 节点和 `/teleop_turtle` 节点如何通过主题相互通信。 `/teleop_turtle` 节点正在将数据（您输入的用于移动乌龟的击键）发布到 `/turtle1/cmd_vel` 主题，并且 `/turtlesim` 节点已订阅该主题以接收数据

3. 新终端中运行 命令将返回系统中当前活动的所有主题的列表：`ros2 topic list`

   ```
   /parameter_events
   /rosout
   /turtle1/cmd_vel
   /turtle1/color_sensor
   /turtle1/pose
   ```

4. `ros2 topic list -t`将返回相同的主题列表，这次主题类型附加在括号中

   ```
   /parameter_events [rcl_interfaces/msg/ParameterEvent]
   /rosout [rcl_interfaces/msg/Log]
   /turtle1/cmd_vel [geometry_msgs/msg/Twist]
   /turtle1/color_sensor [turtlesim/msg/Color]
   /turtle1/pose [turtlesim/msg/Pose]
   ##这些属性，特别是类型，是节点在主题移动时知道它们正在谈论相同信息的方式
   ```

5. 主题回显

   ```shell
   ros2 topic echo <topic_name>
   '''
   eg：
   ros2 topic echo /turtle1/cmd_vel
   
   output:
   linear:
     x: 2.0
     y: 0.0
     z: 0.0
   angular:
     x: 0.0
     y: 0.0
     z: 0.0
     ---
   '''
   ```

6. 主题不一定只是点对点的交流；它可以是一对多、多对一或多对多

   ```
   ros2 topic info /turtle1/cmd_vel  ##运行查看信息
   ```

7. 节点使用消息通过主题发送数据。 发布者和订阅者必须发送和接收相同类型的消息才能进行通信

   ```shell
   ros2 topic list -t
   ->geometry_msgs/msg/Twist
   
   #可以在该类型上运行来了解其详细信息，特别是消息期望的数据结构
   ros2 interface show geometry_msgs/msg/Twist
   ```

8. 现在已经有了消息结构,可以使用以下命令直接从命令行将数据发布到主题上

   ```shell
   ros2 topic pub <topic_name> <msg_type> '<args>'
   '''
   #参数需要以 YAML 语法输入 --once是一个可选参数，意思是“发布一条消息然后退出
   ros2 topic pub --once /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.8}}"
   '''
   ```

9. 连续移动，删除了 `--once` 选项并添加了 选项，该选项告诉 以 1 Hz 的稳定流发布命令

   ```shell
   ros2 topic pub --rate 1 /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.8}}"
   ```

10. 主题上运行 `echo` 并重新检查 rqt_graph

    ```
    ros2 topic echo /turtle1/pose
    ```

11. 可以使用以下命令查看数据发布的速率

    ```
    ros2 topic hz /turtle1/pose
    ```

    