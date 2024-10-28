<template>
  <div>
    <NuxtRouteAnnouncer />


    <!-- 顯示資料，可以用檢查原始碼判斷是不是 SSR -->
    {{ res }}


    <!-- 使用 useFetch 需要在 onclick 的時候重新獲取資料 -->
    <button @click="refreshData">refresh</button>


    <!-- <NuxtWelcome /> -->
  </div>
</template>


<script setup>
// 先不使用 typescript => 專注於非同步工具的差異
// 比較使用 axios, $fetch, useFetch, asyncData 的差異
import axios from 'axios'


// 會觸發兩次 API，一次在伺服器端，一次在瀏覽器端
// const res = ref(null)
// const response = await axios.get('https://nuxr3.zeabur.app/api/v1/rooms/');
// res.value = response.data; // 只取 response.data

// 放在 onMounted 就會在瀏覽器端使用，不會在伺服器端使用
// const res =ref(null)
//     onMounted(async() => {
//       res.value = await axios.get('https://nuxr3.zeabur.app/api/v1/rooms/')
//     })

  // 因為有 nuxt3 的約定， 所以 $fetch 跟 useFetch 跟 asyncData 都不用 import，會自動注入
  // 使用 $fetch => 會直接打兩次 API (一次在伺服器，一次在瀏覽器)
  // 改使用 useFetch 就只會打一次 API，在伺服器端
  // useFetch 不能放在 fuction 裡面，不然會報錯
  // $fetch 使用在 fuction 裡面，不會報錯，例如 onclick 的時候
  // 想使用 axios 在伺服器端可以使用 useAsyncData ，就會有 SSR 的效果
  // useAsync + $fetch = useFetch (官方有說)

  // 使用 $fetch => 會直接打兩次 API (一次在伺服器，一次在瀏覽器)
  // const res = ref(null)
  // res.value = await $fetch('https://nuxr3.zeabur.app/api/v1/rooms/')


  // 使用 useFetch 就只會打一次 API，在伺服器端
  // const res = ref(null)
  // res.value = await useFetch('https://nuxr3.zeabur.app/api/v1/rooms/')




  // 使用 asyncData
  // const res = ref(null)
  // res.value =await useAsyncData("rooms",()=>{
  //   $fetch('https://nuxr3.zeabur.app/api/v1/rooms/')
  // })


// useFetch 需要在 onclick 的時候重新獲取資料，可以使用官方提供的 refresh 方式
// const { data, pending, error, refresh } = await useFetch('https://nuxr3.zeabur.app/api/v1/rooms/');

//   const res = ref(null)
//   res.value = data

// 將此方法綁定在 onclick 上 ，但是這一次 refresh 就是瀏覽器發出的請求， client side rendering
const refreshData = async () => {
    await refresh()
}



// useFetch 不能使用在 function 裡面，不然會報錯
// function 裡面要使用 $fetch
// 但是忘記差別在哪裡了


</script>