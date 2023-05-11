<template>
  <div class="about">
    <h1>This is an about page</h1>
    <h1>{{ postData.id }}</h1>
  </div>
</template>

<style></style>
<script setup>
import { onMounted, ref } from "vue";

const postData = ref({});

const getPost = async () => {
  return fetch("https://fakestoreapi.com/products/1").then((response) =>
    response.json()
  );
};
onMounted(() => {
  getPost().then((data) => {
    postData.value = data;
  });
});
</script>
