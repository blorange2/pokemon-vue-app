<template>
    <div class="mx-auto grid w-full max-w-xl grid-cols-4 gap-4">
        <article
            class="mx-auto my-auto h-40 w-full cursor-pointer rounded-lg border-2 border-gray-300 bg-slate-100 p-4 capitalize shadow-md transition-all delay-75 hover:scale-110"
            v-for="(pokemon, index) in pokemon"
            :key="index"
            @click="setPokemonUrl(pokemon.url)"
        >
            <img class="mx-auto" :src="pokemon.imageUrl" alt="" />
            <h3 class="mx-auto my-0 text-center">{{ pokemon.name }}</h3>
        </article>
        <div
            id="scroll-trigger"
            ref="infinateScrollTrigger"
            class="flex w-full items-center justify-items-center"
        >
            <font-awesome-icon icon="spinner" spin />
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    created() {},
    mounted() {
        this.currentPageUrl = this.apiUrl
        this.fetchPokemon()
        this.scrollTrigger()
    },
    data: () => {
        return {
            pokemon: [],
            currentPageUrl: null,
            nextPageUrl: null,
        }
    },
    props: ['apiUrl', 'imageUrl'],
    methods: {
        fetchPokemon() {
            axios
                .get(this.currentPageUrl)
                .then((response) => {
                    this.nextPageUrl = response.data.next

                    response.data.results.forEach((pokemon) => {
                        const urlParts = pokemon.url.split('/')
                        pokemon.id = urlParts[urlParts.length - 2]
                        pokemon.imageUrl = `${this.imageUrl}/${pokemon.id}.png`

                        this.pokemon.push(pokemon)
                    })
                })
                .catch((error) => {})
        },
        scrollTrigger() {
            const observer = new IntersectionObserver((entries) => {
                entries.forEach((entry) => {
                    if (entry.intersectionRatio > 0 && this.nextPageUrl) {
                        this.next()
                    }
                })
            })

            observer.observe(this.$refs.infinateScrollTrigger)
        },
        next() {
            this.currentPageUrl = this.nextPageUrl
            this.fetchPokemon()
        },
        setPokemonUrl(url) {
            this.$emit('set-pokemon-url', url)
        },
    },
}
</script>

<style lang="scss" scoped></style>
