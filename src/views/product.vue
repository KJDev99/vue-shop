<template>
    <div class="container">
        <div class="grid grid-cols-1 sm:grid-cols-2 sm:gap-20 gap-5 mx-auto">
            <div class="sm:p-20 p-0">
                <img class="h-[30vh] sm:h-[50vh] mx-auto" :src="element.image" alt="">
            </div>
            <div class="p-5 sm:p-20">
                <h4 class="sm:mb-10 mb-5 sm:font-bold text-lg sm:text-2xl">{{ element.title }}</h4>
                <p class="mb-10 sm:mb-20 italic text-justify">{{ element.description }}</p>
                <div class="price">
                    <i>#{{ element.category }}</i>
                    <b>{{ element.price }} $</b>
                </div>
            </div>
        </div>
        <hr class="mb-10">
        <div class="grid grid-cols-1 p-5 sm:grid-cols-4 gap-4 mb-5">
            <div @click="otish(item)" class="card" v-for="item of another" :key="item.id">
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
            id: '',
            element: {},
            category: '',
            another: []
        }
    },
    methods: {
        async getElementById() {
            let res = await axios.get(`http://fakestoreapi.com/products/${this.id}`)
            if (res.status == 200) {
                this.element = { ...res.data };
                this.anotherProduct()
            }
        },
        async anotherProduct() {
            let res = await axios.get(`http://fakestoreapi.com/products/category/${this.element.category}`)
            if (res.status == 200) {

                this.another = res.data.filter(el => el.id != this.id)
                this.another.length > 4 && this.another.splice(4, this.another.length - 1)

            }
        },
        otish(a) {
            this.$router.push(`/${a.id}`)
            this.id = a.id
            this.getElementById()
        }
    },
    mounted() {
        this.id = this.$route.params.id
        this.getElementById()
    }
}
</script>

<style></style>