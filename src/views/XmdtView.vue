<template>
    <div class="flex  w-full h-full bg-gray-200 ">
        <div class="bg-gray-200 w-[400px] min-h-full px-2 py-2 flex flex-col items-center">
          <label v-show="counter.loading_get_mail" class="relative h-[60px] bg-gray-400 py-3 rounded-xl mb-2 w-full flex justify-center items-center text-[20px] font-semibold text-green-500">
            <p v-show="counter.mail_get_new" id="get_mail_new" class="text-slate-600">{{ counter.mail_get_new }}</p>
            <div v-show="!counter.mail_get_new" class="loader"></div>
          </label>
          <button v-on:click="counter.F_Export_mail_new();" class=" flex items-center justify-center  gap-2  px-2 py-2 bg-green-600 hover:bg-green-700 font-bold text-gray-100 rounded-2xl">
            <p class="">Get new Mail</p>
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" width="16">
                <path fill="white" d="M502.6 278.6c12.5-12.5 12.5-32.8 0-45.3l-128-128c-12.5-12.5-32.8-12.5-45.3 0s-12.5 32.8 0 45.3L402.7 224 32 224c-17.7 0-32 14.3-32 32s14.3 32 32 32l370.7 0-73.4 73.4c-12.5 12.5-12.5 32.8 0 45.3s32.8 12.5 45.3 0l128-128z"/>
            </svg>
          </button>
          <div v-show="counter.mail_get_available" class="flex flex-col gap-1 mt-2 justify-center items-center">
            <p class="text-[16px] font-bold">Mail is available:</p>
            <div class="flex flex-col">
                <div class="flex gap-1 text-[14px]">
                    <p>{{ counter.mail_get_available }}</p>
                    <button v-on:click="counter.F_Export_inbox_available()" class=" flex items-center justify-between  gap-2    font-bold text-gray-100 rounded-2xl">
                        <p class="text-[#22c55e]">Get Inbox</p>
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" width="16">
                            <path fill="#22c55e" d="M502.6 278.6c12.5-12.5 12.5-32.8 0-45.3l-128-128c-12.5-12.5-32.8-12.5-45.3 0s-12.5 32.8 0 45.3L402.7 224 32 224c-17.7 0-32 14.3-32 32s14.3 32 32 32l370.7 0-73.4 73.4c-12.5 12.5-12.5 32.8 0 45.3s32.8 12.5 45.3 0l128-128z"/>
                        </svg>
                    </button>
                </div>
            </div>
          </div>
          <div class="flex justify-between items-center bg-gray-300 px-2 py-1 rounded-full mt-2 w-full">
                <input  id="input_name"  v-model="counter.mail_get_search" @keyup.enter="counter.F_Export_inbox_mail_search();" type="text" placeholder="Enter email to get inbox" class=" text-[15px] border-none outline-none bg-transparent bg-none"/>
                <div v-on:click="counter.F_Export_inbox_mail_search();"  class="px-1 py-1 bg-gray-700 rounded-full cursor-pointer w-[24px] h-[24px]" title="Thêm">
                  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" width="14">
                    <path fill="white" d="M438.6 278.6c12.5-12.5 12.5-32.8 0-45.3l-160-160c-12.5-12.5-32.8-12.5-45.3 0s-12.5 32.8 0 45.3L338.8 224 32 224c-17.7 0-32 14.3-32 32s14.3 32 32 32l306.7 0L233.4 393.4c-12.5 12.5-12.5 32.8 0 45.3s32.8 12.5 45.3 0l160-160z"/>
                  </svg>
                </div>
            </div>
        </div>
        <div class="flex flex-col bg-gray-200 w-full min-h-full border-l-[1px] border-gray-300 px-2 py-2">
            <div v-show="counter.mail_inbox" class="flex gap-2 items-center w-full bg-gray-700 px-2 py-2 text-gray-100">
                <p>Inbox content :</p>
                <p id="get_inbox_mail" class="text-lime-500">{{ counter.mail_inbox }}</p>
                <div class="loader1"></div>
                <!-- <select v-model="selected" class="bg-gray-400 text-gray-800 rounded-md outline-none border-none px-1 py-1">
                    <option disabled value="">Type Inbox</option>
                    <option>Latest</option>
                    <option>All</option>
                </select> -->
                <!-- <input type="radio" id="one" value="Latest" v-model="picked" class="cursor-pointer" />
                <label for="one" class="cursor-pointer">Latest</label>

                <input type="radio" id="two" value="All" v-model="picked"  class="cursor-pointer"/>
                <label for="two" class="cursor-pointer">All</label> -->
            </div>
            <table v-show="counter.data_export_inbox && counter.data_export_inbox.length > 0" class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
                <thead class="text-xs text-gray-700 uppercase bg-gray-400 dark:bg-gray-700 dark:text-gray-400">
                    <tr>
                        <th scope="col" class="px-4 py-3">
                            Sender
                        </th>
                        <th scope="col" class="px-4 py-3">
                            Title
                        </th>
                        <th scope="col" class="px-4 py-3">
                            Content
                        </th>
                        <th scope="col" class="px-4 py-3">
                            Time
                        </th>
                        <th scope="col" class="px-4 py-3">
                            Code
                        </th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(i,index) in counter.data_export_inbox" class="odd:bg-white odd:dark:bg-gray-900 even:bg-gray-50 even:dark:bg-gray-800 border-b dark:border-gray-700">
                        <th scope="row" class="px-4 py-3 font-semibold text-gray-900 whitespace-nowrap dark:text-white">
                            {{ i.Sender }}
                        </th>
                        <td class="px-4 py-4 text-gray-900">
                            {{ i.Title }}
                        </td>
                        <td  class="cursor-pointer  px-4 py-4 text-gray-900">
                            {{ i.Content }}
                        </td>
                        <td class="cursor-pointer  px-4 py-4 text-gray-900">
                            {{ i.Time }}
                        </td>
                        <td class=" flex flex-col gap-2 justify-center items-center px-4 py-6">
                            <div v-for="(j,index) in i.Code" class="flex items-center justify-between w-full">
                                <p class="text-gray-900">{{ j }}</p>
                                <div class="flex relative  justify-center items-center">
                                    <svg @click="copyText(j,j)" class=" cursor-pointer " xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" width="16">
                                        <path fill="balck"  d="M384 336H192c-8.8 0-16-7.2-16-16V64c0-8.8 7.2-16 16-16l140.1 0L400 115.9V320c0 8.8-7.2 16-16 16zM192 384H384c35.3 0 64-28.7 64-64V115.9c0-12.7-5.1-24.9-14.1-33.9L366.1 14.1c-9-9-21.2-14.1-33.9-14.1H192c-35.3 0-64 28.7-64 64V320c0 35.3 28.7 64 64 64zM64 128c-35.3 0-64 28.7-64 64V448c0 35.3 28.7 64 64 64H256c35.3 0 64-28.7 64-64V416H272v32c0 8.8-7.2 16-16 16H64c-8.8 0-16-7.2-16-16V192c0-8.8 7.2-16 16-16H96V128H64z"/>
                                    </svg>
                                    <p v-show="this.showCopied == j" class=" bottom-5 absolute text-gray-200 bg-gray-600 px-1 py-1 rounded-md">Copied</p>
                                </div>
                            </div>
                        </td>
                    </tr>
                </tbody>
            </table>
            <div v-show="counter.data_export_inbox && counter.data_export_inbox.length == 0" class="flex justify-center items-center w-full h-full bg-gray-300">
                <p class="font-semibold text-[18px] " >Empty Inbox</p>
            </div>
        </div>
    </div>
</template>  
  <script>
  import { useCounterStore } from "@/stores/counter";
  import axios from "axios";
  import VueCookies from "vue-cookies";
  
  export default {
    data() {
      return {
        showCopied: ''
      };
    },
    setup() {
      const counter = useCounterStore();
      return { counter };
    },
    mounted: function () {
      this.counter.F_Export_mail_available();
    },
    computed: {},
    methods: {
        copyText(text,xx) {
        // Tạo một thẻ textarea ẩn để sao chép văn bản
        const textarea = document.createElement('textarea');
        textarea.value = text;
        document.body.appendChild(textarea);
        textarea.select();
        document.execCommand('copy');
        document.body.removeChild(textarea);
        
        // Hiển thị thông báo "Copied" trong 1 giây
        this.showCopied = xx;
        setTimeout(() => {
            this.showCopied = '';
        }, 500);
    }
    },
    components: {},
  };
  </script>
  
  <style>
  #cjss::-webkit-scrollbar {
    width: 5px;
    height: 8px; /* Chiều rộng vùng chứa scrollbar */
  }
  #cjss::-webkit-scrollbar-track {
    background: #1f2937; /* Màu nền ngoài của thanh scrollbar */
  }
  #cjss::-webkit-scrollbar-thumb {
    background-color: #7dd3fc; /* Màu của thanh cuộn (scroll thumb) */
    border-radius: 1px; /* Bo góc scroll thumb */
    /* border: 2px solid #ccc;  Không hỗ trợ padding, margin, transition nên dùng viền cùng màu nên để padding scroll thumb */
  }
  #cjss::-webkit-scrollbar-thumb:hover {
    background-color: #e0f2fe; /* Hiệu ứng di chuột đổi màu*/
  }
  
  #cjss1::-webkit-scrollbar {
    width: 5px;
    height: 8px; /* Chiều rộng vùng chứa scrollbar */
  }
  #cjss1::-webkit-scrollbar-track {
    background: #393636; /* Màu nền ngoài của thanh scrollbar */
  }
  #cjss1::-webkit-scrollbar-thumb {
    background-color: #595857; /* Màu của thanh cuộn (scroll thumb) */
    border-radius: 1px; /* Bo góc scroll thumb */
    /* border: 2px solid #ccc;  Không hỗ trợ padding, margin, transition nên dùng viền cùng màu nên để padding scroll thumb */
  }
  #cjss1::-webkit-scrollbar-thumb:hover {
    background-color: #655f58; /* Hiệu ứng di chuột đổi màu*/
  }
  
  #video {
    transform: rotateY(180deg);
    -webkit-transform: rotateY(180deg); /* Safari and Chrome */
    -moz-transform: rotateY(180deg); /* Firefox */
  }

  .loader {
  display: block;
  --height-of-loader: 4px;
  --loader-color: #111827;
  width: 130px;
  height: var(--height-of-loader);
  border-radius: 30px;
  background-color: rgba(0,0,0,0.2);
  position: relative;
}

.loader::before {
  content: "";
  position: absolute;
  background: var(--loader-color);
  top: 0;
  left: 0;
  width: 0%;
  height: 100%;
  border-radius: 30px;
  animation: moving 1s ease-in-out infinite;
  ;
}

@keyframes moving {
  50% {
    width: 100%;
  }

  100% {
    width: 0;
    right: 0;
    left: unset;
  }
}

.loader1 {
  display: block;
  --height-of-loader: 4px;
  --loader-color: #84cc16;
  width: 130px;
  height: var(--height-of-loader);
  border-radius: 30px;
  background-color: #6b7280;
  position: relative;
}

.loader1::before {
  content: "";
  position: absolute;
  background: var(--loader-color);
  top: 0;
  left: 0;
  width: 0%;
  height: 100%;
  border-radius: 30px;
  animation: moving 1s ease-in-out infinite;
  ;
}

  </style>
  