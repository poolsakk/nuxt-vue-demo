<template>
    <div class="container">
        <v-card-actions class="justify-center">
            <h1 class="title">{{name}}</h1>
        </v-card-actions>
        <v-container fluid>
            <v-row justify="space-around">
                <v-col cols="5">
                    <v-img :src="image.original" aspect-ratio="1.4" contain></v-img>
                </v-col>
            </v-row>
        </v-container>
        <v-card-actions class="justify-center">
            <p v-html="summary">{{summary}}</p>
        </v-card-actions>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    validate ({ params }) {
        return !isNaN(+params.id)
    },
    async asyncData({ params, error }) {
        try {
            const { data } = await axios.get(`https://api.tvmaze.com/shows/${+params.id}`)
            return data
        } catch(e) {
            error({message: 'id not found', statusCode: 404})
        }
    },
    transition: 'bounce'
}
</script>