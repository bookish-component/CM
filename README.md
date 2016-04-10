# CM

## Introduction

一个适用于json配置的配置管理构件

- 支持动态加载配置文件
- 可变的配置文件位置
- 可直接配置成Java对象
- 可以根据键读值
- 支持链式调用，可以读取嵌套配置

## Installation

File -> project structure -> Libraries

![import jar](https://github.com/bookish-component/CM/tree/master/img/importjar.png)

## Usage
- First, new a Config object,
```java
Config config = new Config();
```
- Second, load json configuration file,
```java
config.readFile("config/conf.json");
```
- Third, invoke relevant API.
```java
//get nested configuration
Config getConf(String key);

//get String value of key
String getString(String key);

//get int value of key
int getInt(String key);

//get float value of key
int getFloat(String key);

//get String array value of key
String[] getStringArray(String key)

//directly convert to a Java bean
<T> T toObj(Class<T> t);
```

## API Example
#### config/conf.json
```json
{
  "server":{
    "host":"localhost",
    "port":8080,
    "MaxMsgNumber":100,
    "MaxMsgNumberPerSec":5
  },
  "strArray":["aa","bb"]
}
```
#### Configuration class
```java
public class Configuration {
    private String host;
    private int port;
    private int maxMsgNumber;
    private int maxMsgNumberPerSec;
    //setters and getters
    ...
```
#### Kick off!!!
```java
import sse.tongji.bookish-meme.cm

Config config = new Config();
config.readFile("config/conf.json");
//convert to Confihuration class
Configuration configuration = config.getConf("server").toObj(Configuration.class);
//get String value-"host"
String host = config.getConf("server").getString("host");
//get String Array
 String[] result = config.getStringArray("strArray");
...其他API调用类似
```
