<template>
	<view class="content">
		<!-- 电影信息 -->
		<view class="moviemsg">
			<!-- 右边图片 -->
			<view class="rightpic">
				<image :src="mdata.images.large" mode=""></image>
			</view>
			<!-- 左边信息 -->
			<view class="leftmsg">
				<!-- 电影中文标题 -->
				<view class="mtitle">
					{{mdata.title}}({{mdata.year}})
				</view>
				<!-- 电影英文标题 -->
				<view class="etitle">
					{{mdata.original_title}}
				</view>
				<!-- 电影类型 -->
				<view class="mclass">
					<text v-for="(item,index) in mdata.genres" :key='index'>{{item}}</text>/
					<text v-for="(i,ind) in mdata.countries" :key='ind'>{{i}}</text>
				</view>
				<!-- 选项 -->
				<view class="btn">
					<!-- 想看 -->
					<view class="look">
						<image src="../../static/star.png" mode=""></image>
						<text>
							想看
						</text>
					</view>
					<view class="look">
						<image src="../../static/666s.png" mode=""></image>
						<text>
							看过
						</text>
					</view>
				</view>
			</view>
		</view>
		<!-- 评分 -->
		<view class="score">
			<!-- 评分标题 -->
			<view class="stitle">
				<view class="ti">
					<text class="dbsc"> 豆瓣评分</text>
					<text class="tm">TM</text>
				</view>
				<text>></text>
			</view>
			<!-- 评分 -->
			<view class="scorebox">
				<text>
					{{mdata.rating.average}}
				</text>
				<uni-rate :readonly="true" :value="mdata.rating.average" />
			</view>
		</view>
		<!-- 简介 -->
		<view class="int">
			<text class="intclass">简介</text>
			<view>
				{{mdata.summary}}
			</view>
		</view>

		<!-- 影人 -->
		<view class="movieman">
			<!-- 标题 -->
			<view class="mantitle">
				影人
			</view>
			<!-- 剧照 -->
			<scroll-view scroll-x="true" class="castsbox">
				<view class="casts" v-for="(item,index) in mdata.directors" :key='index'>
					<!-- 图片 -->
					<image :src="item.avatars.large" mode=""></image>
					<!-- 名字 -->
					<view class="name">
                         {{item.name}}
					</view>
					<!-- 职位 -->
					<view class="position">
                         导演
					</view>
				</view>
				<view class="casts" v-for="(items,index) in mdata.casts" :key='index'>
					<!-- 图片 -->
					<image :src="items.avatars.large" mode=""></image>
					<!-- 名字 -->
					<view class="name">
				         {{items.name}}
					</view>
					<!-- 职位 -->
					<view class="position">
				         演员
					</view>
				</view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	import {
		uniRate
	} from '@dcloudio/uni-ui'
	export default {
		data() {
			return {
				mdata: {}
			}
		},
		onLoad(res) {
			uni.showLoading({
			    title: '拼命加载中'
			});
			
			console.log(res)
			setTimeout(()=>{
				uni.request({
					url: `http://t.yushu.im/v2/movie/subject/${res.id}?apikey=0df993c66c0c636e29ecbb5344252a4a`, 
				
					success: (res) => {
						  uni.hideLoading();
						console.log(res.data);
						res.data.rating.average = parseFloat((res.data.rating.average / 2).toFixed(1))
						this.mdata = res.data
						console.log(this.mdata)
					}
				});
			},3000)
			
		},
		methods: {

		},
		components: {
			uniRate
		}
	}
</script>





<style lang="less">
	page {
		background-color: #F5F6F8;
	}

	.content {
		height: 100%;
		width: 100%;

	}

	.moviemsg {
		display: flex;
		padding: 20rpx;

		image {
			width: 200rpx;
			height: 300rpx;
			margin-right: 20rpx;
		}

		.mtitle {
			font-size: 22px;
			color: #333333;
			font-weight: bold;
		}

		.etitle {
			font-size: 14px;
			color: #808080;
		}

		.mclass text {
			font-size: 12px;
			color: #808080;
			margin-right: 10rpx;
		}

		.btn {
			display: flex;

			.look {
				width: 200rpx;
				height: 80rpx;
				background-color: #FFFFFF;
				margin-right: 20px;
				border-radius: 10px;
				text-align: center;
				line-height: 80rpx;

				image {
					width: 30rpx;
					height: 30rpx;
				}
			}
		}
	}

	.score {
		width: 710rpx;
		margin: 30px auto;
		background-color: #FFFFFF;
		border-radius: 10rpx;
		box-sizing: border-box;
		padding: 20rpx;

		.stitle {
			display: flex;
			justify-content: space-between;
		}

		.ti {
			display: flex;
			align-items: flex-start;

			.dbsc {
				font-size: 16px;
				margin-right: 5rpx;
			}

			.tm {
				font-size: 8px;
			}
		}
	}

	.int {
		padding: 20rpx;
	}

	.movieman {
		padding: 20rpx;

		.castsbox {
			width: 100%;
			white-space: nowrap;

			.casts {
				display: inline-block;
				margin-right: 20rpx;
				image{
					width: 200rpx;
					height: 300rpx;
					margin-bottom: 20rpx;
				}
				.name{
					font-size: 20rpx;
				}
				.position{
					font-size: 14rpx;
				}
			}
		}
	}
</style>
