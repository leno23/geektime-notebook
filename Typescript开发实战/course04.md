### 第一个HelloWorld程序

创建工程目录

```
mkdir ts-action
cd ./ts-action
```

初始化工程

```
npm init -y
```

安装typescript

```
npm install typescript -g
```

初始化配置文件

```
tsc --init
```

新建index.ts

```tsx
let hello:string = 'hello TypeScript'
```

编译index.ts文件

```
tsc ./index.ts
```

安装依赖

```
npm install webpack webpack-cli webpack-dev-server -D
```

安装loader

```
npm install ts-loader typescript -D
```

安装插件

```
npm install html-webpack-plugin clear-webpack-plugin
```

创建webpack配置文件

./build/webpack.base.config.js

```js
 module.exports = {
    entry:'./src/index.js', // 入口
    output:{
        filename:'app.js'   // 生成的文件名，目录默认为/dist
    },
    module:{
        rules:[
            {
                // ts或tsx文件使用ts-loader解析
                test:/\.tsx?$/i,
                use:[
                    {loader: 'ts-loader'}
                ],
                // 不对node_modules目录进行处理
                exclude:/node_modules/
            }
        ]
    },
    plugins:[
        // 指定文件作为项目html模板
        new HtmlWebpackPlugin({
            template:'./src/index.html'
        })
    ]
}
```

./build/webpack.dev.config.js

```javascript
module.exports = {
	// 各个字段的含义：
	// cheap 忽略文件列信息
	// module定位到ts源码，而不是编译后的js
	// 会将sourcemap以dataurl形式打包到文件中，重编译速度快
	devtools:'cheap-module-eval-source-map'
}
```

./build/webpack.prod.config.js

```js
const {CleanWebpackPlugin} = require('clean-webpack-plugin')

// 为了避免缓存，通常我们会将打包后的文件加上hash值，这样的话，在多次打包会生成会很多冗余文件，占用资源。该插件可以在每次构建前清空dist目录
module.exports = {
	plugins:[
		new ClearWebpackPlugin()
	]
}
```

./build/webpack.config.js

```js
const merge = require('webpack-merge')
const baseConfig = require('./webpack.base.config.js')
const devConfig = require('./webpack.dev.config.js')
const prodConfig = require('./webpack.prod.config.js')

let config = process.env.NODE_ENV === 'development' ? devConfig : prodConfig
module.exports = merge(baseConfig, config)
```

安装webpack-merge

```
npm i webpack -D 
```

package.json

```json
{
    "scripts":{
        "start":"webpack-dev-server --mode=development --config ./build/webpack.config.js",
        "build":"webpack --mode=production --config ./build/webpack.config.js"
    }
}
```



