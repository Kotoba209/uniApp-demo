<template>
    <view class="dengLoadingVue">
        <view class="maskVueHiddenShow" v-if="statusLoading" @click="onCheckHiddenApi">
            <view class="maskVueHiddenShowWrapper">
                <image src="../../../../static/loading/1001.gif" class="maskVueHiddenShowWrapperGif"></image>
            </view>
        </view>
    </view>
</template>

<script>
	
    export default {
        props: {
            status:false,
        },
		created() {
			console.log('created')
			if (this.statusLoading == true) {
				var that = this
				setTimeout(function(){
					that.statusLoading = false
				},5000)
			}
		},
        data() {
            return {
                statusLoading:true,
            };
        },
		watch:{
			status(e) {
				console.log(e,'e')
				this.statusLoading = e
				
			}
		},
		methods: {
			onCheckHiddenApi() {
				this.statusLoading = false
			}
		}
    }
</script>

<style lang="scss">
    .dengLoadingVue {
        .maskVueHiddenShow {
            z-index: 101;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: #fff;
            opacity: 0.8;
            //
            display: flex;
            align-items: center;
            justify-content: center;
            .maskVueHiddenShowWrapper {
                width: 80%;
                height: 300rpx;
                display: flex;
                align-items: center;
                justify-content: center;
                .maskVueHiddenShowWrapperGif {
                    width: 400rpx;
                    height: 300rpx;
                }
            }
        }
    }
</style>
