Django，uWSGI和Nginx在一个容器中，使用Supervisord
这个Dockerfile向您展示了如何使用uWSGI和Nginx为Django构建一个相当标准和快速的Docker容器。

来自许多基准测试的uWSGI已经证明是python应用程序的最快服务器，并且具有很大的灵活性。但请注意，我们尚未对此软件包进行任何形式的优化。根据您的需要进行修改。

Nginx已经成为提供Web应用程序的标准，并且具有使用uWSGI协议与uWSGI通信的额外好处，进一步消除了开销。

大多数此设置来自https://uwsgi.readthedocs.org/en/latest/tutorials/Django_and_nginx.html上的优秀教程

使用此存储库的最佳方法是作为示例。将存储库克隆到您喜欢的位置，然后开始添加文件/根据需要更改配置。一旦你真正开始制作你的项目，你会发现你已经触及了大多数文件。

建立并运行
用python3构建
docker build -t webapp .
docker run -d -p 80:80 webapp
转到127.0.0.1查看是否有效
用python2构建
docker build -f Dockerfile-py2 -t webapp .
docker run -d -p 80:80 webapp
转到127.0.0.1查看是否有效
如何插入您的应用程序
在/ app中，目前使用startproject创建了一个django项目。您可能希望将/ app的内容替换为django项目的根目录。然后还从Dockerfile中删除django-app startproject行

uWSGI chdirs到/ app所以在uwsgi.ini中你需要确保wsgi.py文件的python路径是相对的。
