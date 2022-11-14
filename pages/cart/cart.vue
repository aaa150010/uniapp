<template>
	<view class="cart-container" v-if="cart.length!==0">
		<my-address></my-address>
		<view class="cart-title">
			<uni-icons type="shop" size="18"></uni-icons>
			<text class="cart-title-text">购物车</text>
		</view>
		
		<uni-swipe-action>
			<block v-for="(goods ,i) in cart" :key="i">
			<uni-swipe-action-item :options=options :right-options='options' @click="swiperItemClickHandler(goods)">
				<my-goods :goods="goods" :showRadio="true" :showNum="true" @radio-change="radioChangeHandler" @num-change=numberChangeHandler></my-goods>
			</uni-swipe-action-item>
			</block>
		</uni-swipe-action>
		<my-settle></my-settle>
	</view>
	<view class="empty-cart" v-else>
		<image src="/static//cart_border@2x.png" class="empty-img"></image>
		<text class="tip-text">空空如也~</text>
	</view>
</template>

<script>
	import badgeMix from '@/mixins/tabbar-badge.js'
	import {mapState,mapMutations} from 'vuex'
	export default {
		mixins:[badgeMix],
		computed:{
			...mapState('m_cart',['cart'])
		},
		data() {
			return {
				options:[{
					text:'删除',
					style:{
						backgroundColor:'#C00000'
					}
				}]
			}
		},
		methods:{
			radioChangeHandler(e){
				this.updateGoodsState(e)
			},
			...mapMutations('m_cart',['updateGoodsState','updateGoodsCount','removeGoodsById']),
			numberChangeHandler(e){
				this.updateGoodsCount(e)
			},
			swiperItemClickHandler(goods){
				this.removeGoodsById(goods.goods_id)
			}
		}
	}
</script>

<style lang="scss">
	.cart-container{
		padding-bottom: 50px;
	}
	
.cart-title{
	height: 40px;
	display: flex;
	align-items: center;
	padding-left: 5px;
	border-bottom: 1px solid #efefef;
	.cart-title-text{
		font-size: 14px;
		margin-left: 10px;
	}
}
.empty-cart{
	display: flex;
	flex-direction: column;
	align-items: center;
	padding-top: 150px;
	.empty-img{
		width: 90px;
		height: 90px;
	}
	.tip-text{
		font-size: 12px;
		color: gray;
		margin-top: 15px;
	}
}
</style>
