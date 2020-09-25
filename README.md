# sun

#include <MPython.h> 
#include <DFRobot_Iot.h> 
// 函数声明 
void obloqMqttEventT0(String& message); 
// 静态常量 
const String topics[5] = {"O8Yb6kFGg","zt3bekFGg","","",""}; 
const MsgHandleCb msgHandles[5] = {obloqMqttEventT0,NULL,NULL,NULL,NULL}; 
// 创建对象 
DFRobot_Iot myIot; 


// 主程序开始 
void setup() { 
	mPython.begin(); 
	myIot.setMqttCallback(msgHandles); 
	myIot.wifiConnect("HONOR 9X", "28a45429fc0a"); 
	while (!myIot.wifiStatus()) {yield();} 
	display.setCursorLine(1);
	display.printLine("wifi已经连接成功了");
	myIot.init("iot.dfrobot.com.cn","XQZAekFGR","","XwZAezFMgz",topics,1883);
	myIot.connect();
	while (!myIot.connected()) {yield();}
	display.setCursorLine(2);
	display.printLine("mqtt连接成功");
}
void loop() {
	if ((buttonA.isPressed())) {
		myIot.publish(topic_1, "2018764225 陈淇诗");
	}
}


// 事件回调函数
void obloqMqttEventT0(String& message) {
	display.setCursorLine(3);
	display.printLine(message);
}
