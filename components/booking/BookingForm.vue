
import { important } from '#tailwind-config';

import { _none } from '#tailwind-config/theme/animation';

import { important } from '#tailwind-config';

<template>
   <section :id="block.id" :style="{ background: block.background }" :data-cms-bind="dataBinding" class="section-form border-b border-main">
     <div class="container">
      <div class="w-full h-full flex flex-col">
         <div class="flex flex-col gap-6 pt-10">
            <h2 class="text-black uppercase text-center">{{ block.title }}</h2>

            <ul class="w-full lg:flex-row flex flex-col justify-between items-between lg:rounded-full rounded-3xl bg-gray-300 overflow-hidden">
               <li
                  v-for="(menu, index) in block.menuTab"
                  :key="index"
                  :class="{ 'text-secondary bg-main rounded-full border-none': isActiveMenuItem(index) }"
                  @click="setActiveMenuItem(index)"
                  class="w-full border-r hover:opacity-80 text-center text-main whitespace-nowrap cursor-pointer p-4 font-[16px]"
               >
                  <button class="uppercase">{{ menu.tab }}</button>
               </li>
            </ul>
            <div v-for="(menu, index) in block.menuTab" :key="index" class="bg-[#F5F5F5] flex flex-col w-full" v-show="isActiveMenuItem(index)">
               <div v-if="index === 0" class="bg-[#F5F5F5] flex flex-col w-full">
                  <div v-for="(item, index) in block.listService" :key="index" class="flex flex-col hover:bg-gray-200">
                     <div class="flex justify-between items-center px-6 py-4 w-full border-b border-black">
                        <span class="w-full uppercase text-black">{{ item.title }}</span>
                        <div class="flex gap-2 justify-end items-center">
                           <div class="rounded-full w-4 h-4 border border-black p-2 flex flex-col justify-center items-center">
                              <span class="text-xs font-sans">{{ index + 1 }}</span>
                           </div>
                           <div
                              class="cursor-pointer transition-transform transform p-2"
                              :class="{ 'rotate-180': isActiveDown(index) }"
                              @click="toggleActiveDown(index)"
                           >
                              <img src="/images/down.png" alt="" class="object-cover w-6 h-6"/>
                           </div>
                        </div>
                     </div>
                     <div v-if="isActiveDown(index)" class="bg-[#EAEAEA] p-6 grid lg:grid-cols-2 grid-cols-1 gap-4">
                        <div v-for="(elm, key) in item.menuItem" :key="key" class="bg-white flex flex-col gap-4 p-4 rounded-3xl hover:shadow-md">
                           <div class="flex justify-between items-center">
                              <div class="flex flex-col gap-2">
                                 <h4 class="text-black">{{ elm.title }}</h4>
                                 <p class="font-sans text-xs">{{ elm.time }}</p>
                              </div>
                              <div class="flex gap-4 items-center justify-center">
                                 <p class="font-sans text-xs">From</p>
                                 <span class="text-black text-2xl">{{ elm.price }}</span>
                                 <div>
                                    <UCheckbox class="text-main" @change="handleCheckboxChange(index, key)"/>
                                 </div>
                              </div>
                           </div>
                           <div class="font-sans text-xs">{{ elm.description }}</div>
                        </div>
                     </div>
                  </div>
               </div>
               <div v-if="index === 1" class="bg-[#F5F5F5] flex flex-col w-full">
                  <div class="flex flex-col">
                     <div class="border-b border-black px-6 py-4">
                        <h4 class="uppercase text-black">{{ block.title_staff }}</h4>
                     </div>
                     <div class="grid lg:grid-cols-2 grid-cols-1 justify-between items-center gap-4 p-6 bg-[#EAEAEA]">
                        <div v-for="(item, index) in block.listStaff" :key="index" class="bg-white  hover:shadow-md rounded-3xl p-4 flex justify-between items-center">
                           <img :src="item.img"/>
                           <div class="flex flex-col gap-2 w-2/3">
                              <b>{{ item.name }}</b>
                              <p class="font-sans text-xs">{{ item.position }}</p>
                           </div>
                           <div>
                              <UCheckbox name="notifications" class="text-main"/>
                           </div>
                        </div>
                     </div>
                  </div>
               </div>
               <div v-if="index === 2" class="bg-[#F5F5F5] flex flex-col w-full">
                  <div class="flex flex-col">
                     <div class="border-b border-black px-6 py-4">
                        <h4 class="uppercase text-black">{{ block.title_time }}</h4>
                     </div>
                     <div class="p-6 bg-[#EAEAEA] flex flex-col gap-10">
                        <div class="grid grid-cols-2 justify-center items-center gap-4 custom_height">
                           <div class="p-4 w-full h-full flex flex-col">
                              <VueDatePicker v-model="date" :inline="{ input: false }" auto-apply id="custom_date" />
                           </div>
                           <div class="flex flex-col w-full custom_heightTime">
                              <div v-for="(time, index) in arrTime" :key="index" class="custom_time hover:text-main p-4 border-b border-[#B2B2B2] text-center">
                                 <span>{{ time.time }}</span>
                              </div>      
                           </div>
                        </div>
                        <div class="lg:flex-row flex flex-col lg:gap-10 gap-4 justify-center items-center pb-10">
                           <button class="transition hover:bg-white hover:text-main hover:transition-all bg-main text-white border border-main text-center lg:w-1/4 w-full py-4 rounded-full">{{ block.button_confirm }}</button>
                           <button class="transition hover:bg-main hover:text-white hover:transition-all bg-white text-main border border-main text-center lg:w-1/4 w-full py-4 rounded-full">{{ block.button_clear }}</button>
                        </div>
                     </div>
                  </div>
               </div> 
            </div>

            <div class="mt-20">
               <div class="bg-[#F7F5FF] border border-main rounded-t-3xl lg:p-20 p-10 flex flex-col gap-10">
                  <h4 class="uppercase text-black">{{ block.lable }}</h4>
                  <div class="flex flex-col gap-6 border-b border-black pb-10">
                     <div class="bg-white rounded-3xl p-4 flex justify-between items-center lg:w-1/2 w-full">
                           <img src="/images/staff.png"/>
                           <div class="flex flex-col gap-2 w-2/3">
                              <b>Emily Martinez</b>
                              <p class="font-sans text-xs">Entry stylist</p>
                           </div>
                           <div>
                              <UCheckbox :model-value="true" class="text-main"/>
                           </div>
                     </div>
                     <div class="flex flex-col gap-4 rounded-3xl ">
                        <div class="flex justify-between items-center">
                              <div class="flex flex-col gap-2">
                                 <h4 class="text-black">Deluxe 1-2 Row Maintenence</h4>
                                 <p class="font-sans text-xs">Approx 90 mins</p>
                              </div>
                              <div class="flex gap-4 items-center justify-center">
                                 <p class="font-sans text-xs">From</p>
                                 <span class="text-black text-2xl">$172</span>
                                 <div @click="removeItem()" class="cursor-pointer">
                                    <img src="/images/del.png" />
                                 </div>
                              </div>
                        </div>
                        <div class="font-sans text-xs">1 or 2 Rows moved up; Full Service Includes a relaxing shampoo, scalp treatment, extension restoration treatment, blow dry, and styled finish.</div>
                     </div>
                  </div>
                  <div class="border-dashed border border-black	 p-4 flex justify-center items-center gap-4">
                     <img src="/images/add.png" alt="" class="cursor-pointer w-10 h-10"/>
                     <span>{{ block.text_input }}</span>
                  </div>
                  <div class="flex flex-col justify-center items-center w-full">
                     <button @click="isOpen = true" class="transition hover:opacity-90 hover:transition-all bg-[#B2B2B2] text-white text-center lg:w-1/3 w-full p-4 rounded-full">{{ block.button }}</button>
                  </div>
               </div>
            </div>
            <div class="lg:hidden block">
               <UModal v-model="isOpen" id="custom-modal" prevent-close class="h-full">
                  <UCard :ui="{ ring: '', divide: 'divide-y divide-gray-100 dark:divide-gray-800 ' }">
                        <div class="flex items-center justify-end">
                           <UButton color="gray" variant="ghost" icon="i-heroicons-x-mark-20-solid" class="-my-1" @click="isOpen = false" />
                        </div>
                        <div class="flex flex-col gap-4 justify-center items-center pb-10">
                           <h2 class="text-main text-3xl text-center">Congratulations on your upcoming appointment!</h2>
                           <p class="text-center font-sans font-light"> We can't wait to pamper you and make your visit memorable</p>
                        </div>      
                  </UCard>
               </UModal>
            </div>
         </div>
      </div>
     </div> 
   </section>
 </template>
 
 <script setup lang="ts">
 import { defineProps, ref } from 'vue';
 import VueDatePicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css'

 interface Props {
   dataBinding: any;
   block: any;
 }
 
 const { dataBinding, block } = defineProps<Props>();
 const isOpen = ref(false);
 const activeMenuItem = ref(0); 
 const activeDownIndexes = ref<number[]>([]);
   const arrTime = [];

for (let i = 7; i <= 17; i++) {
  if (i === 12) continue;
  const hour = i % 12;
  const period = i < 12 ? 'AM' : 'PM';
  const time = `${hour.toString().padStart(2, '0')}:00 ${period}`;
  arrTime.push({ time });
}


 const isActiveDown = (index: number) => {
   return activeDownIndexes.value.includes(index);
 };
 
 const toggleActiveDown = (index: number) => {
   if (isActiveDown(index)) {
     activeDownIndexes.value = activeDownIndexes.value.filter((i) => i !== index);
   } else {
     activeDownIndexes.value.push(index);
   }
 };
 
 const isActiveMenuItem = (index: number) => {
   return index === activeMenuItem.value;
 };
 
 const setActiveMenuItem = (index: number) => {
   activeMenuItem.value = index;
 };
 </script> 

 <style lang="scss" scoped>
 .section-form {
   .custom_time:hover {
      background: linear-gradient(90deg, rgba(255, 255, 255, 0.00) -2.83%, #FFF 49.27%, rgba(255, 255, 255, 0.00) 97.49%);
   }
   .custom_height{
      height: calc(100% - 130px);
      overflow-y: hidden;
      .custom_heightTime {
         overflow: auto;
         height: calc(100% - 130px);
      }
   }
   #custom-modal{

    .sm\:max-w-lg {
       padding: 10px;
       border: 1px solid #6C5CE7;
    }
    .bg-gray-200\/75 {
    }
  }

  #custom_date {
    background-color: #EAEAEA !important;
    width: 100%;
    display: block;
    overflow: auto;
    height: calc(100% - 130px);

    .dp__instance_calendar {
        background-color: #EAEAEA !important;

        .dp__menu_inner {
            background-color: #EAEAEA !important;
        }

        .dp__today {
            background: #6C5CE7 !important;
            border: 1px solid #6C5CE7 !important;
        }
    }

    .dp__month_year_row {
        .dp__btn {
            display: none !important;
        }
    }
}
 }
 </style>
 