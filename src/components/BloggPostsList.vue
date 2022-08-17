<template> 
<h1>Mina inlägg</h1>
<div v-for="posts in bloggPostobj" :key="posts.id">
    <div class="wrapper">
        <div class="blogg-container">
            <router-link :to="'/posts/' + posts.id"><h2>{{ posts.title }}</h2></router-link>
            <h4>{{ posts.summary }}</h4>
        </div>
    </div>
</div>
<router-link :to="'/create-new'"><button>Skapa nytt inlägg</button></router-link>
</template>

<script>

export default {
    name: "bloggList",

    data() {
        return {
            bloggPostobj: []
        }
    },
 
    created() {
        fetch('http://localhost:5050/api/Blogg')
        .then(response => response.json())
        .then(posts => {
            console.log(posts)
            this.bloggPostobj = posts;
        }) 
    }
}
</script>
<style scoped>
.wrapper {
    display: flex;
    flex-direction:column;
    justify-content: center;
    align-items: center;
    
}
.blogg-container {
    width:100%;
    max-width:500px;
    border: 2px solid #42b983;   
    background: rgba(128, 128, 128, 0.205); 
    margin: 5px  ;
}
a {
    color: #42b983;
}
</style>

<style>
button {
    background: transparent;
    border: none;
    background:#42b983;
    color: black;
    border-radius: 20px;
    cursor: pointer;
    padding: 25px 25px;
    font-size: 20px;
    box-shadow: 0px 0px 10px 2px inset;
    margin: 50px;
}
button:hover {
    opacity: 0.90;
    box-shadow: 0px 0px 0px 2px inset;
}
</style>
