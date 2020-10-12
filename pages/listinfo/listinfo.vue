<template>
	<view>
		<!-- 图片 -->
		<view class="img">
			<image :src="src" mode=""></image>
		</view>
		<!-- 排名 -->
		<view class="ranking"  v-for="(item,index) in datalist" :key='index'>
			<view class="rankbox">
				No.{{index+1}}
			</view>
			<view class="mdata">
				<!-- 电影图片 -->

				<image :src="item.images.large" mode=""></image>
				<!-- 信息 -->
				<view class="mbox">
					<!-- 标题 -->
					<view class="title">
                         {{item.title}}
					</view>
					<!-- 评分 -->
					<view class="ra">
						<uni-rate v-model="item.rating.five" readonly />
						<text>{{item.rating.average}}</text>
					</view>
					<!-- 国家类型演员 -->
					<view class="cls">
						<text v-for="(i,ind) in item.countries" :key='ind'>{{i}}</text>/
						<text v-for="(it,inde) in item.genres" :key='inde'>{{it}}</text>/
						<text v-for="(ite,indx) in item.casts" :key='indx'>{{ite.name}}</text>
					</view>
				</view>
				<!-- 看过 -->
				<view class="look">
					<image src="../../static/666s.png" mode=""></image>
					<view class="lookbox">
						看过
					</view>
				</view>
			</view>
			<!--  -->
			<view class="int">
				希望让人自由
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
				obj:{},
				src: '',
				datalist:[],
				// 开始索引
				start:0,
				//加载多少条
				count:10
			}
		},
		onLoad(res) {
			//获取数据
			console.log(res)
			
			this.start=parseInt(res.start)
			this.count=parseInt(res.count)
			this.src = res.img
			this.obj=res
			this.request(this.obj)
			
			
		},
		//上拉刷新数据
		onReachBottom(){
			this.start+=parseInt(this.count)
			this.request(this.obj)
		},
		methods: {
          // 封装请求函数、
		  request(res){
			  uni.request({
			  	url: `http://t.yushu.im/v2/movie/${res.jk}`, //仅为示例，并非真实接口地址。
			  	data: {
			  		apikey:'0df993c66c0c636e29ecbb5344252a4a',
					start:this.start,
					count:this.count
					
			  	},
			  
			  	success: (res) => {
			  		console.log(res.data);
			  		for(let obj of res.data.subjects){
			  			obj.rating.five=obj.rating.average/2
			  		}
			         this.datalist=this.datalist.concat(res.data.subjects)
			  	}
			  });
		  }
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

	.img image {
		width: 100%;
		height: 400rpx;
	}

	.ranking {
		background-color: #FFFFFF;
		padding: 20rpx;
        margin-bottom: 40rpx
		;
		.rankbox {
			display: inline-block;
			padding: 5px;
			background-color: #FDD08B;
			color: #C79043;
			margin-bottom: 20rpx;
			border-radius: 5px;
			text-align: center;
			line-height: 50rpx;
		}

		.mdata {
			display: flex;
			justify-content: space-between;
			margin-bottom: 10px;
			image{
				width: 150rpx;
				height: 250rpx;
				margin-right:20rpx ;
			}
			.mbox{
				flex: 1;
				border-right: 1px solid #A0A0A0;
				.title{
					font-size: 18px;
					color: #333333;
				}
				.cls{
					color: #A0A0A0;
					text{
						margin-right: 5rpx;
					}
				}
				.ra{
					display: flex;
					margin: 10px;
				}
			}
			.look{
				width:150rpx ;
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: center;
				image{
					width: 20px;
					height: 20px;
					margin-bottom: 10rpx;
				}
				.lookbox{
					color:#E5B37F ;
				}
			}
		}
		.int{
			background-color:#F7F7F7 ;
			color:#A1A1A1 ;
			padding: 20rpx;
			}
	}
</style>
