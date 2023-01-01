<template >
  <v-card style="position: sticky; top: 0; z-index: 2">
    <v-layout>
      <v-app-bar color="black">
        <v-toolbar-title @click.prevent="direction(0)"
          ><strong style="cursor: pointer" @click="$router.push('home')"
            >MyBlog</strong
          >
        </v-toolbar-title>
        <v-spacer></v-spacer>
        <v-col cols="auto">
          <v-row no-gutters>
            <v-col>
              <v-btn
          
                color="white"
                class="ml-2"
                v-for="(link, index) in links"
                :key="index"
                @click="direction(index)"
              >
                <v-icon class="mr-1">{{ link.icon }}</v-icon
                ><strong>{{ link.name }}</strong>
              </v-btn>
            </v-col>
          </v-row>
        </v-col>
      </v-app-bar>
      <v-main></v-main>
    </v-layout>
  </v-card>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  data() {
    return {
      links: [
        {
          id: 1,
          name: "home",
          icon: "mdi-home",
        },
        {
          id: 2,
          name: "create",
          icon: "mdi-plus",
        },
      ],
    };
  },
  methods: {
    direction(i: number) {
      this.$router.push({ name: this.links[i].name });
    },
  },
});
</script>
