<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-back-button></ion-back-button>
        </ion-buttons>
        <ion-title class="bg-warning"> Loop </ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <swiper :slides-per-view="1" :space-between="50" @swiper="onSwiper">
        <swiper-slide v-for="(banner, i) in banners" :key="i">
          <img class="banner" :src="banner" />
        </swiper-slide>
      </swiper>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { menu, home, person } from 'ionicons/icons';
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';

import {
  IonBackButton,
  IonButtons,
  IonToolbar,
  IonTitle,
  IonHeader,
  IonPage,
  IonContent,
  IonIcon,
  IonRouterOutlet,
} from '@ionic/vue';

export default defineComponent({
  name: 'swiperloopScreen',
  components: {
    IonBackButton,
    IonButtons,
    IonToolbar,
    IonTitle,
    IonHeader,
    IonPage,
    IonContent,
    IonIcon,
    IonRouterOutlet,
    Swiper,
    SwiperSlide,
  },
  data() {
    return {
      swiper: {} as any,
      banners: [
        'https://www.creatopy.com/blog/wp-content/uploads/2024/04/1.Adobe-examples.png',
        'https://cdn.prod.website-files.com/5b5729421aca332c60585f78/63f5fa224df9195bd8c86b7a_6181ae8222cefae4ebee33fe_flash-sale-banner-example.png',
        'https://www.creatopy.com/blog/wp-content/uploads/2024/04/5.Apple-Music-examples.png',
        'https://i.pinimg.com/600x315/59/57/92/5957925d0bce4ff9019ccf2bd88833f2.jpg',
        'https://mir-s3-cdn-cf.behance.net/projects/808/1504e3171878803.Y3JvcCwzMjMyLDI1MjgsMCww.jpg',
        'https://img.freepik.com/premium-vector/black-friday-social-media-web-banner-template_542922-202.jpg',
      ],
    };
  },
  methods: {
    async onSwiper(event: any) {
      this.swiper = event;
    },
  },
  setup() {
    return {
      menu,
      home,
      person,
    };
  },
});
</script>

<style scoped>
.banner {
  width: 100vw;
  height: 260px;
  object-fit: cover;
  object-position: center;
}
</style>
