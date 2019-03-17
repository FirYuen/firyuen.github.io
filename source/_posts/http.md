---
title: http
date: 2018-05-15 21:40:10
tags:
---
## 请求与响应
Server + Client + HTTP

1. 浏览器负责发起请求
2. 服务器在 80 端口接收请求
3. 服务器负责返回内容（响应）
4. 浏览器负责下载响应内容
HTTP 的作用就是指导浏览器和服务器如何进行沟通。

### 请求示例
`curl -s -v -H "Frank: xxx" -- "https://www.baidu.com"`
请求的内容为
```http
GET / HTTP/1.1
Host: www.baidu.com
User-Agent: curl/7.54.0
Accept: */*
Frank: xxx
```
`curl -X POST -s -v -H "Frank: xxx" -- "https://www.baidu.com"`
请求的内容为
```http
POST / HTTP/1.1
Host: www.baidu.com
User-Agent: curl/7.54.0
Accept: */*
Frank: xxx
```

`curl -X POST -d "1234567890" -s -v -H "Frank: xxx" -- "https://www.baidu.com"`
请求的内容为
```http
POST / HTTP/1.1
Host: www.baidu.com
User-Agent: curl/7.54.0
Accept: */*
Frank: xxx
Content-Length: 10
Content-Type: application/x-www-form-urlencoded

1234567890
```

## 请求的格式
1 动词 路径 协议/版本
2 Key1: value1
2 Key2: value2
2 Key3: value3
2 Content-Type: application/x-www-form-urlencoded
2 Host: www.baidu.com
2 User-Agent: curl/7.54.0
3 
4 要上传的数据

1. 请求最多包含四部分，最少包含三部分。（也就是说第四部分可以为空）
2. 第三部分永远都是一个回车（\n）
3. 动词有 GET POST PUT PATCH DELETE HEAD OPTIONS 等
4. 这里的路径包括「查询参数」，但不包括「锚点」
5. 如果你没有写路径，那么路径默认为 /
6. 第 2 部分中的 Content-Type 标注了第 4 部分的格式

## 响应的格式
1 协议/版本号 状态码 状态解释
2 Key1: value1
2 Key2: value2
2 Content-Length: 17931
2 Content-Type: text/html
3
4 要下载的内容

##状态码
1. 1xx 不常用
2. 2xx 表示成功
3. 3xx 表示滚吧
4. 4xx 表示你丫错了
5. 5xx 表示好吧，我错了

##用 Chrome 查看响应
1. 打开 Network
2. 输入网址
3. 选中第一个响应
4. 查看 Response Headers，点击「view source」，点击「view source」，点击「view source」
5. 你会看到响应的前两部分
6. 查看 Response 或者 Preview，你会看到响应的第 41 部分

## 请求头
![request](/img/request.png)

## 响应头
![response](/img/response.png)

## curl命令是一个利用URL规则在命令行下工作的文件传输工具。它支持文件的上传和下载，所以是综合传输工具，但按传统，习惯称curl为下载工具。作为一款强力工具，curl支持包括HTTP、HTTPS、ftp等众多协议，还支持POST、cookies、认证、从指定偏移处下载部分文件、用户代理字符串、限速、文件大小、进度条等特征。做网页处理流程和数据检索自动化，curl可以祝一臂之力。

## 实例
###文件下载
curl命令可以用来执行下载、发送各种HTTP请求，指定HTTP头部等操作。如果系统没有curl可以使用yum install curl安装，也可以下载安装。curl是将下载文件输出到stdout，将进度信息输出到stderr，不显示进度信息使用--silent选项。
`curl URL --silent`

这条命令是将下载文件输出到终端，所有下载的数据都被写入到stdout。
使用选项-O将下载的数据写入到文件，必须使用文件的绝对地址：
`curl http://man.linuxde.net/text.iso --silent -O`
选项-o将下载数据写入到指定名称的文件中，并使用--progress显示进度条：
```bash
curl http://man.linuxde.net/test.iso -o filename.iso --progress
######################################### 100.0%
```
##更多方法,可以参考[curl命令帮助](http://man.linuxde.net/curl)





















