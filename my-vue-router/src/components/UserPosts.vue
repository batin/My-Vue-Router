<template>
<div>
    <router-link :to="profileLink">Back to User</router-link>
    <div v-for="post in posts">
        <h3>{{post.title}}</h3>
        <p>{{post.body}}</p>

    </div>
</div>
</template>

<script>
export default {
    name: 'UserPosts',
    data() {
        return {
            posts: {}
        }
    },
    computed: {
        profileLink(){
            return `/user/${this.$route.params.userId}`
        }
    },
    created() {
        fetch(`https://jsonplaceholder.typicode.com/posts?userId=${this.$route.params.userId}`)
            .then(response => response.json())
            .then(data => {
                this.posts = data
            })
    },
}
</script>
