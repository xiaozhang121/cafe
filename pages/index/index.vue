<template>
	<view class="content">
		<!-- 通知框占位 -->
		<view class="mess">
		</view>
		<!-- 日期选择 -->
		<view class="top">
			<view class="top-left">
				<picker :value="xb" :range="array" @change="select">
					<view class="">
						{{array[xb]}}
					</view>
				</picker>
			</view>
			<view class="top-right">
					一键导航
			</view>
		</view>
		<!-- 座位选择 -->
		<view class="main">
			<view class="main-tp">
				<text>使用中</text>
				<text>使用中</text>
				<text>使用中</text>
				<text>使用中</text>
				<text>使用中</text>
			</view>
			<view class="main-md">
				<image src="../../static/sit.png" mode="" class="bg"></image>
				<view class="md-all">
					<view class="oneline-a">
						<view class="left-a-line">
							<view class="a-one" v-if="index<=5" v-for="(item,index) in numberList" :key = 'item.id' :data-id='item.id' @click="selectsit"  :data-active='item.current'>
								<image :src="item.image" mode=""></image>
								<view class="a-one-id">
									{{item.id}}
								</view>
							</view>
						</view>
						<view class="left-b-line">
							<view class="b-one" v-if="index>=6&&index<=10" v-for="(item,index) in numberList" :key='item.id' :data-id = 'item.id' @click="selectsit" :data-active='item.current'>
								<image :src="item.image" mode=""></image>
								<view class="b-one-id">
									{{item.id}}
								</view>
							</view>
						</view>
					</view>
					<view class="oneline-b">
							<view class="left-c-line">
								<view class="c-one"  v-if="index>10&&index<=11" v-for="(item,index) in numberList" :key = 'item.id' :data-id='item.id' @click="selectsit" :data-active='item.current'>
									<image :src="item.image" mode=""></image>
									<view class="c-one-id">
										{{item.id}}
									</view>
								</view>
							</view>
							<view class="left-d-line">
								<view class="d-one" v-if="index>11" v-for="(item,index) in numberList" :key = 'item.id' :data-id='item.id' @click="selectsit" :data-active='item.current'> 
									<image :src="item.image" mode=""></image>
									<view class="d-one-id">
										{{item.id}}
									</view>
								</view>
							</view>
					</view>
					</view>
					
					
				</view>
				<!-- 预约 -->
				<view class="main-bd" @click="makesure">
					确认选座
				</view>
			</view>
			<!-- 遮罩区域 -->
			<view class="black" v-if="sure">
				<!-- 预定时间 -->
				<view class="time" >
					<view class="time-text">
						预计到店时间
					</view>
					<picker :range="timearr"  :value="tm" @change="suretime">
						<view>{{timearr[tm]}}</view>
					</picker>
					<view class="btn" @click="pay">
						确认时间
					</view>
					<view class="cha" @click="sure=false">
						X
					</view>
				</view>
			</view>
		</view>
</template>

<script>
	export default {
		data() {
			return {
				sure:false,
				xb:0,
				array:['昨天','今天','明天'],
				timearr:['1:00','2:00','3:00','4:00','5:00','6:00','7:00','8:00','9:00','10:00','11:00','12:00'],
				tm:0,
				selectlist:[],
				numberList: [{
						id: 1,
						image: "../../static/sofa.png",
						current:0
					},
					{
						id: 2,
						image: "../../static/sofa.png",
						current:0
					},
					{
						id: 3,
						image: "../../static/sofa.png",
						current:0
					},
					{
						id: 4,
						image: "../../static/sofa.png",current:0
					},
					{
						id: 5,
						image: "../../static/sofa.png",current:0
					},
					{
						id: 6,
						image: "../../static/sofa.png",current:0
					},
					{
						id: 7,
						image: "../../static/sofa.png",current:0
					},
					{
						id: 8,
						image: "../../static/sofa.png",current:0
					},
					{
						id: 9,
						image: "../../static/sofa.png",current:0
					},
					{
						id: 10,
						image: "../../static/sofa.png",current:0
					},
					{
						id: 11,
						image: "../../static/sofa.png",current:0
					},
					{
						id: 12,
						image: "../../static/sofa.png",current:0
					},
					{
						id: 13,
						image: "../../static/sofa.png",current:0
					},
					{
						id: 14,
						image: "../../static/sofa.png",current:0
					},
					{
						id: 15,
						image: "../../static/sofa.png",current:0
					},
					{
						id: 16,
						image: "../../static/sofa.png",current:0
					},
					{
						id: 17,
						image: "../../static/sofa.png",current:0
					},
					{
						id: 18,
						image: "../../static/sofa.png",current:0
					},
					{
						id: 19,
						image: "../../static/sofa.png",current:0
					},
					{
						id: 20,
						image: "../../static/sofa.png",current:0
					}
				],
				actived:'',
				
				
				
			}
		},
		onShow() {
		
		this.show()
		},
		methods: {
			suretime(e){
				this.tm = e.detail.value;
				
			},
			show(){
				this.selectlist = uni.getStorageSync('paymessage').sele;
				this.selectlist.filter((item,index)=>{
					for(let i = 0;i<this.numberList.length;i++){
						if(this.numberList[i].id===item){
							this.numberList[i].image = '../../static/lan.png'
						}
					}
				})
			},
			pay(){
				
					var param = {
						day:this.array[this.xb],
						time:this.timearr[this.tm],
						sele:this.selectlist
					}
					uni.setStorageSync('paymessage',param);
					this.sure = false;
					uni.showToast({
					            title: '预订成功'
					          })
					uni.switchTab({
						url:'../find/index'
					})
					
					// this.seldel()
				
			},
			
			makesure(){
				if(this.selectlist.length!=0){
					this.sure = true;
				}else{
					uni.showToast({
						title:"请选择座位",
						'icon':'none'
					})
				}
			},
		select(e){
			this.xb = e.detail.value
		},
		selectsit(e){
				if(e.currentTarget.dataset.active){
					this.actived = e.currentTarget.dataset.id;
					// this.selectlist.push(e.currentTarget.dataset.id)
					// this.selectlist = Array.from(new Set(this.selectlist))
					// console.log(this.selectsit)
					this.numberList[this.actived].image = '../../static/sofa.png';
					this.numberList[this.actived].current = 0;
					//清除数组中的取消的元素
					this.selectlist = this.selectlist.filter((value,item)=>{
						return value-e.currentTarget.dataset.id
					})
					
				}
					else{
						console.log(e.currentTarget.dataset.id)
						this.actived = e.currentTarget.dataset.id;
						// this.selectlist.splice()
						this.numberList.filter((item,index)=>{
							if(item.id===this.actived){
								item.image = '../../static/lan.png'
								item.current = 1;
							}
						})
						// this.numberList[this.actived].image = '../../static/lan.png'
						// this.numberList[this.actived].current = 1;
						//去重
						if(this.selectlist.indexOf(e.currentTarget.dataset.id)===-1){
							this.selectlist.push(e.currentTarget.dataset.id)
						}
					}
				console.log(this.selectlist)
		}
		}
	}
</script>

<style lang="less" scoped>
	.content{
		.mess{
			height: 50rpx;
			width: 100%;
			box-sizing: border-box;
		}
		.top {
			height: 100rpx;
			padding: 4% 2%;
			line-height: 100rpx;
			text-align: center;
			.top-left {
				width: 400rpx;
				border-radius: 200rpx;
				height: 100rpx;
				border: 2rpx solid #333;
				float: left;
				
			}
			.top-right {
				float: right;
				width: 240rpx;
				height: 100rpx;
				border-radius:200rpx;
				border: 2rpx solid #333;
				
			}
		}
		.main {
		margin-top: 20rpx;
		.main-tp{
			display: flex;
			padding: 2%;
			text {
				flex: 1;
				text-align: center;
			}
		}
		.main-md {
			margin:8%;
			position: relative;
			.bg {
				width: 100%;
				height: 812rpx;
			}
			.md-all{
				display: flex;
				width: 97%;
				position: absolute;
				justify-content: space-between;
				left: 0;
				top: 7%;
				padding: 2%;
				height: 730rpx;
				.oneline-a{
					width: 43%;
					display: flex;
					justify-content: space-between;
					.a-one{
						position: relative;
						>image{
							width: 60rpx;
							height: 60rpx;
							transform: rotate(90deg);
						}
						.a-one-id {
							position: absolute;
							top: 0;
							left: 5rpx;
						}
					}
					.a-one{
						position: relative;
						>image{
							width: 60rpx;
							height: 60rpx;
							transform: rotate(90deg);
						}
						.a-one-id {
							position: absolute;
							top: 0;
							left: 5rpx;
							width: 60rpx;
							height: 60rpx;
							line-height: 60rpx;
							text-align: center;
						}
					}
					.b-one{
						position: relative;
						>image{
							width: 60rpx;
							height: 60rpx;
							transform: rotate(-90deg);
						}
						.b-one-id {
							position: absolute;
							top: 0;
							left: 5rpx;
							width: 60rpx;
							height: 60rpx;
							text-align: center;
							line-height: 60rpx;
						}
					}
				}
				.oneline-b{
					width: 49%;
					display: flex;
					justify-content: space-between;
					.left-c-line{
						width: 25%;
					}
					.left-d-line{
						width: 45%;
						padding: 0 4%;
						display: flex;
						align-content: flex-start;
						// height: 86rpx;
						flex-wrap: wrap;
						justify-content: space-between;
						// view:first-child :nth-child(2){
						// 	margin-top: 0;
						// 	}
						.d-one{
							position: relative;
							margin-bottom:4%;
							image{
								width: 60rpx;
								height: 60rpx;
							}
							.d-one-id {
								
								position: absolute;
								top: 0;
								left: 5rpx;
								width: 60rpx;
								height: 60rpx;
								text-align: center;
								line-height: 60rpx;
							}
						}
					}
					.c-one{
						position: relative;
						>image{
							width: 60rpx;
							height: 60rpx;
							transform: rotate(90deg);
						}
						.c-one-id {
							position: absolute;
							top: 0;
							left: 5rpx;
							width: 60rpx;
							height: 60rpx;
							text-align: center;
							line-height: 60rpx;
						}
					}
				}
			}
		}
		.main-bd{
			height: 100rpx;
			margin: 50rpx auto;
			width: 60%;
			border-radius: 20rpx;
			background-color: yellow;
			text-align: center;
			line-height: 100rpx;
		}
		
		}
		.black {
			width: 100%;
			height: 100%;
			position: fixed;
			background-color: rgba(0,0,0,.3);
			top: 0;
			left: 0;
			bottom: 0;
			.time {
				position: absolute;
				top: 60%;
				left: 50%;
				width: 600rpx;
				height: 400rpx;
				transform: translate(-50%,-50%);
				border-radius: 20rpx;
				background-color: white;
				padding: 5%;
				.time-text{
					text-align: center;
					margin-bottom: 100rpx;
				}
				picker{
					width: 200rpx;
					height: 80rpx;
					border: 2rpx solid #ccc;
					margin: 0 auto;
					line-height: 80rpx;
					text-align: center;
				}
				.btn {
					width: 80%;
					height: 80rpx;
					margin: 40rpx auto 0;
					background-color: yellow;
					text-align: center;
					line-height: 80rpx;
					border-radius: 40rpx;
				}
				.cha {
					position: absolute;
					top: 20rpx;
					right: 30rpx;
				}
			}
		}
	}
</style>