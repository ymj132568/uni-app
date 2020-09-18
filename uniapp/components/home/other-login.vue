<template>
	<view class="other-login u-f-ac">
		<block v-for="(item,index) in providerList" :key="index">
			<view class="u-f-ajc u-f1" @tap="tologin(item)">
				<view class="icon iconfont u-f-ajc"
				:class="['icon-'+item.icon]">
				</view>
			</view>
		</block>
	</view>
</template>

<script>
	export default{
		data() {
			return {
				providerList: []
			}
		},
		onReady(){
			this.getLoginAuth()
		},
		methods:{
			getLoginAuth(){
				uni.getProvider({
					service:'oauth',
					success:(result)=>{
						this.providerList=result.provider.map((value)=>{
							let providerName='';
							let icon='';
							switch(value){
								case 'weixin':
								providerName='微信登录';
								icon:'weixin';
								break;
								case 'qq':
									providerName = 'QQ登录';
									icon='QQ';
									break;
								case 'sinaweibo':
									providerName = '新浪微博登录';
									icon='xinlangweibo';
									break;
								case 'alipay':
									providerName = '支付宝登录';
									icon='';
									break;
							}
							return{
								name:providerName,
								icon:icon,
								id:value
							}
						})
					},
					fail:(error)=>{
						
					}
				})
			},
			tologin(provider){
				uni.login({
					provider:provider.id,
					success:(res)=>{
						uni.getUserInfo({
							provider:provider.id,
							success:(infoRes)=>{
								
							}
						})
					},
					fail:(err)=>{
						
					}
				})
			}
		}
	}
</script>

<style>
	.other-login{
		padding: 20upx 80upx;
	}
	.other-login>view>view{
		width: 100upx;
		height: 100upx;
		border-radius: 100%;
		font-size: 55upx;
		color: #FFFFFF;
	}
	.other-login .icon-QQ{
		background: #2CAEFC;
	}
	.other-login .icon-weixin{
		background: #2BD19B;
	}
	.other-login .icon-xinlangweibo{
		background: #FC7729;
	}
</style>
