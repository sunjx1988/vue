<!DOCTYPE html>
<html>
<head>
	<title></title>
	<meta charset="utf-8">
	<script type="text/javascript" src="../js/vue/vue.min.js"></script>
	<style type="text/css">
		.class1{color: red;}
	</style>
</head>
<body>
<div id="userInfo">
	<h1>uname:{{uname}}</h1>
	<h1>age:{{age}}</h1>
</div>

<hr/>
<div id="bindHtml" v-html="bhtml">
	
</div>

<hr/>
<div id="vBind">
	<p v-bind:class="{'class1':hasClass1}">v-bind:用来绑定html元素属性，如 class v-bind:class="{'class1':hasClass1}"</p>
</div>

<hr/>
<div id="vif">
	<div v-if="show">show</div>
	<div v-if="hide">hide</div>
</div>

<hr/>
<div id="vhref">
	<a v-bind:href="href">v-bind:href</a>
	<a :href="href">v-bind:href</a>
</div>

<hr/>
<div id="vclick">
	<a v-on:click="click" href="javascript:;">v-on:click</a>
</div>

<hr/>

<hr/>
<div id="vmodel">
	<p>input:<input type="text" v-model="message" />{{message}}</p>
</div>

<hr/>
<div id="reverse">
	<a href="javascript:;" v-on:click="reverse">{{message}}</a>
	<a href="javascript:;" @click="reverse">{{message}}</a>
</div>

<hr/>
<div id="filter">
	<input v-model="message" />{{message|upcase}}
</div>

<hr/>
<div id="each">
	<ul>
		<li v-for="e in list">{{e}}</li>
	</ul>

	<ul>
		<li v-for="e in list2">{{e}}</li>
	</ul>

	<ul>
		<li v-for="(v, k) in list2">{{k}} {{v}}</li>
	</ul>

	<ul>
		<li v-for="(v, k, i) in list2">{{i}} {{k}} {{v}}</li>
	</ul>
</div>

<hr />
<div id="computed">
	<input v-model="message" />message:{{message}} / upcaseMessage: {{upcaseMessage}} / upcaseMessageMeshod: {{upcaseMessageMeshod()}}
	<br/>
	<input v-model="message2" />name & age:{{message2}} / name:{{name}} / age:{{age}}
</div>

<hr/>
<div id="watch">
	<input v-model="message" />message:{{message}}
</div>
.
<hr/>
<div id="input">
	<input v-model="sex" type="radio" name="sex" value="male"/>male  <input v-model="sex" type="radio" name="sex" value="female"/>female  选中：{{sex}}<br/>
	<input v-model.number="age" type="checkbox" name="age" value="10" /> 10
	<input v-model.number="age" type="checkbox" name="age" value="20" /> 20
	<input v-model.number="age" type="checkbox" name="age" value="30" /> 30 选中：{{age}}<br/>
	<select v-model="city" name="city">
		<option value="shanghai">上海</option>
		<option value="beijing">北京</option>
	</select>
	选中：{{city}}<br/>
</div>

</body>
<script type="text/javascript">
	var input = new Vue({
		el: "#input",
		data: {
            sex: "male",
            age: [10,20],
			city: []
		}
	});

	var vwatch = new Vue({
		el: "#watch",
		data: {
		    message: ""
		},
		watch: {
		    message: function (newVal, oldVal) {
		        //一种监听方式
                console.log("newVal:" + newVal + ", oldVal:" + oldVal);
            }
		}
	});

	vwatch.$watch("message",function (newVal, oldVal) {
	    //另一种监听方式
		console.log("another watch：newVal:" + newVal + ", oldVal:" + oldVal);
    });

	var computed = new Vue({
		el: "#computed",
		data: {
		    message:"",
			name: "sun",
			age: 20
		},
		computed:{
		    upcaseMessage: function () {
                if(this.message) {
                    console.log("计算属性是基于缓存");
                    return this.message.toUpperCase();
                }
            },
			
			message2:{
		        set: function (newValue) {
		            if(newValue){
                        var array = newValue.split("/");
                        if(array.length > 1){
                            this.name = array[0];
                            this.age = array[1];
                        }
                    }
                },
				
				get: function () {
					return this.name + "/" + this.age;
                }
			}
			
		},
		methods: {
		    upcaseMessageMeshod: function () {
                if(this.message){
                    console.log("方法是基于实时执行方法");
                    return this.message.toUpperCase();
                }
            }
		}
	});

	var each = new Vue({
		el: "#each",
		data: {
		    list: [1,2,3],
			list2: {
		        name: "sun",
				age: 20
			}
		}
	});

	var filter = new Vue({
		el: "#filter",
		data: {
		    message: ""
		},
		filters: {
		    upcase: function (value) {
		        if(value){
                    return value.toUpperCase();
                }
            }
		}
	});


	var reverse = new Vue({
		el: "#reverse",
		data: {
		    message: "hello"
		},
		methods:{
		    reverse : function () {
				this.message = this.message.split("").reverse().join("");
            }
		}
	});
	
	var vmodel = new Vue({
		el: "#vmodel",
		data: {
		    message: ""
		}
	});

	var userVm = new Vue({
		el: "#userInfo",
		data: {
			uname: "sun",
			age: 20
		}
	});

	var bindHtml = new Vue({
		el: "#bindHtml",
		data: {
			bhtml: "<h1>this is v-html</h1>"
		}
	});

	var vbind = new Vue({
		el: "#vBind",
		data: {
			hasClass1: true
		}
	});

	var vif = new Vue({
		el: "#vif",
		data: {
			show: true,
			hide: false
		}
	});

	var vhref = new Vue({
		el: "#vhref",
		data: {
			href: "#"
		}
	});

	var vclick = new Vue({
		el: "#vclick",
		data: {
			click: function(){
				console.log("click...")
			}
		}
	});

</script>
</html>