<script>
  import { store } from '@/data/store';
  import axios from 'axios';
  import Loader from '../Loader.vue';
  import { Swiper, SwiperSlide } from 'swiper/vue';
  import { EffectCoverflow, Pagination } from 'swiper/modules';

  export default {
    components:{
      Loader,
      Swiper,
      SwiperSlide,
    },
    data(){
      return{
        store,
        favServices : [],
        loading : true,
      }
    },
    setup() {
      return {
        modules: [EffectCoverflow, Pagination],
      };
    },

    methods:{
      getApi(){
        axios.get(store.apiUrl + 'services')
            .then(result =>{
              console.log(result.data);
              store.services = result.data 
              this.getFavServices();
            })
            .catch(errors =>{
              console.log(errors);
            })
      },
      getFavServices(){
        this.favServices = store.services.filter(service => {
          return service.name === 'Cene di Gala' || 
            service.name === 'Mostre d\'Arte' ||
            service.name === 'Spettacoli Teatrali' ||
            service.name === 'Rievocazioni Storiche' ||
            service.name === 'Concerti' ||
            service.name === 'Maneggio' || 
            service.name === 'Golf'  
        });
        console.log(this.favServices)
        return this.favServices
      },

      toggleService(service) {
        const index = store.searchServices.indexOf(service.id);
        store.serviceName = service.name;
        store.searchServices = [];

        if (index > -1) {
          store.searchServices.splice(index, 1);
        } else {
          store.searchServices.push(service.id);
        }
        console.log(store.searchServices);
      },
      
    },
    mounted(){
      this.getApi();
    }
  }
</script>
<template>
  <div class="my-5 pt-5">

    <h3 class="text-center my-3 fw-bold">Servizi esclusivi</h3>

    <div class="container-fluid my-3 p-5" v-if="loading">

      <swiper
      :effect="'coverflow'"
      :grabCursor="true"
      :centeredSlides="true"
      :slidesPerView="'auto'"
      :coverflowEffect="{
        rotate: 50,
        stretch: 0,
        depth: 100,
        modifier: 1,
        slideShadows: true,
      }"
      :pagination="true"
      :initialSlide="3"
      :modules="modules"
      class="mySwiper"
    >
      <swiper-slide v-for="service in favServices" :key="service.id" class="position-relative">

        <div class="text p-2">
          <router-link @click="store.inputAddress = '' , toggleService(service)" :to="{name: 'houses'}" class="text-light">
            <h5 class="title"><i :class="service.icon" class="me-2"></i>{{service.name}}</h5>
            <p class="description">{{ service.description }}</p>
          </router-link>
        </div>

        <img :src="`/img/${service.img}`" />
      </swiper-slide>
    </swiper>

    </div>
    <Loader v-else />
  </div>
</template>



<style lang="scss" scoped>
@use '../../../assets/scss/main.scss' as * ;

h3{
  color: $dark-color;
}

.swiper {
  width: 100%;
  padding-top: 50px;
  padding-bottom: 50px;
}

.swiper-slide {
  background-position: center;
  background-size: cover;
  width: 400px;
  height: 400px;
  box-shadow: 10px 10px 20px rgba(0, 0, 0, 0.7);
}

.swiper-slide img {
  display: block;
  width: 100%;
  object-fit: cover;
  aspect-ratio: 1;
}



.swiper-slide .text{
  position: absolute;
  width: 100%;
  bottom: 0px;
  left: 0px ;
  color: $light-color;
  background-color: rgba(5, 28, 44, 0.699);


}

@media screen and (max-width: 550px) {
  .swiper-slide {
    width: 300px;
    height: 300px;
  }
}
@media screen and (max-width: 420px) {
      .swiper-slide {
      width: 200px;
      height: 200px;
    }

    .swiper-slide .text{
      font-size: 0.7rem;
      h5{
        font-size: 0.8rem;
      }
    }
  }

</style>