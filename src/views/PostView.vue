<template>
    <div class="wrapper">
        <div class="container">
            <h1>{{ title }}</h1>
            <h4>{{ summary }}</h4>
            <div class="content-container">
                <p>{{ content }}</p>
            </div>
        </div>
    </div>

    <div class="container-input">
        <label>Title:</label>
        <input type="text" placeholder="title" v-model="title" />
        <label>Summary:</label>
        <input type="text" placeholder="summary" v-model="summary" />
        <label>Content:</label>
        <input type="text" placeholder="content" v-model="content" />
    </div>
    <button @click="editPost()">Edit</button>
    <button @click="deletePost()">Delete</button>

</template>

<script>
export default {
    data() {
        return {
            title: "",
            content: "",
            summary: ""
        }
    },

    methods: {
        editPost() {
            const post = {
                title: this.title,
                summary: this.summary,
                content: this.content
            }
            const id = this.$route.params.id
            fetch('http://localhost:5050/api/Blogg/' + id, {
                method: 'PUT',
                body: JSON.stringify(post),
                headers: { "content-type": "application/json" },
            })
                .then(() => {
                    alert("Post has been updated")
                    this.$router.push('/')
                })
        },
        deletePost() {
            const id = this.$route.params.id
            fetch('http://localhost:5050/api/Blogg/' + id, {
                method: 'DELETE',
            })
                .then(() => {
                    alert('Delete post successfully')
                    this.$router.push('/')
                })
        }
    },
    created() {
        const id = this.$route.params.id
        fetch('http://localhost:5050/api/Blogg/' + id)
            .then(response => response.json())
            .then(posts => {
                this.title = posts.title
                this.content = posts.content
                this.summary = posts.summary
            })
    }
}
</script>

<style scoped>
.wrapper
{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border: 2px solid black;
    border-radius: 50px;
    margin-bottom: 50px;
}

h1
{
    color: #42b983;
}

.container
{
    width: 70%;
    line-height: 30px;
}

.content-container
{
    background: lightgray;
    border: 2px solid black;
    padding: 20px;
    margin-bottom: 40px;
}

p
{
    font-size: 18px;
    color: black;
    opacity: 1;
}

wrapper-input
{
    gap: 500px;
}

.container-input
{
    display: flex;
    justify-content: center;
    align-content: center;
    align-items: center;
    margin-top: 10px;
    margin-bottom: 20px;
    width: 100%;
    gap: 20px;
    border: 2px solid black;
    border-radius: 50px;
}

button
{
    width: 100%;
    margin: 20px 0px;
}
</style>
<style>
input
{
    width: 100%;
    padding: 10px;
    margin: 20px 20px;
}

label
{
    padding-left: 50px;
    margin-left: 0px;
}
</style>