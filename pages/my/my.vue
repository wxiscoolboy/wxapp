<template>
	<view>
		<view class="abox">
			<button type="default" size="default" style="width: 190px;">登录</button>
		</view>
		<view class="bbox">
			<view style="display: flex;justify-content: space-between;">
				<text style="margin-left: 10px;">我的书影音</text>
				<text style="color: #979797;margin-right: 15px;">登录查看></text>
			</view>


			<view style="display: flex;justify-content: space-around;margin-top: 20px;padding: 5px;">
				<image src="../../static/book%20(2).png" style="width:30px;height:30px;margin-right: 5px;"></image>
				<view style="display: flex;flex-direction: column;margin-top: -13px;">
					<text style="font-size: 13px;">观影分析</text>
					<text style="color: #8F8F8F;font-size: 14px;margin-top: 10px;">0听过</text>
				</view>
				<view style="display: flex;flex-direction: column;margin-left: 10px;">
					<text style="color: #979797;font-size: 13px;">标记10部影片</text>
					<text style="color: #979797;font-size: 13px;">开启观影分析</text>
				</view>
				<button size="mini" style="margin-left: 7px;">立即开启</button>
				<text style="color: #979797;font-size: 16px;">></text>
			</view>
			<view style="width: 330px;border-top: 1px solid #979797;margin-left: 80px;">

			</view>

			<view style="display: flex;justify-content: space-around;margin-top: 20px;padding: 5px;">
				<image src="../../static/book%20(1).png" style="width:30px;height:30px;margin-right: 5px;"></image>
				<view style="display: flex;flex-direction: column;margin-top: -13px;">
					<text style="font-size: 13px;">读书分析</text>
					<text style="color: #8F8F8F;font-size: 14px;margin-top: 10px;">0读过</text>
				</view>
				<view style="display: flex;flex-direction: column;margin-left: 10px;">
					<text style="color: #979797;font-size: 13px;">标记10本书</text>
					<text style="color: #979797;font-size: 13px;">开启读书分析</text>
				</view>
				<button size="mini" style="margin-left: 7px;">立即开启</button>
				<text style="color: #979797;font-size: 16px;">></text>
			</view>

			<view style="width: 330px;border-top: 1px solid #979797;margin-left: 80px;">

			</view>

			<view style="display: flex;justify-content: space-around;margin-top: 20px;padding: 5px;">
				<image src="../../static/book%20(3).png" style="width:30px;height:30px;margin-right: 5px;"></image>
				<view style="display: flex;flex-direction: column;margin-top: -13px;">
					<text style="font-size: 13px;">音乐分析</text>
					<text style="color: #8F8F8F;font-size: 14px;margin-top: 10px;">0听过</text>
				</view>
				<view style="display: flex;flex-direction: column;margin-left: 10px;">
					<text style="color: #979797;font-size: 13px;">标记10部唱片</text>
					<text style="color: #979797;font-size: 13px;">开启音乐分析</text>
				</view>
				<button size="mini" style="margin-left: 7px;">立即开启</button>
				<text style="color: #979797;font-size: 16px;">></text>
			</view>

		</view>



	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		methods: {

		}
	}
</script>

<style>
	.abox {
		height: 200px;
		background-color: #4CD964;
		display: flex;
		width: 100%;
		align-items: center;
	}

	.bbox {
		display: flex;
		flex-direction: column;
		padding: 10px;

	}
</style>
