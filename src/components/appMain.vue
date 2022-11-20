<template>
    <main class="main-cont">
    <!-- Sezione ricerca -->
        <searchAlbum :genreResp="this.albumGenre" @genreN="genreAnswer" />
    <!-- Container Album -->
        <div class="album-container">
        <!-- Ablum -->
            <singleAlbum v-for="(album, index) in selAlbumResponse" :albumName="album.title" 
            :authorInfo="album.author" :albumYear="album.year" :albumThumb="album.poster" 
            :key="index" :albumGenre="album.genre" />
        <!-- Caricamento ed errori -->
            <albumLoader :requestState="reqState" />
        </div>
    </main>
</template>

<script>

    import axios from 'axios'
    import singleAlbum from './album-containers/singleAlbum.vue';
    import albumLoader from './album-containers/albumLoader.vue';
    import searchAlbum from './searchAlbum.vue';

    export default {
        name: 'appMain',
        components: {
            singleAlbum,
            albumLoader,
            searchAlbum,
        },

        data() {
            return {
                // Richiesta api
                source: 'https://flynn.boolean.careers/exercises/api/array/music',
                // Stato 
                reqState: '',
                // Risposta
                albumResponse: [],
                albumResponseFiltered: [],
                selAlbumResponse: [],
                // Filtraggio Generi
                albumGenre: [],
                filterGenre: '',
            }
        },

        created() { this.getAlbum();},

        methods: {
            async getAlbum() {
                try {
                    const response = await axios.get(this.source);
                    this.albumResponse = response.data.response;
                    this.reqState = 'loading';
                    // Creo aray generi senza ripetizioni
                    this.getGenres();
                    console.log('Request State:' + ' ' + this.reqState);
                    this.checkFeed();
                    this.genreAnswer("seleziona un genere");
                } catch (error) {
                    this.reqState = 'error';
                    console.log('Request State Feed:' + ' ' + this.reqState);
                }
                console.log('Request State:' + ' ' + this.reqState);
            },
            checkFeed() {
                this.reqState = 'loading complete';
            },
            // Creo array con generi senza ripetizioni per ricerca
            getGenres() {
                for (let i = 0; i < this.albumResponse.length; i++) {
                    let genre = this.albumResponse[i].genre;
                    while (!this.albumGenre.includes(genre)) {
                        this.albumGenre.push(genre);
                    }
                }
                console.log('Generi Album:' + '  ' + this.albumGenre);
            },
        // Seleziona Filtro
            genreAnswer(genre) {
                this.filterGenre = genre.toLowerCase().trim();
                console.log('Filtro impostato:' + ' ' + this.filterGenre);
                if (this.filterGenre == 'seleziona un genere') {
                    this.selAlbumResponse = this.albumResponse;
                }
                else {
                    for (let i = 0; i < this.albumResponse.length; i++) {
                        let albRes = this.albumResponse[i].genre.toLowerCase().trim();
                        if (albRes == this.filterGenre) {
                            this.albumResponseFiltered.push(this.albumResponse[i]);
                        }
                    }
                    this.selAlbumResponse = this.albumResponseFiltered;
                }
            },
        }
    }

</script>

<style lang="scss">
@import '../styles/vars.scss';
    @import '../styles/general.scss';

    main {
        min-height: calc(100vh - 5rem);
        background-color: $brand_color;
        z-index: -2;

        .album-container {
            background-color: $brand_color;
            text-align: center;
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            align-items: stretch;
            width: 80%;
            margin: auto;
            min-height:calc(100% - 130px);

            @media screen and (max-width:"980px") {
                width: 90%;
                @media screen and (max-width:"780px"){
                    width: 100%;
                    margin: 1rem;
                }
            }
        }
    }
</style>