<template>
    <div class="chatroom_wrapper">
        <h3> Dialogue History </h3>
        <div class="chatroom">
            <div class="message-list">
                <ChatMessage v-for="d in dials" :key="dials.indexOf(d)" :message="d.dialogue[0]"/>
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

var api_server = "{YOUR_API_SERVER}"

export default {
    name: 'ChatRoom',
    components: {
        ChatMessage
    },
    data () {
        return {
            did: 'yura',
            inputText: '',
            dials: [],
            state: []
        }
    },
    methods: {
        submitItem: function () {
            // this inside methods points to the Vue instance
            var dial = this.wrapInput(this.inputText)
            this.dials.push(dial)
            console.log(this.dials)
            this.emptyInput()
            axios.post(api_server, dial).then( response => {
                let system_response = response.data
                console.log(system_response['system-utter'])
                console.log(system_response['state'])
                this.dials.push(this.wrapResponse(system_response))
            })
        },

        emptyInput: function () {
            this.inputText = ''
        },

        wrapInput: function (text) {
            return {
                    'dialogue_idx': this.did,
                    'new_input': true,
                    'dialogue': [
                            {
                                'role': 'user',
                                'text': text
                            }
                        ]
                    }
        },

        wrapResponse: function (response_content) {
            return {
                'dialogue_idx': this.did,
                'dialogue': [
                    {
                        'role': 'system',
                        'text': response_content['system-utter']
                    }
                ],
                'state': response_content['state']
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
    overflow-y: scroll;
}
</style>