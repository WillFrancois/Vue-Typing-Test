<template>
    <div>
        <input @keyup="runTimer();newWord(inputString);" v-model="inputString" id="user-input">
    </div>
</template>

<script>
export default {
    'name': 'Input',
    props:{
        currentWord: String,
        newWord: Function,
        runTimer: Function
    },
    data(){
        return{
            inputString: ""
        }
    },
    mounted: function(){
        document.getElementById("user-input").focus()
    }
}
</script>

<style scoped>
    #user-input{
        caret-color: gray;
        outline-width: 0px;
        height: 50vh;
        width: 100vw;
        font-size: 10vh;
        text-align: center;
        border: 0px;
    }
</style>