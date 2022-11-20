<template>
    <header>
        <nav>
            <img src="https://upload.wikimedia.org/wikipedia/commons/1/19/Spotify_logo_without_text.svg"
                alt="Logo Spotify">
            <!-- <span>
                <select name="genere" id="genere" >
                    <option v-for="(test, index) in test" :key="index" value="genre"></option>
                </select>
            </span> -->
        </nav>
    </header> 
</template>

<script>

    export default {
        name:'appHeader',
    }

</script>

<style lang="scss">

    @import '../styles/vars.scss';
    @import '../styles/general.scss';

    header {
        background-color: $brand_color_light;
        height: 5rem;
        box-shadow: 2px 2px 7px $dark_color;
        z-index: 10;

        img {
            width: 3rem;
            margin: 15px 0 15px 20px;
        }
    }
    
</style>