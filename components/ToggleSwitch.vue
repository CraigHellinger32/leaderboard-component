<template>
    <form class="form">
        <input id="toggle-switch" class="form__checkbox" type="checkbox"><label class="form__label" for="toggle-switch">Sort by: <strong>Games Played</strong><span class="visually-hidden"> or </span><strong class="rank-label">Rank</strong></label>
    </form>
</template>

<style lang="scss" scoped>
    $color-primary: #f26a2c;
    $color-white: #fff;

    .form__checkbox {
        height: 0;
        width: 0;
        visibility: hidden;
    }

    .form__label {
        color: $color-white;
        cursor: pointer;
        font-size: 14px;
        padding-right: 4rem;
        position: relative;
        transition: color .3s;
    }

    .form__label::after {
        background: $color-primary;
        border-radius: .5rem;
        box-shadow: 0 0 0 1px $color-white;
        content: '';
        display: block;
        height: 1rem;
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        right: 0;
        width: 3rem;
        z-index: 1;
    }

    .form__label::before {
        border-radius: .5rem;
        border: 2px solid $color-primary;
        background: $color-white;
        content: '';
        display: inline-block;
        height: .75rem;
        position: absolute;
        top: 50%;
        transform: translateX(0) translateY(-50%);
        transition: transform .3s ease, background-color .3s, width .3s;
        left: calc(100% - 3rem);
        width: .75rem;
        z-index: 2;
    }

    .form__checkbox:checked + .form__label::before {
        left: auto;
        right: 2rem;
        transform: translateX(2rem) translateY(-50%);
    }

    .form__label:active::before {
        width: 1.25rem;
    }

    .rank-label {
        position: absolute;
        left: 100%;
    }
</style>
