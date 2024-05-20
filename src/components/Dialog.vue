<template>
    <div class="text-center pa-4">
        <v-dialog v-model="dialog" width="auto">
            <v-card min-width="500"
                :title="item.name">
                <img :src="imageUrl">
                <template v-slot:actions>
                    <v-btn class="ms-auto" @click="closeDialog()">Close</v-btn>
                </template>
            </v-card>
        </v-dialog>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'Dialog',
    data() {
        return {
            dialog: false,
            imageUrl: null
        }
    },
    props: {
        item: {
            type: Object,
        }
    },

    watch: {
    async item(newItem) {
      if (newItem && newItem.id) {
        try {
          const response = await axios.get(`https://api.vandvietnam.com/api/pokemon-api/pokemons/${newItem.id}/sprite`, {
            responseType: 'arraybuffer' 
          });
          const blob = new Blob([response.data], { type: 'image/png' });
          this.imageUrl = URL.createObjectURL(blob);
        } catch (error) {
          console.error(error);
        }
      }
    }
  },
    
    methods: {
        openDialog() {
            this.dialog = true;
        },

        closeDialog() {
            this.dialog = false;
            this.imageUrl = null;
        }
    }
}
</script>