<template>
	<view class="find">
		<view class="fill">
			
		</view>
		<view class="title">
			<view class="order">
				预约
			</view>
			<view class="goon">
				进行
			</view>
		</view>
		<view class="ordery">
			<view class="one" v-for="(item,index) in ticket">
				<view class="one-tp">
					<view style="font-size: 36rpx;color: #333;margin-bottom: 30rpx;">
						南岸书吧(胜太点)
					</view>
					<view style="font-size: 28rpx;color: #333;">
						预约时间:{{time}}
					</view>
					<view style="font-size: 28rpx;color: #333;">
						最迟到店:{{time}}
					</view>
				</view>
				<view class="one-bt">
					取消预约
				</view>
				<view class="sitnum">
					<view style="font-size: 44rpx;color: #FFE60F;font-weight: 700;">
						{{item}}
					</view>
					<view class="">
						座位号
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		onShow() {
			console.log(uni.getStorageSync('paymessage'))
			this.ticket = uni.getStorageSync('paymessage').sele
			this.time = uni.getStorageSync('paymessage').time
			// this.$set(this.ticket, uni.getStorageSync('paymessage').sele)
			// this.$set(this.time, uni.getStorageSync('paymessage').time)
			console.log(this.ticket)
		},
		data(){
			return {
				ticket:[],
				time:''
			}
		}
	}
</script>

<style lang="less" scoped>
	.find{
		.fill{
			height: 25rpx;
			background-color: yellow;
			width: 100%;
		}
		.title{
			display: flex;
			justify-content: center;
			height: 10%;
			.goon,.order{
				margin: 4% 4% 0 4%;
				font-size: 36rpx;
				height: 55rpx;
			}
			.order:hover{
				border-bottom: 6rpx solid yellow;
			}
			.goon:hover{
				border-bottom: 6rpx solid yellow;
			}
			
		}
		.ordery{
			box-sizing: border-box;
			padding: 10% 3%;
			width: 100%;
			position: absolute;
			top: 114rpx;
			left: 0;
			bottom: 0;
			background-color: rgb(242, 242, 242);
			.one {
				margin-bottom: 10%;
				position: relative;
				height: 320rpx;
				background-color: white;
				border-radius: 20rpx;
				.one-tp{
					padding: 0 4%;
					height: 220rpx;
					border-radius: 20rpx;
					background-color: white;
					position: relative;
					bottom: -20rpx;
				}
				.one-bt{
					height: 100rpx;
					 border-radius:  20rpx;
					background-color: #FFE60F;
					line-height: 120rpx;
					text-align: center;
					color: white;
				}
				.sitnum{
					position: absolute;
					right: 10%;
					top: 15%;
				}
			}
		}
	}
</style>
