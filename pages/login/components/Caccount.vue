<template>
	<view class="" style="width: 90%; margin: auto">
		<uni-forms ref="form" :modelValue="formData" :rules="rules">
			<uni-forms-item label="" name="name">
				<uni-easyinput type="text" v-model="formData.name" placeholder="请输入手机号" />
			</uni-forms-item>
			<uni-forms-item label="" name="email" style="position: relative">
				<uni-easyinput style="width: 70%" type="text" v-model="formData.email" placeholder="请输入验证码" />
				<view @click="capt" class="image" style="position: absolute; right: 5%; top: 30%">获取验证码</view>
			</uni-forms-item>
		</uni-forms>
		<button type="default" class="button">登录</button>
	</view>
</template>

<script setup lang="ts">
import { reactive } from 'vue';
import { captcha } from '../../../api/login';

const formData = reactive({
	name: '',
	email: ''
});
const rules = reactive({
	name: {
		rules: [
			{
				required: true,
				errorMessage: '请输入手机号'
			},
			{
				minLength: 11,
				errorMessage: '手机长度最少{minLength}个字符'
			}
		]
	},
	// 对email字段进行必填验证
	email: {
		rules: [
			{
				format: 'email',
				errorMessage: '请输入验证码'
			}
		]
	}
});
const capt = () => {
	captcha({
		key: 12345678
	}).then((res) => {
		console.log(res);
	});
};
</script>

<style lang="scss">
.button {
	width: 90%;
	margin: 5%;
	background-color: #ee4f3e;
	border-radius: 20px;
	color: #fff;
	border: 0;
}
</style>
