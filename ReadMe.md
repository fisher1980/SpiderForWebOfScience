### 说明手册

#### 整个代码参数极少，只有三个，并且都是显示易懂的参数。
#### 整个代码运行的前提是 能打开web of science并能展示出条件检索结果
#### 整个爬虫代码在Spider_by_VZ里面只有三个主要的py文件分别如下
* Main_Methods 里面包含了所有需要提取的信息抽取代码，无需关心
* main是使用的入口，main里面有三个参数需要指定，具体后面阐述。
* DownloadPdf 是 下载web of science 直接可获取的 文献pdf


#### main.py 参数说明：
总共有三个参数需要制定，我将分别用图片文字说明

1. 此时我们已经打开了web of science页面，但是这时候的url链接并不符合这个代码的要求（因为没有翻页参数）
![web of science检索结果页面](https://github.com/tangweize/SpiderForWebOfScience/tree/master/assets/ReadMe-1594282295341.png)
2. 这时候，我们需要在下图箭头标志出随便输入一个页码，激活带有page参数的url。
![获取带有page的url](https://github.com/tangweize/SpiderForWebOfScience/tree/master/assets/ReadMe-1594282533769.png)
3. 最终，我们可以根据该页面获得main函数里面的两个参数。

* url_root的设置 带有pages的url链接，但是不需要数字（比如上图里面的2删掉）注意：这个url_root里面是带有验证信息的，一般24小时，需要更换一次
* nums_page的设置为下图圆圈里面数字,也就是总页码
![页码数设置](https://gitee.com/tangweize/SpiderForWebOfScience/tree/master/assets/ReadMe-1594282742570.png)
* filename 指定文献信息表格存的路径以及名字
    
![页码数设置](data:image/jpeg;base64,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)

### 环境 
* python 3.6
* 依赖的包
requests 
pandas  
beautifulsoup4 
tqdm
