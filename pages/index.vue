<template>
    <v-layout
        column
        justify-center
        align-center
    >
        <v-container>
            <v-row dense>
                <v-col v-for="(item, i) in shows" :key="i" cols="12">
                    <NuxtLink :to="`posts/${item.id}`">
                        <v-card color="grey" max-width="440" class="mx-auto">
                            <div class="d-flex flex-no-wrap justify-space-between">
                                <div>
                                    <v-card-title class="headline" v-text="item.name"></v-card-title>
                                    <v-card-subtitle v-text="item.type"></v-card-subtitle>
                                </div>
                                <v-avatar class="ma-3" size="125" tile>
                                    <v-img :src="item.image.medium"></v-img>
                                </v-avatar>
                            </div>
                        </v-card>
                    </NuxtLink>
                </v-col>
            </v-row>
        </v-container>
    </v-layout>
</template>

<script>
import axios from 'axios'

export default {
    async asyncData() {
        const { data } = await axios.get('https://api.tvmaze.com/search/shows?q=batman')
        return { shows: data.map(entry => entry.show) }
    }
}
</script>