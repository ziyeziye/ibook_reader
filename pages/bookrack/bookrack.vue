<template>
	<view class="content">
		<view class="l-fixed">
			<!-- #ifndef MP-WEIXIN -->
			<view class="l-status"></view>
			<!-- #endif -->
			<!-- l-head -->
			<view class="l-head">
				<view class="l-search">
					<image class="l-icon-search" src="../../static/l-icon-search.png" mode=""></image>
					<input type="text" class="l-search-input" disabled="" value="" placeholder="精彩热搜：金光布袋戏《羽国志异》" placeholder-class="l-holder" />
				</view>
			</view>
		</view>

		<view class="l-placeholder"></view>

		<view class="l-body l-clear-both">
			<view class="l-li" v-for="(item,key) in 20" :key="key" @tap="navtoDetail">
				<image class="l-li-img" :src="bookimg" mode="aspectFill"></image>
				<view class="l-li-txt">
					JavaScript高级程序设计（第三版）
				</view>
			</view>
			<view class="l-add">
				<view class="l-add-view">
					<image class="l-icon-add" src="../../static/l-icon-add.png" mode=""></image>
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
				bookimg: `../../static/152b74dd6eb4c583fd8921a3f634b5dc.jpg`
			}
		},
		onLoad() {

		},
		methods: {
			navtoDetail() {
				uni.navigateTo({
					url: `/pages/detail/detail`
				})
			}
		}
	}
</script>

<style>
	/* l-body */

	.l-body {
		padding: var(--pad-lr) 0 var(--pad-lr) var(--pad-lr);
	}

	.l-ul {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding-bottom: 32rpx;
	}

	.l-add,
	.l-li {
		width: 28%;
		float: left;
		height: 392rpx;
		margin-right: 5%;
		margin-bottom: 32rpx;
	}

	.l-li {
		text-align: center;
	}

	.l-add-view,
	.l-li-img {
		width: 100%;
		height: 300rpx;
		border-radius: 10rpx;
		margin-bottom: 8rpx;
	}

	.l-add-view {
		box-sizing: border-box;
		display: flex;
		border: 6rpx solid rgba(126, 127, 148, 1);
		align-items: center;
		justify-content: center;
	}

	.l-icon-add {
		width: 36rpx;
		height: 36rpx;
	}

	.l-li-txt {
		padding: 0 10rpx;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 2;
		overflow: hidden;
	}
</style>
