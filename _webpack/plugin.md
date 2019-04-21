### webpack proxy代码配置

### eslint配置

vue/cli3.x中默认安装了eslint插件，使用vs code编辑器可以安装eslint插件，配置"eslint.autoFixOnSave": true文件保存时，自动修复不符合规范的代码，不用编译时发现错误

`eslint配置`

```js
module.exports = {
  root: true,
  env: {
    node: true
  },
  'extends': [
    'plugin:vue/essential',
    '@vue/standard'
  ],
  rules: {
    'no-console': process.env.NODE_ENV === 'production' ? 'error' : 'off',
    'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off',
    "indent": [2, 2], // 缩进2个空格
    "no-const-assign": 2, // 禁止修改const声明的变量
    "no-multi-spaces": 1, // 禁止使用多余的空格
    "no-multiple-empty-lines": [1, {"max": 2}], // 空行不能超过两行
    "no-trailing-spaces": 1,  //一行结束后面不要有空格
    "eqeqeq": 2, // 必须使用全等
    "quotes": [1, "single"], //引号使用单引号
    "semi": 2, //不使用分号结尾
  },
  parserOptions: {
    parser: 'babel-eslint'
  }
}
```

`vs code配置eslint规范自动修复,包含js和vue文件`

```js
"eslint.autoFixOnSave": true,
"eslint.validate": [
    "javascript",{
        "language": "vue",
        "autoFix": true
    },"html",
    "vue"
]
```