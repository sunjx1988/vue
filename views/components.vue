<!DOCTYPE html>
<html>
<head>
    <title></title>
    <meta charset="utf-8">
    <script type="text/javascript" src="../js/vue/vue.min.js"></script>
    <style type="text/css">
    </style>
</head>

<body>
<div id="vueroot">
    <input v-model="msg" />
    <my :content="msg"></my>
    <counter v-on:total='totalhandle'></counter>
    <counter v-on:total='totalhandle'></counter>
    <counter v-on:total='totalhandle'></counter>
    total: {{totalCount}}
</div>
</body>

<script type="text/javascript">
    //注册一个全局组件
    Vue.component("my",{
        //组件的属性,类似参数功能
        props: ["content"],
        template: "<div>{{content}}</div>"
    });

    //注册一个全局组件
    Vue.component("counter",{
        template: "<button @click='countMethod'>{{count}}</button>",
        data:function(){
            return {
                count: 0
            }
        },
        methods: {
            countMethod: function () {
                this.count ++;
                //触发自身的total事件,进而调用totalhandle方法
                this.$emit('total');
            }
        }
    });

    //创建根实例以解析自定义组件
    new Vue({
        el: "#vueroot",
        data: {
            msg: "",
            totalCount: 0
        },
        methods: {
            totalhandle: function () {
                this.totalCount ++;
            }
        }
    });
</script>
</html>