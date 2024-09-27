<template>
    <Header />
    <h1>Hello User, Welcome on Update Restaurant Page</h1>
    <form class="update">
        <input type="text" placeholder="Enter Name" v-model="restaurant.name" name="name" />
        <input type="text" placeholder="Enter Address" v-model="restaurant.address" address="address" />
        <input type="text" placeholder="Enter Contact" v-model="restaurant.contact" contact="contact" />
        <button type="button" v-on:click="addRestaurant">Update  Restaurant</button>
    </form>
</template>
  
<script>
import Header from './Header.vue';

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
    mounted() {
        let user = localStorage.getItem('user-info');
        if (!user) {
            this.$router.push({ name: 'SignUp' });
        }
    }
}
</script>
  