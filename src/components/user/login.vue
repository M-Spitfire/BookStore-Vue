<!--  -->
<template>
<div>
  <div id="login_header">
			<img class="logo_img" alt="" src="../../assets/img/logo.gif" >
		</div>
		
			<div class="login_banner">
			
				<div id="l_content">
					<span class="login_word">login</span>
				</div>
				
				<div id="content">
					<div class="login_form">
						<div class="login_box">
							<div class="tit">
								<h1>atguigu vip</h1>
								<router-link to="/register">注册</router-link>
							</div>
							<div class="msg_cont">
								<b></b>
								<span class="errorMsg">{{login_info}}</span>
							</div>
							<div class="form">
								<form><!--action="userService" method="post"-->
									<label>username:</label>
									<input class="itxt" type="text" placeholder="input username"
										   autocomplete="off" tabindex="1" v-model="username" />
									<br />
									<br />
									<label>password:</label>
									<input class="itxt" type="password" placeholder="input password"
										   autocomplete="off" tabindex="1" v-model="password" />
									<br />
									<br />
									<input type="button" value="login" id="sub_btn" @click="login()"/>
								</form>
							</div>
							
						</div>
					</div>
				</div>
			</div>
		<div id="bottom">
			<span>
				atguigu BookStore.Copyright &copy;2015
			</span>
		</div>
</div>
</template>

<script>
//这里可以导入其他文件（比如：组件，工具js，第三方插件js，json文件，图片文件等等）
//例如：import 《组件名称》 from '《组件路径》';

export default {
//import引入的组件需要注入到对象中才能使用
components: {},
data() {
//这里存放数据
return {
	username:"",
	password:"",
	login_info:"input username and pasword"
};
},
//监听属性 类似于data概念
computed: {},
//监控data中的数据变化
watch: {},
//方法集合
methods: {
	login(){
		// console.log("username:",this.username);
		// console.log("password:",this.password);
		let self = this;
		this.$axios({
			method: 'post',
			url: '/BookStore/userService',
			// url: '/BookStore/loginServlet',
			data: {
				"action":"login",
				"username":self.username,
				"password":self.password
			}
		})
		.then((response) => {
			// console.log(response.data);
			this.login_info = response.data.info;
			this.$message(response.data.info)
			if(response.data.state == 4){
				this.$router.push("/login_success")
			}
		})
		.catch(function (error) {
			console.log(error);
		});
	}
},
//生命周期 - 创建完成（可以访问当前this实例）
created() {

},
//生命周期 - 挂载完成（可以访问DOM元素）
mounted() {

},
beforeCreate() {}, //生命周期 - 创建之前
beforeMount() {}, //生命周期 - 挂载之前
beforeUpdate() {}, //生命周期 - 更新之前
updated() {}, //生命周期 - 更新之后
beforeDestroy() {}, //生命周期 - 销毁之前
destroyed() {}, //生命周期 - 销毁完成
activated() {}, //如果页面有keep-alive缓存功能，这个函数会触发
}
</script>
<style scoped>
/*// @import url(); 引入公共css类*/
/* @import url("../../static/css/style.css"); */
</style>