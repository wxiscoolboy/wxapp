<template>
	<view>
		<!-- 大榜单 -->
		<view class="yearlist" v-for="(item,index) in list" :key='index'>
			<image :src="item.src" mode=""></image>
		</view>
		<!-- 小榜单 -->
		<view class="slist" v-for="(items,index) in slist" :key='index' @tap='listdata(items.u)'>
			<!-- 右边图片 -->
			<view class="img">
				<image :src="items.src" mode=""></image>
			</view>
			<!-- 左边电影名 -->
			<view class="mname">
				<view class="rank" v-for="(i,ind) in items.arr" :key='ind'>
					<text>{{ind+1}}.</text>
					<text>{{i.title}}</text>
					<text class="soc">{{i.rating.average}}分</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				//大榜单
				list: [{
					id: 0,
					src: '../../static/111.jpg',
					url: ''
				}, {
					id: 1,
		 			src: '../../static/222.jpg',
					url: ''
				}],
				//小榜单
				slist: [{
						id: 0,
						src: '../../static/333.jpg',
						url: 'http://t.yushu.im/v2/movie/top250?apikey=0df993c66c0c636e29ecbb5344252a4a&start=0&count=3',
						arr: [],
						u:'../listinfo/listinfo?jk=top250&apikey=0df993c66c0c636e29ecbb5344252a4a&start=0&count=20&img=../../static/333.jpg'
					},
					{
						id: 1,
						src: '../../static/444.jpg',
						url: 'http://t.yushu.im/v2/movie/in_theaters?apikey=0df993c66c0c636e29ecbb5344252a4a&start=0&count=3',
						arr: [],
						u:'../listinfo/listinfo?jk=in_theaters&apikey=0df993c66c0c636e29ecbb5344252a4a&start=0&count=10&img=../../static/444.jpg'
					},
					{
						id: 2,
						src: '../../static/555.jpg',
						url: 'http://t.yushu.im/v2/movie/coming_soon?apikey=0df993c66c0c636e29ecbb5344252a4a&start=0&count=3',
						arr: [],
						u:'../listinfo/listinfo?jk=coming_soon&apikey=0df993c66c0c636e29ecbb5344252a4a&start=0&count=10&img=../../static/555.jpg'
					}
				],
			}
		},
		onLoad() {
			for (let o of this.slist) {
				this.request(o)
			}
		},

		methods: {
			//封装请求函数
			request(obj) {
				uni.request({
					url: obj.url, //仅为示例，并非真实接口地址。
					success: (res) => {
						console.log(res.data);
						obj.arr = res.data.subjects
					}
				});
			},
			//跳转页面
			listdata(u) {
               uni.navigateTo({
                   url: u
               });
			}


		}
	}
</script>

<style lang="less" scoped>
	.yearlist {
		margin: 15rpx;
		padding: 15rpx;

		image {
			width: 100%;
			height: 340rpx;
		}
	}

	.slist {
		display: flex;
		padding: 0 20rpx;
		margin-bottom: 20rpx;
		align-items: center;

		image {
			width: 200rpx;
			height: 200rpx;
		}

		.mname {
			height: 160rpx;
			flex: 1;
			padding: 20rpx;
			border: 1px solid #808080;
			border-left: none;
			box-sizing: border-box;
            .rank{
				display: flex;
                // justify-content: space-between;
				font-size: 14px;
			}
			.soc {
				color: #EFCB97;
			}
		}
	}
</style>
