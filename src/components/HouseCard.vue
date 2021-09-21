<template>
    <div class="w-full bg-white sm:w-80 sm:rounded-lg sm:shadow-lg sm:m-2 lg:w-96">
        <!-- images and favorite -->
        <div class="h-48 bg-gray-100 sm:rounded-t-lg">
            <!-- favorite icon -->
<!--             <div class="m-2 right-0 top-0">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
                    <path d="M12 9.229c.234-1.12 1.547-6.229 5.382-6.229 2.22 0 4.618 1.551 4.618 5.003 0 3.907-3.627 8.47-10 12.629-6.373-4.159-10-8.722-10-12.629 0-3.484 2.369-5.005 4.577-5.005 3.923 0 5.145 5.126 5.423 6.231zm-12-1.226c0 4.068 3.06 9.481 12 14.997 8.94-5.516 12-10.929 12-14.997 0-7.962-9.648-9.028-12-3.737-2.338-5.262-12-4.27-12 3.737z"></path>
                </svg>
            </div> -->
            <!-- Carousel -->
            <Carousel class="h-48 bg-gray-100 sm:rounded-t-lg">
                <Slide class="h-48 bg-gray-100 sm:rounded-t-lg bg-center bg-cover" v-for="slide in data.photos" :key="slide" :style="'background-image: url(' + slide + ')'">
                        <!-- <img class="carousel__item" v-bind:src="slide"> -->
                <Pagination class="absolute bottom-0"/>
                </Slide>
                <template #addons>
                    <Navigation />
                </template>
            </Carousel>
        </div>
        <!-- Info for house -->
        <div class="p-4 border-b border-gray-200">
            <div class="card-text uppercase font-semibold">
                {{data.type}} - {{data.age}}y old
            </div>
            <div class="text-xl">
                ${{data.price}}
            </div>
            <div class="card-text">
                {{data.address}}
            </div>
        </div>
        <div class="p-4 border-b border-gray-200">
            <div class="card-text">
                {{data.bedroom}} Bedrooms
                {{data.bathroom}} Bathrooms
            </div>
        </div>
        <!-- Realtor info -->
        <div class="p-4 border-b border-gray-200 ">
            <div class="card-text text-xs uppercase font-semibold">
                Realtor
            </div>
            <div class="grid grid-cols-6 mt-2">
                <!-- Realtor Image -->
                <div class="rounded-full h-12 w-12 bg-gray-100 bg-center bg-cover" :style="'background-image: url(' + realtor.image + ')'">
                </div>
                <!-- Realtor contact info -->
                <div class="col-span-5">
                    <div class="card-text font-bold">
                        {{realtor.name}}
                    </div>
                    <div class="card-text">
                        {{realtor.number}}
                    </div>
                </div>
            </div>
        </div>
        <!-- Bed/Bath -->
        <div></div>
        <!-- Realtor info -->
        <div></div>
    </div>
</template>
<script>
import 'vue3-carousel/dist/carousel.css';
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel';
export default {
    name: 'HouseCard',
    components: {
        Carousel,
        Slide,
        Pagination,
        Navigation,
    },
    props: {
        data: Object,
        realtor: Object
    }
};
</script>
<style>
.card-text {
    @apply text-gray-600 text-sm;
}
.carousel__item {
  min-height: 200px;
  width: 100%;
  background-color: var(--carousel-color-primary);
  color:  var(--carousel-color-white);
  font-size: 20px;
  border-radius: 8px;
  display: flex;
  justify-content: center;
  align-items: center;
  @apply rounded-lg;
}

.carousel__slide {
  padding: 10px;
}
.carousel__pagination-button--active {
  background-color: white;
}
.carousel__pagination-button,
.carousel__pagination-button--active{
  @apply rounded-full;
}
.carousel__prev,
.carousel__next {
  /*box-sizing: content-box;*/
}
</style>