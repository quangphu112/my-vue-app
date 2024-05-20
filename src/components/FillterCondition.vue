<template>
    <v-expansion-panels>
        <v-expansion-panel style="text-align: center;">
            <v-expansion-panel-title>
                <span>Fillter Condition</span>
            </v-expansion-panel-title>
            <v-expansion-panel-text>
                <v-row>
                    <v-col cols="6">
                        <v-text-field v-model="params.name" label="Name" clearable></v-text-field>
                    </v-col>
                    <v-col cols="6">
                        <v-select v-model="params.type" :items="types" label="Type" item-title="name" item-value="id" clearable @click:clear="params.type = ''">
                        </v-select>
                    </v-col>
                </v-row>
                <v-btn color="white" @click="search()">Search</v-btn>
            </v-expansion-panel-text>
        </v-expansion-panel>
    </v-expansion-panels>
</template>
<script>
export default {
    name: 'FillterCondition',
    data() { },
    props: {
        types: {
            type: Array,
        },
        params: {
            type: Object,
        }
    },

    methods: {
        search() {
            this.$emit('search');
        }
    }
}
</script>
<style lang="scss"></style>
