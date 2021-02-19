<template>
  <main class="container">
    <div>
      <Logo />
      <h1 class="title">
        Scrabble Leaderboard
      </h1>
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
                filteredData: []
            }
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
}

.links {
  padding-top: 15px;
}

.visually-hidden {
    @include visuallyhidden;
}
</style>
