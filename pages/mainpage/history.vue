<template>
	<view>
		<view class="Titlemain">
			<view class="Titlesearch">
				<picker mode="date" :value="date" :start="startDate" :end="endDate" @change="bindDateChange">
					<view class="uni-input">{{date}}</view>
				</picker>
			</view>
			<view class="Titlebtn">
				<button type="primary" size="mini" @click="Search">搜索</button>
			</view>
		</view>
		<view class="contant" v-for="item in datalist">
			<view class="contanttab">
				<view class="tabtitle">{{item.title}}</view>
				<view class="tabmain">
					<view class="tabimg" v-if="item.pic"><image :src="item.pic"></image></view>
					<view>{{item.des}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			const currentDate = this.getDate({
				format: true
			})
			return {
				date: currentDate,
				datalist:[]
			}
		},
		computed: {
			startDate() {
				return this.getDate('start');
			},
			endDate() {
				return this.getDate('end');
			}
		},
		methods: {
			Search(){
				let datamonth = this.date.split('-')[1]
				let dataday = this.date.split('-')[2]
				let _self = this;
				uni.request({
					url: 'http://api.juheapi.com/japi/toh?key=1e7bb3261d71a8673d98bd2ef07520c7&v=1.0&month=' + datamonth + '&day='+ dataday,
					data: {
					},
					header: {},
					success: (res) => {
						console.log(res);
						_self.datalist = res.data.result
					}
				});
			},
			bindDateChange: function(e) {
				this.date = e.target.value
			},
			getDate(type) {
				const date = new Date();
				let year = date.getFullYear();
				let month = date.getMonth() + 1;
				let day = date.getDate();

				if (type === 'start') {
					year = year - 60;
				} else if (type === 'end') {
					year = year + 2;
				}
				month = month > 9 ? month : '0' + month;;
				day = day > 9 ? day : '0' + day;
				return `${year}-${month}-${day}`;
			}
		}
	}
</script>

<style>
	.tabimg{
		width: 80%;
		height: 80%;
		padding: 10px;
	}
	.tabtitle{
		border: 1px solid #E1E1E1;
		font-size: 16px;
		padding: 2px;
		font-weight: 600;
	}
	.tabmain{
		border: 1px solid #E1E1E1;
		border-top: none;
	}
	.contant{
		width: 98%;
		height: auto;
		margin: 10px 1% 0 1%;
	}
</style>
