<template>
	<view class="content">
		<view class="title">
			{{title}}
			<rich-text class="richText" :nodes="strings"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title : '',
				strings : ''
			}
		},
		onLoad(e) {
			console.log(e.newsid)
			uni.showLoading({
				title: '加载中',
				mask: false
			});
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news/36kr/'+e.newsid,
				method: 'GET',
				data: {},
				success: res => {
					console.log(res)
					this.title = res.data.title;
					this.strings = res.data.content
					uni.hideLoading()
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}
</script>

<style scoped>
.content{
	padding: 10upx 2%;
	width: 96%;
	flex-wrap: wrap;
}
.title{
	line-height: 2em;
	font-weight: 700;
	font-size: 38upx;
}
.art-content{
	line-height: 2em;
}
</style>
