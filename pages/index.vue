<template>
  <main class="container">
    <div>
      <Logo />
      <h1 class="title">
        Scrabble Leaderboard
      </h1>
      <ToggleSwitch @toggle-update="toggleUpdateHandler($event)" />
      <Leaderboard :filteredData="filteredData" :players="players" />
    </div>
  </main>
</template>

<script>
    import leaderboardJson from '@/static/leaderboard.json'
    import playersJson from '@/static/players.json'

    export default {
        data() {
            return {
                players: playersJson,
                results: leaderboardJson.Results,
                filteredData: [],
                state: 'rank'
            }
        },
        methods: {
            filterHandler: function() {
                this.filteredData = this.players.Players;

                var resultsData = this.results,
                    resultsIdCheck = function(id, resultsData) {
                        if (id === resultsData.PlayerId) return true;
                    },
                    compareRank = function(a, b) {
                        if ( a.results[0].TotalScore > b.results[0].TotalScore ){
                            return -1;
                        }
                        if ( a.results[0].TotalScore < b.results[0].TotalScore ){
                            return 1;
                        }
                        return 0;
                    },
                    compareGamesPlayed = function(a, b) {
                        if ( a.results[0].GamesPlayed > b.results[0].GamesPlayed ){
                            return -1;
                        }
                        if ( a.results[0].GamesPlayed < b.results[0].GamesPlayed ){
                            return 1;
                        }
                        return 0;
                    }

                this.filteredData.forEach(combineResults);

                function combineResults(item) {
                    item.results = resultsData.filter(obj => resultsIdCheck(item.PlayerId, obj));
                }

                if (this.state === 'rank') {
                    this.filteredData.sort(compareRank);
                } else {
                    this.filteredData.sort(compareGamesPlayed);
                }
            },
            toggleUpdateHandler(toggleChecked) {
                if (toggleChecked == true) {
                    this.state = 'rank'
                } else {
                    this.state = 'games-played'
                }

                this.filterHandler();
            }
        },
        mounted() {
            this.filterHandler();
        }
    }
</script>

<style lang="scss">
 @import '~assets/sass/_mixins.scss';

/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  display: block;
  font-weight: 300;
  font-size: 30px;
  color: #fff;
  letter-spacing: 1px;
  line-height: 1.1;
}

.links {
  padding-top: 15px;
}

.visually-hidden {
    @include visuallyhidden;
}
</style>
