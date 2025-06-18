<script setup>
import { ref, onMounted } from "vue";
import gsap from "gsap";


const text = ref("Hii, I am JOHN");
const textContainer = ref(null);

onMounted(() => {
  const letters = textContainer.value.querySelectorAll(".letter");

  gsap.fromTo(
    letters,
    { opacity: 0, y: 20 },
    {
      opacity: 1,
      y: 0,
      stagger: 0.05, // Jeda antar huruf iya kali, lupa guaa
      duration: 2.0,
      ease: "power3.out",
    }
  );
});

const images = [
  "/images/elon.jpg",
  "/images/mesi.png",
  "/images/obama.jpg",
  // "/images/image4.jpg",
];



const currentIndex = ref(0);
let timeout = null;

const changeImage = () => {
  if (timeout) return; 
  
  timeout = setTimeout(() => {
    currentIndex.value = (currentIndex.value + 1) % images.length;
    timeout = null;
  }, 100); 
};

onMounted(() => {
  window.addEventListener("mousemove", changeImage);
});

onUnmounted(() => {
  window.removeEventListener("mousemove", changeImage);
  clearTimeout(timeout);
});


// Daftar font
const fonts = [
  "font-display",
  "font-second",
  "font-third",
  "font-fourth",
  "font-fifth"
];

// Buat dua state untuk font yang berbeda
const currentFontFrontEnd = ref(fonts[0]);
const currentFontGameDev = ref(fonts[0]);

// Fungsi untuk mendapatkan font secara acak
const getRandomFont = (currentFont) => {
  let randomIndex;
  do {
    randomIndex = Math.floor(Math.random() * fonts.length);
  } while (fonts[randomIndex] === currentFont.value); // Pastikan font baru berbeda dari yang sebelumnya
  return fonts[randomIndex];
};

// GSAP untuk mengganti font Front End
onMounted(() => {
  gsap.to({}, {
    duration: 1,
    repeat: -1,
    onRepeat: () => {
      currentFontFrontEnd.value = getRandomFont(currentFontFrontEnd);
    }
  });
});

// GSAP untuk mengganti font Game Dev
onMounted(() => {
  gsap.to({}, {
    duration: 0.3,
    repeat: -1,
    onRepeat: () => {
      currentFontGameDev.value = getRandomFont(currentFontGameDev);
    }
  });
});
</script>



<template>
  <main class="w-full flex flex-col gap-40 justify-center h-screen">
    <div ref="textContainer" class="text-7xl  text-center break-words whitespace-normal ">
       <span v-for="(letter, index) in text.split('')" :key="index" class="letter text-wrap font-display">
     {{ letter === ' ' ? '\u00A0' : letter }}
   </span>
   <div>
    <h2>
      <span class="transition-all duration-500 ease-in-out" :class="currentFontFrontEnd">Front end</span> And <span class="transition-all duration-500 ease-in-out" :class="currentFontGameDev">Game Dev </span>
   </h2>
  </div>

  </div>
  <div class="flex justify-center items-center">
   <img
    :src="images[currentIndex]"
     alt="Dynamic Image"
     class=" w-32 transition-opacity duration-300"
   />
 </div>
 

  </main>

  <div class="h-screen">

  </div>
  
</template>

<style scoped>
.letter {
  display: inline-block;
}

.text-container {
  overflow: hidden;
  white-space: pre;
}

</style>