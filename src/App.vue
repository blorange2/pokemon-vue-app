<script>
import PokemonList from './components/PokemonList.vue'
import PokemonDetail from './components/PokemonDetail.vue'
import PokemonSearch from './components/PokemonSearch.vue'

export default {
    data() {
        return {
            apiUrl: 'https://pokeapi.co/api/v2/pokemon',
            imageUrl:
                'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon',
            individualPokemonUrl: null,
            showDetail: false,
        }
    },
    components: { PokemonList, PokemonDetail, PokemonSearch },
    methods: {
        onSetPokemonUrl(url) {
            this.individualPokemonUrl = url
            this.showDetail = true
        },
        onCloseDetail() {
            this.showDetail = false
            this.individualPokemonUrl = null
        },
    },
}
</script>

<template>
    <div class="container mx-auto bg-blue-400 py-4">
        <PokemonSearch :apiUrl="apiUrl" @set-pokemon-url="onSetPokemonUrl" />
        <PokemonList
            :imageUrl="imageUrl"
            :apiUrl="apiUrl"
            @set-pokemon-url="onSetPokemonUrl"
        />
        <PokemonDetail
            v-if="showDetail"
            :pokemonUrl="individualPokemonUrl"
            :imageUrl="imageUrl"
            @close-detail="onCloseDetail"
        />
    </div>
</template>

<style scoped></style>
