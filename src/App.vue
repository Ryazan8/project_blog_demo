<template>
  <div class="d-flex">
    <v-card>
      <v-layout>
        <v-navigation-drawer
            class="bg-red-darken-4"
            permanent
        >
          <v-list color="transparent" >
            <router-link class="text-white text-decoration-none" to="/"><v-list-item prepend-icon="mdi-home" title="Home"></v-list-item></router-link>
             <router-link class="text-white text-decoration-none" to="/post_index"><v-list-item prepend-icon="mdi-post" title="Posts"></v-list-item></router-link>
            <router-link class="text-white text-decoration-none" to="/category_index"><v-list-item prepend-icon="mdi-shape" title="Categories"></v-list-item></router-link>
            <router-link class="text-white text-decoration-none" to="/tag_index"><v-list-item prepend-icon="mdi-tag" title="Tags"></v-list-item></router-link>
          </v-list>

          <template v-slot:append>
            <div class="pa-2">
              <v-btn block>
                Logout
              </v-btn>
            </div>
          </template>
        </v-navigation-drawer>
        <v-main style="height: 400px"></v-main>
      </v-layout>
    </v-card>
    <div>
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style scoped>

</style>