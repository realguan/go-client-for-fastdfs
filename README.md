go-client-for-fastdfs
=====================

简介：go-client-for-fastdfs是实现了使用go语言来调用fastdfs的接口，本质就是用fastdfs 的c api写成相关的c功能函数并输出为 .so文件,go语言调用.so文件来调用c功能函数
现在只实现了两个接口:

//上传文件到fdfs
func FdfsUploadFile(conf string,imagePath string)(result map[string]interface{},err error)

//删除fdfs文件
func FdfsDeleteFile(conf string,fileId string)(result map[string]interface{},err error)


使用方法(fastdfs是基于4.0.6版本编译的)：

１．进入目录　go-client-for-fastdfs
２．
gcc -Wall -D_FILE_OFFSET_BITS=64 -D_GNU_SOURCE -g -O -DDEBUG_FLAG -DOS_LINUX -DIOEVENT_USE_EPOLL  -fPIC -shared  -o libfdfs.so fdfs.c -L/usr/local/lib -lfastcommon -lfdfsclient  -lpthread -ldl -rdynamic -I/usr/local/include/fastcommon -I/usr/local/include/fastdfs
３．把生成的文件复制到libfdfs.so　复制到/usr/local/lib ，注意文件的权限
４．查看/etc/ld.so.conf，看一下路径/usr/local/lib是否存在，没有就添加进去，最后ldconfig更新路径
# cat /etc/ld.so.conf
include ld.so.conf.d/*.conf
# echo "/usr/local/lib" >> /etc/ld.so.conf
# ldconfig
５．实例代码请查看test.go


注意，在使用go语言调用c函数的时候，本人踩过的一个超坑人的坑,详细请看：http://www.newjueqi.com/?p=106







