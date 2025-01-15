<script setup>
import {onMounted, ref} from "vue";
import axios from 'axios';
import {ElMessage} from "element-plus";

const configText = ref("");

const fetchMessage = async () => {
	try {
		const response = await axios.get("http://192.168.0.102:9002/config");
		configText.value = JSON.stringify(response.data, null, 4);
		ElMessage.success("成功获取配置信息")
	} catch (err) {
		console.log(err.message)
		ElMessage.error("获取配置信息失败");
	}
};

const postMessage = async () => {
	try {
		const config = JSON.parse(configText.value);
		await axios.post("http://192.168.0.102:9002/config", config);
		ElMessage.success("成功保存配置信息")
	} catch (err) {
		console.log(err.message);
		ElMessage.error("保存配置信息失败");
	}
}

onMounted(() => {
	fetchMessage()
});
</script>

<template>
	<h1>配置信息修改</h1>
	<el-input v-model="configText" :rows="30" style="width: 500px" type="textarea"/>
	<br>
	<el-button type="primary" @click="fetchMessage">刷新</el-button>
	<el-button type="success" @click="postMessage">保存</el-button>
</template>

<style scoped>
h1 {
	display: flex;
	justify-content: center;
	align-content: center;
}

</style>