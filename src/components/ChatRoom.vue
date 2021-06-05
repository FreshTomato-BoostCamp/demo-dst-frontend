<template>
    <div class="chatroom_wrapper">
        <h3> Dialogue History </h3>
        <div class="chatroom">
            <div class="message-list">
            <!-- <div v-for="msg in messages" :key="msg.message">
                {{ msg.message }}
            </div> -->
                <ChatMessage v-for="msg in messages" :key="msg.message" :message="msg"/>
            </div>
            <input type="text" v-model="inputText" @keyup.enter="submitItem()" placeholder="Input your message"/>
            <v-btn elevation="2" @click="submitItem()"> 전송 </v-btn>
        </div>
    </div>
</template>

<script>
// import { ChatMessage } from '../components/ChatMessage.vue' // 이건 왜 안될까..
import ChatMessage from '../components/ChatMessage.vue'
import axios from 'axios'

var api_server = "http://b26a6c6ac5ae.ngrok.io"

export default {
    name: 'ChatRoom',
    components: {
        ChatMessage
    },
    data () {
        return {
            inputText: '',
            messages: [],
            state: []
        }
    },
    methods: {
        submitItem: function () {
            // this inside methods points to the Vue instance
            var msg = this.specifyUser('yura', this.inputText)
            // this.messages.push(this.specifyUser(this.inputText))
            this.messages.push(msg)
            console.log(this.messages)
            this.emptyInput()
            axios.post(api_server, msg).then(
                response => console.log(response))
        },

        emptyInput: function () {
            this.inputText = ''
        },

        specifyUser: function (user, text) {
            return {
                    'user': 'yura',
                    'message': text
                    }
        }

    },
}
</script>

<style scoped>
.message-list {
    background: #FFD2D2;
    /* display: flex; */
    width: 463px;
    height: 656px;
    position: relative;
    margin: auto;
}
</style>