# lerna-flow

## 初始化

```bash
    # 1. 全局安装 lerna
    npm i lerna -g

    # 2. 创建项目文件夹 && 进入该目录
    mkdir lerna-flow && cd $_

    # 3. 初始化项目（两种方式）
    # 方式一： 第一种方式初始化后，lerna.json 文件中“version”:"independent"
    #   每次publish时，都会得到提示，提示每个已更改的包，以指定是补丁、次要更改、主要更改还是自定义更改。
    ① lerna init --independent

    # 方式二：（固定模式），在publish的时候，会在 lerna.json 文件里面 "version":"0.1.5"，依据这个版本号进行增加，只选择一次，其他有改动的包自动更新版本号。
    #   vue、babel都是用的这种
    ② npm lerna init

```

## 创建包
```bash
    # 1. 根目录的 lerna.json
    "packages": [
        "packages/*",
        "packages/sub/*"
    ],

    # 2. 创建包
    # 创建一个 alpha 的包,默认放在packages[0]所指位置
    lerna create alpha

    # 创建一个 subpackage 包 指定放在 packages/sub 文件夹下，注意必须在 lerna.json 中的 packages 数组中写入 packages/sub 。 看上面
    lerna create subpackage packages/sub
```

## 查看包列表

```bash
    # 列出所有的包，如果与你文件里面的不符，进入那个包，运行 yarn init -y 解决
    lerna list
```

## 安装依赖
### 1. 添加依赖
```bash
    # lerna add <package>[@version][--dev][--exact]
    #   增加本地或者远程package作为当前项目packages里面的依赖
    #   --dev devDependencies 代替 dependencies
    #   --exact 安装准确版本，就是安装的包版本前面不带 ^ ，例如：“^2.20.0” -> "2.20.0"

    lerna add vue --scope=alpha
    lerna add react --scope=beta
    lerna add webpack --scope=work
    lerna add antd --scope=sub/subpackage
```
### 2. 安装依赖
```bash
    lerna bootstrap
    # 默认是 npm install，可以指定为 yarn。
```

### 3. 项目包建立软链
```bash
    # 项目包建立软链，类似 npm link
    lerna link 
    lerna link --force-local
```

### 4. 删除依赖
```bash
    # 删除所有包的 node_modules 目录
    lerna clean
```

## 发布
### 查看变化
> 列出下次发版 lerna publish 要更新的包。
原理：
需要先 git add，git commit 提交。
然后内部会运行 git diff --name-only v版本号，搜集改动的包，就是下次要发布的。并不是网上说的所有包都是同一个版全发布

```bash
    lerna changed
```

### 发布测试版本
```bash
    # 发布测试版本
    lerna publish --dist-tag alpha
```

### 发布正式版本
```bash
    # 发布正式版本
    lerna publish --conventional-commits --conventional-graduate --force-publish=@liepin/im-basic --dist-tag next 

```