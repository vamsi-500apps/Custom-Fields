<template>
  <CollectionsList
    :CustomData="getCustomData"
    @slideout="openSidebar"
  />
  <div v-if="slideout" :key="render">
    <CollectionsAdd @postDatabody="postData" />
  </div>
</template>
<script setup lang="ts">
const slideout = ref(false);
const render = ref(0);
//GET Call
const getOptions = {
  method: "GET",
  headers: {
    "Content-Type": "application/json",
    Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiYzNlZTRlOWU1NTk2NDdjZDk4NGVmMzFhNjc4ODNkMmEiLCJkIjoiMTY4MDEwOCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMzNDkzOTB9.0V2YBlGbEMRMwE5sh1m-7WqAqfbB4_Fmqy9PX5rQoRo`,
  },
};
let getData = useAuthLazyFetch(
  "https://v1-orm-lib.mars.hipso.cc/api/custom-fields/CONTACTS?offset=01&limit=100&sort_column=id&sort_direction=desc",
  getOptions
);
let getCustomData = ref(getData.data._rawValue);
console.log("++++++++++==",getData.data)
console.log("=======",getCustomData._rawValue)
//POST Call
const postData = async (body: Object) => {
  const options = {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiYzNlZTRlOWU1NTk2NDdjZDk4NGVmMzFhNjc4ODNkMmEiLCJkIjoiMTY4MDEwOCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMzNDkzOTB9.0V2YBlGbEMRMwE5sh1m-7WqAqfbB4_Fmqy9PX5rQoRo`,
    },
    body: JSON.stringify(body),
  };
   useAuthLazyFetchPost(
    "https://v1-orm-lib.mars.hipso.cc/api/custom-fields/",
    options
  );
  
  getCustomData.value.unshift(body);
  console.log("main body",body)
  slideout.value = false;
};
const openSidebar = () => {
  slideout.value = true;
  render.value++;
};
</script>
