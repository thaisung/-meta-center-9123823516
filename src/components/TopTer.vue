<template>
    <div class="flex flex-col max-w-[1200px] w-full  items-center  bg-sky-400">
        <div  class="flex  w-full h-full   bg-gray-900 justify-between items-center border-green-500 border-b-[4px]">
            <div class="flex px-2 py-2 h-full items-center text-[25px] font-bold bg-green-500">
                <router-link to='/' class="router_link1"><img src="@/assets/logo_thai.png" class="rotate-and-shake h-[60px]"/></router-link>
            </div>
            <div class="flex items-center justify-center font-bold">
                <router-link to='/' class="router_link flex justify-center items-center px-3 text-white  min-h-full h-[76px]"><span class="content">Temp Mail</span></router-link>
                <router-link to='/xmdt' class="router_link flex justify-center items-center px-3 text-white  min-h-full h-[76px]"><span class="content">XMDT</span></router-link>
                <router-link to='/api-document' class="router_link flex justify-center items-center px-3 text-white   min-h-full h-[76px]"><span class="content">API Document</span></router-link>
            </div>
            <div class="text-white font-bold px-2">
                <button class="px-2 py-1 bg-green-500 rounded-full text-black text-[14px] font-bold">Đăng nhập</button>
            </div>
        </div>
    </div>
</template>


<script >

    import { useCounterStore } from '@/stores/counter';
    import axios from 'axios';
    import VueCookies from 'vue-cookies'


    export default {

    setup() {
        const counter = useCounterStore();
        return {counter}
    },
    }
</script>

<style>
.router_link {
    display: inline-block;
    position: relative;
    overflow: hidden;
}

.router_link .content {
    position: relative;
}

.router_link::before {
    content: '';
    position: absolute;
    top: 100%;
    left: 0;
    width: 100%;
    height: 100%;
    opacity: 0;
    background-color: rgb(34 197 94); /* Set opacity ban đầu thành 0 */
    transition: top 0.9s ease, opacity 0.9s ease; /* Thêm transition cho opacity */
    /* z-index: -1; */
}

.router_link:hover::before {
    opacity: 1;
    top: 0;
}

.router_link:hover .content {
    color: #000; /* Thay đổi màu chữ khi hover */
}



.router_link1 {
    display: inline-block;
    position: relative;
}

.rotate-and-shake {
    transition: transform 0.5s ease;
}

.rotate-and-shake:hover {
    animation: rotateAndShake 1s forwards, shake 0.5s 1s infinite alternate;
}

@keyframes rotateAndShake {
    0% {
        transform: rotateY(0deg);
    }
    50% {
        transform: rotateY(360deg);
    }
    100% {
        transform: rotateY(0deg);
    }
}

@keyframes shake {
    0% {
        transform: translateX(0);
    }
    25% {
        transform: translateX(-5px);
    }
    50% {
        transform: translateX(5px);
    }
    75% {
        transform: translateX(-5px);
    }
    100% {
        transform: translateX(0);
    }
}


</style>




