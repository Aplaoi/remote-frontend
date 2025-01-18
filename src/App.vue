<script setup>
import {onMounted, ref} from "vue";
import axios from 'axios';
import {ElMessage} from "element-plus";

const configText = ref("");
const imageSrc = ref("");
const url = "http://192.168.0.105:9002";

const fetchMessage = async () => {
	try {
		const response = await axios.get(url + "/config");
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
		await axios.post(url + "/config", config);
		ElMessage.success("成功保存配置信息")
	} catch (err) {
		console.log(err.message);
		ElMessage.error("保存配置信息失败");
	}
}

const fetchVideoStream = async () => {
	try {
		const res = await axios.get(url + "/video", {responseType: "blob"});
		imageSrc.value = URL.createObjectURL(res.data);
		fetchVideoStream();
	} catch (err) {
		console.log("获取图片流失败" + err);
	}
}

onMounted(() => {
	fetchMessage();
	fetchVideoStream();
});
</script>

<template>
	<h1>配置信息修改</h1>
	<el-row>
		<el-col>
			<el-input v-model="configText" :rows="30" style="width: 500px" type="textarea"/>
			<br>
			<el-button type="primary" @click="fetchMessage">刷新</el-button>
			<el-button type="success" @click="postMessage">保存</el-button>
		</el-col>
		<el-col>
			<el-image :src="imageSrc" fit="cover"></el-image>
		</el-col>
	</el-row>

</template>

<style scoped>
h1 {
	display: flex;
	justify-content: center;
	align-content: center;
}

</style>