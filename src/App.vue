<script setup>
import { ref } from "vue";
import axios from 'axios';

const message = ref("");

const fetchMessage = async () => {
	try {
		const response = await axios.get("http://192.168.0.102:9002/config");
		message.value = response.data;
		console.log("响应数据:", response.data); // 打印响应数据
		console.log("响应头:", response.headers); // 打印响应头
	} catch (err) {
		console.error("访问失败", err);
		if (err.response) {
			console.error("响应状态码:", err.response.status);
			console.error("响应头:", err.response.headers);
		}
	}
};
</script>

<template>
	<h1>接收信息</h1>
	<p>{{ message }}</p>
	<button @click="fetchMessage">刷新</button>
</template>

<style scoped>
</style>