<template>
	<view class="rui-tabber-content" v-if="tabberList.length > 1 && tabberList.length < 6">
		<view class="rui-tabber-li" @tap="tabbertap(item.tabberStatus)" :style="curStatus == item.tabberStatus ? tabberStyleActive : tabberStyle" v-for="(item,index) in tabberList" :key="index">
			<image class="rui-tabber-img" v-if="curStatus == item.tabberStatus" :src="item.selectedIconPath" mode=""></image>
			<image class="rui-tabber-img" v-if="curStatus != item.tabberStatus" :src="item.iconPath" mode=""></image>
			<text>{{item.text}}</text>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'rui-tabber',
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
			tabberList: Array
		},
		data() {
			return {
				tabberStyle: 'color:' + this.color,
				tabberStyleActive: 'color:' + this.colorActive,
				curStatus: this.status
			}
		},
		created(){
			console.log('rui-taber 组件加载完成！')
		},
		methods: {
			tabbertap(status){
				this.curStatus = status;
				this.$emit('tabbertap', status);
			}
		}
	}
</script>

<style>
	.rui-tabber-content{
		width: 100vw;
		height: 16vw;
		border-top: 1px solid #eee;
		display: flex;
		justify-content: space-around;
		align-items: center;
		color:#02212d;
		font-size:3.2vw;
		background-color: #ffffff;
	}
	.rui-tabber-li{
		display:flex;
		align-items:center;
		justify-content:center;
		flex-direction:column;
	}
	.rui-tabber-img{
		width:6.7vw;
		height:6.7vw;
		flex:0 0 auto;
		margin-bottom:1vw;
	}
</style>
