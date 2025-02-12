<template>
  <nav class="w-full h-20 p-4 flex flex-col items-center justify-center">
    <div class="max-w-7xl mx-auto flex w-full items-center justify-between ">
      <div class="text-black  text-2xl font-bold">OBAMA</div>
      <ul class="flex gap-10">
        <li
          v-for="(item, index) in menuItems"
          :key="index"
          class="relative cursor-pointer flex items-center text-black text-lg font-semibold w-fit"
          @mouseenter="onEnter(index)"
          @mouseleave="onLeave(index)"
        >
          <span ref="mainText" class="block relative">{{ item.label }}</span>
          <span ref="hoverText" class="absolute top-full left-0 w-full">{{ item.hoverText }}</span>
        </li>
      </ul>
    </div>
    <div class="border border-black w-5/6 ">

    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted } from "vue";
import gsap from "gsap";

const menuItems = ref([
  { label: "Home", hoverText: "Here" },
  { label: "About", hoverText: "who Iam" },
  { label: "Services", hoverText: "What We Do" },
  { label: "Project", hoverText: "Look" },
  { label: "Contact", hoverText: "Get in Touch" },
]);

const mainText = ref([]);
const hoverText = ref([]);

const onEnter = (index) => {
  gsap.to(mainText.value[index], { y: "-100%", duration: 0.5, ease: "power2.out", opacity: 0});
  gsap.to(hoverText.value[index], { y: "-100%", duration: 0.5, ease: "power2.out", opacity: 1 });
};

const onLeave = (index) => {
  gsap.to(mainText.value[index], { y: "0%", duration: 0.5, ease: "power2.out", opacity: 1 });
  gsap.to(hoverText.value[index], { y: "0%", duration: 0.5, ease: "power2.out", opacity: 0 });
};

onMounted(() => {
  menuItems.value.forEach((_, index) => {
    gsap.set(hoverText.value[index], { opacity: 0, y: "100%" });
  });
});

</script>

<style scoped>
li {
  height: 30px;
  /* overflow: hidden; */
}
</style>
