#UniqueLab Mission 1

##编译方法：
    Cmake

##执行方法
    ./index 绝对路径
    ./search 单词1 单词2...

##需要环境
    本地redis数据库 127.0.0.1:6379
    gcc 6.2.1
    libhiredis.so libmagic.so
    
##简介：

本次任务要求编写程序构建一个本地文本文件全文索引，并实现简单的搜索功能。具体来说，你需要完成两个程序，一个用以构建索引，一个用以在索引内搜索所需结果。

##要求：

1. 使用C语言在linux下完成，不能使用system, execv一类的函数调用外部命令完成。可以使用非标准库，但简单的目录遍历需要自己完成；
2. 数据的存储推荐使用Redis，但不作限制；
3. 索引构建程序接受一个命令行参数，该参数为需要建立全文索引的目录名字，比如 "./index_builder /home/anne_frank/diary" 表示对/home/anne_frank/diary"目录下的所有文本文件建立全文索引；
4. 本文中的“文本文件” 定义为MIME类型以text/前缀开头的所有文件（如text/plain, text/x-c等），建立索引的时候只需要考虑文中的“单词”（正则地说，就是[_[:alnum:]]+）；
5. 搜索程序接受一串“单词”作为命令行参数，以下称为list，然后向stdout中打印搜索结果，结果按相关度排序（匹配list中元素数目越多的排在越前面，当匹配list中元素的数目一样时，匹配单词总数目越多的排在越前面），结果应该包含文件的绝对路径、匹配了哪些单词以及每个单词有多少个匹配。

##可选要求：

1. 实现多线程构建索引（注意避免race condition）；
2. 实现增量式构建: 
  1. 用户停止程序后，如果再次处理同一目录，则程序可以自动从上次停止的地方继续进行构建；
  2. 如果两次执行之间有文件的内容发生了改变，则对发生了改变的文件进行重新处理。 