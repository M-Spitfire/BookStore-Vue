<!--  -->
<template>
<div>
  <div id="header">
			<img class="logo_img" alt="" src="../../assets/img/logo.gif" >
			<span class="wel_word">订单管理系统</span>
			<div>
				<router-link to="/book_manager">图书管理</router-link>
				<router-link to="/order_manager">订单管理</router-link>
				<router-link to="/">返回首页</router-link>
			</div>
	</div>
	
	<div id="main">
		<table>
			<tr>
				<td>日期</td>
				<td>金额</td>
				<td>详情</td>
				<td>发货</td>
				
			</tr>		
			<tr v-for="order in orderList" :key="order.orderId">
				<td>{{order.createTime | formatDate}}</td>
				<td>{{order.price}}</td>
				<td><a href="#">查看详情</a></td>
				<td>{{order.status}}</td>
			</tr>	
				
		</table>
	</div>
	
	<div id="bottom">
		<span>
			尚硅谷书城.Copyright &copy;2015
		</span>
	</div>
</div>
</template>

<script>
//这里可以导入其他文件（比如：组件，工具js，第三方插件js，json文件，图片文件等等）
//例如：import 《组件名称》 from '《组件路径》';
import {formatDate} from '../../common/date.js';

export default {
//import引入的组件需要注入到对象中才能使用
components: {},
data() {
//这里存放数据
return {
	orderList:[]
};
},
//监听属性 类似于data概念
computed: {},
//监控data中的数据变化
watch: {},
//方法集合
methods: {

},
//生命周期 - 创建完成（可以访问当前this实例）
created() {

},
//生命周期 - 挂载完成（可以访问DOM元素）
mounted() {
	this.$axios({
		method:'post',
		url:'/BookStore/orderService',
		data:{
			'action':'showAllOrders'
		}
	})
	.then((result) => {
		// console.log(result.data);
		let items = result.data;
		for(let index in items){
			this.orderList.push(items[index]);
		}
		// console.log('orderList:')
		// console.log(this.orderList);
	}).catch((err) => {
		console.log(err);
	});
},

filters: {
	formatDate(time) {
		var date = new Date(time);
		return formatDate(date, 'yyyy-MM-dd hh:mm');
	}
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

</style>