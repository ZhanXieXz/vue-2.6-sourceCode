### vue 源码阅读记录
```
npm i 安装依赖
```
- 随后开启源码地图，开启后打包完会多一个.map文件，开启方法是package.json -> script -> dev命令中添加 --sourcemap
- 先删除dist目录，然后执行npm run dev后就会多一份.map文件
- 如果想恢复之前dist其他版本的vue文件，可以执行npm run build

- 查找入口文件：
  - 进入package.json文件中，定位到script下的dev命令，命令中scripts/config.js关键字开始，进入该文件
  <Br/>
  - 一般在文件底部都会出现export，从export中我们可以得知该文件导出的内容，再往上进行查找，而不需要从头开始一行一行的读   
  <Br/>
  - scripts/config.js底部导出了genConfig方法，转到定义中。第一行中定义了 otps=builds[name]，继续跳转到build定义可以发现builds是一个对象，里面定义了入口和出口文件，但是在根目录下并不存在web目录。那么继续再跳转到resolve的定义位置。在resolve中截取了数组下标[0]，再从aliases中获取，由此可继续跳转到aliases.js文件中，便可发现目录就在src/platforms/web中，再通过path.resolve拼接成绝对路径

  