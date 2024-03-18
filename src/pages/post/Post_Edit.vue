<template>
<div class="container mt-10">
  <div v-if="post" class="post">

    <div >
      <input class="post_title mb-5" v-model="post.title" type="text" placeholder="Title">
    </div>
    <div >
      <textarea class="post_content mb-5 py-2 px-5 " style="width: 400px; resize: none; height: 100px " v-model="post.content"></textarea>

    </div>

    <!--  <div class="">-->
    <!--    <img :src="post.image_url" alt="">-->
    <!--  </div>-->

    <div>
      <input @change="setImage" type="file" class="img">
    </div>

    <div class="d-flex justify-space-between mt-5">
      <div>
        <select v-model="post.category.id">
          <option value="" disabled>Category</option>
          <option v-for="category in categories" :value="category.id">{{ category.title }}</option>
        </select>
      </div>

      <div>

        <select multiple v-model="curren_tags">
          <option value="" disabled>Tag</option>
          <option v-for="tag in tags" :value="tag.id">{{ tag.title }}</option>
        </select>
      </div>
    </div>


    <div class="mt-5" @click.prevent="editPost"><span class="mdi mdi-content-save-outline text-red-darken-3 text-h4 "></span></div>
  </div>
</div>

</template>

<script>
export default {
  data() {
    return {
      sum_tags: [],
      curren_tags: [],
      title: '',
      content: '',
      image: null,
      category_id: '',
      categories: [],
      tags: [],
      tag_id: '',
      category: '',
      post: null
    }
  },
  mounted() {
    this.getTags()
    this.getCategories()
    this.getPostShow(this.$route.params.id)
  },

  methods: {
    editPost() {
      let formData = new FormData()
      formData.append('title', this.post.title)
      formData.append('content', this.post.content)
      formData.append('category_id', this.post.category.id)
      
      this.curren_tags.forEach(tag => {
        formData.append('tags[]', tag)
      })
      formData.append('image', this.image)
      formData.append('_method', 'patch')
      axios.post(`http://79.174.91.91:81/api/posts/${this.post.id}`, formData)
    .then(res => {
        this.posts = res.data
      })
      console.log(this.post)

    },
    getPostShow(id) {
      axios.get(`http://79.174.91.91:81/api/posts/${id}`)
    .then(res => {
        this.post = res.data
        this.curren_tags = this.post.tags.map(tag => tag.id)
      })
    },

    getCategories() {
      axios.get(`http://79.174.91.91:81/api/categories`)
    .then(res => {
        this.categories = res.data
      })
    },
    getTags() {
      axios.get('http://79.174.91.91:81/api/tags')
          .then(res => {
            this.tags = res.data
          })
    },
    setImage(e) {
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

.post{
  background: #ededed;
  padding: 20px 40px;
  margin-bottom: 20px;
  color: #262626;
}

.post_title{
  padding-top: 20px;
  font-size: 30px;
  font-weight: 500;
  line-height: 1.1;
}
.post_content{
  padding: 20px 0;
  line-height: 28px;
  font-size: 16px;
  color: #3f3f3f;
}
</style>