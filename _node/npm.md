### npm install安装过程

通过npm install命令可以安装项目中package文件中的所有依赖包，它的过程如下

1. 首先在node_module中查找是否存在对于的包，存在则不重新安装，不存在则安装
2. npm会向registry 查询模块的压缩包地址
3. 然后把压缩包下载到根目录的.npm文件
4. 把压缩包解压到node_module目录