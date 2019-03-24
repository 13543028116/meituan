<template>
  <div class="cartcontrol">
    <transition name="move">
			<div class="cart-decrease icon-remove_circle_outline" @click.stop.prevent="decreaseCart" v-show="food.count">
			</div>
		</transition>
		<div class="cart-count" v-show="food.count">{{food.count}}</div>
		<!-- @click.stop.prevent停止冒泡事件 -->
			<div class="cart-add icon-add_circle" @click.stop.prevent="increaseCart">
					<i class="bg"></i>
			</div>
  </div>
</template>

<script>
// 拥有全局的api
import Vue from 'vue'

export default {
	props:{
			food:{
				type:Object
			}
	},
  methods:{
		decreaseCart(){
			this.food.count--
		},
		increaseCart(){
			// 判断当前的这个东西存不存在 
			if(!this.food.count){
				// 往数据里添加数据
				Vue.set(this.food,"count",1)
			}else{
				this.food.count++
			}
		}
	}
}
</script>


<style scoped>
@import url(../../common/css/icon.css);
.cartcontrol{
	font-size: 0;
}

.cartcontrol .cart-decrease{
	display: inline-block;
	width: 26px;
	height: 26px;
	font-size: 26px;
	color: #b4b4b4;
}

.cartcontrol .cart-add .bg{
	width: 20px;
	height: 20px;
	border-radius: 50%;
	background: black;
	position: absolute;
	left: 3px;
	top: 3px;
	z-index: -1;
}


.cartcontrol .cart-count{
	display: inline-block;
	width: 25px;
	text-align: center;
	font-size: 12px;
	line-height: 26px;
	vertical-align: top;
}

.cartcontrol .cart-add{
	display: inline-block;
	width: 26px;
	height: 26px;
	font-size: 26px;
	color: #ffd161;
	position: relative;
}

.move-enter-active,.move-leave-active{
	transition: all 0.5s linear;
}
.move-enter,.move-leave-to{
	transform: translateX(20px) rotate(180deg);
}
</style>