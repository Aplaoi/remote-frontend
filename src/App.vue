<script setup>
	import {ref} from "vue";
	import axios from 'axios';
	const message=ref("")
	const fetchMessage=async ()=>{
		try{
			const response=await axios.get("http://192.168.230.197:8080/message");
			message.value=response.data;
		}catch (err){
			console.error("访问失败",err)
		}
	};
</script>

<template>
	<h1>接收信息</h1>
	<p>{{message}}</p>
	<button @click="fetchMessage">刷新</button>
</template>

<style scoped>


</style>
