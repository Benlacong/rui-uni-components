<template>
	<view class="content">
		<view class="rui-head">
			粒度时间：second
		</view>
		<view class="rui-flex">
			<text>选择时间：</text>
			<ruiDatePicker
				fields="second"
				start="2010-00-00 00:00:00"
				end="2030-12-30 23:59:59"
				:value="value"
				@change="bindChange"
				@cancel="bindCancel"
			></ruiDatePicker>
		</view>
		<view class="rui-head">
			粒度时间：minute
		</view>
		<view class="rui-flex">
			<text>选择时间：</text>
			<ruiDatePicker
				fields="minute"
				start="2010-00-00 00:00"
				end="2030-12-30 23:59"
				:value="value1"
				@change="bindChange1"
			></ruiDatePicker>
		</view>
		<view class="rui-head">
			粒度时间：hour
		</view>
		<view class="rui-flex">
			<text>选择时间：</text>
			<ruiDatePicker
				fields="hour"
				start="2010-00-00 00"
				end="2030-12-30 23"
				:value="value2"
				@change="bindChange2"
			></ruiDatePicker>
		</view>
		<view class="rui-head">
			粒度时间：day
		</view>
		<view class="rui-flex">
			<text>选择时间：</text>
			<ruiDatePicker
				fields="day"
				start="2010-00-00"
				end="2030-12-30"
				:value="value3"
				@change="bindChange3"
			></ruiDatePicker>
		</view>
		<view class="rui-head">
			粒度时间：month
		</view>
		<view class="rui-flex">
			<text>选择时间：</text>
			<ruiDatePicker
				fields="month"
				start="2010-00"
				end="2030-12"
				:value="value4"
				@change="bindChange4"
			></ruiDatePicker>
		</view>
		<view class="rui-head">
			粒度时间：year
		</view>
		<view class="rui-flex">
			<text>选择时间：</text>
			<ruiDatePicker
				fields="year"
				start="2010"
				end="2030"
				:value="value5"
				@change="bindChange5"
			></ruiDatePicker>
		</view>
		<view class="rui-head">
			粒度时间：second（时段选择）
		</view>
		<view class="rui-flex">
			<text>开始时间：</text>
			<ruiDatePicker
				fields="second"
				start="2010-00-00 00:00:00"
				end="2030-12-30 23:59:59"
				:value="valueStart"
				@change="bindChangeStart"
			></ruiDatePicker>
		</view>
		<view class="rui-flex" style="margin-top: 4vw;">
			<text>结束时间：</text>
			<ruiDatePicker
				fields="second"
				start="2010-00-00 00:00:00"
				end="2030-12-30 23:59:59"
				:value="valueEnd"
				@change="bindChangeEnd"
			></ruiDatePicker>
		</view>
	</view>
</template>

<script>
	import ruiDatePicker from '@/components/rattenking-dtpicker/rattenking-dtpicker.vue';
	export default {
		data() {
			return {
				value: '2019-03-20 11:02:34',
				value1: '2019-03-20 11:02',
				value2: '2019-03-20 11',
				value3: '2019-03-20',
				value4: '2019-03',
				value5: '2019',
				valueStart: '2019-03-20 11:02:34',
				valueEnd: '2019-03-28 06:02:56',
			}
		},
		components: { ruiDatePicker},
		onLoad() {
			console.log(this.value)
		},
		methods: {
			bindChange(value){
				this.value = value;
			},
			bindChange1(value){
				this.value1 = value;
			},
			bindChange2(value){
				this.value2 = value;
			},
			bindChange3(value){
				this.value3 = value;
			},
			bindChange4(value){
				this.value4 = value;
			},
			bindChange5(value){
				this.value5 = value;
			},
			bindChangeStart(value){
				this.valueStart = value;
			},
			bindChangeEnd(value){
				this.valueEnd = value;
			},
			bindCancel(value){
				console.log('激活取消函数')
			}
		}
	}
</script>
	
<style>
	.content {
		text-align: center;
		height: 400upx;
	}
	.rui-head{
		font-size: 4vw;
		height: 10vw;
		line-height: 10vw;
		padding: 0 4vw;
		text-align: left;
	}
	.rui-flex{
		display: -webkit-flex;
		display: flex;
		align-items: center;
		font-size: 4vw;
		padding: 0 4vw;
	}
</style>
