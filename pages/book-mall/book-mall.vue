<template>
	<view class="content">
		<!-- l-head -->

		<view class="l-head">
			<view class="l-search" @tap="$toast(`搜索`)">
				<image class="l-icon-search" src="../../static/l-icon-search.png" mode=""></image>
				<input type="text" class="l-search-input" disabled="" value="" placeholder="精彩热搜：金光布袋戏《羽国志异》" placeholder-class="l-holder" />
			</view>
		</view>

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

			<view class="l-body-tab">
				<view class="l-tab-item" @tap="$toast(`榜单`)">
					<image class="l-tab-item-img l-tab-item-img-1" src="../../static/book-mall/l-icon-book-mall-1.png" mode=""></image>
					<view class="l-tab-item-value">
						榜单
					</view>
				</view>
				<view class="l-tab-item" @tap="$toast(`新书`)">
					<image class="l-tab-item-img l-tab-item-img-2" src="../../static/book-mall/l-icon-book-mall-2.png" mode=""></image>
					<view class="l-tab-item-value">
						新书
					</view>
				</view>
				<view class="l-tab-item" @tap="$toast(`特价`)">
					<image class="l-tab-item-img l-tab-item-img-3" src="../../static/book-mall/l-icon-book-mall-3.png" mode=""></image>
					<view class="l-tab-item-value">
						特价
					</view>
				</view>
				<view class="l-tab-item" @tap="navtoClssify">
					<image class="l-tab-item-img l-tab-item-img-4" src="../../static/book-mall/l-icon-book-mall-4.png" mode=""></image>
					<view class="l-tab-item-value">
						分类
					</view>
				</view>
			</view>

		</view>

		<view class="l-view">
			<view class="l-h3">
				<text class="l-h3-title">好友在读</text>
				<view class="l-h3-more" @tap="$toast(`好友在读的换一换`)">换一换<image class="l-icon-refresh" src="../../static/book-mall/l-icon-refresh.png"
					 mode=""></image>
				</view>
			</view>

			<view class="l-dl" v-for="(s,i) in 2" :key="i" @tap="navtoDetail">
				<image class="l-dt" :src="bookimg" mode="aspectFill"></image>
				<view class="l-dd">
					<view class="l-dd-title">
						这个明星有些咸鱼
					</view>
					<view class="l-dd-content">
						重生平行世界，前世的疲惫，让李寒只想做一条安静的咸鱼。明星？出名？算了，虚无缥缈的东西！但是……他回家前写的一首主题曲却火了。我出名了？罢了，那就做一条明星中的咸鱼……
					</view>
					<view class="l-dd-footer">
						根据您读过的《离世人》推荐
					</view>
				</view>
			</view>
		</view>

		<view class="l-view">
			<view class="l-h3">
				<text class="l-h3-title">最新上架</text>
				<view class="l-h3-more" @tap="$toast(`最新上架的查看全部`)">查看全部<image class="l-icon-more" src="../../static/l-icon-more.png"
					 mode="widthFix"></image>
				</view>
			</view>

			<view class="l-dl-view" v-for="(s,i) in list" :key="i" @tap="navtoDetail">
				<view class="l-dl-bg"></view>
				<view class="l-dl-content">
					<image class="l-dt-view l-lay-gray" :src="s.isShow ? bookimg : ``" mode="aspectFill"></image>
					<view class="l-dd-view">
						<view class="l-dd-view-content">
							<view class="l-dd-view-title">
								<view class="l-dd-view-ta">
									三体：死神永生
								</view>
								<view class="l-dd-view-tb">
									作者：刘慈心
								</view>
							</view>
							<image class="l-icon-dot" src="../../static/l-icon-dot.png" mode="widthFix"></image>
						</view>
						<view class="l-dd-view-footer">
							刘慈欣创作的系列长篇科幻小说地球往事三部曲的第三部作品
						</view>
					</view>
				</view>
			</view>
		</view>

		<view class="l-view l-view-not-border">
			<view class="l-h3">
				<text class="l-h3-title">热门分类</text>
				<view class="l-h3-more" @tap="navtoClssify">全部分类<image class="l-icon-more" src="../../static/l-icon-more.png" mode="widthFix"></image>
				</view>
			</view>

			<view class="l-list-classify">
				<view class="l-list-item" v-for="(s,i) in 4" :key="i" @tap="$toast(`分类`)">
					<view class="l-item_view">
						<view class="l-item__value">
							<view class="l-item__value-title">
								漫画杂志
							</view>
							<view class="l-item__value-sub">
								16196本
							</view>
						</view>
						<image class="l-img-classify" :src="`../../static/classify/l-img-classify-1.png`" mode="aspectFill"></image>
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
				cover: `../../static/152b74dd6eb4c583fd8921a3f634b5dc.jpg`,
				list:[
					{isShow:!1},
					{isShow:!1},
					{isShow:!1},
					{isShow:!1},
					{isShow:!1}
				],
				el:[],
				scrollTop:0,
				timeout:null
			}
		},
		onReady() {
			let _this = this;
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
			navtoClssify() {
				uni.navigateTo({
					url: `/pages/classify/classify`
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
		computed:{
			wh(){
				return this.$system.windowHeight
			}
		}
	}
</script>

<style>
	/* l-body-tab */

	.l-body-tab {
		display: flex;
		margin: 20rpx 0 0;
		align-items: center;
		white-space: nowrap;
		justify-content: space-around;
	}

	.l-tab-item-img {
		margin-bottom: 10rpx;
	}

	.l-tab-item-img-3,
	.l-tab-item-img-1 {
		width: 60rpx;
		height: 58rpx;
	}

	.l-tab-item-img-2 {
		width: 52rpx;
		height: 56rpx;
	}

	.l-tab-item-img-4 {
		width: 54rpx;
		height: 54rpx;
	}

	.l-tab-item-value {
		text-align: center;
		font-size: 26rpx;
		color: var(--c-txt-2);
	}

	/* l-view */

	.l-view {
		padding: 40rpx var(--pad-lr);
		border-bottom: 1rpx solid #222337;
	}

	.l-view-not-border {
		padding-bottom: 0;
		border-bottom: none;
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

	.l-icon-refresh {
		width: 33rpx;
		height: 25rpx;
		margin-left: 12rpx;
	}

	.l-icon-dot {
		width: 30rpx;
		margin-top: 10rpx;
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

	.l-dd-view-footer,
	.l-dd-content {
		width: 100%;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		overflow: hidden;
	}

	.l-dd-view-footer {
		color: #868DAB;
		font-size: var(--f-size-1);
		-webkit-line-clamp: 2;
	}

	.l-dd-content {
		-webkit-line-clamp: 3;
	}

	.l-dd-footer {
		display: flex;
		align-items: center;
	}

	.l-dd-img {
		width: 40rpx;
		height: 40rpx;
		border-radius: 50%;
		margin-right: 6rpx;
	}


	/* l-dl-view */

	.l-dl-view {
		position: relative;
		height: 282rpx;
		margin-top: 32rpx;
	}

	.l-dl-bg {
		height: 250rpx;
		background: rgba(34, 35, 55, 1);
		box-shadow: 0px 30px 60px 0px rgba(17, 21, 26, 0.1);
		border-radius: 20rpx;
		position: absolute;
		top: 32rpx;
		left: 0;
		width: 100%;
	}

	.l-dl-content {
		position: relative;
		z-index: 1;
		display: flex;
		padding: 0 48rpx;
	}

	.l-dt-view {
		width: 168rpx;
		height: 250rpx;
		border-radius: 10rpx;
		margin-right: 30rpx;
	}

	.l-dd-view {
		width: calc(100% - 198rpx);
		padding: 62rpx 0 14rpx;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}

	.l-dd-view-content {
		display: flex;
		justify-content: space-between;
	}

	.l-dd-view-title {
		width: calc(100% - 62rpx);
		border-bottom: 1rpx solid #5D637C;
	}

	.l-dd-view-ta,
	.l-dd-view-tb {
		width: 100%;
		overflow: hidden;
		white-space: normal;
		text-overflow: ellipsis;
	}

	.l-dd-view-ta {
		font: bold var(--f-size-3) normal;
	}

	.l-dd-view-tb {
		color: #5D637C;
		padding: 14rpx 0 25rpx;
		font-size: var(--f-size-1);
	}

	/* l-classify */

	.l-list-classify {
		padding: 32rpx 0 0;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
	}

	.l-list-item {
		width: 330rpx;
		height: 160rpx;
		background-color: #F5F7F9;
		border-radius: 16rpx;
		margin-bottom: 24rpx;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.l-item_view {
		width: calc(100% - 64rpx);
		height: 122rpx;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	.l-item__value-title {
		font-size: var(--f-size-2);
		color: #2B3133;
		margin-bottom: 12rpx;
	}

	.l-item__value-sub {
		font-size: var(--f-size-1);
		color: #95A1A6;
	}

	.l-img-classify {
		width: 98rpx;
		height: 100%;
	}
</style>
