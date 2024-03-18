<template>
  <div class="div_table">
    <div class="text-h4 mb-5 font-weight-bold">
      Category Table:
    </div>
    <div class="mb-5">
      <router-link class="text-h4 mb-5" to="/category_create"><span class="mdi mdi-plus-box text-red-darken-"></span></router-link>
    </div>

    <table class="table">
      <thead>
      <tr class="text-center">
        <th class="w-50">
          ID
        </th>
        <th class="w-50">
          Category
        </th>
        <th class="w-50">
          Tools
        </th>
      </tr>
      </thead>
      <tbody>
      <tr
          v-for="category in categories"
          :key="category.id"
      >
        <td>{{ category.id }}</td>
        <td>{{ category.title }}</td>
        <td class="d-flex"><button @click.prevent="removeCategory(category.id)"><span class="mdi mdi-delete text-h5 mr-3 text-red-darken-4"></span></button>
          <router-link :to="{name: 'category_edit.page', params: {id: category.id}}"><button><span class="mdi mdi-pencil text-h5 text-blue-accent-2"></span></button></router-link></td>
      </tr>
      </tbody>
    </table>
  </div>

</template>

<script>
export default {
  data () {
    return {
      categories: []
    }
  },
  mounted() {
    this.getCategories()
  },
  methods: {
    getCategories() {
      axios.get(' http://79.174.91.91:81/api/categories')
          .then(res => {
            this.categories = res.data
          })
    },
    removeCategory(id) {
      axios.delete(`http://79.174.91.91:81/api/categories/${id}`)
          .then(res => {
            this.categories = this.categories.filter(category => {
              return parseInt(category.id) !== parseInt(id)
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
  background: #ddd;
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