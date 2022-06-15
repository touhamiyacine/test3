
<script src="https://unpkg.com/vue-router@4"></script>
<template>
  <div class="overflow-auto">
   
    <p class="mt-3">Current Page: {{ currentPage }}</p>

    <b-table
    thead-class="green-bg bg-dark text-white"
  bordered @row-clicked="onRowClicked"
 
      id="my-table"
      :items="items"
      :per-page="perPage"
      :current-page="currentPage"
      small
    ></b-table>
     <b-pagination
      v-model="currentPage"
      :total-rows="rows"
      :per-page="perPage"
      aria-controls="my-table"
    ></b-pagination>

  </div>
</template>
<script>
  import Vue from 'vue'
 import BootstrapVue from 'bootstrap-vue'

 Vue.use(BootstrapVue)
 
 export default {
    data() {
      return {
        items: [],
         filter: '',
      perPage: 10,
      currentPage: 1,
      selectedItem:'',
      }
    },
    async fetch() {
      this.items = await fetch(
        'https://jsonplaceholder.typicode.com/albums/'
      ).then(res => res.json())
    },
     computed: {
      rows() {
        return this.items.length
      }},
       methods: {
        onRowClicked(item) {
      this.selectedItem = item.id
      alert(this.selectedItem);
    this.$router.push({name: 'photos', params: {id: this.selectedItem}})
    
     //window.location.href = 'gallery.html?id=' + this.selectedItem;

    },
    },
  }
</script>
 