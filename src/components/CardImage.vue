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
    width: 60px;
    height: 60px;
    padding:5px;
}
    #cardImg {
        box-sizing: border-box;
        background: #ffe9c6,
        
    }
</style>