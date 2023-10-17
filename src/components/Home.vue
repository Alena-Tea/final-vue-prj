<template>
    <div v-if="isAuth">
        <div>
            Приветствую вас, уважаемый(ая) <b>{{ userName }}</b>
        </div>
        <button @click="logOut">Выйти</button>
    </div>
    <div v-else>
        <div>
            <label for="">Введите ваше имя:</label>
            <input v-model="userName" @keyup.enter="login">
        </div>
        <button @click="login">Войти</button>
    </div>
</template>
<script>
export default {
    name: 'HomePage',
    data() {
        return {
            isAuth: false,
            userName: ''
        };
    },
    created() {
        if (localStorage.getItem('isAuth')) {
            this.isAuth = true;
            this.userName = localStorage.getItem('userName');
        }
    },
    methods: {
        login() {
            if (this.userName !== '') {
                this.isAuth = true;

                localStorage.setItem('isAuth', true);
                localStorage.setItem('userName', this.userName);

                this.$router.push({
                    name: 'Chat',
                    query: {
                        userName: this.userName
                    }
                })
            }
            else {
                alert('Пожалуйста, введите ваше имя')
            }
        },
        logOut() {
            this.isAuth = false;
            this.userName = '';
            localStorage.removeItem('isAuth')
            localStorage.removeItem('userName')
        }
    }
}
</script>

<style scoped>
div {
    padding: 30px;
    font-size: 22px;
}


label {
    margin: 0 15px;
}

input {
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    border: 1px solid #bdbdbd;
    outline: 0;
}

button {
    margin-left: 5px;
    padding: 0.5em 2em;
    font-size: 1rem;
}
</style>