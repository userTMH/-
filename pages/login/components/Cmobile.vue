<template>
	<view class="" style="width: 90%; margin: auto">
		<uni-forms ref="seedForm" :model="formData" :rules="rules" label-position="top">
			<uni-forms-item label="" name="account">
				<input type="text" v-model="formData.account" placeholder="请输入姓名" />
			</uni-forms-item>
			<uni-forms-item label="" name="password">
				<input type="text" v-model="formData.password" placeholder="请输入密码" />
			</uni-forms-item>
		</uni-forms>
		<button type="default" class="button" @click="submit">登录</button>
	</view>
</template>

<script setup lang="ts">
import { onReady } from '@dcloudio/uni-app';
import { reactive, ref } from 'vue';
import {login} from '@/api/login'

const seedForm = ref();
const formData = reactive({
	account: '',
	password: ''
});
const rules = reactive({
	account: {
		rules: [
			{
				required: true,
				errorMessage: '请输入账号'
			},
			{
				minLength: 3,
				maxLength: 10,
				errorMessage: '账号长度在 {minLength} 到 {maxLength} 个字符'
			}
		]
	},
	// 对email字段进行必填验证
	password: {
		rules: [
			{
				required: true,
				errorMessage: '请输入密码'
			}
		]
	}
});
onReady(() => {
	seedForm.value.setRules(rules);
});
const submit = () => {
	seedForm.value.validate((valid: any) => {
		if (!valid) {
			console.log('校验成功');
			login(formData).then(res=>{
				console.log(res);
			})
		} else {
			console.log('验证失败');
			console.log(valid);
		}
	});
};
</script>

<style lang="scss">
.uni-input {
	height: 35px;
	border: 1px solid #e5e5e5;
	border-radius: 5px;
	padding-left: 10px;
	font-size: 12px;
}
.button {
	width: 90%;
	margin: 5%;
	background-color: #ee4f3e;
	border-radius: 20px;
	color: #fff;
	border: 0;
}
</style>
