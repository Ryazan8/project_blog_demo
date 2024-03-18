<template>

  <div class="header">
    <div class="name">Alexandr Ryazanov</div>
    <div class="subtitle">Personal Blog Template</div>
    <router-link class="text-h4 mb-5" to="/post_create"><span class="mdi mdi-plus-box text-red-darken-3"></span></router-link>
  </div>

  <div class="container">
    <div class="posts">
      <div class="post" v-for="post in posts">
        <div v-if="post.image_url">
          <img
              :src="post.image_url"
              :title="post.title"
              :alt="post.title"
              class="img"
              cover
          >
        </div>
        <div class="post_title">
          {{ post.title }}
        </div>
        <div class="post_content">
          {{ post.content }}
        </div>

        <div class="d-flex justify-space-evenly">
          <div>{{ post.category.title }}</div>
          <div v-for="tag in post.tags">
            <div class="d-flex">
              #{{ tag.title }}
            </div>
          </div>
        </div>

        <div class="d-flex text-h5 mt-5">
          <router-link class="mr-3" :to="{name: 'post_edit.page', params: {id: post.id}}">
            <span class="mdi mdi-pencil text-blue-darken-3"></span>
          </router-link>
          <router-link class="mr-3" :to="{name: 'post_show.page', params: {id: post.id}}">
            <span class="mdi mdi-eye-outline text-green-darken-3"></span>
          </router-link>
          <button @click.prevent="removePost(post.id)"><span class="mdi mdi-delete mr-2 text-red-darken-3"></span></button>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
export default {

  data() {
    return {
      categories: [],
      posts: []
    }
  },
  mounted() {
    this.getPosts()
  },
  methods: {
    getPosts() {
      axios.get('http://79.174.91.91:81/api/posts')
          .then(res => {
            this.posts = res.data
          })
    },
    removePost(id) {
      axios.delete(`http://79.174.91.91:81/api/posts/${id}`)
          .then(res => {
            this.posts = this.posts.filter(post => {
              return parseInt(post.id) !== parseInt(id)
            })
          })
    }
  }
}
</script>

<style scoped>

.header{
  width: 500px;
  margin-left: 350px;
  text-align: center;
  margin-bottom: 30px;
  margin-top: 50px;
}
.name{
  font-size: 48px;
  font-weight: 500;
  color: #3d3d3d;
}
.subtitle{
  font-size: 14px;
  font-weight: 300;
  color: #828282;
}

.container{
  max-width: 800px;
  text-align: center;
  margin-left: 250px;
  align-items: center;
}

.post{
  background: #ededed;
  padding: 20px 20px;
  margin-bottom: 20px;
  color: #262626;
}

.img{
  width: 700px;
  height: 450px;
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