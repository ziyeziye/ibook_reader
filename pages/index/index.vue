<template>
	<view class="content">
		<view class="l-fixed">
			<!-- #ifndef MP-WEIXIN -->
			<view class="l-status"></view>
			<!-- #endif -->

			<!-- l-head -->

			<view class="l-head">
				<view class="l-search" @tap="$toast(`搜索`)">
					<image class="l-icon-search" src="../../static/l-icon-search.png" mode=""></image>
					<input type="text" class="l-search-input" disabled="" value="" placeholder="精彩热搜：金光布袋戏《羽国志异》" placeholder-class="l-holder" />
				</view>
				<button class="l-nav-bookrack" @tap="navto">书城</button>
			</view>
		</view>

		<view class="l-placeholder"></view>

		<view class="l-body">

			<!-- l-swiper -->

			<swiper class="l-swiper" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="500" indicator-color="var(--c-bg-2)"
			 indicator-active-color="#41bdb2" circular @tap="$toast(`轮播图`)">
				<swiper-item>
					<view class="l-swiper-item">
						<image class="l-carousel-img" :src="img" mode="aspectFill"></image>
					</view>
				</swiper-item>
				<swiper-item>
					<view class="l-swiper-item">
						<image class="l-carousel-img" :src="img" mode="aspectFill"></image>
					</view>
				</swiper-item>
			</swiper>

			<!-- l-madin -->
			<view class="l-main">

				<view class="l-h3">
					<text class="l-h3-title">好友在读</text>
					<view class="l-h3-more" @tap="$toast(`好友在读的查看全部`)">查看全部<image class="l-icon-more" src="../../static/l-icon-more.png"
						 mode="widthFix"></image>
					</view>
				</view>

				<view class="l-dl" v-for="(s,i) in list" :key="i" @tap="navtoDetail">
					<image class="l-dt l-lay-gray" :src="s.isShow ? bookimg :`#`" mode="aspectFill"></image>
					<view class="l-dd">
						<view class="l-dd-title">
							这个明星有些咸鱼
						</view>
						<view class="l-dd-content">
							重生平行世界，前世的疲惫，让李寒只想做一条安静的咸鱼。明星？出名？算了，虚无缥缈的东西！但是……他回家前写的一首主题曲却火了。我出名了？罢了，那就做一条明星中的咸鱼……
						</view>
						<view class="l-dd-footer">
							<image class="l-dd-img" lazy-load src="../../static/logo.png" mode="aspectFill"></image>
							<image class="l-dd-img" lazy-load src="../../static/logo.png" mode="aspectFill"></image>
							<image class="l-dd-img" lazy-load src="../../static/logo.png" mode="aspectFill"></image>
							3位好友在读
						</view>
					</view>
				</view>

			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				img: `../../static/152b74dd6eb4c583fd8921a3f634b5dc.jpg`,
				bookimg: `../../static/152b74dd6eb4c583fd8921a3f634b5dc.jpg`,
				list:[
					{isShow:!1},
					{isShow:!1},
					{isShow:!1},
					{isShow:!1},
					{isShow:!1},
					{isShow:!1},
					{isShow:!1},
					{isShow:!1},
					{isShow:!1},
					{isShow:!1}
				],
				el:[],
				wh:0,
				scrollTop:0,
				timeout:null
			}
		},
		onLoad() {
			
		},
		onShow() {
			
		},
		onReady() {
			let _this = this;
			_this.wh = this.$system.windowHeight
			setTimeout(function(){
				_this.getNode()
			},300)
		},
		onPageScroll(e) {
			let _this = this;
			_this.timeout && clearTimeout(_this.timeout)
			
			_this.timeout = setTimeout(() => {
				_this.scrollTop = e.scrollTop;
				_this.layImg()
			},100)
			
		},
		methods: {
			navto() {
				uni.navigateTo({
					url: `/pages/book-mall/book-mall`
				})
			},
			navtoDetail() {
				uni.navigateTo({
					url: `/pages/detail/detail`
				})
			},
			layImg(){
				let _this = this;
				let el = _this.el;
				if(el.length === 0 ) return;
				let wh = _this.wh;
				let list = _this.list;
				let scrollTop = _this.scrollTop;
				
				el.forEach((e,i) => {
					if(!e.bool && e.top < (scrollTop + wh)){
						list[i].isShow = !0
						e.bool = !0;
					}
					
				})
				if(el[el.length - 1].bool){
					_this.el = []
				}else{
					_this.el = el
				}
				
				_this.list = list;
			},
			getNode(){
				let _this = this
				let query = uni.createSelectorQuery()
				query.selectAll(`.l-lay-gray`).boundingClientRect(function(e){
					_this.el = e
					_this.layImg()
				}).exec()
				
			}
		},
	}
</script>

<style>
	/* l-head */

	.l-nav-bookrack {
		font-size: 30rpx;
	}


	/* l-main */

	.l-main {
		padding-bottom: 32rpx;
	}

	.l-h3 {
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	.l-h3-title {
		font: bold var(--f-size-5) normal;
	}

	.l-h3-more {
		display: flex;
		align-items: center;
		color: var(--c-bg-2);
	}

	.l-dl {
		margin-top: 32rpx;
		display: flex;
		width: 100%;
		height: 224rpx;
	}

	.l-dt {
		width: 160rpx;
		height: 100%;
		border-radius: 10rpx;
		margin-right: 24rpx;
	}

	.l-dd {
		flex: 1;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}

	.l-dd-title {
		color: var(--c-txt-3);
		font: var(--f-size-3) normal;
	}

	.l-dd-content,
	.l-dd-footer {
		color: var(--c-txt-2);
		font: var(--f-size-2)/var(--f-size-4) normal;
	}

	.l-dd-content {
		width: 100%;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 3;
		overflow: hidden;
	}

	.l-dd-footer {
		display: flex;
		align-items: center;
	}

	.l-dd-view-footer {
		width: 100%;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		overflow: hidden;
		-webkit-line-clamp: 2;
	}

	.l-dd-img {
		width: 40rpx;
		height: 40rpx;
		border-radius: 50%;
		margin-right: 6rpx;
	}
</style>
