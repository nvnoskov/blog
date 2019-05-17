+++
date = "2016-04-06T09:50:54+06:00"
draft = false
title = "redux"

+++

### Команды
```
mkdir kursapp
cd kursapp/
mkdir client server common static
npm init
npm i --save react react-dom axios react-router redux react-redux express redux-thunk react-router-redux
npm i --save-dev webpack webpack-dev-server babel-{core,loader,register,preset-react,preset-stage-0,preset-es2015} react-hot-loader
echo '{"presets":["es2015","react","stage-0"]}' > .babelrc

```

#### webpack.dev.config.js
```
var webpack = require('webpack')

module.exports = {
    entry: [
        'webpack-dev-server/client?http://127.0.0.1:8282/',
        'webpack/hot/only-dev-server',
        './client/index'
    ],
    output: {
        filename: 'static/bundle.js'
    },
    module:{
        loaders:[
            {
                test: /\.jsx?$/,
                exclude: /node_modules/,
                loaders:[
                    "react-hot",
                    "babel"
                ]
            }
        ]
    },
    plugins:[
        new webpack.HotModuleReplacementPlugin(),
    ]

}

```
