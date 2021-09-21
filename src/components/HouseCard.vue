<template>
    <div class="w-full bg-white sm:w-80 sm:rounded-lg sm:shadow-lg sm:m-2 lg:w-96">
        <!-- images and favorite -->
        <div class="h-48 bg-gray-100 sm:rounded-t-lg relative">
            <!-- favorite icon from: https://heroicons.dev/ -->
            <div v-if="!favorite" class="absolute top-0 right-0 z-10 p-1 cursor-pointer  transform hover:scale-110" v-on:click="emitToggleFavorite()">
                <svg class="w-6 h-6" fill="none" stroke="white" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"></path>
                </svg>
            </div>
            <div v-if="favorite" class="absolute top-0 right-0 z-10 p-1 cursor-pointer  transform hover:scale-110" v-on:click="emitToggleFavorite()">
                <svg class="w-6 h-6" fill="red" stroke="red" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"></path>
                </svg>
            </div>
            <!-- Carousel -->
            <Carousel class="h-48 bg-gray-100 sm:rounded-t-lg">
                <Slide class="h-48 bg-gray-100 sm:rounded-t-lg bg-center bg-cover" v-for="slide in data.photos" :key="slide" :style="'background-image: url(' + slide + ')'">
                    <!-- <img class="carousel__item" v-bind:src="slide"> -->
                    <Pagination class="absolute bottom-0" />
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
    emits: ['toggledFavorite'],
    props: {
        data: Object,
        favorite: Boolean,
        realtor: Object
    },
    setup(props, context) {
        const emitToggleFavorite = () => {
            context.emit("toggledFavorite", { "id": props.data.id })
        }
        return { emitToggleFavorite }
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
    color: var(--carousel-color-white);
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
.carousel__pagination-button--active {
    @apply rounded-full;
}

.carousel__prev,
.carousel__next {
    /*box-sizing: content-box;*/
}
</style>