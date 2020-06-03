<template>
	<view class="container">
		<!-- <text class="trantitle">在线翻译</text> -->
		<view class='translateInput'>
			<picker style="border-bottom: 1px solid #e1e1e1;" @change="bindPickerChangeto" :value="indexto" :range="arrayto">
				<view class="uni-input">{{arrayto[indexto]}}</view>
			</picker>
			<image class="tranIcon" src="../../static/images/tranIcon.png"></image>
			<picker style="border-bottom: 1px solid #e1e1e1;" @change="bindPickerChangefrom" :value="indexfrom" :range="arrayfrom">
				<view class="uni-input">{{arrayfrom[indexfrom]}}</view>
			</picker>
		</view>
		<view class='tranMain'>
			<textarea v-model="textCont" auto-height />
		</view>
		<button type="primary" @click='ontran' style="margin-top: 10px;">翻译</button>
		<view class='resultCont' v-if="tranresult">
			<text class='TranTip'>释义:</text><text>{{tranresult}}</text>
		</view>
	</view>
</template>

<script>
	import md5 from 'js-md5'
	export default {
		data() {
			return {
				tranresult: '',
				arrayto: ['中文', '英语', '粤语', '日语', '韩语'],
				arrayfrom: ['中文', '英语', '粤语', '日语', '韩语'],
				indexto: 0,
				transultTO: '',
				indexfrom: 1,
				transultFrom: '',
				textCont: '',
			}
		},
		methods: {
			bindPickerChangeto: function(e) {
				this.indexto = e.target.value
				console.log(this.indexto)
				console.log(this.transultTO)
			},
			bindPickerChangefrom: function(e) {
				this.indexfrom = e.target.value
				console.log(this.indexfrom)
				console.log(this.transultFrom)
			},
			ontran() {
				if (this.indexto == '0') {
					this.transultTO = 'zh'
				} else if (this.indexto == '1') {
					this.transultTO = 'en'
				} else if (this.indexto == '2') {
					this.transultTO = 'yue'
				} else if (this.indexto == '3') {
					this.transultTO = 'jp'
				} else if (this.indexto == '4') {
					this.transultTO = 'kor'
				}
				
				if (this.indexfrom == '0') {
					this.transultFrom = 'zh'
				} else if (this.indexfrom == '1') {
					this.transultFrom = 'en'
				} else if (this.indexfrom == '2') {
					this.transultFrom = 'yue'
				} else if (this.indexfrom == '3') {
					this.transultFrom = 'jp'
				} else if (this.indexfrom == '4') {
					this.transultFrom = 'kor'
				}
				console.log(this.transultFrom)
				console.log(this.transultTO)
				let sign = md5('20200527000472592' + this.textCont + '1435660288iirv8vNzEyU7ImT7lTuY')
				console.log(sign)
				let _self = this
				uni.request({
					url: 'https://fanyi-api.baidu.com/api/trans/vip/translate',
					data: {
						q: this.textCont,
						from: this.transultTO,
						to: this.transultFrom,
						appid: '20200527000472592',
						salt: '1435660288',
						sign: sign
					},
					header: {},
					success: (res) => {
						console.log(res);
						_self.tranresult = res.data.trans_result[0].dst
					}
				});
			}
		},
		mounted: function() {}
	}
</script>

<style>
	.trantitle{
		font-size: 18px;
		color: #d9d6c3;
	}
	.container {
		padding: 10px 20px 0px 20px;
		font-size: 14px;
		line-height: 24px;
	}

	.translateInput {
		width: 100%;
		height: 50px;
		display: flex;
		justify-content: space-around;
		align-items: center;
	}

	.resultCont {
		margin-top: 10px;
		font-size: 16px;
	}

	.tranMain {
		width: 100%;
		margin-top: 10px;
		overflow-y: auto;
		height: 150px;
		border-radius: 5px;
		border: 1px solid #e1e1e1;
	}

	.tranBtn {
		width: 100%;
		margin-top: 10px;
	}

	.SelectF {
		width: 40%;
	}

	.SelectT {
		width: 40%;
	}

	.tranIcon {
		width: 25px;
		height: 25px;
	}

	.TranTip {
		color: #636363;
		margin-right: 10px;
	}
</style>
