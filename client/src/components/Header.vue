<template>
    <div>
        <div class="big_container flex justify-center items-center content-center">
            <div class="container flex flex-row justify-around p-6 w-90
            items-center">
                <div class=" logo-container">
                    <span class="text-primary bold fs-4">B</span>
                    <span class="text-secondary semi-bold fs-4">Car</span>
                </div>
                <div class="link_container flex flex-row justify-between items-center text-primary">
                    <li class="fs-3 mx-15 semi-bold" v-for="route,i in routes" :key="i">
                        <a :href="route.to" class="text-none text-dark" >{{route.name}}</a>
                    </li>
                </div>
                <div class="add_to_cart_container">
                    <img class="add_to_cart w-50"
                        src="../assets/add-to-cart.png" 
                        title="Add to cart" 
                        alt="Add to cart image" 
                    >
                </div>
                <div class="text-primary menu pointer hide" @click="showMenu">
                    <BarIcon :color="color"/>
                </div>
            </div>
        </div>

      
            <div id = "mobile_menu_container" class="mobile_menu_container flex justify-center content-center">
                <Transition name="bounce">
                    <div v-if="show" class="mobile_menu bg-white modal shadow radius-8 flex flex-row p-6 w-90 justify-center text-left">
                        <li class="flex flex-col justify-center content-center fs-3 mx-10 " v-for="route,i in routes" :key="i">
                            <a :href="route.to" class="text-none text-dark" >{{route.name}}</a>
                        </li>
                    </div>
                </Transition>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import  AddToCart  from './icons/AddToCart.vue';
import BarIcon from './icons/BarIcon.vue';
import HomeIcon from './icons/HomeIcon.vue';

export default defineComponent({
    setup() {
        let routes = ref([
            {
                name: "Acceuil",
                to: "#",
                icon: "BarIcon"
            },
            {
                name: "Contactez Nous",
                to: "#",
                icon: "BarIcon"
            },
            {
                name: "Blog",
                to: "#",
                icon: "BarIcon"
            }
        ]);
        let color = ref('#000');
        let show = ref(false)

        let showMenu = () =>  {
            if (show.value == false) {
                color.value = '#fff';
                document.querySelector('body')!.style.backgroundColor = 'rgba(0,0,0,.7)';
            } else {
                document.querySelector('body')!.style.backgroundColor = '#fff';
                color.value = '#000';
            }
             show.value = !show.value;

        }

        return {
            routes,
            showMenu,
            show,
            color
        };
    },
    components: { BarIcon, AddToCart }
})
</script>



<style scoped>
    .container {
        justify-content: space-between;
    }
    .add_to_cart {
        cursor: pointer;
    }
    .logo-container {
        cursor: pointer;
    }

    li {
        list-style: none;
        text-align: center;
        
    }
    a:hover {
        color: #4BD5E7;
        /* border-bottom: 1px solid #E75D4B; */
    }

    .bounce-enter-active {
        animation: bounce-in 0.5s;
    }
    .bounce-leave-active {
    animation: bounce-in 0.4s reverse;
    }
    @keyframes bounce-in {
        0% {
            top: -500px;
            opacity: 0;
        }
        100% {
            top: 50%;
            opacity: 1;
        }
    }

    /* Media Queries */

    @media (max-width: 650px) {
        .add_to_cart_container, .link_container {
            display: none;
        }
        .menu {
            display: inherit;
        }
        body {
            background-color: white;
        }

    }

    @media (min-width: 651px) {
        .mobile_menu {
            display: none;
        }
         body {
            background-color: white;
        }
    }
</style>