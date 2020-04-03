<template>
	<scroll-view :style="{'background-color': currentThemeColor.backgroundColor}" scroll-y class="ss-slider">
		<block>
			<view>
				<h3 style="display: flex;justify-content: center;padding: 15px" :style="{'color':currentThemeColor.color}">章节目录</h3>
			</view>
			<view style="padding: 10px;">
				<text style="float: left" :style="{'color':currentThemeColor.color}">共256章</text>

				<text @click="reverse_list" style="float: right" :style="{'color':currentThemeColor.color}">倒序</text>
			</view>
			<view class="title_line" :style="{'background-color': currentThemeColor.borderColor}">
				正文卷
			</view>
		</block>
		<view v-if="chapterList.length>0">
			<block v-for="(item, index) in chapterList" :key="index">
				<view @click="chapterItemAction(index)" class="chapter-item" :style="{'color': currentChapter ==  index ? '#449bda' : currentThemeColor.color}" :class="{'chapter-current-item': currentChapter ==  index}">
					<text>{{item.title}}</text>
				</view>
				<view class="line" :style="{'background-color': currentThemeColor.borderColor}"></view>
			</block>
		</view>
		<view v-else style="text-align: center;margin-top: 100%;">暂无更多章节~</view>
	</scroll-view>
</template>

<script>
	export default {
		name: 'ss-slider',
		props: {
			chapterList: {
				type: Array,
				default () {
					return [];
				}
			},
			index: {
				type: Number,
				default () {
					return 0;
				}
			},
			currentChapter: {
				type: Number,
				default () {
					return 0;
				}
			},
			isNightTheme: {
				type: Boolean,
				default () {
					return false;
				}
			}

		},
		computed: {
			currentThemeColor: function () {
				return this.isNightTheme ? this.nightThemeColor : this.dayThemeColor;
			}
		},
		data () {
			return {
				dayThemeColor: {
					backgroundColor: '#fff',
					color: '#333',
					borderColor: '#f0f0f0'
				},
				nightThemeColor: {
					backgroundColor: '#333',
					color: '#808080',
					borderColor: '#808080'
				}
			}
		},
		methods: {
			reverse_list() {
				this.chapterList = this.chapterList.reverse()
			},
			chapterItemAction (index) {
				this.$emit('chapterItemTap', index);
			}
		}
	}
</script>

<style lang="scss">
	.ss-slider {
		height: 100%;
		display: flex;
		flex-direction: column;

		.title_line {
			background-color: rgb(240, 240, 240);
			padding: 8px;
			margin: 25px 0 auto;
			display: flex;
			/*justify-content: center;*/
			align-items: center;
			color: #c7c5c0;
			clear: both;
		}

		.line {
			margin: 0 10upx 0upx 30upx;
			height: 1px;
		}

		.chapter-item {
			padding: 20upx 30upx;
			font-size: $uni-font-size-base;
		}

		.chapter-current-item {
			color: #449bda;
		}
	}
</style>
