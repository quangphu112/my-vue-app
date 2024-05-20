<template>
    <v-data-table :items="items" :headers="headers">
        <template v-slot:item.name="{ value }">
            <v-link class="custom-link" text @click="showDetail(value)">{{ value }}</v-link>
        </template>
    </v-data-table>
    <Dialog :item="item" ref="dialog" />
</template>

<script>
import Dialog from './Dialog.vue'
import axios from 'axios';
export default {
    name: 'CommonTable',
    components: {
        Dialog
    },
    data() {
        return {
            item: null
        }
    },
    props: {
        items: {
            type: Array,
        },
        headers: {
            type: Array,
        }
    },

    methods: {
        async showDetail(value) {
            await axios.get(`https://api.vandvietnam.com/api/pokemon-api/pokemons?filter[name]=${value}`)
                .then((response) => {
                    this.item = response.data.data[0];
                })
                .catch((error) => {
                    console.log(error);
                });
            this.$refs.dialog.openDialog();
        }
    }
}
</script>
<style scoped>
    .custom-link {
        cursor: pointer;
        color: #1da1f2;
        text-decoration:underline;
    }
</style>