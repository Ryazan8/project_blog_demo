<template>
  <div class="ml-15 mt-10" style="width: 300px" >
    <div class="mb-5 text-h5 font-weight-bold">Edit Category:</div>
    <div v-if="category">
      <v-combobox
          clearable
          v-model="category.title"
          label="Категория"
          :items="['Business', 'Home', 'Work', 'Chill']"
          variant="solo-filled"
      ></v-combobox>
      <button @click.prevent="updateCategory" class=" px-4 py-2 bg-red-darken-3" style="border-radius: 5px">Update</button>
    </div>

  </div>
</template>

<script>
export default {
  data(){
    return{
      category: null,
    }
  },
  mounted() {
    this.getCategory(this.$route.params.id)
  },
  methods: {
    getCategory(id){
      axios.get(`http://79.174.91.91:81/api/categories/${id}`)
          .then(res => {
            this.category = res.data
          })
    },

    updateCategory(){
      axios.patch(`http://79.174.91.91:81/api/categories/${this.category.id}`, {
        title: this.category.title
      })
          .then(res => {
            this.category = res.data
            this.$router.push({name: 'category_index.page'})
          })
    }
  },

}
</script>

<style lang="scss" scoped>
.btn_hover{
  transition: all .3s ease-in-out;
  background: #2c3535;
  color: aliceblue;
}
.btn_hover:hover{
  background: #fff;
  color: #2c3535;
}
</style>