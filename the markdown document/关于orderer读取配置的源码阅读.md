# 关于orderer读取配置的源码阅读

​      主要阅读了关于orderer处启动时的start函数中的调用localconfig中的load函数去进行读取orderer的配置的源码部分，本次源码阅读涉及到fabric/orderer/main.go、fabric/orderer/common/server/main.go、fabric/orderer/localconfig/config.go、fabric/core/config/config.go。

##### 脉络梳理

​      首先orderer目录下的main函数会调用到orderer/common/server/main.go中的Main函数，Main函数显示会先解析输入参数中的第二个参数，通过第而参数来判断是否是orderer节点启动命令还是打印orderer节点的版本的命令，如果第二个参数是version，则调用orderer/common/metadata/metadata.go中的GetVersionInfo函数，打印出orderer的版本信息；如果不是打印版本信息的命令，则默认执行orderer启动的命令，首先是调用orderer/localconfig/config.go中的load函数去加载orderer的基本的配置信息。

##### fabric/common/localconfig/config.go文件介绍

​     这个文件中主要是关于对静态配置文件中类的声明，以及对于读取的类中属性的填充函数load,具体的逻辑是，先给所有的配置项赋予默认的值，然后根据不同的配置项去调用到fabric/core/config/config.go文件中的函数，根据传入的配置文件的路径填充各个配置项，最后，由load函数返回一个配置对象，里面包含了所有的配置信息。[orderer配置类结构示意图](https://github.com/TryAndDare/the-document-of-read-fabric-source-code/blob/master/the Xmind document/the constructrue of orderer config.xmind)。







