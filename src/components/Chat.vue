<template>
    <div v-if="userName">
        <div class="chat">
            <h2>Чат</h2>

            <div class="text" v-for="message in messages" :key="message.id">
                {{ message.user }} : {{ message.text }}
            </div>

            <div v-show="emptyMsg" class="empty">Текущих сообщений нет</div>
        </div>
        <input v-model="newMessage" placeholder="Введите ваше сообщение">

        <button @click="sendMessage" @keyup.enter="sendMessage">Отправить</button>
        <button v-show="deleteBtn" @click="delMessage">Удалить</button>
    </div>
    <div v-else class="alert">
        Для авторизации перейдите по <router-link :to="{ name: 'Home' }">ссылке</router-link>
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
            userName: localStorage.getItem('userName')
        }
    },
    computed() {
        localStorage.setItem('userName', this.$route.query.userName);
    },
    methods: {
        sendMessage() {
            if (!this.userName) {
                this.userName = 'Аноним';
            }
            if (this.newMessage !== '') {
                this.emptyMsg = false;

                this.messages.push({ id: new Date().getTime(), text: this.newMessage, user: this.userName })
                console.log(this.messages);

                this.newMessage = '';
                this.deleteBtn = true;

            } else {
                alert('Пожалуйста, введите сообщение!')
            }
        },
        delMessage() {
            this.messages = [];
            alert('Все сообщения были удалены');
            this.emptyMsg = true;
        }
    }
}
</script>

<style scoped>
h2 {
    color: #144D69;
}

.text {
    margin-bottom: 20px;
}

.chat {
    width: 500px;
    height: 100%;
    border: 2px solid #144D69;
    background-color: white;
    color: #144D69;
    font-weight: 18px;
    font-weight: bold;
    margin: 20px;
    padding: 15px;
}

.empty {
    margin-bottom: 25px;
    font-style: italic;
}

input {
    margin-right: 10px;
    /**/
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    border: 1px solid #bdbdbd;
    outline: 0;
}

button {
    margin-left: 5px;
    margin-bottom: 25px;
    /**/
    padding: 0.5em 2em;
    font-size: 1rem;

}


.alert {
    padding: 30px;
}
</style>