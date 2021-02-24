# github子模块使用

### 子模块说明

`.gitmodules` 文件该配置文件保存了项目 URL 与已经拉取的本地目录之间的映射

### 添加子模块

`git submodule add ` 命令后面加上想要跟踪的项目的相对或绝对 URL 

例：`$ git submodule add https://github.com/chaconinc/DbConnector`

### 查看子模块

`git submodule`

### 删除子模块

`git submodule deinit subPath/`

`git rm subpath`

`rm -rf .got/modules/subPath`

### 克隆包含子模块的项目

- 方式一：

  1. `git clone`  克隆主项目
  2. `git submodule init` 始化本地配置文件
  3. `git submodule update` 则从该项目中抓取所有数据
  4. 可以执行`git submodule update --init --recursive` 同时执行3、4步

- 方式二：

  ​	执行`$ git clone --recurse-submodules url` 命令克隆项目