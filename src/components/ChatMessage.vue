<template>
<div class="wrapper">
    <div v-bind:class="getClass" class="bubble" @click="changeUser">
        <p>
            {{ this.message.text }}
        </p>
    </div>
</div>
</template>


<script>
export default {
    name: 'ChatMessage',
    props: {
        'message': Object
    },
    data () {
        return {
        }
    },
    methods: {
        // dummy function for visualization TODO: remove
        changeUser: function () {
            this.message.role = this.message.role === 'system' ? 'user': 'system';
        }
    },
    computed: {
        'getClass': function () {
            return this.message.role === 'system' ? "system-bubble" : "user-bubble"
        }
    }
}
</script>


<style scoped>
p {
    word-break: break-all;
    margin: 10px;
}

.wrapper {
    display: grid;
}

.bubble {
    margin-bottom: 1em;
    margin-top: 1em;
    min-height: 56px;
    min-width: 177px;
    max-width: 400px;
    /* margin-right: 80px; */
    /* width: 177px; */
}

.user-bubble {
    justify-self: flex-end;
    position: relative;
    /* right: -24%; */
    right: 0em;
    background: #FFE03D;
    border-radius: 9px;
    display: inline-block;
    text-align: center;
    line-height: 1.5em;
    margin-right: 25px;
}

.system-bubble {
    justify-self: flex-start;
    position: relative;
    left: 0em;
    background: #FBFBFB;
    border-radius: 9px;
    display: inline-block;
    text-align: center;
    line-height: 1.5em;
    margin-left: 25px;
}

.user-bubble::after {
    position: absolute;
    bottom: 2.5px;
    right: 0%;
    content: '';
    width: 0;
    height: 0;
    margin-right: -1em;
    border-bottom: 20px solid #FFE03D;
    border-right: 20px solid transparent;
}

.system-bubble::after {
    position: absolute;
    bottom: 2.5px;
    left: 0%;
    content: '';
    width: 0;
    height: 0;
    margin-left: -1em;
    border-bottom: 20px solid #FBFBFB;
    border-left: 20px solid transparent;
}

</style>