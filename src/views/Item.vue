<template>
  <div class="container">
    <div class="product">
      <img v-bind:src="postData.image" alt="baju" />
      <div class="text">
        <h1>{{ postData.title }}</h1>
        <div class="flex-row">
          <h5>{{ postData.category }}</h5>
          <h5>{{ postData.rating }}</h5>
        </div>
        <p>{{ postData.description }}</p>
        <h1>{{ postData.price }}</h1>
        <div class="flex-row">
          <button>Buy Now</button>
          <!-- <h2>{{ $route.params.id }}</h2> -->
          <button
            @click="
              () => {
                getPost(
                  Number($route.params.id) == 20
                    ? 1
                    : Number($route.params.id) + 1
                );
                $router.push(
                  `/product/${
                    Number($route.params.id) == 20
                      ? 1
                      : Number($route.params.id) + 1
                  }`
                );
              }
            "
          >
            Next Product
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;700&display=swap");
* {
  font-family: "Poppins", sans-serif;
}
.container {
  /* background-color: red; */
  width: 100%;
  height: 700px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.flex-row {
  display: flex;
  flex-direction: row;
}
.text {
  display: flex;
  flex-direction: column;
}
img {
  height: 80%;
  width: 40%;
}
.product {
  background-color: white;
  width: 80%;
  height: 500px;
  border-radius: 10px;
  padding: 20px;
  display: flex;
  flex-direction: row;
}
</style>
<script setup>
import { useRoute } from "vue-router";
const route = useRoute();
import { onMounted, ref } from "vue";

const postData = ref({});

// console.log(postData.value);

const getPost = async (asd) => {
  return fetch(`https://fakestoreapi.com/products/${asd}`).then((response) =>
    response.json().then((data) => {
      postData.value = data;
      console.log(data);
    })
  );
};
onMounted(() => {
  getPost(Number(route.params.id)).then((data) => {
    postData.value = data;
  });
});
</script>
