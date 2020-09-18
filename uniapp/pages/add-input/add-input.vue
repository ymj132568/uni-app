<template>
	<view>
		<uni-nav-bar :statusBar="true" rightText="发布" left-icon="back" @click-left='back' @click-right='submit'>
			<view class="u-f-ajc" @tap="changelook">
				{{yinsi}}
				<view class="icon iconfont icon-xialazhankai">
				</view>
			</view>
		</uni-nav-bar>
		<view class="uni-textarea">
			<textarea v-model="text" placeholder="输入文字"></textarea>
		</view>
		<uploud-images @uploud="uploud"></uploud-images>
		<uni-popup :show="showpopup" position="middle" mode='fixed' @hidePopup="hidePopup">
			<view class="gonggao">
			<view class="u-f-ajc">
					<image src="../../static/common/addinput.png" mode="widthFix"></image>
				</view>
				<view>1.涉及黄色，政治，广告及骚扰信息</view>
				<view>2.涉及黄色，政治，广告及骚扰信息</view>
				<view>3.涉及黄色，政治，广告及骚扰信息</view>
				<view>4.涉及黄色，政治，广告及骚扰信息</view>
				<button type="default" @tap="hidePopup">朕知道了</button>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	let changelook=['所有人可见','自己可见'];
	import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue";
	import uploudImages from "../../components/common/uploud-images.vue";
	import uniPopup from "../../components/uni-popup/uni-popup.vue";
	export default{
		components:{
			uniNavBar,
			uploudImages,
			uniPopup
		},
		data() {
			return {
				isget: false,
				yinsi:'所有人可见',
				imglist:[],
				text:'',
				showpopup:true
			}
		},
		onBackPress(){
			if(!this.text && this.imglist.length<1){return}
			if(!this.isget){
				this.baocun()
				return true
			}
		},
		methods:{
			baocun(){
				uni.showModal({
					content: '是否要保存为草稿？',
					cancelText: '不保存',
					confirmText: '保存',
					success: res => {
						if(res.confirm){
							console.log("保存")
						}else{
							console.log("不保存")
						}
						this.isget=true;
						uni.navigateBack({
							delta: 1
						});
					},
				});
			},
			back(){
				uni.navigateBack({delta:1})
			},
			submit(){},
			changelook(){
				uni.showActionSheet({
					itemList:changelook,
					success:(res)=>{
						this.yinsi=changelook[res.tapIndexd]
					}
				})
			},
			uploud(arr){
				this.imglist=arr;
				console.log(this.imglist)
			},
			hidePopup(){
				this.showpopup=false;
			}
		}
	}
</script>

<style>
	.uni-textarea{
		border: 1upx solid #EEEEEE;
	}
	.gonggao{
		width: 500upx;
	}
	.gonggao image{
		width: 75%;
		margin-bottom: 20upx;
	}
	.gonggao button{
		margin-top: 20upx;
		background: #FFE934;
		color: #171606;
	}
</style>
