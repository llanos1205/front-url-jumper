<template>
  <div>

  </div>
  <ul v-if="!loading && data && data.length">
    <li v-for="post of data">
      <p><strong></strong></p>
      <p></p>
    </li>
  </ul>

  <p v-if="loading">
    Still loading..
  </p>
  <p v-if="error">


  </p>
</template>

<script>
import {ref, computed} from 'vue';

export default {
  name: "WallContainer",
  props: {},
  setup() {
    const data = ref(null);
    const loading = ref(true);
    const error = ref(null);

    function fetchData() {
      loading.value = true;
      return fetch(process.env.API_URL + "Wall/", {
        method: "get",
        headers: {
          'content-type': 'application/json'
        }
      }).then(res => {
        if (!res.ok) {
          const error = new Error(res.statusText);
          error.json = res.json();
          throw error;
        }
      })
          .then(json => {
            // set the response data
            data.value = json.data;
          })
          .catch(err => {
            error.value = err;
            // In case a custom JSON error response was provided
            if (err.json) {
              return err.json.then(json => {
                // set the JSON response message
                error.value.message = json.message;
              });
            }
          })
          .then(() => {
            loading.value = false;
          });
    }

    onMounted(() => {
      fetchData();
    });
    return {
      data,
      loading,
      error
    };
  }
}
</script>

<style scoped>

</style>