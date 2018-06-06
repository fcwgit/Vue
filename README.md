# Vue

!:自动构建html

1、安装服务器node.js

2、 Ctrl + ~  启动控制台

3、全局安装服务器  sudo npm install -g live-server

4、启动server：live-server

5、npm init：初始化一下项目，在项目目录生成package.json文件

6、新建helloworld.html文件
7、创建Vue对象，并输出data


========= v-if  v-else  v-show =============
3、v-if 和v-show的区别：
v-if： 判断是否加载，可以减轻服务器的压力，在需要时加载。
v-show：调整css dispaly属性，可以使客户端操作更加流畅。

============ v-for ============
v-for遍历，并通过{{}} 输出

注意：computed对data中的数据进行处理，需要使用新的变量接收
data:{
                items:[1,2,4,3,6,8,7]
            },
            computed:{
                itemsComputed:function(){
                    return [1,2,3,4,5,6,7,8];
                }
            }
对数组排序
data:{
                items:[1,2,4,7,6,8,3]
            },
            computed:{
                sortItems:function(){
                    return this.items.sort();
                }
            }
需要使用新变量进行接收

自定义数字排序函数
function sortNumber(a,b){
            return a>b;
        }
调用排序函数
computed:{
                sortItems:function(){
                    return this.items.sort(sortNumber);
                }
            }

遍历对象
data:{
                items:[1,2,4,7,26,8,3],
                students:[
                    {name:'zhangsan',age:33},
                    {name:'lisi',age:32},
                    {name:'wangwu',age:43},
                    {name:'zhaoliu',age:13}
                ]
            },
<ul>
            <li v-for="student in students">
                {{student.name}}——{{student.age}}
            </li>
        </ul>
输出对象序号
<ul>
            <li v-for="(student,index) in students">
                {{index}}={{student.name}}——{{student.age}}
            </li>
        </ul>

//数组对象方法排序:
        function sortByKey(array,key){
            return array.sort(function(a,b){
                var x=a[key];
                var y=b[key];
                return ((x<y)?-1:((x>y)?1:0));
            });
        }
sortStudent:function(){
                    return sortByKey(this.students,'age');
                }
 <ul>
            <li v-for="(student,index) in sortStudent">
                {{index}}={{student.name}}——{{student.age}}
            </li>
        </ul>               

=================v-text v-html=====================

<span>{{message}}</span>有弊端，如果js出错，抛出的错误很不友好
会直接输出{{message}}

<div id="app">
        <span>{{message}}</span>
        =
        <span v-text="message"></span>
    </div>

如果message出现问题，或者网速慢，不会显示{{message}}

data:{
                message:'hello world!',
                dodo:'<h2>Hello World</h2>'
            }
<span>{{dodo}}</span>，不会解释执行dodo的值，直接显示 “<h2>Hello World</h2>”

<span v-html="dodo"></span>解析HTML标签
注意：这样存在注入攻击的漏洞xss

=================v-on=====================
methods:{
                jiafen:function(){
                    this.fenshu++;
                },
                jianfen:function(){
                    this.fenshu--;
                }
            }
本场比赛得分：{{fenshu}}
        <p>
            <button v-on:click="jiafen">加</button>
            <button v-on:click="jianfen">减</button>
        </p>

绑定事件
<input type="text" v-on:keyup.enter="onEnter" v-model="fenshu2">
onEnter:function(){
                    this.fenshu += parseInt(this.fenshu2);
                }
注意：可以使用键盘码代替，例如：enter——>13

=================v-model=====================
双向数据绑定
<div id="app">
        <p>{{message}}</p>
        <p><input type="text" v-model="message"></p>
    </div>
懒加载模式
<div id="app">
        <p>原始文本信息：{{message}}</p>
        <h3>文本框</h3>
        <p><input type="text" v-model.lazy="message"></p>
    </div>
必须为数字
<p><input type="text" v-model.number="message"></p>
去空格
<p><input type="text" v-model.trim="message"></p>

<h3>文本域</h3>
<textarea cols="30" rows="10" v-model="message"></textarea>
<h3>多选框绑定一个值</h3>
        <input type="checkbox" id="isTrue" v-model="isTrue">
        <label for="isTure">{{isTrue}}</label>

<p>
            <input type="checkbox" id="jspang" value="jspang" v-model="web_names">
            <label for="isTure">jspang</label>
            <input type="checkbox" id="panda" value="panda"  v-model="web_names">
            <label for="isTure">panda</label>
            <input type="checkbox" id="panpan" value="panpan"  v-model="web_names">
            <label for="isTure">panpan</label>
        </p>
        <p>{{web_names}}</p>
data:{
                message:'hello world!',
                isTrue:true,
                web_names:[]
            }
<h3>单选框绑定</h3>
        <p>
            <input type="radio" id="one" value="男" v-model="sex">
            <label for="one">男</label>
            <input type="radio" id="two" value="女" v-model="sex">
            <label for="two">女</label>
            <p>你选择的性别是:{{sex}}</p>
        </p>
=================v-bind=====================
绑定标签的属性
<p><img v-bind:src="imgSrc" alt="" width="200px"></p>

data:{
                message:'hello world!',
                imgSrc:'http://jspang.com/wp-content/uploads/2018/04/vuekoa2.jpg',
                webUrl:'http://www.jspang.com',
                className:'classA',
                isOk:false
            }

绑定class中的判断
<div :class="{classA:isOk}">2、绑定class中的判断</div>
data:{
                message:'hello world!',
                imgSrc:'http://jspang.com/wp-content/uploads/2018/04/vuekoa2.jpg',
                webUrl:'http://www.jspang.com',
                className:'classA',
                isOk:false
            }
<div :class="isOk?classA:classB">4、三元运算符</div>

<div :style="{olor:red,font-size:font}">5、绑定style</div>

<div :style="{color:red,fontsize:font}">5、绑定style</div>
classA:'classA',
classB:'classB',
red:'red',
font:'20px'

<div :style="styleObject">6、绑定style对象</div>
styleObject:{
                    color:'green',
                    fontSize:'24px'
                }
 注意：在css中font-size这样写。
 在Vue中不支持此种写法，必须为小驼峰写法               







