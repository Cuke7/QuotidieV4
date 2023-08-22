<template>
  <div class="h-screen flex overflow-auto flex-col p-8 text-black">
    <Notification />
    <h1 class="text-red-800 font-mono text-5xl mx-auto">Quotidie</h1>

    <div v-html="versetHTML" class="my-8 px-2" />
    <div
      v-html="evangileHTML"
      class="border-red-800 rounded-lg border-2 p-4 shadow-2xl"
    />
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import Notification from "./notification.vue";

const evangileHTML = ref("");
const versetHTML = ref("");

let date = new Date();
const formatedDate = date.toISOString().split("T")[0];

const APIURL = `https://api.aelf.org/v1/messes/${formatedDate}/france`;

console.log(APIURL);

fetchData(APIURL);

async function fetchData(APIURL: string) {
  try {
    const response = await fetch(APIURL);
    if (!response.ok) {
      throw new Error(
        `Network response was not ok, status: ${response.status}`
      );
    }
    const data = await response.json();
    // console.log("Fetched data:", data);
    let evangile = data.messes[0].lectures.find(
      (item) => item.type == "evangile"
    );

    console.log(evangile);

    evangileHTML.value = evangile.contenu;
    versetHTML.value = evangile.verset_evangile;
  } catch (error) {
    console.error("Fetch error:", error);
  }
}
</script>

<style>
body {
  background-image: url("./assets/background.jpg");
  background-repeat: repeat;
}
</style>
