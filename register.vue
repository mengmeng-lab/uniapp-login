<!-- 个人中心 -->
<template>
	
					<button type="primary" @click="login">授权登录</button>
					
</template>

<script>
	export default {
		data() {
			return {
				nickName:"",
        avatarUrl:""
			}
		},
		
		methods: {
			login() { 
							uni.getUserProfile({
								desc: '注册',
								success: (res) => {
									console.log("用户信息："+JSON.stringify(res.userInfo));
									uni.login({
										provider:'weixin',
										success:(res2) =>{
											uni.showLoading({
												title:'登录中'
											})
											var code = res2.code
											console.log("获取code成功：" + JSON.stringify(res2))
											
											uni.request({
												url:'',
												method:'POST',
												header:{
													"content-type": "application/x-www-form-urlencoded",
													"source":"fromApp"
												},
												data: {
													info:JSON.stringify({
														"code":code,
														"nickName":UserInfo.nickName
													})
												},
												success: (res3) => {
													console.log('登录成功：'+JSON.stringify(res3))
													uni.hideLoading()
													this.nickName = userInfo.nickName
													this.avatarUrl = userInfo.avatarUrl
												},
												fail: (err) => {
													uni.hideLoading()
													uni.showToast({
														title:'登录失败',
														icon:'none'
													})
												}
											})
										}
									})
								},
								fail: (res) => {
									console.log(res)
								}
							});
						},
		
		}
	}
</script>

<style>
</style>
