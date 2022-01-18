<template>
    
    <h1 v-if="!pokemon">Espere por favor...</h1>

    <div v-else>
        <h1>¿Quién es este pokémon?</h1>
        <!-- TODO: Componente Picture -->
        <pokemon-picture 
            :pokemonId='pokemon.id' 
            :showPokemon='showPokemon'
        />
        <!-- TODO: Componente Opciones -->
        <pokemon-options 
            :pokemons='pokemonArr'
            @selection-pokemon="checkAnswer"
        />

        <div v-if="showAnswer">
            <h2 class="fade-in">{{ message }}</h2>
            <button class="btn-new-game" 
                @click="newGame">
                Nuevo Juego
            </button>
        </div>
    </div>

  
</template>

<script>
import PokemonOptions from '@/components/PokemonOptions.vue'
import PokemonPicture from '@/components/PokemonPicture.vue'
import getPokemonOptions from '@/helpers/getPokemonOptions.js'

export default {
    components: { 
        PokemonPicture,
        PokemonOptions 
    },
    data() {
        return {
            pokemonArr: [],
            pokemon: null,
            showPokemon: false,
            showAnswer: false,
            message: ''
        }
    },
    methods: {
        async mixPokemonArray() {
            this.pokemonArr = await getPokemonOptions();

            const rndInt    = Math.floor( Math.random() * 4 );
            this.pokemon    = this.pokemonArr[ rndInt ];
        },

        checkAnswer( selectedId ) {
            this.showPokemon    = true;
            this.showAnswer     = true;

            if( selectedId === this.pokemon.id ){
                this.message = `Correcto, ${ this.pokemon.name }`;
            }else{
                this.message = `Oops, era ${ this.pokemon.name }`;
            }
        },

        newGame() {

            this.pokemon        = null;
            this.pokemonArr     = [];
            this.showPokemon    = false;
            this.showAnswer     = false;
            this.mixPokemonArray();

        }
    },
    mounted() {
        this.mixPokemonArray();
    }


}
</script>

<style scoped>
    .btn-new-game {

        box-shadow:inset 0px 1px 0px 0px #d9fbbe;
        background:linear-gradient(to bottom, #b8e356 5%, #a5cc52 100%);
        background-color:#b8e356;
        border-radius:6px;
        border:1px solid #83c41a;
        display:inline-block;
        cursor:pointer;
        color:#ffffff;
        font-family:Arial;
        font-size:15px;
        font-weight:bold;
        padding:12px 44px;
        text-decoration:none;
        text-shadow:0px 1px 0px #86ae47;

    }

    .btn-new-game:hover {
        background:linear-gradient(to bottom, #a5cc52 5%, #b8e356 100%);
	    background-color:#a5cc52;
    }


</style>

