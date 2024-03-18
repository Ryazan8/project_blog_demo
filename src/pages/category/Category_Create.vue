<template>
  <div class="ml-15 mt-10" style="width: 300px">
    <div class="mb-5 text-h5 font-weight-bold">Создание категорий:</div>
    <v-combobox
        clearable
        v-model="title"
        label="Категория"
        :items="['Business', 'Home', 'Work', 'Chill']"
        variant="solo-filled"
    ></v-combobox>
    <button @click.prevent="createCategory" class=" px-4 py-2 btn_hover bg-red-darken-3" style="border-radius: 5px">Create</button>
  </div>
</template>

<script>
export default {
  data(){
    return{
      title: ''
    }
  },
  methods: {
    createCategory(){
      if (!this.title) return
      axios.post('http://79.174.91.91:81/api/categories', {
        title: this.title
      })
          .then(res => {
            this.title = ''
            this.$router.push({name: 'category_index.page'})
          })
    }
  }
}
</script>

<style lang="scss" scoped>

</style>