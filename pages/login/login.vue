<template>
	<view class="content">
		<view class="toptex">
			<view class="tex">{{ act == 1 ? '账号登录' : '手机号登录' }}</view>
			<view class="tex-right">
				<text @click="checkeng" class="tex-content">{{ act == 0 ? '账号登录' : '手机号登录' }}</text>
				<text class="iconfont icon-caret"></text>
			</view>
		</view>
		<ZH v-show="act==1"></ZH>
		<SJ v-show="act==0"></SJ>
	</view>
</template>

<script setup lang="ts">
import ZH from './components/Cmobile.vue';
import SJ from './components/Caccount.vue';
import { ref } from 'vue';

const act = ref(0);

const checkeng = () => {
	act.value = !act.value;
};
</script>

<style lang="scss">
.toptex {
	width: 90%;
	margin: 5%;
	display: flex;
	justify-content: space-between;
	align-items: baseline;
	.tex {
		font-weight: 700;
		font-size: 36rpx;
	}
	.tex-right {
		color: $uni-primary;
		font-size: $uni-font-size-base;
		display: flex;
		align-items: center;
	}
	.icon-caret {
		font-size: 50%;
		margin-left: 10rpx;
	}
}

</style>
