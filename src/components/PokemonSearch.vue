<template>
    <div class="relative mx-auto mb-4 w-full max-w-xl">
        <form @submit.prevent="setPokemonUrl">
            <input
                class="w-full rounded border-none pb-2 pl-4 pr-4 pt-2 shadow outline-none"
                type="text"
                name=""
                id=""
                v-model="searchTerm"
            />
        </form>

        <font-awesome-icon
            icon="search"
            class="absolute right-[10px] top-[10px]"
            @click="setPokemonUrl"
        />
    </div>
</template>

<script>
export default {
    props: ['apiUrl'],
    data() {
        return {
            searchTerm: null,
        }
    },
    methods: {
        setPokemonUrl(url) {
            if (this.searchTerm !== '') {
                this.$emit(
                    'set-pokemon-url',
                    this.apiUrl + '/' + this.searchTerm.toLowerCase()
                )
            }
        },
    },
}
</script>

<style lang="scss" scoped></style>
