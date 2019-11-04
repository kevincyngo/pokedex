<template>
    <div id='cardImg'>
        <img :src="imgUrl">
    </div>
</template>


<script>
export default {
    props: ['imgUrl']
}
</script>


<style scoped>
img {
    width: 50px;
    height: 50px;
}
    #cardImg {
        box-sizing: border-box;
        background: #ffe9c6,
        
    }
</style>