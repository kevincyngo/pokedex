<template>
    <div id='cardImg'>
        <img :src=imgUrl>
    </div>
</template>


<script>
export default {
    props: ['imgUrl']
}
</script>


<style scoped>
    #cardImg {
        box-sizing: border-box;
        background: #ffe9c6
    }
</style>