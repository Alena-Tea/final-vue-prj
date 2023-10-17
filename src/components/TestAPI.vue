<template>
    <div class="container">
        <div class="title">Команды</div>
        <div v-if="isLoad" class="loading">Загрузка данных...</div>
        <div v-else class="data">
            <div v-for="(el, i) in teamData" :key="el.id">
                {{ i + 1 }}. {{ el.abbreviation }} {{ el.city }}
                <img src="https://icon2.kisspng.com/20180712/rkr/kisspng-rubbish-bins-waste-paper-baskets-computer-icons-waste-basket-5b4705a29b79a7.9110417015313811546368.jpg"
                    alt="" style="width: 15px; height: 15px;" @click="removeTeam(el.id)">
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'TestAPI',
    data() {
        return {
            teamData: [],
            isLoad: true
        }
    },
    mounted() {
        const url = 'https://free-nba.p.rapidapi.com/teams?page=0';
        const options = {
            method: "GET",
            headers: {
                "X-RapidAPI-Key": "488f437511msh2d3854838388c55p13692cjsn135921cfebdf",
                "X-RapidAPI-Host": "free-nba.p.rapidapi.com",
            },
        };
        fetch(url, options)
            .then((res) => res.json())
            .then((res) => {
                this.teamData = res.data;
                this.isLoad = false;
            });
    },
    methods: {
        removeTeam(id) {
            this.teamData = this.teamData.filter((el) => el.id != id);
        }
    }
}
</script>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding-bottom: 25px;
}

.title {
    font-size: 2em;
    color: #144D69;
    text-transform: uppercase;
    margin: 10px;
    font-weight: bold;
}

.loading {
    padding-bottom: 20px;
}

img {
    cursor: pointer;
    margin-left: 10px;
}
</style>