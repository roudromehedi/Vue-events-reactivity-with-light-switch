<script setup>
import { ref, reactive } from "vue";
const lightOnImage = "//img.icons8.com/?size=512&id=12244&format=png";
const lightOffImage = "//img.icons8.com/?size=512&id=75&format=png";

const getBackgroundColorClass = () => {
  const lightsOnCount = lights.filter((light) => light.lightOn).length;
  if (lightsOnCount === 1) {
    return "bg-yellow-50";
  }
  if (lightsOnCount === 2) {
    return "bg-yellow-100";
  }
  if (lightsOnCount === 3) {
    return "bg-yellow-200";
  } else {
    return "bg-gray-300";
  }
};
const lights = reactive([
  {
    id: 1,
    lightImage: lightOffImage,
    lightOn: false,
  },
  {
    id: 2,
    lightOn: false,
    lightImage: lightOffImage,
  },
  {
    id: 3,
    lightOn: false,
    lightImage: lightOffImage,
  },
]);

const lightSwitch = (id, lightOffImage, lightOnImage) => {
  const lightToUpdate = lights.find((light) => light.id === id);
  if (lightToUpdate) {
    lightToUpdate.lightOn = !lightToUpdate.lightOn;
    lightToUpdate.lightImage = lightToUpdate.lightOn
      ? lightOnImage
      : lightOffImage;
  }
};
</script>

<template>
  <section class="container mx-auto flex items-center flex-col">
    <h1 class="text-center text-2xl py-10">Light Switch Vue3</h1>
    <p class="p-5">Make These Buttons Work</p>
    <div class="flex justify-between space-x-6">
      <div class="p-10 border w-96 flex flex-col space-y-5">
        <button
          v-for="light in lights"
          :key="light.id"
          @click="lightSwitch(light.id, lightOffImage, lightOnImage)"
          class="text-white font-bold py-2 px-4 rounded"
          :class="
            light.lightOn
              ? 'bg-blue-500 hover:bg-blue-700'
              : 'bg-gray-500 hover:bg-gray-700'
          "
        >
          Light {{ light.id }} On
        </button>
      </div>
      <div
        :class="`${getBackgroundColorClass()} p-10 border w-96 flex flex-col space-y-5 `"
      >
        <img
          v-for="light in lights"
          :key="light.id"
          class="w-20"
          :src="light.lightImage"
          alt="light image"
        />
      </div>
    </div>
  </section>
</template>

<style scoped></style>
