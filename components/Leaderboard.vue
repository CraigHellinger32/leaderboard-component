<template>
    <div class="leaderboard">
        <ol class="list leaderboard__list" v-for="list in players">
            <li class="list__item" v-for="player in list" :key="player.id">{{ player.Name }}</li>
        </ol>
    </div>
</template>

<script>
    export default {
        name: 'Leaderboard',
        props: [
            'filteredData',
            'players'
        ]
    }
</script>

<style lang="scss" scoped>
    .leaderboard__list {
        text-align: left;
    }
</style>
