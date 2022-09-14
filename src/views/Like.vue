<template>


    <div class="like-boxs">
        <router-link :to="{ name: 'home'}" class="back-like">Back</router-link>
        <div v-for="(r,index) in data" class="like-box" :key="r.title">
            <p>{{r}}</p>
        <router-link :to="{ name: 'about', params: { id: index }}" class="link">Read more</router-link>
        </div>
    </div>
</template>

<script>
export default {
    name: "App",
    data() {
        return {
            data: {}
        }
    },
    mounted() {
        this.data = JSON.parse(this.$route.params.items)
        console.log(this.data);
    }
}
</script>

<style >

.like-boxs {
    width: 100%;
    height: auto;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
}

.like-box {
    width: 90%;
    height: auto;
    margin: 20px;
    box-sizing: border-box;
    border: 1px solid black;
    padding: 5px;
    justify-content: center;
    align-items: center;
}

.back-like {
    text-decoration: none;
    color: white;
    border: 1px solid black;
    background-color: black;
    padding: 10px;
    height: 5vh;
}
</style>
