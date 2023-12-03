<template>
  <div>
    <h1>Mina Resor</h1>
    <ul>
      <li v-for="destination in destinations" :key="destination.id">
        <h2>{{ destination.destination }}</h2>
        <p>{{ formatDates(destination.dates) }}</p>
        <p>{{ destination.description }}</p>
        
        <ul>Highlights:
          <li v-for="highlight in destination.highlights" :key="highlight">
            {{ highlight }}
          </li>
        </ul>
        <img :src="require(`../img/${destination.images}`)" alt="" />
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      destinations: [],
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
  try {
    const response = await axios.get('../travel.json');
    this.destinations = response.data;
  } catch (error) {
    console.error('Error fetching data:', error);
  }
},
    formatDates(dates) {
      return dates.map(date => `${date.month} ${date.year}`).join(', ');
    },
  },
};
</script>

<style scoped>
  div {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
  }

   ul {
    padding-left: 0;
    list-style: none;
    padding-bottom: 20px;
   }

 
  img {
    max-width: 500px;
    max-height: 400px;
    padding-bottom: 30px;
  }
</style>
