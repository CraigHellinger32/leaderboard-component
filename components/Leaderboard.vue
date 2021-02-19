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
                if (letter === ' ') {
                    return 'tiles__tile tiles__tile--space';
                } else {
                    return 'tiles__tile tiles__tile--' + letter.toLowerCase();
                }
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
        margin: .5rem 0;
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

    @function str-split($string, $separator) {
        // empty array/list
        $split-arr: ();
        // first index of separator in string
        $index : str-index($string, $separator);
        // loop through string
        @while $index != null {
            // get the substring from the first character to the separator
            $item: str-slice($string, 1, $index - 1);
            // push item to array
            $split-arr: append($split-arr, $item);
            // remove item and separator from string
            $string: str-slice($string, $index + 1);
            // find new index of separator
            $index : str-index($string, $separator);
        }
        // add the remaining string to list (the last item)
        $split-arr: append($split-arr, $string);

        @return $split-arr;
    }

    $alphabetArray: str-split("a,b,c,d,e,f,g,h,i,j,k,l,m,n,o,p,q,r,s,t,u,v,w,x,y,z,_", ",");

    @each $value in $alphabetArray {
        .tiles__tile--#{$value} {
            background-image: url("/leaderboard-component/scrabble-tiles/#{to-upper-case($value)}.svg");
        }
    }
</style>
