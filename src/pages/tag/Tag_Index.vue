<template>
  <div class="div_table">
    <div class="text-h4 mb-5 font-weight-bold">
      Tag Table:
    </div>
    <div class="mb-5">
      <router-link class="text-h4 mb-5" to="/tag_create"><span class="mdi mdi-plus-box text-red-darken-3"></span></router-link>
    </div>

    <table class="table">
      <thead>
      <tr class="text-center">
        <th class="w-50">
          ID
        </th>
        <th class="w-50">
          Tag
        </th>
        <th class="w-50">
          Tools
        </th>
      </tr>
      </thead>
      <tbody>
      <tr
          v-for="tag in tags"
          :key="tag.id"
      >
        <td>{{ tag.id }}</td>
        <td>{{ tag.title }}</td>
        <td class="d-flex"><button @click.prevent="removeTag(tag.id)"><span class="mdi mdi-delete text-h5 mr-3 text-red-darken-4"></span></button>
          <router-link :to="{name: 'tag_edit.page', params: {id: tag.id}}"><button><span class="mdi mdi-pencil text-h5 text-blue-accent-2"></span></button></router-link></td>
      </tr>
      </tbody>
    </table>
  </div>

</template>

<script>
export default {
  data () {
    return {
      tags: []
    }
  },
  mounted() {
    this.getTags()
  },
  methods: {
    getTags() {
      axios.get(' http://79.174.91.91:81/api/tags')
          .then(res => {
            this.tags = res.data
          })
    },
    removeTag(id) {
      axios.delete(`http://79.174.91.91:81/api/tags/${id}`)
          .then(res => {
            this.tags = this.tags.filter(tag => {
              return parseInt(tag.id) !== parseInt(id)
            })
          })
    }
  }
}
</script>

<style>
.div_table{
  margin: 50px 200px;
}

.table {
  width: 500px;
  border: none;
  margin-bottom: 20px;
  border-collapse: separate;
}
.table thead th {
  font-weight: bold;
  text-align: center;
  border: none;
  padding: 10px 15px;
  background: #ddd;
  font-size: 20px;
  border-top: 1px solid #ddd;
}
.table tr th:first-child, .table tr td:first-child {
  border-left: 1px solid #ddd;
}
.table tr th:last-child, .table tr td:last-child {
  border-right: 1px solid #ddd;
}
.table thead tr th:first-child {
  border-radius: 20px 0 0 0;
}
.table thead tr th:last-child {
  border-radius: 0 20px 0 0;
}
.table tbody td {
  text-align: center;
  border: none;
  padding: 10px 15px;
  font-size: 18px;
  vertical-align: top;
}
.table tbody tr:nth-child(even) {
  background: #F8F8F8;
}
.table tbody tr:last-child td{
  border-bottom: 1px solid #ddd;
}
.table tbody tr:last-child td:first-child {
  border-radius: 0 0 0 20px;
}
.table tbody tr:last-child td:last-child {
  border-radius: 0 0 20px 0;
}
</style>