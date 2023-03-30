<script setup>
getDogs();

definePageMeta({
  title: "Department",
});

const changedata = ref(false);
const field = ["Nama", "Details", "Action"];
const data = ref([]);

// const _click = async (id) => {
//   console.log(id);
// };

async function _click(id) {
  console.log(id);

  window.open('/user/' + id);

}

async function getDogs() {
  await useFetch("https://api.restful-api.dev/objects", { method: "GET" })
    .then((res) => {
      console.log('res :', res.data.value);
      // res.data.value convert object into array
      const dataFetchAPI = res.data.value;

      // data2 foreach element to data

      dataFetchAPI.forEach((element) => {
        // console.log('element :', element);
        // console.log('element :', element.id);
        // console.log('element :', element.name);
        // console.log('element :', element.age);
        // console.log('element :', element.email);
        // console.log('element :', element.id);
        // push element data2 into data


        data.value.push({
          id: element.id,
          fullName: element.name,
          action: ""
        });
      });




      console.log('data2 :', data2);
      // push element data2 into data
      // data.push(...data2);



      console.log('data :', JSON.stringify(data));
    })
    .catch((err) => {
      console.log(err);
    });
}

</script>

<template>
  <div>
    <LayoutsBreadcrumb />

    <rs-card>
      <template #header>
        List Department
      </template>

      <template #body>

        <rs-table v-if="data && data.length > 0" :data="data" :options-advanced="{
          sortable: true,
          responsive: true,
        }" advanced>

          <template v-slot:action="data">
            <nuxt-link :to="'/department/' + data.value.id" class="btn btn-primary">
              <rs-button variant="primary">Edit</rs-button>
            </nuxt-link>
            <!-- <rs-button type="danger" size="small">Delete</rs-button> -->
          </template>

        </rs-table>
      </template>


    </rs-card>
  </div>
</template>
    
    