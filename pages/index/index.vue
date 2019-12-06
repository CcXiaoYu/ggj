	<template>
	<view class="contentView">
		<!-- 视频广告 -->
		<view class="contentVideoBox">
			<video @ended="playComplete(viewMain.id)" :src="viewMain.vSrc" :controls="false" :loop="viewMain.isLoop" objectFit="fill" :show-fullscreen-btn="false" :show-center-play-btn="false" preload="auto" :autoplay="autoplay"></video>
		</view>
		<!-- 图文广告 -->
		<view class="contentPicBox">
			<image :src="viewMain.pSrc" mode="widthFix"></image>
		</view>
		<!-- 代理商广告 -->
		<view class="contentAgentBox">
			<view class="agentAdBox">
				<text>代理加盟热线：0471-3484526</text>
				<text>微众网络传媒</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				n: 0,
				autoplay:false,
				interval:15000,
				duration:300,
				viewMain: {
					vSrc: "",
					pSrc: "",
					id: ""
				},
				adList: [{
						vSrc: "../../static/video/1.mp4",
						pSrc: "../../static/picAdImg1.jpg",
						isLoop:false,
						id: 1
					},
					{
						vSrc: "../../static/video/2.mp4",
						pSrc: "../../static/picAdImg2.jpg",
						isLoop:true,
						id: 2
					},
					{
						vSrc: "../../static/video/3.mp4",
						pSrc: "../../static/picAdImg3.jpg",
						isLoop:true,
						id: 3
					}
				]
			}
		},
		onLoad() {
			// this.viewMianFunc()
		},
		onReady(){
			this.viewMianFunc()
		},
		methods: {
			playComplete(id) {
				for( let i = 0; i < this.adList.length; i++ ) {
					if( this.adList[i].id === id ) {
						this.viewMain.pSrc = this.adList[i+1].pSrc
						this.viewMain.vSrc = this.adList[i+1].vSrc 
						this.viewMain.id = this.adList[i+1].id 
						return
					} else {
						this.viewMain.pSrc = this.adList[0].pSrc
						this.viewMain.vSrc = this.adList[0].vSrc 
						this.viewMain.id = this.adList[0].id 
					}
				}
			},
			viewMianFunc() {
				this.viewMain.pSrc = this.adList[0].pSrc
				this.viewMain.vSrc = this.adList[0].vSrc 
				this.viewMain.id = this.adList[0].id 
				this.autoplay = true
			}
		},
		
	}
</script>

<style lang="less">
	.contentVideoBox {
		width: 100vw;
		height: 30vh;
		video {
			display: block;
			width:100vw;
			height:30vh;
		}
	}

	.contentPicBox {
		height:65vh;
		overflow:hidden;
		image {
			width:100%;
			height:65vh;
			display:inline-block;
		}
	}
	.contentAgentBox{
		padding-top:0.2vh;
		height:4.8vh;
		background:#F0AD4E;
		.agentAdBox{
			text{
				display:block;
				text-align:center;
				font-size:0.6rem;
				&:last-of-type{
					font-size:1.6vh;
				}
			}
		}
	}
</style>
