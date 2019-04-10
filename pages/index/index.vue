<template>
	<view class="rui-content">
		<ruiList v-for="(item,index) in menu" :title="item.title" :url="item.url" :key="index"></ruiList>
	</view>
</template>

<script>
	import ruiList from '@/components/rattenking-list/rattenking-list.vue';
	import menu from './menu.js';
	export default {
		data() {
			return {
				menu: menu
			}
		},
		components: { ruiList},
		onLoad() {
			console.log(this.menu)
		},
		methods: {
			change(e){
				console.log(e)
			},
			cancel(e){
				console.log(e)
			}
		}
	}
</script>

<style>
</style>
