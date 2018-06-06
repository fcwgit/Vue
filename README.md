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

======================================