# Robotics-ROS-03-Communication
ROS course on Shenlanxueyuan.com

## Initialization

<img src="https://github.com/ChenBohan/Robotics-ROS-03-Communication/blob/master/readme_img/create_workspace.png" width = "80%" height = "80%" div align=center />

### Initialize a workspace

<img src="https://github.com/ChenBohan/Robotics-ROS-03-Communication/blob/master/readme_img/create_package.png" width = "80%" height = "80%" div align=center />

### Initialize a package

<img src="https://github.com/ChenBohan/Robotics-ROS-03-Communication/blob/master/readme_img/create_package.png" width = "80%" height = "80%" div align=center />

## Topic

<img src="https://github.com/ChenBohan/Robotics-ROS-03-Communication/blob/master/readme_img/topic.png" width = "80%" height = "80%" div align=center />

### Publishir

<img src="https://github.com/ChenBohan/Robotics-ROS-03-Communication/blob/master/readme_img/publisher.png" width = "80%" height = "80%" div align=center />

```cpp
  // ROS节点初始化
  ros::init(argc, argv, "talker");

  // 创建节点句柄
  ros::NodeHandle n;
  
  // 创建一个Publisher，发布名为chatter的topic，消息类型为std_msgs::String
  ros::Publisher chatter_pub = n.advertise<std_msgs::String>("chatter", 1000);

  // 设置循环的频率
  ros::Rate loop_rate(10);
```

```cpp
while (ros::ok())
  {
	// 初始化std_msgs::String类型的消息
    std_msgs::String msg;
    std::stringstream ss;
    ss << "hello world " << count;
    msg.data = ss.str();

	// 发布消息
    ROS_INFO("%s", msg.data.c_str());
    chatter_pub.publish(msg);

	// 循环等待回调函数
    ros::spinOnce();
	
	// 按照循环频率延时
    loop_rate.sleep();
    ++count;
  }
```

### Subscriber

<img src="https://github.com/ChenBohan/Robotics-ROS-03-Communication/blob/master/readme_img/subscriber.png" width = "80%" height = "80%" div align=center />

```cpp
  // 创建一个Subscriber，订阅名为chatter的topic，注册回调函数chatterCallback
  ros::Subscriber sub = n.subscribe("chatter", 1000, chatterCallback);
```

```cpp
// 接收到订阅的消息后，会进入消息回调函数
void chatterCallback(const std_msgs::String::ConstPtr& msg)
{
  // 将接收到的消息打印出来
  ROS_INFO("I heard: [%s]", msg->data.c_str());
}
```

### CMakeList

<img src="https://github.com/ChenBohan/Robotics-ROS-03-Communication/blob/master/readme_img/cmakelist.png" width = "80%" height = "80%" div align=center />

```cpp
add_executable(talker src/talker.cpp)
target_link_libraries(talker ${catkin_LIBRARIES})
#add_dependencies(talker ${PROJECT_NAME}_generate_messages_cpp)

add_executable(listener src/listener.cpp)
target_link_libraries(listener ${catkin_LIBRARIES})
#add_dependencies(listener ${PROJECT_NAME}_generate_messages_cpp)
```

### Msg

<img src="https://github.com/ChenBohan/Robotics-ROS-03-Communication/blob/master/readme_img/msg.png" width = "80%" height = "80%" div align=center />

```
string name
uint8  sex
uint8  age

uint8 unknown = 0
uint8 male    = 1
uint8 female  = 2
```

```
add_message_files(FILES Person.msg)
```

## Server

<img src="https://github.com/ChenBohan/Robotics-ROS-03-Communication/blob/master/readme_img/server.png" width = "80%" height = "80%" div align=center />

### Server

<img src="https://github.com/ChenBohan/Robotics-ROS-03-Communication/blob/master/readme_img/server_node.png" width = "80%" height = "80%" div align=center />

### Client

<img src="https://github.com/ChenBohan/Robotics-ROS-03-Communication/blob/master/readme_img/client_node.png" width = "80%" height = "80%" div align=center />

### CMakeList

<img src="https://github.com/ChenBohan/Robotics-ROS-03-Communication/blob/master/readme_img/cmakelist2.png" width = "80%" height = "80%" div align=center />

### Srv

<img src="https://github.com/ChenBohan/Robotics-ROS-03-Communication/blob/master/readme_img/srv.png" width = "80%" height = "80%" div align=center />

## Launch

### Launch & Node

<img src="https://github.com/ChenBohan/Robotics-ROS-03-Communication/blob/master/readme_img/launch.png" width = "80%" height = "80%" div align=center />

### Param & arg

<img src="https://github.com/ChenBohan/Robotics-ROS-03-Communication/blob/master/readme_img/param.png" width = "80%" height = "80%" div align=center />
