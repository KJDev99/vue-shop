<template>
  <div class="container">
    <div class="grid grid-cols-4 gap-4 mb-5">
      <div @click="$router.push(`/${item.id}`)" class="card" v-for="item of product" :key="item.id">
        <h4>{{ item.title }}</h4>
        <img :src="item.image" alt="">
        <p>{{ item.description }}</p>
        <div class="price">
          <i>#{{ item.category }}</i>
          <b>{{ item.price }} $</b>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      product: [],
    }
  },
  methods: {
    async Product() {
      let res = await axios.get(`https://fakestoreapi.com/products`)
      if (res.status == 200) {
        this.product = [...res.data];
      }
    }
  },
  mounted() {
    this.Product()
  }
}
</script>

<style>
.container {
  width: 1200px !important;
  margin: auto;
}

.card {
  border: 1px solid #111;
  border-radius: 5px;
  overflow: hidden;
  transition: 0.3s;
}

.card:hover {
  box-shadow: 0px 0px 30px 0px #111111b1;
}

.card h4 {
  padding: 10px 15px;
  height: 65px;
  background: #e7e7e7;
  color: black;
  text-align: center;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  overflow: hidden;
  text-overflow: ellipsis;
}

.card img {
  height: 300px;
  margin-top: 10px;
  margin-left: auto;
  margin-right: auto;
  padding: 10px;
}

.card p {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 4;
  text-align: justify;
  padding-left: 10px;
  padding-right: 10px;
  overflow: hidden;
  text-overflow: ellipsis;
  height: 100px;
}

.price {
  display: flex;
  padding-left: 10px;
  padding-right: 10px;
  height: 50px;
  background: #e7e7e7;
  align-items: center;
  justify-content: space-between;
  cursor: pointer;
}
</style>