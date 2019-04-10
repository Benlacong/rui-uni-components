<template>
	<scroll-view class="rui-sticky-content" scroll-y="true">
		<ruiNavber :navberList="navberList" @navbertap="navbertap" :status="status"></ruiNavber>
	</scroll-view>
</template>

<script>
	import ruiNavber from '@/components/rui-navber/rui-navber.vue';
	export default {
		data() {
			return {
				status: 0,
				navberList:[
					{
						"navberStatus":"0",
						"text":"全部"
					},
					{
						"navberStatus":"1",
						"text":"待服务"
					},
					{
						"navberStatus":"2",
						"text":"待支付"
					},
					{
						"navberStatus":"3",
						"text":"待评价"
					}
				]
			}
		},
		components: { ruiNavber },
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
	.rui-navber-li text{
		height: 82upx;
		box-sizing: border-box;
		display: flex;
		align-items: center;
		justify-content: center;
		border-bottom: 3px solid #fff;
	}
	.rui-navber-li{
		height: 82upx;
		font-size: 30upx;
	}
	.rui-navber-li.rui-active text{
		border-bottom: 3px solid #2ED39E;
	}
</style>
