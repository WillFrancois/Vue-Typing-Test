<template>
    <h2 :id="[currentWord[3] == ' ' ? 'completedTest' : '']">{{ currentWord }}</h2>
</template>

<script>
export default {
    'name':'WordBox',
    props:{
        currentWord: String
    }
}
</script>

<style scoped>
    h2{
        font-size: 10vh;
    }
    #completedTest{
        font-size: 15vh;
    }
</style>