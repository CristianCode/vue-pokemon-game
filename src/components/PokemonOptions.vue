<template>

    <div class="options-container">

        <ul>
            <li v-for="pokemon in pokemons" 
                :key="pokemon.id"
                @click="$emit( 'selection-pokemon', pokemon.id )">
                {{pokemon.name}}
            </li>
        </ul>

    </div>
  
</template>

<script>
export default {

    props: {
        pokemons: {
            type: Array,
            required: true
        }
    },

}
</script>

<style scoped>
    /* Pokemon Options */
    ul {
        list-style-type: none;
        padding-inline-start: 0px;
    }
    li {
        box-shadow: 3px 4px 0px 0px #1564ad;
        background:linear-gradient(to bottom, #79bbff 5%, #378de5 100%);
        background-color:#79bbff;
        border-radius:5px;
        border:1px solid #337bc4;
        margin-bottom: 10px;
        cursor:pointer;
        color:#ffffff;
        font-family:Arial;
        font-size:15px;
        font-weight:bold;
        padding:12px 44px;
        text-decoration:none;
        text-shadow:0px 1px 0px #528ecc;
    }

    li:hover {
        background:linear-gradient(to bottom, #378de5 5%, #79bbff 100%);
	    background-color:#378de5;
    }

    .options-container {
        display: flex;
        justify-content: center;
    }

</style>