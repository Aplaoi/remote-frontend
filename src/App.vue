<script setup>
import {onMounted, ref} from "vue";
import axios from 'axios';
import {ElMessage} from "element-plus";

const configText = ref("");
const videoUrl = ref("");
const url = "http://192.168.31.192:9002";

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

// const fetchVideoStream = async () => {
// 	try {
// 		const res = await axios.get(url + "/video", {responseType: "blob"});
// 		const newImageSrc = URL.createObjectURL(res.data);
//
// 		const img = new Image();
// 		img.src = newImageSrc;
// 		img.onload = () => {
// 			imageSrc.value = newImageSrc;
// 			// console.log("成功获取图片");
// 			setTimeout(fetchVideoStream, 33);
// 		}
// 		img.onerror = () => {
// 			console.log("图片加载失败");
// 			setTimeout(fetchVideoStream, 33);
// 		}
//
// 	} catch (err) {
// 		console.log("获取图片流失败" + err);
// 		setTimeout(fetchVideoStream, 33)
// 	}
// }

const handleError=()=>{
	console.log("获取视频流失败");
	ElMessage.error("获取视频流失败")
}


onMounted(() => {
	fetchMessage();
	videoUrl.value = `${url}/video`
});
</script>

<template>
	<h1>Debug面板</h1>
	<el-row :gutter="40">
		<el-col :span="12">
			<el-input v-model="configText" :rows="30" type="textarea"/>
			<br>
			<el-button type="primary" @click="fetchMessage">刷新</el-button>
			<el-button type="success" @click="postMessage">保存</el-button>
		</el-col>
		<el-col :span="12">
			<img :src="videoUrl" style="width: 100%; height: 500px; object-fit: cover" alt="" @error="handleError">
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