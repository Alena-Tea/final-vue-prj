<template>
    <div class="container">
        <nav>
            <router-link to="/">Домашняя страница</router-link>
            <router-link to="/chat">Чат</router-link>
            <router-link to="/test">Подгрузка API данных</router-link>
        </nav>
    </div>
</template>

<script>
export default {
    name: 'NavComp'
}
</script>
<style scoped>
.container {
    margin: 0px 0px 20px;
    background-color: #70B1D0;
    /*other color*/
    height: 70px;
    width: 100%;
    display: flex;
    justify-content: center;
}

nav {
    width: 600px;
    height: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0px 50px;

}


a {
    display: inline-block;
    position: relative;
    padding-bottom: 5px;
    text-decoration: none;
    font-size: 1.2em;
    color: white;
}

a::after {
    content: '';
    position: absolute;
    left: 0;
    bottom: 0px;
    width: 100%;
    height: 2px;
    background-color: white;
    opacity: 0;
    transition: opacity 0.3s ease-in-out;
}

a:hover::after {
    opacity: 1;
}
</style>