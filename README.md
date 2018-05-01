# protobuf 
protobuf学习

官方：
http://code.google.com/intl/zh-CN/apis/protocolbuffers/docs/javatutorial.html
protobuf-2.4.1 源码包 ----> 需要自己maven编译成 jar
protoc-2.4.1-win32    ----> protoc.exe 编辑器


/**========== 写入 ===============**/
Person.Builder person = Person.newBuilder();

Person.PhoneNumber.Builder phoneNumber = Person.PhoneNumber.newBuilder();
person.addPhone(phoneNumber);//重复 repeated PhoneNumber phone = 4;

person.setId(11); //属性

person.setName("test");

Person p = person.build(); //Person.Builder --转换为--> Person
p.writeTo( fileOutputStream ); //写入



/**========== 读取 ===============**/
Person.parseFrom( fileInputStream ); //调用Person类的方法：读取




运行编译器：
protoc --java_out=输出目录   xxx.proto

toString()	: 按照人可阅读方式输出

/**========== proto =============**/
// required string name = 1;
public boolean hasName();
public java.lang.String getName();
public Builder setName(String value);
public Builder clearName();

// required int32 id = 2;
public boolean hasId();
public int getId();
public Builder setId(int value);
public Builder clearId();

// optional string email = 3;
public boolean hasEmail();
public String getEmail();
public Builder setEmail(String value);
public Builder clearEmail();

// repeated .tutorial.Person.PhoneNumber phone = 4;
public List<PhoneNumber> getPhoneList();
public int getPhoneCount();
public PhoneNumber getPhone(int index);
public Builder setPhone(int index, PhoneNumber value);
public Builder addPhone(PhoneNumber value);
public Builder addAllPhone(Iterable<PhoneNumber> value);
public Builder clearPhone();


/************* 官方英文资料阅读整理 ***********/
required string name = 1;
required int32 id = 2;
optional string email = 3;
数字唯一，在生成的二进制文件中，唯一标识字段  

required: 
optional: 
repeated: 重复：0或多次

原生数据类型对应关系：
.proto Type		Java Type
--------------------------
double			double
float			float
int32			int
int64			long
bool			boolean
string			String


[default = 默认值]、
若不指定默认值：
1、string 默认 ""
2、bools 默认 false
3、numeric数字  默认  0
4、enums枚举  默认  第一个元素


/************* protobuf介绍 ***********/
protobuf是google提供的一个开源序列化框架。主要应用于通信协议，数据存储中的结构化数据的序列化。
它类似于XML，JSON这样的数据表示语言，其最大的特点是基于二进制，因此比传统的XML表示高效短小得多。
虽然是二进制数据格式，但并没有因此变得复杂，开发人员通过按照一定的语法定义结构化的消息格式，
然后送给命令行工具，工具将自动生成相关的类，可以支持java、c++、python等语言环境。
通过将这些类包含在项目中，可以很轻松的调用相关方法来完成业务消息的序列化与反序列化工作。

序列化到磁盘中的数据是部分二进制的，不能被人直接读取。这个不如xml方便。

