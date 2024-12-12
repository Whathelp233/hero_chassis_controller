这里大概是最终考核完成的情况：
	运行rm_descrition 
	运行simple_chassis_controller
SimpleChassisController（简单底盘控制器）
	init 获取四个麦轮的句柄。（初始化）
	update：给四个麦轮设置角速度（实时更新参数）（个人认为类似订阅者的回调函数）
	谈谈对ros_control的理解？
	中介，对gazebo有很好的支持。包含了一系列的控制器接口，传动装置接口，硬件接口，控制器工具，多种多样的controller。
	硬件层 进行硬件资源管理，controller通过forward command controller向抽象层发消息，我写的controller也是借用这里的模板
	joint limits硬件的限位数据结构
	transmission 传动系统
	controller manager
pluginlib
	首先我们写了一个effortjointcontroller的继承类，然后用pluginlib把这个类转化成一个插件（保存在动态链接库（.so形式））
	然后我们再通过controller manager包加载对应的控制器然后通过里面的接口来控制机器人
选做内容
PID控制：用了ros_control的模版，并且用ros包进行了调整PID参数
逆运动学解算对着论文
正运动学解算对着论文
TF变换先进行正运动学解算核心速度
里程计
TF变化执行用的是在cmdvel callback里transformVector（）
 vel_local,vel_global
 vel_global来接收/cmd_vel数据然后通过函数转换到vel_local;
 

C++键盘控制：实时读取输入然后发布一个/cmd_vel参数。用一个char来存键入的字符，然后转化为它的ASCII码的16位形式，然后再用switch；case这一队来一个个检测，然后输出对应的速度



