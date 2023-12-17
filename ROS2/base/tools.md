# turtlesim

1. 背景

   `turtlesim` 是ROS（机器人操作系统）中的一个基础模拟器，用于教学和学习ROS的基本概念和编程。它是一个简单的二维图形化仿真工具，通过模拟一个小海龟（turtle）在二维空间中的运动，可以帮助初学者理解ROS中的发布/订阅（publish/subscribe）通信模式和基本的运动控制

2. 安装

   ```shell
   sudo apt update
   sudo apt install ros-galactic-turtlesim
   ```

3. 启动

   ```shell
   ros2 run turtlesim turtlesim_node
   ##模拟器窗口应该出现，中间有一只随机的海龟
   ```

4. 使用

   ```shell
   #打开新终端并再次获取 ROS 2
   ros2 run turtlesim turtle_teleop_key
   ###使用上下左右控制海龟运动
   ```



# rqt

1. 下载

   ```shell
   sudo apt update
   sudo apt install ~nros-galactic-rqt*
   ```

2. 使用

   ```shell
   rqt
   ```

   - 第一次运行 rqt 后，窗口将为空白。 不用担心;只需选择**Plugins** > **Services** > **Service Caller**来自顶部菜单栏
   - rqt 可能需要一些时间才能找到所有插件本身。 如果您点击 插件，但没有看到服务或任何其他选项，您应该关闭 rqt，在终端中输入命令 。rqt --force-discover

3. 基本用法

   ![2023-12-17_22-07](https://github.com/nsj12/ROS-LEARNING/issues/1#issue-2045299201)

   - 首先打开turtlesim

     ```shell
     ros2 run turtlesim turtlesim_node
     
     #打开新终端并再次获取 ROS 2
     ros2 run turtlesim turtle_teleop_key
     ```

   - 点击rqt中刷新按钮这个时候下拉节点消息会看到现在全部发布的节点

   - 选择/spawn，这个时候你可以利用这个服务新建海龟，设置信息如下，点击call这个时候你会在界面上看到第二只

     ```
     x:1.0
     y:1.0
     name:'t2' 
     ```

   - 选择/turtle1/set_pen`服务为turtle1提供一支独特的笔在这里你可以设置乌龟移动轨迹的颜色和粗细,点击call，之后在运控部分进行移动就可以看到自己设置效果了

     ```
     r:255
     g:0
     b:0
     width:5
     ```

   - 对乌龟2进行修改，刷新节点，这个时候就可以看到乌龟2的消息了，其他操作和乌龟1一致

     ```shell
     #打开终端
     ros2 run turtlesim turtle_teleop_key --ros-args --remap turtle1/cmd_vel:=turtle2/cmd_vel
     ```

   
