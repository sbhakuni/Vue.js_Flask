<template>
    <Header />
    <h1>Hello User, Welcome on Add Restaurant Page</h1>
    <form class="add">
        <input type="text" placeholder="Enter Name" v-model="restaurant.name" name="name" />
        <input type="text" placeholder="Enter Address" v-model="restaurant.address" address="address" />
        <input type="text" placeholder="Enter Contact" v-model="restaurant.contact" contact="contact" />
        <button type="button" v-on:click="addRestaurant">Add New Restaurant</button>
    </form>
</template>
  
<script>
import Header from './Header.vue';
import axios from 'axios'
export default {
    name: 'AddPage',
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
        async addRestaurant() {
            console.warn(this.restaurant);

            // Corrected typo in URL and object property separators
            const result = await axios.post("http://localhost:3000/restaurant", {
                name: this.restaurant.name,
                address: this.restaurant.address,
                contact: this.restaurant.contact
            });
            if (result.status==201)
            {
                this.$router.push({ name: 'HomePage' })  
            }
            console.warn("result", result)
        }
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if (!user) {
            this.$router.push({ name: 'SignUp' });
        }
    }
}
</script>
  