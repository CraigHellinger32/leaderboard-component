<template>
    <div class="leaderboard">
        <ol class="list leaderboard__list">
            <li class="list__item" v-for="player in filteredData" :key="player.id">
                <span class="leaderboard__tiles tiles">
                    <span :class="getTileClass(letter)" v-for="letter in splitWord(player.Name)" />
                </span>
                <span class="visually-hidden">{{ player.Name }}</span>
                <ul class="leaderboard__stats stats">
                    <li class="stats__item stats__item--score">
                        <span class="stats__label">Score:</span>
                        <span class="stats__value">{{ player.results[0].TotalScore }}</span>
                    </li>
                    <li class="stats__item stats__item--games">
                        <span class="stats__label">Games Played:</span>
                        <span class="stats__value">{{ player.results[0].GamesPlayed }}</span>
                    </li>
                </ul>
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
    .leaderboard {
        padding: .5rem 1rem;
    }

    .leaderboard__list {
        counter-reset: list_item_count;
        text-align: left;
    }

    .list__item {
        border-bottom: 1px solid #ccc;
        color: #fff;
        counter-increment: list_item_count;
        margin: .5rem 0;
        padding: .5rem 0 .5rem 3rem;
        position: relative;

        &::before {
            content: counter(list_item_count) 'th';
            font-size: 18px;
            font-weight: bold;
            left: 0;
            position: absolute;
            text-align: center;
            // transform: translateX(-($list-inset-margin / 3 + $list-bullet-size / 2));
        }

        &:last-child {
            border-bottom: 0;
        }

        &:nth-child(-n+3) {
            &::after {
                background-size: contain;
                background-repeat: no-repeat;
                background-position: left;
                content: '';
                display: block;
                height: 40px;
                left: -.5rem;
                position: absolute;
                top: 2.5rem;
                width: 3rem;
            }
        }

        &:nth-child(1) {
            &::before {
                content: counter(list_item_count) 'st';
            }

            &::after {
                background-image: url('@/static/trophy-gold.svg');
            }
        }

        &:nth-child(2) {
            &::before {
                content: counter(list_item_count) 'nd';
            }

            &::after {
                background-image: url('@/static/trophy-silver.svg');
            }
        }

        &:nth-child(3) {
            &::before {
                content: counter(list_item_count) 'rd';
            }

            &::after {
                background-image: url('@/static/trophy-bronze.svg');
            }
        }
    }

    .leaderboard__tiles {
        display: flex;
        flex-wrap: wrap;
    }

    .tiles__tile {
        border-radius: 3px;
        box-shadow: 1px 1px 4px 0px rgba(0, 0, 0, .75);
        height: 44px;
        margin: 0 3px 3px 0;
        width: 44px;

        &:nth-child(odd) {
            transform: rotate(1deg);
        }

        &:nth-child(even) {
            transform: rotate(-1deg);
        }

        &:nth-child(3n-4) {
            transform: rotate(-2deg);
        }

        &:nth-child(5n-4) {
            transform: rotate(2deg);
        }
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
