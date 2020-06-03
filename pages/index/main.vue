<template>
	<view>
		<view class="mainmodel" style="color:white;background-image: url(../../static/images/history.gif);background-size: 100% 100%;">
			<navigator url="/pages/mainpage/history" hover-class="navigator-hover">
				历史上的今天
			</navigator>
		</view>
		<view class="mainmodel" style="color:white;background-image: url(../../static/images/waether.gif);background-size: 100% 100%;">
			<navigator url="/pages/mainpage/weather" hover-class="navigator-hover">
				天气预报
			</navigator>
		</view>
	</view>
</template>

<script>
</script>

<style>
	.mainmodel {
		width: calc(48% - 2px);
		margin: 1%;
		height: 100px;
		/* background-color: #FAEBD7; */
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 16px;
		font-weight: bold;
		border-radius: 5px;
		float: left;
	}
</style>
