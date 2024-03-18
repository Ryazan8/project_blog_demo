<template>
<div class="ml-15 mt-10" style="width: 300px" >
<div class="mb-5 text-h5 font-weight-bold">Edit Tag:</div>
<div v-if="tag">
  <v-combobox
      clearable
      v-model="tag.title"
      label="Тег"
      :items="['job', 'relax', 'training', 'home']"
      variant="solo-filled"
  ></v-combobox>
  <button @click.prevent="updateTag" class=" px-4 py-2 bg-red-darken-3" style="border-radius: 5px">Update</button>
</div>

</div>
</template>

<script>
export default {
  data(){
    return{
      tag: null,
    }
  },
  mounted() {
    this.getTag(this.$route.params.id)
  },
  methods: {
    getTag(id){
      axios.get(`http://79.174.91.91:81/api/tags/${id}`)
          .then(res => {
            this.tag = res.data
          })
    },

    updateTag(){
      axios.patch(`http://79.174.91.91:81/api/tags/${this.tag.id}`, {
        title: this.tag.title
      })
          .then(res => {
            this.tag = res.data
            this.$router.push({name: 'tag_index.page'})
          })
    }
  },

}
</script>

<style lang="scss" scoped>

</style>