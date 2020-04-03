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
			<view class="l-list-item" v-for="(s,i) in list" :key="i">
				<view class="l-item_view">
					<view class="l-item__value">
						<view class="l-item__value-title">
							漫画杂志
						</view>
						<view class="l-item__value-sub">
							16196本
						</view>
					</view>
					<image class="l-img-classify l-lay-gray" :src="s.isShow ? `../../static/classify/l-img-classify-1.png` : `#`" mode="aspectFill"></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	let list = []
	for (let i=0; i< 30; ++i) {
		let a = {isShow:!1}
		list.push(a)
	}
	export default {
		data(){
			return {
				list:list,
				el:[],
				wh:0,
				scrollTop:0,
				timeout:null
			}
		},
		onLoad() {
			
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
		methods:{
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
		}
	}
</script>

<style>
	.l-body {
		padding: var(--pad-lr);
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
	}

	.l-list-item {
		width: 330rpx;
		height: 160rpx;
		display: flex;
		align-items: center;
		justify-content: center;
		background-color: #F5F7F9;
		border-radius: 16rpx;
		margin-bottom: 24rpx;
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
