<template>
	<view class="rui-flex-list" @tap="jumpNextPage(url)" :url="url">
		<view class="rui-flex-left">
			<text class="rui-line-clamp" style="-webkit-line-clamp:1;">{{title}}</text>
		</view>
		<text class="rui-li-more"></text>
	</view>
</template>

<script>
	const warn = (msg, getValue) => {
	  console.warn(msg);
	  console.log('接受到的值为：', getValue);
	};
	export default {
		name: 'rattenking-list',
		props: {
			/**
			 * list的title
			 */
			title: {
			  type: String,
			  default: ''
			},
			/**
			 * list的linkType
			 */
			linkType: {
			  type: String,
			  default: 'navigateTo'
			},
			/**
			 * list的url
			 */
			url: {
			  type: String,
			  default: ''
			}
		},
		data() {
			return {
			}
		},
		created(){
		},
		methods:{
			jumpNextPage(eurl){
				// console.log(eurl)
				const url = eurl;
				if(!url || url === '') return;

				if (['navigateTo', 'redirectTo', 'switchTab', 'reLaunch'].indexOf(this.linkType) === -1) {
					warn('linkType 属性可选值为 navigateTo，redirectTo，switchTab，reLaunch', this.linkType);
					return;
				}
				uni[this.linkType].call(wx, { url });
			}
		}
	}
</script>
	
<style>
	.rui-flex-list{
		display: -webkit-flex;
		display: flex;
		align-items: center;
		/* flex-wrap: wrap; */
		padding:20upx;
		text-align: left;
		font-size: 30upx;
		border-bottom: 1px solid #eee;
	}
	.rui-flex-left{
		flex-grow: 1;
	}
	.rui-line-clamp{
		overflow:hidden;
		text-overflow:ellipsis;
		display:-webkit-box;
		-webkit-box-orient:vertical;
	}
	.rui-li-more{
	  flex: 0 0 auto;
	  position:relative;
	  /* text-align:right; */
	  color:#495060;
	}
	.rui-li-more{
	  padding-right:13px
	}
	.rui-li-more::after{
	  content:" ";
	  display:inline-block;
	  width:6px;
	  height:6px;
	  position:absolute;
	  top:50%;
	  right:2px;
	  border-width:2px 2px 0 0;
	  border-color:#aaa;
	  border-style:solid;
	  transform:translateY(-50%) matrix(.71,.71,-.71,.71,0,0)
	}
</style>
