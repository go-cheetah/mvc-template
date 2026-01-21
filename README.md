# mvc

项目启动

```bash
go install github.com/swaggo/swag/cmd/swag@latest
swag init -g cmd/app/main.go
go run cmd/app/main.go
```


> 个人理解： golang 主推荐比较简单的代码，并且自由风格。所以，只要代码框架是OK的，随性写代码都行。

## 代码目录结构

```bash
.
├── bin                                   # 生成的二进制文件
├── build                                 # 构建相关的脚本或者内容
│   └── Dockerfile
├── cmd                                   # 程序的入口
│   └── app                               # app1 取名例如前台就叫  front，后台叫 backend，一个目录一个入口
│       ├── app                           # app 固定词
│       │   ├── options                   # 处理选项
│       │   │   └── options.go            # 处理选项，处理一些初始化操作
│       │   └── server.go                 # 基本上可以认为是入口函数
│       └── main.go                       # 入口函数，具体的实现都在上面的server之中
├── config                                # 默认配置文件
│   └── config.yaml                       # 默认配置文件
├── docs                                  # 接口文档,主要是swagger
├── go.mod                                # go.mod
├── internal                              # 内部资源，外部不允许调用  请查看 https://golang.org/doc/go1.4#internalpackages
│   ├── config                            # 配置文件，主要就是设置一下配置的相关结构体之类
│   │   ├── config.go                     # 配置项
│   │   ├── db.go                         # 数据库的配置项
│   │   ├── log.go                        # 日志的配置项
│   │   └── server.go                     # 服务器配置项
│   ├── handler                           # handler函数，主要处理业务逻辑
│   │   └── health                        # 案例
│   │       ├── handler.go                # handler函数
│   │       ├── res
│   │       │   └── response_code.go      # 错误码，可注册
│   │       └── service.go                # service层
│   ├── model                             # model层，数据结构，操作内容在repository
│   │   ├── health.go     
│   │   └── model.go     
│   ├── pkg                               # 跟上面的pkg一样的说法，不推荐，但是很多代码库有这个习惯，看个人使用，这里是可以其他代码库进行调用
│   │   ├── migration                     # migrate内容
│   │   │   ├── migration.go              # migrate的初始化操作
│   │   │   └── model.go                  # model层
│   │   └── response                      # 响应内容
│   │       ├── common.go                 # 响应内容
│   │       └── response.go               # 响应内容
│   ├── repository                        # 数据库操作
│   │   └── health                        # health内容
│   │       ├── client.go                 # 数据库操作客户端，以及对数据库的crud
│   │       ├── migrate.go                # migrate的初始化操作
│   │       ├── mock.go                   # 测试mock数据
│   │       ├── repository.go             # repository层，接口层
│   │       └── types.go                  # 定义常量等内容
│   └── server                            # 这里也可以改成api， 主要就是上面的入口函数调用的地方，其他的函数主要作用是插件，这里是主要处理逻辑部分
│       ├── migrate.go                    # 处理repository层的migrate
│       ├── router.go                     # 路由在这里，通过传参的方式把配置文件等服务传到handler进行使用
│       └── server.go                     # web框架入口
├── pkg                                   # 跟上面的pkg一样的说法，不推荐，但是很多代码库有这个习惯，看个人使用，这里是可以其他代码库进行调用
│   ├── cors                              # 跨域
│   │   ├── config.go     
│   │   ├── cors.go     
│   │   └── utils.go     
│   ├── database                          # orm，数据库相关，例如MySQL
│   │   ├── gorm.go     
│   │   ├── mysql.go     
│   │   └── sqlite.go     
│   ├── generator                         # id生成器
│   │   └── id.go     
│   ├── log                               # 日志库
│   │   └── log.go     
│   └── pkg.go                            # pkg空文件，查看 https://github.com/golang-standards/project-layout/issues/10 只看讨论即可
└── README.md                             # readme内容
```

## 使用模块

|功能|工具|
|---|---|
| web框架 | `github.com/gin-gonic/gin` |
| 数据库2 | `github.com/go-gorm/gorm` |
| 日志 | `go.uber.org/zap` |
| 命令行 | `github.com/urfave/cli/v2` |
| 配置 | `github.com/spf13/viper` |
| id生成器 | `github.com/sony/sonyflake` |
