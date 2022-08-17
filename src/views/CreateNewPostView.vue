<template>
    <h1>Skapa nytt inlägg</h1>
    <div class="input-group">
        <div class="input-group-addon">
        <input type="text" placeholder="title" v-model="title" /><br />
        <input type="text" placeholder="summary" v-model="summary" /><br />
        <textarea class="content-container" placeholder="content" v-model="content"></textarea>
        </div>
       <button class="btn" @click="SavePost()">Spara</button>
    </div>
    
</template>

<script>
export default {
    data() {
        return {
            title: "",
            summary: "",
            content: "",
        }
    },
    methods: {
        SavePost() {
            const post = {
                title: this.title,
                summary: this.summary,
                content: this.content,
            }
            fetch('http://localhost:5050/api/Blogg', {
                method: 'POST',
                body: JSON.stringify(post),
                headers: { 'content-type': 'application/json' }
            })
                .then(() => {
                    alert("post Saved successfully")
                    this.$router.push("/")
                })
        }
    }
}
</script>

<style scoped>
.input-group
{
    margin-left: 500px;
    width: 50%;
    height: 100%;
    border: 1px solid black;
    border-radius: 5px;
    padding: 10px;
    padding-bottom: 40px;
}
.input-group-addon{
    width: 90%;
}
.content-container {
    margin-left: 20px;
    display: flex;
    height: 200px;
    width: 100%;
    resize: none;
    padding: 10px;
    font-family:Arial, Helvetica, sans-serif;
}
.btn{
    width: 80%;
    margin:0;
    margin-top:20px;
}

</style>