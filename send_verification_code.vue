<!-- 
	2017-11-30 Create by wanlixin
	【功能描述】: 发送验证码 
	父组件使用例如：
	<send-verification-code :count-down-parent="30" @send-verification-code="sendVerificationCode"></send-verification-code>
 -->
<template>
	<button 
		:class="['btn', isSended ? 'gray' : '']"
		:style="btnStyle"
		@click="sendVerificationCode">{{btnText}}</button>
</template>
<script>
	export default {
		data () {
			return {
				btnText: '发送验证码', // 按钮的文本
				timer: null, // 验证码倒计时的计时器
				isSended: false, // 是否点击下发送验证码的按钮
				countDownChild: 0, // 当前组件下的倒计时有，用于接收父组件的倒计时，注意：不能直接使用props里面的倒计时进行--处理，详情请见（https://cn.vuejs.org/v2/guide/components.html#Prop）
			}
		},
		props: {
			btnStyle: { // 自定义按钮的样式
				type: Object,
				default: function () {
					return {
						width: '120px',
						height: '40px',
						background: '#5cadff'
					}
				}
			},
			// 自定义倒计时时长
			countDownParent: {type: Number, default: 60},
		},
		methods: {
			sendVerificationCode () {
				let v = this;
				// vue2.0 props被控制为单向数据流，因此用子组件的属性接受下即可
				v.countDownChild = v.countDownParent;
				if (!v.isSended) {
					// 调用父组件里面的发送验证码的事件，一般为调用后台接口
					v.$emit('send-verification-code')
					v.isSended = true // 幂等控制
					v.timer = setInterval( () => {
						v.countDownChild--;
						v.btnText = `(${v.countDownChild}s)`;
						if (v.countDownChild < 0) {
							v.countDownChild = v.countDownChild;
							v.isSended = false;
							v.btnText = '发送验证码';
							clearInterval(v.timer);
						}
					}, 1000)
				}
			}
		},
		destoryed () { // 防止用户发送验证码之后进行了跳转出来再返回来，出现的计时器错乱
			clearInterval(this.timer)
		}
	}
</script>
<style scoped>
	.btn {
		outline: none;
		border: none;
		color: #fff;
	} 
	.gray {
		background: #d3d3d3 !important;
	}
</style>