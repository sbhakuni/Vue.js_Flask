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
        addRestaurant() {
            console.war
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
  