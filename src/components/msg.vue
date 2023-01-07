<template>
    <div :class="{'message-container' : !msgBAD, 'message-container-bad': msgBAD}">
        <p class="animate__bounce">{{msg}}</p>
    </div>
</template>

<script>
export default {
    name: 'msg',

    props: {
        msg: String,
        msgBAD: Boolean
    }
}
</script>

<style scoped>
    .message-container{
        color: #004085;
        background-color: #cce5ff;
        border: 2px solid #b8daff;
        border-radius: 5px;
        padding: 10px;
        max-width: 600px;
        margin: 30px auto;
    }

    .message-container-bad{
        color: #ad2626;
        background-color: #ffcccc;
        border: 2px solid #b8daff;
        border-radius: 5px;
        padding: 10px;
        max-width: 600px;
        margin: 30px auto;
    }
</style>