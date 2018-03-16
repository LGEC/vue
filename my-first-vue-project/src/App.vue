
<template>
	<div id="app">
		<!--<img src="./assets/logo.png">-->
		<!--<router-view/>-->
		<h1 v-text="title"></h1>
		<input type="text" @keyup.enter="onEnter" v-model="newItem" id="" value="" />
		<ul>
			<li v-for="item in items" :class="{finish:item.isFinished}" @click="btn(item)">{{item.keys}}</li>
		</ul>
		<!--<child>{{message}}</child>-->
		<Component-w msgFromfather="you die!" @child-tell="listen"></Component-w>
	</div>
</template>

<script>
	import Store from './store'
	import ComponentW from './components/component1'
	//console.log(Stores)
	export default {
		name: 'App', 
		components:{ComponentW},
		data: function() {
			return {
				title: 'this is a todo list',
				newItem: '',
				//message:'姓名',
				items: Store.fetch()
			}
		},
		watch:{
			items:{
				handler:function (item) {
					console.log(item)
					Store.save(item)
				},
				deep:true
			}
		},
		methods: {
			btn: function(item) {
				item.isFinished = !item.isFinished
				console.log(item)
			},
			listen:function (msg) {
				console.log(msg)
			},
			onEnter: function() {
				var obj = {
					keys: this.newItem,
					isFinished: false
				};
				this.items.push(obj)
				//var str = JSON.stringify(this.items);
				//window.localStorage.setItem('items',str)
				
				this.newItem = ''; 
				//var str = window.localStorage.getItem('items')
				//console.log(str)
			},
			componentUpdated:function (newdata,olddata) {
				console.log(newdata)
				console.log(olddata)
			}
		}
	} 
</script>

<style>
	#app {
		font-family: 'Avenir', Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
		margin-top: 60px;
	}
	.finish {
		text-decoration: underline;
	}
</style>