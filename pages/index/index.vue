<template>
	<scroll-view>
		<uni-nav-bar fixed="true" status-bar="true">
			<view class="input-view">
				<uni-icon type="search"></uni-icon>
				<input confirm-type="search" @input="inputs" @confirm="sousuo" class="input" type="text" placeholder="输入搜索关键词" />
			</view>
			<view slot="left"><text @click="ceshi">全部</text></view>
			<view slot="right"><uni-icon type="contact" @click="usery"></uni-icon></view>
		</uni-nav-bar>
		<view class="kuangjia">
			<view v-for="item in neirong" :key="item"  class="cat" @click="xxi(item.id)">
				<view><text style="font-size: 38upx;">{{item.name}}</text></view>
				<view class="zhuti">
					<view class="zuo">
						<text class="users">{{item.zuoze}}</text>
					</view>
					<view class="you">
						<text class="times">{{item.time}}</text>
					</view>
				</view>
				<view><text style="font-size: 30upx;">{{item.content}}</text></view>
			</view>
			<view class="cat">3</view>
			<view style="background-color: #F5F5F5;width: 100upx;">1</view>
			<view class="cat">
				<view><text style="font-size: 38upx;">故事名字</text></view>
				<view class="zhuti">
					<view class="zuo">
						<text class="users">admin</text>
					</view>
					<view class="you">
						<text class="times">2019-10-12 08:12:00</text>
					</view>
				</view>
				<view><text style="font-size: 30upx;">1故事内容故事内容故事内容故事内容故事内容故事内容故事内容故事内容故事内容故事内容故事内容故事内容故事内容故事内容故事内容故事内容故事内容故事内容</text></view>
			</view>
			<view class="cat">4</view>
			<view>5</view>
			<view>1</view>
			<view>1</view>
		</view>
	</scroll-view>
</template>

<script>
	import uniNavBar from "@/components/uni-nav-bar/uni-nav-bar.vue"
	import uniIcon from "@/components/uni-icon/uni-icon.vue"
	export default {
		components: {
			uniNavBar,
			uniIcon
		},
		data() {
			return {
				shuju:'1',
				neirong:[]
			}
		},
		onLoad() {
			uni.request({
				url:'https://easy-mock.com/mock/5c46b599765dc578878eaf5b/jielong/list',
				success:(res)=>{
					console.log(res.data.data);
					this.neirong = res.data.data
				}
			})
		},
		onPullDownRefresh() {
			uni.request({
				url:'https://easy-mock.com/mock/5c46b599765dc578878eaf5b/jielong/list',
				success: (res) => {
					console.log(res.data.data);
					this.neirong = res.data.data
					uni.stopPullDownRefresh()
				}
			})
		},
		methods: {
			sousuo:function(event) {
				console.log(event.target.value);
				uni.navigateTo({
					url:'../ceshi/ceshi?id='+event.target.value
				})
			},
			inputs:function(event){
				this.shuju = event.target.value;
			},
			xxi:function(e){
				console.log(e);
				uni.navigateTo({
					url:'../content/content?name=' + e
				})
			},
			ceshi:function(e){
				console.log("点击了左边")
				uni.navigateTo({
					url:'../ceshi/ceshi'
				})
			},
			usery:function(e){
				console.log("点击了右边")
				uni.navigateTo({
					url:'../user/user'
				})
			}
		}
	}
</script>

<style>
	.cat{
		padding: 10upx;
		background-color: #F5F5F5;
		box-shadow: 4px 4px 1px #DCDCDC;
		margin: 30upx;
	}
	.kuangjia{
		padding-top: 160upx;
/* 		padding-left: 24upx;
		padding-right: 24upx; */
	}
	.title {
		font-size: 15px;
		line-height: 20px;
		color: #333333;
		padding: 15px;
	}
	.city {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: center;
		width: 100%;
		margin-left:8px;
	}
	.input-view {
		width: 90%;
		display: flex;
		background-color: #e7e7e7;
		height: 30px;
		border-radius: 15px;
		padding: 0 4%;
		flex-wrap:nowrap;
		margin:7px 0;
		line-height:30px;
	}
	.input-view .uni-icon{
		line-height:30px !important;
	}
	.input-view .input {
		height:30px;
		line-height:20px;
		width:94%;
		padding: 0 3%;
	}
	.zhuti{
        display:flex;         /*flex布局*/
    }
    .zuo{
        /* width:250upx; */
        flex:none;
    }
	.users{
		font-size: 26upx;
		color: #808080;
	}
	.you{
		text-align: right;
        height:100%;
        flex:1;        /*flex布局*/
    }
	.times{
		font-size: 26upx;
		color: #808080;
	}
</style>
	