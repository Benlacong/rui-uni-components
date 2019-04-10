<template>
	<scroll-view class="rui-sticky-content" scroll-y="true">
		<form @submit="formSubmit">
			
			<view class="btn-area">
				<button class="rui-btn rui-choosetime-btn" formType="submit">确定</button>
			</view>
		</form>
	</scroll-view>
</template>

<script>
	export default {
		data() {
			return {}
		},
		components: {  },
		onLoad() {},
		methods: {}
	}
</script>

<style>
	.rui-sticky-content{
		background-color: #fff;
		box-sizing: border-box;
		padding:0 0 13.33333333vw;
		color:#6e6e6e;
		font-size:4vw;
	}
</style>
