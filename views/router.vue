<!DOCTYPE html>
<html>
<head>
    <title></title>
    <meta charset="utf-8">
    <script type="text/javascript" src="../js/vue/vue.min.js"></script>
    <script type="text/javascript" src="../js/vue/vue-router.min.js"></script>
    <style type="text/css">
        .my_active{
            color: red;
        }
        ._active{
            background-color: aqua;
        }
    </style>
</head>

<body>
    <div id="vueroot">
        <!-- 使用 router-link 组件来导航. -->
        <!-- 通过传入 `to` 属性指定链接. -->
        <!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->
        <ul>
            <li><router-link to="/a">a</router-link></li>
            <li><router-link to="/b">b</router-link></li>
            <!-- 设置被激活的链接的class -->
            <li><router-link to="/c" active-class="my_active">active-class</router-link></li>
            <!-- 设置精确匹配时候的class -->
            <li><router-link to="/d" exact-active-class="_active">exact-active-class</router-link></li>
            <!-- 带查询参数，下面的结果为 /q?uname=sun -->
            <li><router-link :to="{ path: 'q', query: { uname: 'sun' }}">query_uname</router-link></li>
            <!-- 渲染为li标签,同样监听路由事件 -->
            <router-link to="/a" tag="li">tag=li</router-link>
            <!-- 声明可以触发路由的事件 -->
            <router-link to="/a" event="mouseover">event=mouseover</router-link>
        </ul>
        <!-- 路由出口 -->
        <!-- 路由匹配到的组件将渲染在这里 -->
        <router-view></router-view>
    </div>
</body>
<script>
    const a = {template: "<div>a</div>"};
    const b = {template: "<div>b</div>"};
    const c = {template: "<div>c</div>"};

    const routes = [
        {path: "/a", component: a},
        {path: "/b", component: b},
        {path: "/c", component: c}
    ];

    const router = new VueRouter({routes});

    new Vue({router}).$mount('#vueroot');
</script>
</html>