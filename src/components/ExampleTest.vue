<script>
import {ref,reactive , computed ,watchEffect , watch , onMounted} from 'vue'
export default {
    setup() {
        const count = ref(0) ;
        const elRef = ref() ;
        const info = reactive({name: 'jason' , hobby: ['swim','play']}) ;
        // 对ref解包，两者同事动态更新
        const deepCount = reactive({count})
        const changeInfo = () => {
            info.hobby.push('watch')
        }

        // 不具有reactive,不依赖函数里的变量做更新
        computed(() => console.log(count.value))

        //立即运行一个函数，同时响应式地追踪其依赖，并在依赖更改时重新执行。但是貌似不支持非primitive
        watchEffect(() => console.log(count.value))
        watchEffect(() => console.log(info.hobby))

        // 支持深层次依赖追踪
        //懒执行副作用；
        //更加明确是应该由哪个状态触发侦听器重新执行；
        //可以访问所侦听状态的前一个值和当前值。
        watch(info,() => console.log(info))

        //注册回调函数，挂载后执行
        onMounted(() => {
            console.log(elRef.value)
        })
        return {
            count,
            info,
            deepCount,
            elRef,
            changeInfo,
        }
    },
}
</script>
<template>
    <button @click="count++">{{ count }}</button>
    <button @click="deepCount.count++">{{ deepCount.count }}</button>
    <p @click="changeInfo" ref="elRef">{{ info.name }}</p>
</template>
