---
title: JavaScript框架vue
author: Xin Lu
date: '2023-04-09'
slug: JavaScript框架vue
categories: []
tags: []
---

### JavaScript框架vue

---



#### el ：命中标签

##### 可在命中标签下任意使用，使用id选择器，一般挂载在div标签，其他标签有渲染效果

```
el:'.app'   命中class选择器
el:'#app'   命中id选择器
```

---

#### data:定义数据

- 字符串	
- 对象：通过点来获取
- 列表
- 数组





#### v-text指令:

##### 普通文本

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div class='ap' id="app">
        {{masasge}}
        <h2 v-text="masasge"></h2>
    </div>
    <!-- 导入vue -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app =new Vue({
            el:'.ap',
            data:{
                masasge:'hello',

            }
        })
    </script>
</body>
</html>
```

---



#### v-html指令：

##### 可以解析普通文本和html语法结构

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div class='ap' id="app">
        {{masasge}}
        <!-- 比较 v-text 和 v-html 的不同 -->
        <h2 v-text="content"></h2>
        <h2 v-html='content'></h2>
        <h2 v-text="masasge"></h2>
        <h2 v-html='masasge'></h2>
    </div>
    <!-- 导入vue -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app =new Vue({
            el:'.ap',
            data:{
                masasge:'hello',
                content:'<a href="https://kawasakih299.netlify.app/" >netlify</a>'

            }
        })
    </script>
</body>
</html>
```

---



#### v-on:事件绑定标签

##### 为元素绑定事件

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div class='ap' id="app">
        {{masasge}}
        <input type="button" value="v-on指令" v-on:click="doIt">
        <!--  v-on:click  简写-->
        <input type="button" value="v-on指令" @click="doIt">
        <!-- 双击才能触发 -->
        <input type="button" value="双击事件" @dblclick="doIt">
    </div>
    <!-- 导入vue -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app =new Vue({
            el:'.ap',
            methods:{
                doIt:function(){
                    alert('v-on指令');
                }
            },
        })
    </script>
</body>
</html>
```

---



#### v-show:控制显示状态（操作样式）

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div class='ap' id="app">
        {{masasge}}
        <input type="button" value="点击查看" @click="changeshow">
       <img v-show="isshow" src="../images/all_box_background.jpg" alt="mylife">
    </div>
    <!-- 导入vue -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app =new Vue({
            el:'#app',
            data:{
                isshow:false
            },
            methods:{
                changeshow:function(){
                    this.isshow = ! this.isshow;
                }
            },

        })
    </script>
</body>
</html>
```

---

#### v-for：响应式数据列表结构

响应的数据有：

- 数组
- 对象
- 迭代器
- 数字
- 字符串

---

#### vue:this对象的理解

````
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div class='ap' id="app">
        <input type="button"value="搜索歌曲" @click="search">
        <li v-for="item in songlist" >
            <b>{{ item.name }}</b>

        </li>
    </div>
    <!-- import vue -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <!-- import axios -->
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script>
        var app =new Vue({ 
            el:'#app',
            data:{
                songlist:[],
                arr :[1,2,3,4,5,6,7,8,9]
            },
            methods:{
                search:function(){
                    // 创建一个新的对象
                    var that = this
                    axios.get('https://autumnfish.cn/search?keywords=失语者').then(function(response){
                
                        console.log(songlist[0].name), 
                        // 将返回的数据给新的对象，此时this的值是刚创建时的空列表
                        that.songlist = response.data.result.songs            
                    },function(err){
                        console.log(err)
                    })
                },
                
            }
        })
    </script>
</body>
</html>
````

---



#### v-mode：获取用户的输入

##### 实现数据双向绑定：更改两边的任意一边，数据都会发生改变

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div class='ap' id="app">
        <input type="text" v-model="massage">
        <h2>{{ massage }}</h2>
    </div>
    <!-- import vue -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <!-- import axios -->
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script>
        var app = new Vue({
            el:'#app',
            data:{
                massage:'hello javascript JavaScript',
            }
        })

    </script>
</body>
</html>
```

---

#### @keyup.enter:监听键盘回车事件

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div class='ap' id="app">
        <input type="text" v-model="massage" @keyup.enter='enter_search()'>
        <h2>{{ enter_words }}</h2>
    </div>
    <!-- import vue -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <!-- import axios -->
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script>
        var app = new Vue({
            el:'#app',
            data:{
                massage:'hello javascript JavaScript',
                enter_words:'',
            },
            methods:{
                enter_search:function(){
                    var that = this;
                    that.enter_words = 'https://autumnfish.cn/search?keywords='+ that.massage
                }
            }
        })

    </script>
</body>
</html>
```





 
