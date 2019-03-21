<template>
<div>
    <a @click="homeLink">Back to Home</a>
    <h1>{{userData.name}}</h1>
    <ul>
        <li>
            {{userData.email}}
            {{userData.phone}}
            {{userData.website}}
        </li>
    </ul>
    <router-link :to="postsLink"> <h1>Posts</h1> </router-link>
    <router-link :to="nextUserLink"> <h1>Next User</h1> </router-link>
</div>
</template>

<script>
export default {
    name: 'UserProfile',
    data() {
        return {
            userData: {}
        }
    },
    watch: { // listen route if its changed call the function we used this because route changes but data was not 
        '$route': 'fetchData'
    },
    computed: {
        postsLink() {
            return `/user/${this.$route.params.id}/posts`
        },
        nextUserLink() {
            return `/user/${ parseInt(this.$route.params.id,10) + 1 }`
        }
    },
    methods: {
        fetchData(){
            fetch(`https://jsonplaceholder.typicode.com/users/${this.$route.params.id}`)
            .then(response => response.json())
            .then(data => {
                this.userData = data
            })
        },
        homeLink() {
            this.$router.push({name: 'home'})
        }
    },
    created() {
        this.fetchData()
    },
}
</script>

<style>

</style>


