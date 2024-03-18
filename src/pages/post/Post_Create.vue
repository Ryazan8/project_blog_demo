<template>
    <div class="container">
      <div >

        <div >
          <input v-model="title" type="text" placeholder="Title">
        </div>
        <div >
          <input v-model="content" type="text" placeholder="Content">
        </div>

        <div >
          <input @change="setImage"  type="file">
        </div>
        <div >
          <select v-model="category_id" >
            <option disabled>Category</option>
            <option v-for="category in categories" :value="category.id">{{ category.title }}</option>
          </select>
        </div>

        <div>
          <select multiple v-model="curren_tags" >
            <option value="" disabled>Tag</option>
            <option v-for="tag in tags" :value="tag.id">{{ tag.title }}</option>
          </select>
        </div>

        <button class="border-solid px-5 py-2" @click="addPost">Create</button>
      </div>
    </div>


</template>

<script>

export default {

  data() {
    return {
      title: '',
      content: '',
      category_id: '',
      tag_id: [],
      posts: [],
      categories:[],
      tags:[],
      curren_tags: []
    }
  },
  mounted() {
    this.getTags()
    this.getCategories()
  },
  methods: {
    addPost() {
      let formData = new FormData()
      this.curren_tags.forEach(tag => {
        formData.append('tags[]', tag)
      })
      formData.append('title', this.title)
      formData.append('content', this.content)
      formData.append('category_id', this.category_id)
      formData.append('image', this.image)
      axios.post('http://79.174.91.91:81/api/posts', formData)
          .then(res => {
            this.posts = res.data
          })

      this.title = ''
      this.content = ''
      this.category_id = null
      this.tag_id = null
      this.image = null
    },
    getCategories(){
      axios.get('http://79.174.91.91:81/api/categories')
          .then(res=>{
            this.categories = res.data
          })
    },
    getTags(){
      axios.get('http://79.174.91.91:81/api/tags')
          .then(res=>{
            this.tags = res.data
          })
    },


    setImage(e){
      this.image = e.target.files[0]
      console.log(e.target.files[0])
    }
  }
}
</script>

<style>

.container{
  max-width: 800px;
  text-align: center;
  margin-left: 250px;
  align-items: center;
}

input::placeholder {
  color: black;
}
</style>