<template>
	<view class="my-settle-container">
		<label class="radio" @click="changeAllState">
			<radio color="#c00000" :checked="ifFullCheck"></radio><text>全选</text>
		</label>
		<view class="amout-box">
			合计：<text class="amout">￥{{checkedGoodsAmout}}</text>
		</view>
		<view class="btn-settle">
			结算({{checkdeCount}})
		</view>
	</view>
</template>
<script>
	import {mapGetters,mapMutations} from 'vuex'
	export default{
		data(){
			return {
				
			}
		},
		computed:{
			...mapGetters('m_cart',['checkdeCount','total','checkedGoodsAmout']),
			ifFullCheck(){
			return	this.total === this.checkdeCount
			}
		},
		methods:{
			...mapMutations('m_cart',['updateAllGoodsState']),
			changeAllState(){
				this.updateAllGoodsState(!this.ifFullCheck)
			}
		}
	}
</script>
<style lang="scss">
	.my-settle-container{
		position: fixed;
		bottom: 0;
		left: 0;
		width: 100%;
		height: 50px;
		background-color: white;
		display: flex;
		justify-content: space-between;
		align-items: center;
		font-size: 14px;
		padding-left: 5px;
	}
	.radio{
		display: flex;
		align-items: center;
	}
	.amout-box{
		.amout{
			color: #c00000;
			font-weight: bold;
		}
		
	}
	.btn-settle{
		background-color: #C00000;
		height: 50px;
		color: white;
		line-height: 50px;
		padding: 0 10px;
		min-width: 100px;
		text-align: center;
	}
</style>
