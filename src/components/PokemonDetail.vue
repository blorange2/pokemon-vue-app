<template>
    <div
        class="fixed left-0 top-0 flex h-full w-full flex-col items-center justify-center bg-gray-600 bg-opacity-70 p-9"
    >
        <div
            class="relative flex w-full max-w-lg flex-col items-center justify-center rounded-lg bg-white p-10 shadow-lg"
            v-if="show"
        >
            <div v-if="pokemon">
                <img
                    class="mb-4 flex items-center justify-center rounded-full bg-gray-600"
                    :src="pokemon.imageUrl"
                    alt=""
                />
            </div>

            <div class="mb-4 w-full" v-if="pokemon">
                <h2 class="mb-4 text-center text-3xl capitalize">
                    {{ pokemon.name }}
                </h2>
                <div
                    class="mb-3 flex w-full flex-col items-center justify-start border-b-2 border-gray-900 pb-2"
                >
                    <div class="flex w-full justify-between">
                        <div class="float-left">Base Experience</div>
                        <div class="float-right">
                            {{ pokemon.base_experience }} XP
                        </div>
                    </div>
                </div>

                <div
                    class="text mb-3 flex w-full flex-col items-center justify-start border-b-2 border-gray-900 pb-2"
                >
                    <div class="flex w-full justify-between">
                        <div class="float-left">Height</div>
                        <div class="float-right">
                            {{ pokemon.height / 10 }} m
                        </div>
                    </div>
                </div>

                <div
                    class="mb-3 flex w-full flex-col items-center justify-start border-b-2 border-gray-900 pb-2"
                >
                    <div class="flex w-full justify-between">
                        <div class="float-left">Weight</div>
                        <div class="float-right">
                            {{ pokemon.weight / 10 }} kg
                        </div>
                    </div>
                </div>

                <h3 class="mb-4 text-left text-2xl">Pokemon Types</h3>
                <div class="flex flex-wrap justify-start">
                    <div
                        class="mb-3 ml-0 mr-3 mt-0 rounded-full bg-green-800 px-3 py-1 capitalize text-white"
                        v-for="(value, index) in pokemon.types"
                    >
                        {{ value.type.name }}
                    </div>
                </div>

                <h3 class="mb-4 text-left text-2xl">Abilities</h3>
                <div class="flex flex-wrap justify-start">
                    <div
                        class="mb-3 ml-0 mr-3 mt-0 rounded-full bg-green-800 px-3 py-1 capitalize text-white"
                        v-for="(value, index) in pokemon.abilities"
                    >
                        {{ value.ability.name }}
                    </div>
                </div>
            </div>

            <button
                class="btn rounded bg-blue-500 px-2 py-2 text-white"
                @click="closeDetail()"
            >
                Close
            </button>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    props: ['pokemonUrl', 'imageUrl'],
    mounted() {
        this.getPokemonData()
    },
    data() {
        return {
            show: false,
            pokemon: {},
        }
    },
    methods: {
        getPokemonData() {
            axios.get(this.pokemonUrl).then((response) => {
                this.pokemon = response.data
                this.pokemon.imageUrl = `${this.imageUrl}/${this.pokemon.id}.png`
                this.show = true
            })
        },
        closeDetail() {
            this.$emit('close-detail')
        },
    },
}
</script>

<style lang="scss" scoped></style>
