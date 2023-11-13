<template>
        <div>
            <div class="title">Teams</div>
            <div v-if="isLoad" class="loading">Loading...</div>
            <div v-else class="data">
                <div v-for="(el, i) in teamData" :key="el.id">{{ i + 1 }}. {{ el.abbreviation }} {{ el.city }}
                    <img src="https://cdn-icons-png.flaticon.com/512/542/542724.png" style="width: 15px; height: 15px" @click="removeTeam(el.id)" >
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
            };
        },
        mounted() {
            const url = 'https://free-nba.p.rapidapi.com/teams?page=0';
            const options = {
                method: 'GET',
                headers: {
                    'X-RapidAPI-Key': '41b720a6f3msheddb55513a5eff4p1ed684jsn2c5955b3b8a0',
                    'X-RapidAPI-Host': 'free-nba.p.rapidapi.com'
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
                this.teamData = this.teamData.filter((el) => el.id !== id)
            }
        }
    }
</script>