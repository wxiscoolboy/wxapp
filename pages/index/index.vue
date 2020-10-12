<template>
	<view class="content">
		<!-- 搜索 -->
		<view class="search_view">
			<input class="uni-input" placeholder="搜索" />
		</view>
		<view class="list">
			<view class="hotmovie" v-for="(i,int) in movieclass" :key='i.id'>
				<!-- 标题 -->
				<view class="titlebox">
					<view class="title">
						{{i.title}}
					</view>
					<view class="more">
						查看更多>
					</view>
				</view>
				<!-- 影片 --> 
				<scroll-view class="ms" scroll-x>
					<view class="msbox" v-for="(item,index) in i.arr" :key='index'>
						<navigator :url="'/pages/movie/movie?id='+item.id">
							<!-- 电影图片 -->
							<image :src="item.images.large" mode=""></image>
							<!-- 电影标题 -->
							<view class="mtitle">
								{{item.title}}
							</view>
							<!-- 评分 -->
							<view class="star">
								<uni-rate :value="item.rating.average" readonly :size="14" />
								<text class="val">{{item.rating.average}}</text>
							</view>
						</navigator>
					</view>
				</scroll-view>
			</view>
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
				//评分的数据
				// value: 5,
				//影片数据

				//分类数据
				movieclass: [{
						id: 0,
						title: '影视热映',
						url: 'http://t.yushu.im/v2/movie/in_theaters?apikey=0df993c66c0c636e29ecbb5344252a4a&start=0&count=10',
						arr: [],
					},
					{
						id: 1,
						title: '豆瓣热门即将上映',
						url: 'http://t.yushu.im/v2/movie/coming_soon?apikey=0df993c66c0c636e29ecbb5344252a4a',
						arr: [],
					},
					{
						id: 2,
						title: '近期热门剧集top250',
						url: 'http://t.yushu.im/v2/movie/top250?apikey=0df993c66c0c636e29ecbb5344252a4a&start=20&count=20',
						arr: [],
					}
				]
			}
		},
		onLoad() {

			for (let o of this.movieclass) {
				// console.log(this.request(o.url))  
				this.request(o)
				// console.log(o.arr)
			}
 


		},
		methods: {

			//封装请求函数
			request(o) {

				//影院热映：
				uni.request({
					url: o.url, //仅为示例，并非真实接口地址。

					success: (res) => {
						console.log(this)
						console.log(res);
						for (let obj of res.data.subjects) {
							obj.rating.average = obj.rating.average / 2
						}
						o.arr = res.data.subjects

					},
				});
			}
		},
		components: {
			uniRate
		}
	}
</script>

<style lang="less" scoped>
	.content {
		display: flex;
		flex-direction: column;
	}

	.list {
		display: flex;
		flex-direction: column;
		flex: 1;
	}

	// 搜索
	.search_view {
		height: 40px;
		background-color: #1296db;
		display: flex;
		justify-content: center;

		.uni-input {
			width: 720rpx;
			background-color: #FFFFFF;
			height: 32px;
			border-radius: 10px;
		}
	}

	.hotmovie {
		flex: 1;
		margin-bottom: 20rpx;

		.titlebox {
			display: flex;
			justify-content: space-between;
			padding: 20rpx;

			.title {
				font-size: 20px;
			}

			.more {
				font-size: 18px;
				color: #1296db;
			}
		}

		.ms {
			width: 100%;
			white-space: nowrap;
			padding-left: 20rpx;

			.msbox {
				display: inline-block;
				margin-right: 20rpx;

				image {
					width: 150rpx;
					height: 240rpx;
				}

				.star {
					width: 150rpx;
					display: flex;
					align-items: center;

					.val {
						font-size: 14px;
						color: #999999;
					}
				}
			}
		}
	}
</style>
