# mini-webpack

## a simple webpack achieve

## mini-webpack can do these now
- [x] supports package
- [x] supports package watch
- [x] supports loader
- [x] supports plugins
- [x] adding hrm....
### UseAge
#### build.js
```js
//you can see example to see a simply use 
//build.js use this file to pack your program
const { webpack } = require('../dist/mini-webpack.cjs.js') //import module
const webpackConfig = require('./webpack.config.js') //import your config
const compiler = webpack(webpackConfig) //create a webpack compiler
compiler.run((err, result) => { //use run function to compile when finished will call callback
})
```
#### webpack.config.js
```js
const { load1, load2 } = require('./loaders') //use your loaders
const { WebPackRunPlugin, WebPackDonePlugin } = require('./plugin') //use your plugins
module.exports = {
    entry: './src/main.js', //pack input
    output: {               //pack output
        path: './dist',
        filename: 'bundle.js'
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                use: [load1,load2]
            }
        ]
    },
    plugins: [new WebPackRunPlugin(), new WebPackDonePlugin()]
}
```
#### use loader
```js
//you can use loader in config
//define your function loader like this
function load1(source) { //source is  code souce when compile
    return source + '\n //add load1'
}
```
#### use plugins
```js
//you can use plugins in config
//define your class plugin like this
class WebPackRunPlugin { //plugin class must have a method called apply
    apply(compiler) { //argument is complier when complie
        compiler.hooks.run.tap('plugin1', () => {
            console.log('run plugin run');
        })
    }
}
```
