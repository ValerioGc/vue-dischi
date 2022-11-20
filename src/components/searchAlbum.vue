<template>
    <div id="search">
        <select v-model="selectedGenre" @change="$emit('genreN', selectedGenre)" id="genreSelector">
            <option selected value="Seleziona un genere">Seleziona un genere</option>
            <option v-for="(album, index) in genreResp" :key="index" :value="album">
                {{album}}
            </option>
        </select>
        <button v-if="selectedGenre !== 'Seleziona un genere'" id="resetFilter"
            @click="() => selectedGenre = 'Seleziona un genere'">Reset filtro</button>
    </div>
</template>

<script>

    export default {
        name: 'searchAlbum',
        props: {
            genreResp: Array,
        },
        data() {
            return {
                selectedGenre:'Seleziona un genere',
                arrayGenres: this.genreResp,
            }
        }
    }

</script>

<style lang="scss">

@import '../styles/vars.scss';
@import '../styles/general.scss';

        #search {
            text-align: center;
            padding: 35px 0 ;

            #genreSelector {
                width: 250px;
            }

            #resetFilter {
                margin: 0 15px;
            }

            #resetFilter,
            #genreSelector {
                padding: 10px;
                text-align: center;
                border-radius: 10px;
            }
        }

</style>