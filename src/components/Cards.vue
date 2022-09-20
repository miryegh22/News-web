<template>
  <div v-if="isLoading" class="loader-wrapper">
    <div class="lds-roller">
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
    </div>
  </div>
  <div v-else>
    <div style="display:flex;justify-content: space-between;">
    <router-link
      :to="{ name: 'like', params: { items: JSON.stringify(likedItems) } }"
      style="
        text-decoration: none;
        width: 20%;
        color: white;
        border: 1px solid black;
        background-color: black;
        padding: 20px;
        font-size: 20px;
        height: 5vh;
      "
      >View Like</router-link
    >
    <input type="text" placeholder="Search..." v-model="search" class="search">
    </div>
    <div class="boxs">
     
      <div v-for="(r, index) in filter" class="box" :key="r.title">
        <div style="min-height: 80%;">
        <h4>{{ r.publishedAt.substring(0, 10) }}</h4>
        <h2>{{ r.title }}</h2>
        <img v-bind:src="r.urlToImage" alt="" class="image" />
        <p>{{ r.description }}</p>
      </div>
        <div class="read-like"><router-link :to="{ name: 'about', params: { id: index } }" class="link"
          >Read more</router-link
        >
        <button
          :class="likedItems.includes(r.description) ? 'is-liked' : 'like'"
          @click="like(r.description)"
        >
          Like
        </button> </div>
        
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "App",
  data() {
    return {
      search:'',
      root: "",
      isLoading: true,
      likedItems: [],
    };
  },
  computed:{
    filter(){
    return this.root.filter(ro=>ro.title.toLowerCase().includes(this.search.toLowerCase()))}
  },
  methods: {
    like(desc) {
      if (this.likedItems.includes(desc)) {
        this.likedItems = this.likedItems.filter((item) => item !== desc);
      } else {
        this.likedItems.push(desc);
      }
      let arr = [];
      this.root.forEach((element) => {
        if (this.likedItems.includes(element.description)) {
          arr.push(element);
        }
      });
      localStorage.setItem("likedItems", JSON.stringify(arr));
      
    },
  },
  async mounted() {
    await fetch(
      "https://newsapi.org/v2/everything?q=apple&from=2022-09-08&to=2022-09-08&sortBy=popularity&apiKey=63d699556937430bbf218b9fa4ae8afc"
    )
      .then((res) => res.json())
      .then((res) => {
        if (res) {
          this.root = res.articles;
          this.isLoading = false;
        }
      });
    const arr = JSON.parse(localStorage.getItem("likedItems"));
    if (arr.length) {
      arr.forEach((item) => {
        this.likedItems.push(item.description);
      });
    }
  },
};
</script>

<style>
.boxs {
  width: 100%;
  height: auto;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  flex-flow: wrap;
}

.box {
  width: 30%;
  height: auto;
  margin: 20px;
  box-sizing: border-box;
  border: 1px solid rgb(211, 207, 207);
  border-radius: 1%;
  display: flex;
  flex-direction: column;
  gap:1vh;
  justify-content: space-between;
}

.box:hover {
  opacity: 0.7;
}

.image {
  width: 80%;
  margin-left: 10%;
  height: 50%;
}

.link {
  text-decoration: none;
  font-size: 20px;
  margin-left: 70%;
  color: black;
}
.like {
  text-decoration: none;
  font-size: 20px;
  margin-left: 70%;
  color: black;
}
.is-liked {
  text-decoration: none;
  font-size: 20px;
  margin-left: 70%;
  color: red;
}
.loader-wrapper {
  height: 50vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.lds-roller {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}

.lds-roller div {
  animation: lds-roller 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  transform-origin: 40px 40px;
}

.lds-roller div:after {
  content: " ";
  display: block;
  position: absolute;
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: black;
  margin: -4px 0 0 -4px;
}

.lds-roller div:nth-child(1) {
  animation-delay: -0.036s;
}

.lds-roller div:nth-child(1):after {
  top: 63px;
  left: 63px;
}

.lds-roller div:nth-child(2) {
  animation-delay: -0.072s;
}

.lds-roller div:nth-child(2):after {
  top: 68px;
  left: 56px;
}

.lds-roller div:nth-child(3) {
  animation-delay: -0.108s;
}

.lds-roller div:nth-child(3):after {
  top: 71px;
  left: 48px;
}

.lds-roller div:nth-child(4) {
  animation-delay: -0.144s;
}

.lds-roller div:nth-child(4):after {
  top: 72px;
  left: 40px;
}

.lds-roller div:nth-child(5) {
  animation-delay: -0.18s;
}

.lds-roller div:nth-child(5):after {
  top: 71px;
  left: 32px;
}

.lds-roller div:nth-child(6) {
  animation-delay: -0.216s;
}

.lds-roller div:nth-child(6):after {
  top: 68px;
  left: 24px;
}

.lds-roller div:nth-child(7) {
  animation-delay: -0.252s;
}

.lds-roller div:nth-child(7):after {
  top: 63px;
  left: 17px;
}

.lds-roller div:nth-child(8) {
  animation-delay: -0.288s;
}

.lds-roller div:nth-child(8):after {
  top: 56px;
  left: 12px;
}

@keyframes lds-roller {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}
.like {
  color: black;
  
}
.read-like{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.search{
  width:80%;
  text-align: center;
  font-size: large;
  border:1px solid black
}
.search:hover{
  border:3px solid red
}
</style>
