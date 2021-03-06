Using Your Swarm Cluster
========================

This directory contains all of the files the Docker CLI will need to
communicate with your Swarm Cluster. The included files are:

* ca.pem - Certificate Authority, used by clients to validate servers
* cert.pem - Client Certificate, used by clients to identify themselves to servers
* key.pem - Client Private Key, used by clients to encrypt their requests
* ca-key.pem - Certificate Authority Key, private file used to generate more client certificates.
* docker.env - Shell environment config file


使用您的群集群
========================

该目录包含所有泊坞窗CLI将需要的文件
与你的群集群通信。所包含的文件是：

* ca.pem - 证书颁发机构，客户端验证服务器使用
* cert.pem - 客户端证书，客户端用来标识自己的服务器
* key.pem - 客户端私钥，客户端使用加密他们的请求
* CA-key.pem - 证书认证中心密钥，用来生成更多的客户端证书的私人文件。
* docker.env - Shell环境配置文件


Configuring Docker CLI
----------------------

The easiest way to configure the Docker CLI to communicate with the Swarm
Cluster is via environment variables. The provided 'docker.env' can be
sourced into your environment to set the required variables. When ever you
start a new shell session you will need to source the 'docker.env' file to
set the proper environment variables. You only need to do this once per
session though.
配置泊坞窗CLI
----------------------

配置多克尔CLI的最简单方法与群进行交流
群集是通过环境变量。所提供的“docker.env”可
源到您的环境来设置所需的变量。当你过
启动一个新的shell会话，您将需要源“docker.env'文件
设置适当的环境变量。你只需要做到这一点每一次
会议虽然。

    $ source docker.env
    $ docker info
    Containers: 4
    Strategy: spread
    Filters: affinity, health, constraint, port, dependency
    Nodes: 2
     swarm-n1: 192.168.1.2:42376
      └ Containers: 2
      └ Reserved CPUs: 0 / 12
      └ Reserved Memory: 0 B / 2.1 GiB
     swarm-n2: 192.168.1.3:42376
      └ Containers: 2
      └ Reserved CPUs: 0 / 12
      └ Reserved Memory: 0 B / 2.1 GiB

When communicating with Swarm, the 'docker info' command will show global
details about the cluster and specific details about each node.
当群通信时，“docekr info ”命令将显示全球关于每个节点的群集和具体细节的详细信息。


Running your first container
----------------------------

If you haven't sourced 'docker.env' you will need to do so before running
your first container. In this example, we will spawn a container running
an interactive shell.
如果你还没有来源“docker.env”，则需要在运行之前，
这样做你的第一个容器。在这个例子中，我们将产生一个容器中运行交互式shell。

First, make sure you've got the proper environment variables set by sourcing
'docker.env'. Next, we will actually run the container with 'docker run --rm
-it <image> <command>'. In our case, we will use the 'cirros' image, which is
a tiny demo image, and the '/bin/sh' command. It will take a short while for
Docker to run the container but when it is done, you will have an interactive
shell. To test out this container, we can run hostname, which will return the
short id of the container. The container also has network access, so you can
use ping to test networking. Lastly, to exit the container, simply issue an
'exit' command.

首先，确保你已经有了由采购设置适当的环境变量“docker.env”。
接下来，我们将实际运行与“docker run --rm容器- it <image> <command>。在我们的例子中，我们将使用“cirros”的形象，这是
一个微小的演示图像，和'/bin/sh'command。这将需要稍等片刻
泊坞窗运行容器，但是当它完成，你将有一个互动
贝壳。为了测试这个容器，我们可以运行的主机名，这将返回
容器的短ID。该容器还具有网络接入，这样你就可以
使用ping测试网络。最后，退出容器，只需发出
“退出”命令。

    $ source docker.env
    $ docker run --rm -it cirros /bin/sh
    / # hostname
    7bcfb8c82455
    / #  ping -c 4 8.8.8.8
    PING 8.8.8.8 (8.8.8.8): 56 data bytes
    64 bytes from 8.8.8.8: seq=0 ttl=42 time=9.457 ms
    64 bytes from 8.8.8.8: seq=1 ttl=42 time=9.633 ms
    64 bytes from 8.8.8.8: seq=2 ttl=42 time=9.527 ms
    64 bytes from 8.8.8.8: seq=3 ttl=42 time=9.654 ms

    --- 8.8.8.8 ping statistics ---
    4 packets transmitted, 4 packets received, 0% packet loss
    round-trip min/avg/max = 9.457/9.567/9.654 ms
    / #  exit

And, with that you've successfully used a Docker container! You can find more
details on available Docker CLI commands in their [documentation](https://docs.docker.com/reference/commandline/cli/ "Docker CLI Documentation").
关于完成使用 Docker container 你可以着更多详细信息 在有效的 Docker CLI command 

