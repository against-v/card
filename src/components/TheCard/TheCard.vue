<script setup lang="ts">
import { computed, onMounted, ref, useCssModule, watch } from "vue";

const CARD_BACK = `public/img/card-back.png`;

const props = defineProps<{
  index: number;
  code: string;
}>();

const style = useCssModule();

const cardStyle = computed(() => {
  return {
    "grid-column-start": `${props.index + 1}`
  };
});

const cardClasses = computed(() => {
  return [
    style.container,
    { [style.isOpening]: isOpening.value },
    { [style.isOpened]: isOpened.value }
  ];
});

const containerRef = ref<HTMLElement>();

const isOpening = ref(false);
const isOpened = ref(false);

const imgSrc = computed(() => {
  if (props.code) {
    return `public/img/card-${props.code}.png`;
  } else {
    return CARD_BACK;
  }
});

const handleAnimationEnd = () => {
  isOpening.value = false;
  isOpened.value = true;
};

watch(
  () => props.code,
  (value) => {
    if (value) {
      isOpening.value = true;
    } else {
      isOpening.value = false;
      isOpened.value = false;
    }
  }
);
onMounted(() => {
  if (containerRef.value) {
    containerRef.value.addEventListener("animationend", handleAnimationEnd);
  }
});
</script>

<template>
  <div :class="cardClasses" :style="cardStyle" ref="containerRef">
    <img :class="$style.back" :src="CARD_BACK" alt="" />
    <img :class="$style.front" :src="imgSrc" alt="" />
  </div>
</template>

<style module>
.container {
  width: 180px;
  padding-bottom: 150%;
  height: 0;
  grid-row-start: 2;
  transform-style: preserve-3d;
  will-change: transform, top;
  position: relative;
}
.img {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  backface-visibility: hidden;
}
.back {
  composes: img;
}
.front {
  composes: img;
  transform: rotateY(180deg);
}
.container.isOpening {
  animation: flip 2s linear forwards;
}
.container.isOpened {
  grid-row-start: 1;
  transform: rotateY(180deg);
}

@keyframes flip {
  0% {
    transform: scale(1) rotateY(0);
  }
  10% {
    transform: scale(1.1) rotateY(0);
  }
  /*100% {
    position: absolute;
    transform: scale(1.1) rotateY(0);
  }*/
  20% {
    transform: scale(1.1) rotateY(0);
  }
  45% {
    transform: scale(1.1) rotateY(180deg);
  }
  55% {
    top: 0;
    transform: scale(1.1) rotateY(180deg);
  }
  70% {
    top: calc(-100% - 40px);
    /*transform: scale(1.1) rotateY(180deg) translateY(calc(-100% - 40px));*/
    transform: scale(1.1) rotateY(180deg);
  }
  90% {
    top: calc(-100% - 40px);
    /*transform: scale(1.1) rotateY(180deg) translateY(calc(-100% - 40px));*/
    transform: scale(1.1) rotateY(180deg);
  }
  100% {
    top: calc(-100% - 40px);
    /*transform: scale(1) rotateY(180deg) translateY(calc(-100% - 40px));*/
    transform: scale(1) rotateY(180deg);
  }
}

@media screen and (max-width: 640px) {
  .container {
    width: 100%;
    padding-bottom: 150%;
  }
}
</style>
