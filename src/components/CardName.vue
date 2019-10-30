<template>
    <div id='cardName'>
        #{{pokeId}} {{pokeName}}
    </div>
</template>

<script>
export default {
    props: ['pokeName', 'pokeId'],
    methods: {

    }
}
</script>


<style scoped>
    #cardName {
        box-sizing: border-box;
        padding: 10px;
        background: #ffdad8;
    }
</style>