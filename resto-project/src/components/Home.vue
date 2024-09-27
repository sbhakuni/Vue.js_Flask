<template>
  <Header />
  <h1>Hello {{ name }}, Welcome on Home Page</h1>
  <table border="1">
    <tr>
      <td>Id</td>
      <td>Name</td>
      <td>Address</td>
      <td>Contact</td>
      <td>Actions</td>
    </tr>
    <tr v-for="item in restaurant" :key="item.id">
      <td>{{ item.id }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.address }}</td>
      <td>{{ item.contact }}</td>
      <td><router-link :to="`/update/${item.id}`">Update Restaurant</router-link>
        <button v-on:click="deleteRestaurant(item.id)">Delete</button>
      </td>
    </tr>
  </table>
</template>
  
<script>
import axios from 'axios';
import Header from './Header.vue';

export default {
  name: 'HomePage',
  data() {
    return {
      name: '',
      restaurant: [],
    };
  },
  methods: {
    async deleteRestaurant(id) {
      // Corrected the typo in the URL ("restsurant" -> "restaurant")
      let result = await axios.delete("http://localhost:3000/restaurant/" + id);
      console.warn(result);

      if (result.status === 200) {
        this.loadData(); // Reload data after successful deletion
      }
    }
    ,
    async loadData() {
      // Check if user is logged in
      let user = localStorage.getItem('user-info');
      if (!user) {
        this.$router.push({ name: 'SignUp' });
      } else {
        // Set user's name from local storage
        this.name = JSON.parse(user).name;

        // Fetch restaurant data from API
        try {
          let result = await axios.get('http://localhost:3000/restaurant');
          console.warn(result); // Debugging - log the result to the console
          if (result.status === 200) {
            this.restaurant = result.data;
          }
        } catch (error) {
          console.error('Error fetching restaurant:', error);
        }
      }
    }
  },
  components: {
    Header,
  },
  async mounted() {
    this.loadData();
  },
};
</script>
  
<style>
td {
  width: 160px;
  height: 40px;
}
</style>
  