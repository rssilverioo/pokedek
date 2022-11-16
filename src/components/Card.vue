<script setup>
import { ref, watchEffect } from "vue";
import {colorsType} from "@/js/dictionary";
import {useRouter} from 'vue-router';

const props = defineProps({
  info: Object,
});

const router = useRouter();

const isLoad = ref(false);
const card = ref(null);

watchEffect(() => {
  if (isLoad.value) {
    card.value.style.borderColor = colorsType[props.info.type];
  }
});

function goDetails() {
  router.push({ name: "Details", params: { id: props.info.id } });
}
</script>

<template>
  <div class="card" ref="card">
    <div class="card__details">
      <div class="card__number">
        <h4 >#{{ info.id }}</h4>
      </div>
      <p class="card__name"> {{ info.name }}</p>
    </div>
    <div class="card__img">
      <img :src="info.img" :alt="info.name" />
    </div>
  </div>
</template>

<style>
.card {
  padding: 20px;
  margin: 10px;
  width: 300px;
  text-align: center;
  border-radius: 5px 5px 15px 15px;
  box-shadow: 1px 1px 5px #c3c3c3;
  border-top: 7px solid #2c3e50;
  transition: border 600ms;
  cursor: pointer;
}
.card__details {
  position: relative;
}
.card__img {
  width: 80%;
  max-height: 100%;
  margin: 5px auto;
}
.card__img img {
  width: 100%;
  height: 100%;
}
.card__name {
  text-transform: capitalize;
  font-weight: bold;
}
.card__skeleton {
  border-radius: 5px;
}
.card__skeleton--img {
  width: 240px;
  height: 240px;
}
.card__skeleton--txt {
  width: 100px;
  height: 15px;
  margin: auto;
  text-align: center;
}
.card__skeleton--number {
  width: 40px;
  height: 15px;
}
.card__number {
  position: absolute;
  left: 0;
}
</style>
