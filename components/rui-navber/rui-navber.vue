<template>
	<view class="rui-navber-content">
		<view :class="curStatus == item.navberStatus ? 'rui-navber-li rui-active' : 'rui-navber-li'" @tap="navbertap(item.navberStatus)" :style="curStatus == item.navberStatus ? navberStyleActive : navberStyle" v-for="(item,index) in navberList" :key="index">
			<view v-if="item.selectedIconPath && item.selectedIconPath !== '' || item.iconPath && item.iconPath !== ''">
				<image class="rui-navber-img" v-if="curStatus == item.navberStatus" :src="item.selectedIconPath" mode=""></image>
				<image class="rui-navber-img" v-if="curStatus != item.navberStatus" :src="item.iconPath" mode=""></image>
			</view>
			<text>{{item.text}}</text>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'rui-navber',
		props: {
			color: {
			  type: String,
			  default: '#000000'
			},
			colorActive: {
			  type: String,
			  default: '#2ed39e'
			},
			status: {
			  type: Number,
			  default: 0
			},
			navberList: {
			  type: Array,
			  default: []
			}
		},
		data() {
			return {
				navberStyle: 'color:' + this.color,
				navberStyleActive: 'color:' + this.colorActive,
				curStatus: this.status
			}
		},
		created(){
			console.log('rui-navber 组件加载完成！')
		},
		methods: {
			navbertap(status){
				// console.log(status)
				this.curStatus = status;
				this.$emit('navbertap', status);
			}
		}
	}
</script>

<style>
	.rui-navber-content{
		display: flex;
		align-items: center;
		color:#02212d;
		font-size:3.2vw;
		background-color: #fff;
		/* border-bottom: 1.33333vw solid #f5f5f5; */
	}
	.rui-navber-li{
		width:25vw;
		height:29.6vw;
		display:flex;
		align-items:center;
		justify-content:center;
		flex-direction:column;
	}
	.rui-navber-img{
		width:13.33333333vw;
		height:13.33333333vw;
		flex:0 0 auto;
		margin-bottom:2vw;
	}
</style>
