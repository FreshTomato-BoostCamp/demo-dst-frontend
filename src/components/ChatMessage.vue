<template>
<div class="wrapper">
    <div v-bind:class="getClass" class="bubble" @click="changeUser">
        {{ this.message.message }}
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
            if (this.message.user === 'system') {
                this.message.user = 'yura'
            }
            else{
                this.message.user = 'system'
            }
        }
    },
    computed: {
        'getClass': function () {
            return this.message.user === 'system' ? "system-bubble" : "user-bubble"
        }
    }
}
</script>


<style scoped>
.bubble {
    margin-bottom: 1em;
    margin-top: 1em;
}

.user-bubble {
    position: relative;
    right: -24%;
    width: 177px;
    height: 56px;
    background: #FFE03D;
    border-radius: 9px;
    display: inline-block;
    text-align: center;
    line-height: 3.5em;
}

.system-bubble {
    position: relative;
    left: -24%;
    width: 177px;
    height: 56px;
    background: #FBFBFB;
    border-radius: 9px;
    display: inline-block;
    text-align: center;
    line-height: 3.5em;
}

.user-bubble::after {
    position: absolute;
    top: 60%;
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
    top: 60%;
    left: 0%;
    content: '';
    width: 0;
    height: 0;
    margin-left: -1em;
    border-bottom: 20px solid #FBFBFB;
    border-left: 20px solid transparent;
}

</style>