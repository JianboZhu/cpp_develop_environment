cpp_develop_environment
=======================

The cpp develop environment

注意：安装完成之后，要将相应的.so文件的路径写入到/etc/ld.so.conf中，然后sudo ldconfig，不然linker就找不到相应的so文件.

1. g++ 4.8
  * c++11 completed.
  * see my article in csdn, http://blog.csdn.net/daodaozhu05/article/details/12502365

2. protobuf
  * ./configure --prefix=/usr
  * make
  * sudo make install

3. thrift
  *  download source codes from github.
  *  ./configure
  *  make;
  *  sudo make install

4. boost
  * ./bootstrap.sh
  * sudo ./b2 install

5. blade
  * 安装blade的依赖文件scons：sudo apt-get install scons
  * 安装blade的依赖文件ccache：sudo apt-get install ccache
  * 到主目录上直接./install
  ps. 这里有一点一定要注意，blade的首页上写着这样一段话：
      “开启C++11: 在配置文件cc_config节确保加上cxxflags='gnu++0x'参数即可：cc_config(cxxflags='gnu++0x')”
      实际上是不对的，应该是这样： cc_config(cxxflags='-std=gnu++0x')

6. glog / gflags
    * ./configure & make & sudo make install
  ps. 在mac上安装glog用glog-0.3.3-R139-libc++.tar.gz， 在github上
7. libevent2
    * ./configure & make & make install
8. gtest
   * 具体安装可以参考 http://blog.csdn.net/chengwenyao18/article/details/7181514
   * 此时，要注意几点：
    1. 但是这时只是编译了gtest的libgtest.a这个静态库， "gtest/gtest.h"等头文件也不再/usr/include中，所以直接引用会找不到，需要自己配置路径, sudo cp -r include/gtest /usr/inclide
    2. 将libgtest.a 复制到/usr/lib, /usr/lib32下，这样系统可以找得到这个库文件
    3. 除了libgtest.a这个库文件，有时还需要"libgtest-main.a"这个库文件，这时可以去src下，运行ar -rv libgtest-main.a gtest-main.o得到库文件，然后copy到/usr/lib下。

9. gperftools
   64位的系统需要先安装libunwind. 然后在安装gperftools。 安装方式都是configure --> make --> make install

10. jemalloc
    * ./configure
    * make
    * sudo make install
    ps. 使用时直接 用g++ -o a a.cpp -ljemalloc即可， 或是blade这届#jemalloc即可。tcmalloc也是一样的。
11. mysql++
    * 见我的csdn：http://blog.csdn.net/daodaozhu05/article/details/12970657

12. rapidjson
    * 无需编译和安装，直接include头文件即可

13. hiredis
    make && sudo make install

13. ubuntu下安装nginx
    * 安装依赖
    1) pcre正则表达式库
          sudo apt-get install libpcre3 libpcre3-dev
    2） ssl  for https
        sudo apt-get install libssl-dev
    * 下载nginx安装文件
       ./configure & make & make install
    * 操作nginx
      sudo /usr/local/nginx/sbin/nginx    (启动)
      /usr/local/nginx/sbin/nginx -s stop (停止)
      /usr/local/nginx/sbin/nginx -s reload (重启)

      也可以使用linux的service服务（其实就是一个脚本，用于管理/etc/init.d下的二进制启动程序）
       sudo cp /usr/local/nginx/sbin/nginx /etc/init.d
      就可以使用service来操作nginx了
      sudo service nginx   (启动)
      sudo service nginx -s stop  （停止）
      sudo service nginx -s reload  （重启）

    * 启动nginx后，在浏览器上输入localhost, 就可以看到nginx的欢迎页面了.
