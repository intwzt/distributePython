一个python分布式多线程程序

taskmanage.py 任务发布端
taskworker.py 任务处理端

taskmanage.py 通过网络将queue注册出去，然后获得注册后的queue，向里面随机写数字。
taskworker.py 通过网络获取任务队列中的数据，计算后放入结果队列，供taskmanage.py使用。
taskmanage.py取得计算结果，讲结果打印。
需要注意的是，taskworker.py要和taskmanage.py通信，需要填写端口和验证码，和taskmanage.py创建的一致。

具体做法是：

manager：
QueueManager(address=('', 5000), authkey='abc')

worker:
server_addr = '127.0.0.1'
QueueManager(address=(server_addr, 5000), authkey='abc')

为了验证分布式的效果，可以在两台机器下分别运行代码，在Linux和Mac下使用"ifconfig"命令查看en0:下的ip地址，填写即可。
具体代码有详细的注释。
