<script setup lang="ts">
import { computed, ref } from "vue";
import TheCard from "@/components/TheCard/TheCard.vue";
type Card = {
  id: number;
  code: string;
};
const cards = ref<Card[]>([
  {
    id: 1,
    code: ""
  },
  {
    id: 2,
    code: ""
  },
  {
    id: 3,
    code: ""
  }
]);

const buttonText = computed(() => {
  return isStarted.value ? "Reset" : "Start";
});

const isStarted = ref(false);

const handleClickButton = () => {
  if (isStarted.value) {
    cards.value[1].code = "";
    isStarted.value = false;
  } else {
    isStarted.value = true;
    cards.value[1].code = "12-clubs";
  }
};
</script>

<template>
  <div :class="$style.container">
    <div :class="$style.desk">
      <TheCard v-for="(item, index) in cards" :key="item.id" :code="item.code" :index="index" />
    </div>
    <button @click.prevent="handleClickButton" :class="$style.button">{{ buttonText }}</button>
  </div>
</template>

<style module>
.container {
  height: 100%;
  background-color: #080911;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 10px;
}
.desk {
  position: relative;
  max-width: 620px;
  max-height: 620px;
  width: 100%;
  height: 100%;
  padding: 20px;
  background-color: #948e8e;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(2, 1fr);
  gap: 40px 20px;
  perspective: 360px;
  margin-bottom: 20px;
}
.button {
  width: 100px;
  height: 40px;
}

@media screen and (max-width: 640px) {
  .container {
    padding: 0 0 10px 0;
  }
  .desk {
    /*grid-template-rows: 2fr 150px;*/
    overflow: hidden;
    gap: 40px 10px;
    padding: 10px;
  }
}
@media screen and (max-width: 440px) {
  .desk {
    /*grid-template-rows: 2fr 100px;*/
  }
}
</style>
