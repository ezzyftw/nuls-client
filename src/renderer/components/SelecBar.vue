<template>
	<!--select-->
	<div class="base-select fl" @click="showDataList">
		<div class="sub-selected-value">
			<img :src="selectedValue.value"  class="language-img">
			<ul class="ul" v-bind:style="{width: widthData}" v-if="showData">
				<li v-for="(item, index) in dataList" @click.stop="select(item, index)">
					<img :src="item.value" class="language-img">
				</li>
			</ul>
		</div>
	</div>
</template>
<script>
	export default {
		data() {
			return {
				showData: false
			}
		},
		props: {
			dataList: Array,
			selectedValue: Object, 
			widthData: {
				type: String,
				default: "160px"
			}
		},
		methods: {
			//下拉框数据加载
			select(item, index) {
				this.showData = false;
				//赋值的时候要分开写
				this.selectedValue.key = item.key;
				this.selectedValue.value = item.value;
				this.$emit('select');
				localStorage.setItem('language',item.key);
			},
            //点击显示隐藏下拉框
            showDataList() {
                this.showData = !this.showData;
            },
		},
        mounted () {
		    //监听点击隐藏
            document.addEventListener('click', (e) => {
                if (!this.$el.contains(e.target)) this.showData = false
            })
        },
	}
</script>
<style lang="less">
	.base-select {
		position: relative;
		top: 0px;
		height: 1.25rem;
		cursor: pointer;
		.sub-selected-value {
			position: absolute;
			top: -0.35rem;
			width: 2rem;
			text-align: center;
			ul {
				position: absolute;
				top: 2.15rem;
				width: 3rem;
				z-index: 9;
				li {
					width: auto;
					min-width: 2rem;
					height: 30px;
					position: relative;
					text-align: center;
					border-radius: 0.2rem;
					.language-img{
    					margin-top: 0.25rem;
					}
				}
				:hover{
					background-color: #17202e;
				}
			}
			.language-img{
				width: 21px;
    			margin-top: 18px;
			}
		}
	}
</style>
