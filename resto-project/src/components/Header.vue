<template>
    <div class="nav">
        <router-link to="/">Home</router-link>
        <router-link to="/add">Add Restaurant</router-link>

        <a v-on:click="logout" href="#">Logout</a>
    </div>
</template>
  
<script>
export default {
    name: 'HeaderComponent',
    methods: {
        logout() {
            localStorage.clear();
            this.$router.push({ name: 'LoginPage' })
        }
    }
}
</script>
  
<style>
.nav {
    background-color: #333;
    overflow: hidden;
}

.nav a {
    float: left;
    color: #f2f2f2;
    text-align: center;
    padding: 16px 14px;
    text-decoration: none;
    font-size: 16px;
    margin-right: 4px;
}

.nav a:hover {
    background-color: #ddd;
    color: #222
}
</style>
  