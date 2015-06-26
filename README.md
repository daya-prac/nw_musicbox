# 网易音乐盒 

使用html5和node.js构建的网易云音乐的跨平台第三方客户端。    
<img style="vertical-align:middle;margin-right:50px" src="http://7xiyak.com1.z0.glb.clouddn.com/icon.png"/>  

###Release  
__version 1.3.0__  
Linux:[x64](http://7xiyak.com1.z0.glb.clouddn.com/1.3.0linux64.zip)  
Windows:[x64](http://7xiyak.com1.z0.glb.clouddn.com/1.3.0windows64.zip)  
其他平台参考`Manual Install`  

###Feature  
1. 设定本地音乐文件夹，播放本地音乐  
2. 搜索播放网络音乐
3. 设置自定义播放列表，可以同时加入网络音乐和本地音乐
4. 手机帐号或邮箱帐号登录
5. UI响应式布局与mini模式  
6. 侧栏列表鼠标拖动排序  
7. 滚动歌词  
8. 私人fm  
9. 系统播放提示  

###TO DO    
1. 托盘图标  
2. 推荐歌单  
3. 喜爱、收藏

###Manual Install  
1. 首先安装[nw.js](https://github.com/nwjs/nw.js)
2. 拷贝chrome安装目录下的`libffmpegsumo.so`(windows下是`libffmpegsumo.dll`)至nw.js的安装目录下  
3. 下载并切换至项目：`git clone https://github.com/stkevintan/nw_musicbox.git && cd nw_musicbox/`  
4. 安装模块: `npm i`  
4. 运行： `/path/to/nw .`   

`libffmpegsumo`的版本一定要与nw.js版本对应，否则会出现问题。比如：nw.js v0.12.0对应chrome 41.0.2272.76


###Update
`cd /path/to/NetEaseMusic/ && git pull`


###Screenshots
<img src="http://7xiyak.com1.z0.glb.clouddn.com/s59.png"/>
<img src="http://7xiyak.com1.z0.glb.clouddn.com/s60.png"/>
<img src="http://7xiyak.com1.z0.glb.clouddn.com/s52.png"/>

###Developer tips  
本项目前端使用jade、stylus与bootstrap框架，源文件包括在src中，使用gulp自动构建至dist文件夹中。  
本项目结构类似于MVC结构，所有定义ui交互等运行于web context中的文件皆置于controller文件夹中，所有定义数据模型、处理网络或本地事务等运行于node context中的文件皆置于model文件夹中。  
controller中包括：   
- category 管理播放列表目录（sidebar）
- account  管理账户
- nav  管理顶栏
- lrc  歌词面板
- player  底部播放器
- playlist 歌曲列表
- radio 私人fm
- settings 设置面板
- index 程序入口，会调用loadPlaylists方法加载entry对象中所有定义的播放源。  

model中包括：   
- EntryModel 定义播放源
- PlaylistModel 定义播放列表
- SongModel 定义歌曲
- FileManager 处理本地文件系统
- NetEaseMusic 处理网络（既api）
- Utils 对node.js中util的扩展，包括二分查找、队列等实用工具  

目前已经定义了本地、用户、云音乐三个播放源。可以通过扩展index.js中的entry对象添加新的播放源比如豆瓣、虾米等。  

###Troubleshooting
遇到什么问题可以尝试一下删除项目主目录中data目录再重启。

####Mini模式还能调窗口大小
这是nw.js的bug

####没有声音或者'糟糕，文件或网络资源无法访问'
首先，可能是由于nw.js自带的音频解码器不支持mp3格式，参考`Manual Install`第二步解决。
也有可能是由于网络延时，网络音乐还未解析完全，这种情况等待一下即可。

