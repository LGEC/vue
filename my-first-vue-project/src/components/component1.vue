<template>
  <div class="hello">
    <h1>{{ title }}</h1>
    <h1>{{msgFromfather}}</h1>
    <button @click="click1">Click</button> 
  </div>
</template>

<script>
export default {
  data:function(){
  	return{
  		title:"in compontent 1！"
  	}
  },
  events:function (msg) {
  	console.log(events)
  },
  props:['msgFromfather'],
  methods:{
  	click1:function (e) {
  		console.log(this.msgFromfather)
  		this.$emit('child-tell',this.msgFromfather);  //emit方法   子组件往父组件传值
  	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
