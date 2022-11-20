<template>
    <div id="loader" v-if="(requestState == 'loading') || (requestState == 'error')" class="fadeIn">
        <font-awesome-icon v-if="requestState == 'loading'" icon="fa-solid fa-spinner" class="fa-spin" />
        <h3 v-if="requestState == 'loading'">Caricamento</h3>
        <h3 v-if="requestState == 'error'">Errore Caricamento</h3>
    </div>
</template>

<script>

    export default {
        name: 'albumLoader',
        props: {
            requestState: String,
        }
    }

</script>

<style lang="scss" scoped>

    @import '../../styles/vars.scss';
    @import '../../styles/general.scss';

    #loader {
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: $dark_color;
        border-radius: 10px;
        padding: 30px;
        margin: auto;

        .fa-spinner,
        h3 {
            display: inline-block;
            margin: 0 10px;
            font-size: 30px;
            color: $light_color;
        }

        h3 {
            text-transform: uppercase;
        }
    }

</style>
