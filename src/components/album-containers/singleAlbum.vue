<template>
    <div class="album fadeIn">
        <img decoding="async" :src="albumThumb" :alt="`Copertina Album ${albumName}`" :genre="albumGenre">
        <h3>{{albumName}}</h3>
        <p>{{authorInfo}}</p>
        <p>{{albumYear}}</p>
    </div>
</template>

<script>

    export default {
        name: 'singleAlbum',
        props: {
            albumName: String,
            authorInfo: String,
            albumYear: String,
            albumThumb: String,
            albumGenre: String,
        }
    }

</script>

<style lang="scss">
@import '../../styles/vars.scss';
    @import '../../styles/general.scss';

    .album {
        background-color: $brand_color_light;
        width: calc(100% / 5);
        height: calc(300px);
        box-shadow: 1px 2px 5px $dark_color;
        margin: 1.5rem;
        @media screen and (max-width:"980px") {
            width: calc(100% / 3 - 1rem);
            margin: 1rem;
            @media screen and (max-width:"780px"){
                width: calc(100% / 2 - 1rem);
                margin: 1rem;
            }
        }

        img {
            color: $brand_color_light;
            width: 100%;
            height: 60%;
            padding: 25px;
        }

        h3 {
            color: $light_color;
            font-size: 18px;
            text-transform: uppercase;
            padding: 0px 15px 3px;
        }

        p,
        span {
            color: $light_color_alt;
        }

        p {
            font-size: 14px;
        }

        span {
            font-size: 12px;
        }
    }
</style>