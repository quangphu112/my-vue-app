<template>
  <v-app>
    <v-main>
      <FillterCondition :types="types" :params="params" @search="search" />
      <CommonTable :items="items" :headers="HEADERS" />
    </v-main>
  </v-app>
</template>

<script>
import axios from 'axios';
import CommonTable from './components/CommonTable.vue'
import FillterCondition from './components/FillterCondition.vue'
export default {
  name: 'App',
  components: {
    CommonTable,
    FillterCondition
  },

  data() {
    return {
      items: [],
      types: [],
      params: {
        name: '',
        type: '',
      }
    }
  },

  computed: {
    HEADERS() {
      return [
        {
          title: 'Number',
          key: 'number',
        },
        {
          title: 'Name',
          key: 'name',
        },
        {
          title: 'Attack',
          key: 'attack',
        },
        {
          title: 'Defense',
          key: 'defense',
        },
        {
          title: 'HP',
          key: 'hp',
        },
        {
          title: 'Sp_Atk',
          key: 'sp_atk',
        },
        {
          title: 'Sp_Def',
          key: 'sp_def',
        },
        {
          title: 'Total',
          key: 'total',
        },
        {
          title: 'Speed',
          key: 'speed',
        },
        {
          title: 'Type 1',
          key: 'type_1',
        },
        {
          title: 'Type 2',
          key: 'type_2',
        },
      ]
    }
  },

  created() {
    this.getData();
    this.getDataType();
  },

  methods: {
    async getData() {
      try {
        const response = await axios.get('https://api.vandvietnam.com/api/pokemon-api/pokemons');
        this.items = response.data.data;
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },

    async getDataType() {
      try {
        const response = await axios.get('https://api.vandvietnam.com/api/pokemon-api/types');
        this.types = response.data.data;
      } catch (error) {
        console.error('Error fetching data types:', error);
      }
    },

    async search() {
      try {
        const response = await axios.get(`https://api.vandvietnam.com/api/pokemon-api/pokemons?filter[name]=${this.params.name}&filter[type]=${this.params.type}`);
        this.items = response.data.data;
      } catch (error) {
        console.error('Error searching data:', error);
      }
    }
  }
}
</script>
