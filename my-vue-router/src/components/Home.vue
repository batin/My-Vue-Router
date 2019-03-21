<template>
<div>
    <div v-for="user in users">
         <user-item :user=user></user-item>

    </div>
</div>
</template>

<script>
import UserItem from './UserItem'
export default {
    name: 'Home',
    data() {
        return {
            users: []
        }
    },
    created() {
        fetch('https://jsonplaceholder.typicode.com/users')
            .then(response => response.json())
            .then(users => {this.users = users})
    },
    components: {
        UserItem
    }
}
</script>
