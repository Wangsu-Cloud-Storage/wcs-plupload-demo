## wcs-plupload-demo
 - [使用指南](#使用指南)
   - [demo部署](#demo部署)
   - [插件集成](#插件集成)
 
### 使用指南
1. 执行WebContent的index.html,可以看到简单的上传界面
2. plupload的配置在WebContent/upload.js，需要修改uptoken_url的路径为生成token的路径
3. 需要修改upload_url的地址为网宿云存储wcs的上传地址

#### demo部署
一、服务端准备
1. 本 SDK 依赖服务端颁发的上传凭证，可以通过以下方式实现：
利用网宿云存储服务端 SDK 构建后端服务，提供一个获取token的URL 地址，供wcs-plupload初始化使用，前端通过 Ajax 请求该地址后获得 uptoken。 Ajax 请求成功后，服务端将token直接以字符串形式原样返回（不能添加双引号等其它字符）。例如 ：
```
115bd5294d15cf22f5bba8ec93276f1a7d2...
*注：解析返回字符串的内容值为uptoken，即上例中uptoken为115bd5294d15cf22f5bba8ec93276f1a7d2...*
```

二、配置信息修改
1. 修改plupload-demo\WebContent\index.html，如下图红框配置信息

![](https://wcsd.chinanetcenter.com/guide-plupload-pics/wcs-plupload-demo1.png)

三、plupload-demo发布
如tomcat发布步骤，可参考[tomcat官网]
1. apache-tomcat-8.5.2\webapps\ROOT目录下文件清空
2. 将plupload-demo\WebContent\下的所有文件拷贝到apache-tomcat-8.5.2\webapps\ROOT目录下
3. 启动tomcat
4. 访问index.html，界面如下图

![](https://wcsd.chinanetcenter.com/guide-plupload-pics/wcs-plupload-demo2.png)

四、文件上传
1. 点击[文件上传]
2. 弹出文件选择窗口
3. 选择要上传的文件
4. 文件开始上传，文件上传成功，如下图所示

![](https://wcsd.chinanetcenter.com/guide-plupload-pics/wcs-plupload-demo3.png)

#### 插件集成
1. 导入plupload插件对应的文件(plupload文件夹下的文件)，引入网宿云存储的SDK(upload.js)，如下图

![](https://wcsd.chinanetcenter.com/guide-plupload-pics/wcs-plupload-demo4.png)

2. 在html文件中引入相应的js

![](https://wcsd.chinanetcenter.com/guide-plupload-pics/wcs-plupload-demo5.png)

3. 初始化uploader（请确保在执行初始化时，页面已经引入 plupload），如下

![](https://wcsd.chinanetcenter.com/guide-plupload-pics/wcs-plupload-demo6.png)
  
#### plupload常见错误码
|属性名称|描述|
|--|--|
|VERSION	|当前plupload的版本号|
|STOPPED	|值为1，代表上传队列还未开始上传或者上传队列中的文件已经上传完毕时plupload实例的state属性值|
|STARTED	|值为2，代表队列中的文件正在上传时plupload实例的state属性值|
|QUEUED	|值为1，代表某个文件已经被添加进队列等待上传时该文件对象的status属性值|
|UPLOADING	|值为2，代表某个文件正在上传时该文件对象的status属性值|
|FAILED	|值为4，代表某个文件上传失败后该文件对象的status属性值|
|DONE	|值为5，代表某个文件上传成功后该文件对象的status属性值|
|GENERIC_ERROR	|值为-100，发生通用错误时的错误代码|
|HTTP_ERROR	|值为-200，发生http网络错误时的错误代码，例如服务气端返回的状态码不是200|
|IO_ERROR	|值为-300，发生磁盘读写错误时的错误代码，例如本地上某个文件不可读|
|SECURITY_ERROR	|值为-400，发生因为安全问题而产生的错误时的错误代码|
|INIT_ERROR	|值为-500，初始化时发生错误的错误代码|
|FILE_SIZE_ERROR	|值为-600，当选择的文件太大时的错误代码|
|FILE_EXTENSION_ERROR	|值为-601，当选择的文件类型不符合要求时的错误代码|
|FILE_DUPLICATE_ERROR	|值为-602，当选取了重复的文件而配置中又不允许有重复文件时的错误代码|
|IMAGE_FORMAT_ERROR	|值为-700，发生图片格式错误时的错误代码|
|IMAGE_MEMORY_ERROR	|当发生内存错误时的错误代码|
|IMAGE_DIMENSIONS_ERROR	|值为-702，当文件大小超过了plupload所能处理的最大值时的错误代码|

范例-服务端返回500异常,文件上传失败（file.status=4， status=500）
```
{
    "code": -200,
    "message": "HTTP Error.",
    "file": {
        "id": "o_1bmt8bkee1mvs1dlpnd11e8a117g10",
        "name": "test.file",
        "type": "video/avi",
        "size": 30351940,
        "origSize": 30351940,
        "loaded": 0,
        "percent": 0,
        "status": 4,
        "lastModifiedDate": "2017-07-26T05:50:14.325Z"
    },
    "response": "{\"code\":\"500\",\"message\":\"Internal Service Error\"}",
    "status": 500,
    "responseHeaders": "Content-Type: application/json;charset=UTF-8\r\n"
}
```

更多plupload信息参考：http://www.plupload.com/
