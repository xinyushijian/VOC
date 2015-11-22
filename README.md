Copyright &copy; 2014 bt4baidu  
http://www.pdawiki.com/forum/thread-12743-1-1.html  
**敬告：本程序所产生的数据仅供个人学习之用；请勿广泛传播，请勿商用牟利。**
***  
1. 词典内嵌js脚本
--------------------
* j_src.js  
联网发音及例句刷新，自动向词条内注入USAGE导航条，直连vocabulary.com语料库。(未压缩空白字符的原始代码)
* l_src.js  
核心词汇表格式化用。(未压缩空白字符的原始代码)
2. 抓词脚本
----------------
* voc_fetcher1.0.py  
为主程序，单线程下载及html->mdx格式转换
* wrapper.py  
为外壳程序，支持开多个进程，支持无人值守、循环检测、自动重试、断点续传  
3. 用法
----------------
1. 安装python 2.7.6
2. windows下要再安装python加载器，否则弹出一堆窗口很烦人  
https://bitbucket.org/vinay.sajip/pylauncher/downloads/launcher.msi
3. 安装lxml 3.3.5
4. 安装BeautifulSoup 4.3.2
5. 安装urllib3
6. 将wordlist.txt和以上两脚本文件放在同一目录下
7. 配置下载进程数及每块的单词数，目前默认设为25个进程，每块1000个单词  
      如果要修改，找到wrapper.py的如下两行：  
      
            if __name__ == '__main__':
                  STEP = 1000        # 每块1000个单词
                  MAX_PROCESS = 25   # 开25个进程
      进程个数的上限视个人PC的配置和网速而定，PC性能好可以开更多  
      不需要用代理，该网站不封IP（如果开几百个进程有可能会被服务器拒绝访问，未实测）  
      单进程的情况下实测平均下载速度为每分钟60个单词左右  
      如果下载单词量大建议多开进程，按目前默认25个的设置，下完148730个单词需要大概1.5~2小时  
8. 双击wrapper.py，会自动生成mdict目录，并将单词分块开始下载。  
下载完后自动合并为单个文本文件（可直接用MdxBuilder压制成mdx词库）；  
同时生成图片目录p、CSS样式表v.css和l.css，将这些连同上述js脚本放入data目录，  
便可用MdxBuilder压制成mdd文件。  
**注：**如果双击voc_fetcher1.0.py，也会开始下载，但只支持一个进程  
　　有一些错误检测和后期格式处理只在wrapper.py写了，本人懒得再往voc_fetcher1.0.py里加  
　　因此为了确保最后生成的文件正确，即使只打算开一个进程也推荐双击wrapper.py执行  
9. voc_fetcher1.0.py文件名不可修改，如果要改，要同时在wrapper.py里改下面一行：  
      
            arg.append('python -u voc_fetcher1.0.py %s %d' % (sdir, i))
