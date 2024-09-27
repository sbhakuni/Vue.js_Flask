<template>
    <Header />
    <h1>Hello User, Welcome on Update Restaurant Page</h1>
    <form class="update">
        <input type="text" placeholder="Enter Name" v-model="restaurant.name" name="name" />
        <input type="text" placeholder="Enter Address" v-model="restaurant.address" address="address" />
        <input type="text" placeholder="Enter Contact" v-model="restaurant.contact" contact="contact" />
        <button type="button" v-on:click="updateRestaurant">Update Restaurant</button>
    </form>
</template>
  
<script>
import Header from './Header.vue';
import axios from 'axios';
export default {
    name: 'UpdatePage',
    components: {
        Header
    },
    data() {
        return {
            restaurant: {
                name: '',
                address: '',
                contact: ''
            }
        };
    },

    methods: {
  async updateRestaurant() {
    console.warn(this.restaurant);
    
    // Corrected typo in the URL ("restsurant" -> "restaurant")
    const result = await axios.put(
      "http://localhost:3000/restaurant/" + this.$route.params.id,
      {
        name: this.restaurant.name,
        address: this.restaurant.address,
        contact: this.restaurant.contact,
      }
    );
    
    // Check if the update was successful
    if (result.status === 200) {
      this.$router.push({ name: 'HomePage' });
    }
  },
},

    async mounted() {
        let user = localStorage.getItem('user-info');
        if (!user) {
            this.$router.push({ name: 'SignUp' });
            return; // Stop further execution if user is not found
        }
        console.log("Restaurant ID:", this.$route.params.id);
        // Correct URL with proper spelling and parameter access
        const result = await axios.get('http://localhost:3000/restaurant/'+this.$route.params.id); 
        console.warn(result.data); // Log the fetched restaurant data
        this.restaurant = result.data
    }

}
</script>
  