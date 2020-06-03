<template>
	<!-- <view style="height: 400px;border-bottom: 1px solid black;">
		<lee-select-city />
	</view> -->
	<view>
		<view>
			<view class="Titlemain">
				<view class="Titlesearch">
					<input class="uni-input" focus placeholder="请输入城市" size='mini' v-model="city" />
				</view>
				<view class="Titlebtn">
					<button type="primary" size="mini" @click="weasearch">搜索</button>
				</view>
			</view>
		</view>
		<view class="weaContant" v-for="item in datalist">
			<view class="weamaintitle">
				{{item.date}}
			</view>
			<view class="weamaincont">
				<text class="weatext1">{{item.direct}}</text>
				<text class="weatext2">{{item.temperature}}</text>
				<text class="weatext3">{{item.weather}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	// import LeeSelectCity from '@/components/lee-select-city/lee-select-city.vue'
	export default {
		// components: {
		// 	LeeSelectCity
		// }
		data: function() {
			return {
				city: '杭州',
				datalist: []
			}
		},
		mounted: function() {
			console.log()
		},
		methods: {
			weasearch() {
				let _self = this
				let utfcity = encodeURI(this.city)
				uni.request({
					url: 'http://apis.juhe.cn/simpleWeather/query?city=' + utfcity + '&key=a3af9278e152012e0df618a2bc962b9b',
					data: {},
					header: {},
					success: (res) => {
						_self.datalist = res.data.result.future
						console.log(_self.datalist)
					}
				});
			}
		}
	}
</script>

<style scoped>
	.weatext1{
		width: 38%;
	}
	.weatext2{
		width: 23%;
	}
	.weatext3{
		width: 38%;
	}
	.weaContant{
		margin-top: 10px;
	}
	.weamaintitle {
		border: 1px solid #e1e1e1;
		width: 94%;
		margin-left: 3%;
		font-size: 16px;
		font-weight: 600;
	}

	.weamaincont {
		border: 1px solid #e1e1e1;
		border-top: none;
		width: 94%;
		margin-left: 3%;
		display: flex;
		padding: 5px 0px;
	}
</style>
