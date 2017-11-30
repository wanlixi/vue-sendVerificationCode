# vue-sendVerificationCode
<br>
### 2017-11-30 Create by wanlixin

##### 效果如下：
![](https://github.com/wanlixi/vue-sendVerificationCode/blob/master/send-verification-code.gif)

##### 基于vue2.0开发的发送验证码组件，
<ul>
  <li>支持自定义按钮的样式；</li>
  <li>支持自定义倒计时的时长；</li>
  <li>支持调用父组件的方法进行接口请求</li>
 </ul>
 
 使用方法如下：
 ###### 父组件
 ```
<template>
	<send-verification-code :btn-style="btnStyle" :count-down-parent="6" @send-verification-code="sendVerificationCode"></send-verification-code>
</template>
<script>
import sendVerificationCode from '@/components/send_verification_code.vue';
export default {
	components:{ sendVerificationCode },
  data () {
    return {
      btnStyle: {
        width: '3rem',
        height: '1.25rem',
        background: 'blue',
        borderRadius: '.5rem'
      }
    }
  },
	methods: {
		sendVerificationCode (i) {
			console.log(i)
			// 调用发送验证码的接口
		}
	}
}
</script>
 ```

