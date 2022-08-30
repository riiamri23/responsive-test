<script setup>
import backgroundPath from "./assets/imgs/background2.webp";
</script>

<template>
  <div
    class="grid place-items-center w-screen min-h-screen"
    :style="{
      backgroundImage: `url(${backgroundPath})`,
      backgroundRepeat: 'no-repeat',
      backgroundSize: 'cover',
    }"
  >
    <div class="mx-auto grid place-items-center">
      <h1 class="text-[#ffffff] text-3xl mb-2">Responsive Check</h1>
      <div class="flex">
        <button class="self-start" @click="onResponsiveChange(1)">
          <DesktopSvg class="w-8 fill-white" />

          <div
            class="mt-1 mx-auto w-1/2 bg-[#ffffff] h-1 rounded-sm"
            :class="{ hidden: button.active != 1 }"
          ></div>
        </button>
        <button class="self-start" @click="onResponsiveChange(2)">
          <TabletSvg class="w-8 fill-white" />

          <div
            class="mt-1 mx-auto w-1/2 bg-[#ffffff] h-1 rounded-sm"
            :class="{ hidden: button.active != 2 }"
          ></div>
        </button>
        <button class="self-start" @click="onResponsiveChange(3)">
          <SmartphoneSvg class="w-8 fill-white" />

          <div
            class="mt-1 mx-auto w-1/2 bg-[#ffffff] h-1 rounded-sm"
            :class="{ hidden: button.active != 3 }"
          ></div>
        </button>
        <button class="selft-start">
          <MoreSvg class="w-8 fill-white" />
        </button>
      </div>
      <div
        class="flex m-4 transition-all duration-1000 hover:w-full"
        id="iframe-container"
      >
        <div class="w-2 h-10 bg-[#b3b3b3] rounded-xl my-auto m-4"></div>
        <iframe
          class=""
          width="100%"
          height="100%"
          src="https://play.tailwindcss.com/suMPwQ7jBY?layout=preview"
          frameborder="0"
          webkitallowfullscreen
          mozallowfullscreen
          allowfullscreen
        ></iframe>
        <div class="w-2 h-10 bg-[#b3b3b3] rounded-xl my-auto m-4"></div>
      </div>
    </div>
  </div>
</template>

<style>
#iframe-container {
  width: 1920px;
  height: 1080px;
}
</style>

<script>
import DesktopSvg from "./svgs/desktopsvg.vue";
import TabletSvg from "./svgs/tabletsvg.vue";
import SmartphoneSvg from "./svgs/smartphonesvg.vue";
import MoreSvg from "./svgs/moresvg.vue";

export default {
  components: { DesktopSvg, TabletSvg, SmartphoneSvg, MoreSvg },
  data() {
    return {
      iFrame: {
        width: 1920,
        height: 1080,
      },
      button: {
        active: 1,
      },
      increment: 1,
    };
  },
  methods: {
    onResponsiveChange(selectedSize) {
      /*
       * list responsive page
       * desktop 1024×768 through 1920×1080.
       * tablet 601×962 through 1280×800.
       * mobile 360×640 through 414×896.
       */

      if (selectedSize == 1) {
        //desktop
        this.iFrame.width = 1920;
        this.iFrame.height = 1080;
        this.button.active = 1;
      } else if (selectedSize == 2) {
        //tablet
        this.iFrame.width = 1280;
        this.iFrame.height = 800;
        this.button.active = 2;
      } else if (selectedSize == 3) {
        //mobile
        this.iFrame.width = 414;
        this.iFrame.height = 896;
        this.button.active = 3;
      }

      //animation
      document.getElementById(
        "iframe-container"
      ).style.width = `${this.iFrame.width}px`;
      document.getElementById(
        "iframe-container"
      ).style.height = `${this.iFrame.height}px`;
    },
  },
  mounted() {
    window.setInterval(() => {
      if(this.button.active == 1){
        this.increment = 1;
      }

      if(this.button.active == 3){
        this.increment = -1;
      }

      this.button.active = this.button.active + this.increment;
      console.log(this.button.active);
      this.onResponsiveChange(this.button.active);
    }, 2500);
  },

  beforeDestroy() {},
};
</script>
