<template>
    <div class="leaderboard">
        <ol class="list leaderboard__list" v-for="list in players">
            <li class="list__item" v-for="player in list" :key="player.id">
                <span class="leaderboard__tiles tiles">
                    <span :class="getTileClass(letter)" v-for="letter in splitWord(player.Name)" />
                </span>
                <span class="visually-hidden">{{ player.Name }}</span>
            </li>
        </ol>
    </div>
</template>

<script>
    export default {
        name: 'Leaderboard',
        props: [
            'filteredData',
            'players'
        ],
        methods: {
            splitWord(name) {
                return name.replace(/ /g,"_").split("");
            },
            getTileClass(letter) {
                return 'tiles__tile tiles__tile--' + letter.toLowerCase();
            }
        }
    }
</script>

<style lang="scss" scoped>
    .leaderboard__list {
        text-align: left;
    }

    .list__item {
        color: #fff;
    }

    .leaderboard__tiles {
        display: flex;
        flex-wrap: wrap;
    }

    .tiles__tile {
        height: 44px;
        margin: 0 3px 3px 0;
        width: 44px;
    }

    .tiles__tile--a {
        background-image: url("/scrabble-tiles/A.svg");
    }

    .tiles__tile--b {
        background-image: url("/scrabble-tiles/B.svg");
    }

    .tiles__tile--c {
        background-image: url("/scrabble-tiles/C.svg");
    }

    .tiles__tile--d {
        background-image: url("/scrabble-tiles/D.svg");
    }

    .tiles__tile--e {
        background-image: url("/scrabble-tiles/E.svg");
    }
</style>
