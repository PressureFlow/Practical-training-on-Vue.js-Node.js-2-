<template>
    <div v-if="username">
        <div class="chat">
            <h2>Чат</h2>

            <div class="text" v-for="message in messages" :key="message.id">
                {{ message.user }}: {{ message.text }}
            </div>

            <div v-show="emptyMsg" class="empty">Текущих сообщений нет</div>
        </div>

        <input v-model="newMessage" placeholder="Введите ваше сообщение">

        <button @click="sendMessage" @keyup.enter="sendMessage">Отправить</button>
        <button v-show="deleteBtn" @click="delMessage">Удалить</button>
    </div>

    <div v-else class="alert">
        Для авторизации перейдите по <router-link :to="{ name: 'Home'}">ссылке</router-link>
    </div>
</template>


<script>
    export default {
        name: 'ChatPage',
        data() {
            return {
                messages: [],
                newMessage: '',
                emptyMsg: true,
                deleteBtn: false,
                username: localStorage.getItem('username')
            }
        },
        computed() {
            localStorage.setItem('username', this.$route.query.username)
        },
        methods: {
            sendMessage() {
                if (!this.username) {
                    this.username = 'Аноним'
                }

                if(this.newMessage !== '') {
                    this.emptyMsg = false;

                    this.messages.push({id: new Date().getTime(), text: this.newMessage, user: this.username})
                    console.log(this.messages)

                    this.newMessage = '';
                    this.deleteBtn = true;
                } else {
                    alert('Пожалуйста, введите сообщение!')
                }

            }, 
            delMessage() {
                this.messages = [];
                alert('Все сообщения были удалены!')
                this.emptyMsg = true;
            }

        }
    }
</script>