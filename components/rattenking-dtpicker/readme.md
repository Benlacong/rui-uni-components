### DatePicker 多时间粒度选择器

可进行多时间粒度选择的时间选择器，组件名：``rattenking-dtpicker``，代码块： ruiDatePicker。

**使用方式：**

在 ``script`` 中引用组件 

```javascript
import ruiDatePicker from '@/components/rattenking-dtpicker/rattenking-dtpicker.vue';
export default {
    components: {ruiDatePicker}
}
```

在 ``template`` 中使用组件

```html
<ruiDatePicker
	fields="second"
	start="2010-00-00 00:00:00"
	end="2030-12-30 23:59:59"
	:value="value"
	@change="bindChange"
	@cancel="bindCancel"
></ruiDatePicker>
```

实际效果参考：[https://github.com/dcloudio/uni-ui](https://github.com/dcloudio/uni-ui)

**DatePicker 属性说明：**

|属性名		|类型	|默认值	|说明					|
|---		|----	|---	|---					|
|value		|Number	|0		|输入框当前值			|
|min		|Number	|0		|最小值					|
|max		|Number	|100	|最大值					|
|step		|Number	|1		|每次点击改变的间隔大小	|
|disabled	|Boolean|false	|是否为禁用状态			|

**事件说明：**

|事件名称	|说明		|
|---|---|
|change	|输入框值改变时触发的事件，参数为输入框当前的 value|