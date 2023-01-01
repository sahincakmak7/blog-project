<template>
  <v-container>
    <v-row class="d-flex align-start" v-for="(post, i) in posts" :key="i">
      <v-col>
        <v-card >
          <v-col
            ><h1>{{ post.title }}</h1>
          </v-col>
          <v-col>{{ post.content }}</v-col>
          <v-col
            ><v-row class="ml-1"
              ><strong>Creator : </strong> {{ post.creator }}</v-row
            >
          </v-col>
          <v-row class="justify-end mb-4 mr-4"
            ><v-btn size="small" color="black" @click.prevent="editRoute(post._id)">
              Edit
            </v-btn>
            <v-btn
              size="small"
              class="ml-2"
              @click.prevent="removePost(post._id)"
              color="black"
            >
              Delete
            </v-btn></v-row
          >
        </v-card></v-col
      ></v-row
    >
  </v-container>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import axios, { AxiosResponse } from "axios";
import CrudModels from "../../models/CrudModels";

export default defineComponent({
  data() {
    return {
      posts: new Array<CrudModels>(),
      API_URL: "http://localhost:5000/crud",
    };
  },
  mounted() {
    this.getPosts();
  },
  methods: {
    async getPosts() {
      await axios(this.API_URL).then(
        (result: AxiosResponse<Array<CrudModels>>) => {
          this.posts = result.data;
        }
      );
    },
    editRoute(id: string | null) {
      this.$router.push({
        name: "update",
        params: {
          id: id,
        },
      });
    },
    async removePost(id: string | null) {
      await axios.delete(`${this.API_URL}/${id}`);
      this.getPosts();
    },
  },
});
</script>
