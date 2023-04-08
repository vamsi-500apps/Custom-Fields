<template>
  <CollectionsList
    :CustomData="getCustomData"
    @deleteDataItem="deleteCustomData"
    @editDataItem="editCustomDataList"
    @slideout="openSidebar"
    
    
  />
  <div v-if="slideout" :key="renderAdd">
    <CollectionsAdd @postDatabody="postData"
    />
  </div>

  <div v-if="Edit" :key="renderEdit" >
    <CollectionsEdit  @customEditemit="editCustomData" :data="dataValue"/>
    </div>
</template>
<script setup lang="ts">
const slideout = ref(false);
const editSlideout=ref(false);
const renderAdd = ref(0);
const renderEdit = ref(0);
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
  renderAdd.value++;
};

const deleteCustomData = async (item: object) => {

  const deleteOptions = {
    method: "DELETE",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiYzNlZTRlOWU1NTk2NDdjZDk4NGVmMzFhNjc4ODNkMmEiLCJkIjoiMTY4MDEwOCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMzNDkzOTB9.0V2YBlGbEMRMwE5sh1m-7WqAqfbB4_Fmqy9PX5rQoRo`,
    },
  };
  await useAuthLazyFetchDelete(
    `https://v1-orm-lib.mars.hipso.cc/api/custom-fields/${item.id}`,
    deleteOptions
  );
  getCustomData.value.shift(item);
  console.log("main item",item)
};
const dataValue = ref({});
const Edit = ref(false);
const render=ref(0);

const editCustomDataList = (data: any) => {
  dataValue.value = data;
  Edit.value = true;
  renderEdit.value++;
  
};
Edit.value=false;
//Edit the Custom Data PUT Call
const editCustomData = async (body: Object) => {
  const options = {
    method: "PUT",
    headers:  {
      "Content-Type": "application/json",
      Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiYzNlZTRlOWU1NTk2NDdjZDk4NGVmMzFhNjc4ODNkMmEiLCJkIjoiMTY4MDEwOCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMzNDkzOTB9.0V2YBlGbEMRMwE5sh1m-7WqAqfbB4_Fmqy9PX5rQoRo`,
    },
    body: JSON.stringify(body),
  };
  await useAuthLazyFetchPut(`https://v1-orm-lib.mars.hipso.cc/api/custom-fields/${body.uid}`,options);
  getCustomData.value.unshift(body);
};
</script>
