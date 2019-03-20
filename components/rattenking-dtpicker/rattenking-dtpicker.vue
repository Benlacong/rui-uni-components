<template>
	<picker class='rui-picker rui-class' mode="multiSelector" :range="times" :value="timesIndex" :disabled="curDisabled" @change='changeDate' @cancel="cancelDate" @columnchange="columnchangeDate">
	  {{value}}
	</picker>
</template>

<script>
	import GetDate from './GetDate.js';
	export default {
		name: 'rattenking-dtpicker',
		props: {
			/**
			 * picker允许选中的最小值
			 */
			start: {
			  type: String,
			  default: '1900-00-00 00:00:00'
			},
			/**
			 * picker允许选中的最大值
			 */
			end: {
			  type: String,
			  default: '2500-12-30 23:59:59'
			},
			/**
			 * picker默认展示的值
			 */
			value: {
			  type: String,
			  default: '2019-03-15 10:45:00'
			},
			/**
			 * picker的时间粒度
			 */
			fields: {
			  type: String,
			  default: 'second'
			},
			/**
			 * picker是否禁止
			 */
			disabled: {
			  type: Boolean,
			  default: false
			}
		},
		data() {
			return {
				times:[['2019','2020'],['01','02']],
				timesIndex: [1,1],
				timesString: null,
				curValue: this.value,
				curDisabled: this.disabled,
				cancel: null
			}
		},
		watch: {
			value(val) {
				this.curValue = val;
			},
			disabled(val){
				this.curDisabled = val;
			},
			curDisabled(val){
				this.curDisabled = val;
			},
			curValue(val) {
				this.$emit('change', val);
			},
			cancel(val) {
				this.$emit('cancel', val);
			}
		},
		created() {
			switch (this.fields){
				case 'year':
				  if (this.value.length !== 4) {GetDate.error('时间粒度和时间格式不一致');this.curDisabled = true;return false;}
				  if (this.start.length !== 4) { GetDate.error('时间粒度和开始时间格式不一致'); this.curDisabled = true; return false;}
				  if (this.end.length !== 4) { GetDate.error('时间粒度和结束时间格式不一致'); this.curDisabled = true; return false;}
				  break;
				case 'month':
				  if (this.value.length !== 7) { GetDate.error('时间粒度和时间格式不一致'); this.curDisabled = true; return false;}
				  if (this.start.length !== 7) { GetDate.error('时间粒度和开始时间格式不一致'); this.curDisabled = true; return false;}
				  if (this.end.length !== 7) { GetDate.error('时间粒度和结束时间格式不一致'); this.curDisabled = true; return false;}
				  break;
				case 'day':
				  if (this.value.length !== 10) { GetDate.error('时间粒度和时间格式不一致'); this.curDisabled = true; return false;}
				  if (this.start.length !== 10) { GetDate.error('时间粒度和开始时间格式不一致'); this.curDisabled = true; return false;}
				  if (this.end.length !== 10) { GetDate.error('时间粒度和结束时间格式不一致'); this.curDisabled = true; return false;}
				  break;
				case 'hour':
				  if (this.value.length !== 13) { GetDate.error('时间粒度和时间格式不一致'); this.curDisabled = true; return false;}
				  if (this.start.length !== 13) { GetDate.error('时间粒度和开始时间格式不一致'); this.curDisabled = true; return false;}
				  if (this.end.length !== 13) { GetDate.error('时间粒度和结束时间格式不一致'); this.curDisabled = true; return false;}
				  break;
				case 'minute':
				  if (this.value.length !== 16) { GetDate.error('时间粒度和时间格式不一致'); this.curDisabled = true; return false;}
				  if (this.start.length !== 16) { GetDate.error('时间粒度和开始时间格式不一致'); this.curDisabled = true; return false;}
				  if (this.end.length !== 16) { GetDate.error('时间粒度和结束时间格式不一致'); this.curDisabled = true; return false;}
				  break;
				case 'second':
				  if (this.value.length !== 19) { GetDate.error('时间粒度和时间格式不一致'); this.curDisabled = true; return false;}
				  if (this.start.length !== 19) { GetDate.error('时间粒度和开始时间格式不一致'); this.curDisabled = true; return false;}
				  if (this.end.length !== 19) { GetDate.error('时间粒度和结束时间格式不一致'); this.curDisabled = true; return false;}
				  break;
				default: 
				  GetDate.error('时间粒度不存在')
				  break;
			  }
			  let values = this.value.split(' ');
			  let targets = this.fields === 'year' || this.fields === 'month' || this.fields === 'day' ? [...(values[0].split('-'))] : [...(values[0].split('-')), ...(values[1].split(':'))];

			  if (GetDate.getTimes(this.value) < GetDate.getTimes(this.start)){
				GetDate.error('默认时间不能小于开始时间')
				this.curDisabled = true
				return false;
			  }
			  if (GetDate.getTimes(this.value) > GetDate.getTimes(this.end)) {
				GetDate.error('默认时间不能大于开始时间')
				this.curDisabled = true
				return false;
			  }
			  let times = GetDate.getDateTimes({
				start: this.start.substring(0, 4),
				end: this.end.substring(0, 4),
				curyear: this.value.substring(0, 4),
				curmonth: this.value.substring(5, 7),
				fields: this.fields,
			  })
			  let timesIndex = GetDate.getTimeIndex(times, targets);
			  let timesString = [];
			  timesIndex.forEach(o => timesString.push(o));

			  this.times = times;
			  this.timesIndex = timesIndex;
			  this.timesString = timesString;
		},
		methods: {
			changeDate(e){
			  let values = e.detail.value;
			  let times = this.times;
			  let curarr = [];
			  for (let i = 0, len = values.length; i < len; i++) {
				curarr.push(times[i][values[i]])
			  }
			  let str = GetDate.format(curarr);
			  console.log(str)
			  this.curValue = str;
			},
			columnchangeDate(e){
			  if ((this.fields === 'year' || this.fields === 'month')){
				let timesIndex = this.timesIndex;
				timesIndex[e.detail.column] = e.detail.value;
				this.timesIndex = timesIndex;
				return false;
			  }
			  // 先对timesIndex做出改变
			  if ((e.detail.column === 0 || e.detail.column === 1 || e.detail.column === 2) && (this.fields !== 'year' || this.fields !== 'month')) {
				let times = this.times;
				let timesIndex = this.timesIndex;
				timesIndex[e.detail.column] = e.detail.value;
				let days = GetDate.getMonthDay(times[0][timesIndex[0]], times[1][timesIndex[1]]);
				if (timesIndex[2] >= days.length) {
				  timesIndex[2] = days.length - 1;
				} else {
				  timesIndex[e.detail.column] = e.detail.value;
				}
				this.timesIndex = timesIndex;
			  } else {
				let timesIndex = this.timesIndex;
				timesIndex[e.detail.column] = e.detail.value;
				this.timesIndex = timesIndex;
			  }
			  // 判断当前选择是否小于开始时间或者大于结束时间
			  let values = this.timesIndex;
			  let times = this.times;
			  let curarr = [];
			  for (let i = 0, len = values.length; i < len; i++) {
				curarr.push(times[i][values[i]])
			  }
			  let str = GetDate.format(curarr);
			  
			  if (GetDate.getTimes(str) < GetDate.getTimes(this.start)) {
				let timesString = this.timesString;
				let timesIndex = [];
				timesString.forEach(o => timesIndex.push(o));
				this.timesIndex = timesIndex;
			  }
			  if (GetDate.getTimes(str) > GetDate.getTimes(this.end)) {
				let timesString = this.timesString;
				let timesIndex = [];
				timesString.forEach(o => timesIndex.push(o));
				this.timesIndex = timesIndex;
			  }
			},
			cancelDate(e){
				this.cancel = e
			}
		}
	}
</script>

<style>
	.rui-picker{
	  height: 10vw;
	  font-size: 4vw;
	  color: #000;
	  display: -webkit-flex;
	  display: flex;
	  align-items: center;
	  padding: 0 10px;
	  box-sizing: border-box;
	  border: 1px solid #aaa;
	  border-radius: 3px;
	}
</style>
