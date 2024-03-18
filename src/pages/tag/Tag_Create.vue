<template>
  <div class="ml-15 mt-10" style="width: 300px">
    <div class="mb-5 text-h5 font-weight-bold">Создание тегов:</div>
    <v-combobox
        clearable
        v-model="title"
        label="Тег"
        :items="['job', 'relax', 'training', 'home']"
        variant="solo-filled"
    ></v-combobox>
    <button @click.prevent="createTag" class="border-solid px-4 py-2 bg-red-darken-3" style="border-radius: 5px">Create</button>
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
    createTag(){
      if (!this.title) return
      axios.post('http://79.174.91.91:81/api/tags', {
        title: this.title
      })
          .then(res => {
            this.title = ''
            this.$router.push({name: 'tag_index.page'})
          })
    }
  }
}
</script>

<style lang="scss" scoped>

</style>