<template>
  <v-card class="mx-auto mt-8" width="800" title="User Registration">
    <v-container>
      <v-form @submit.prevent="submitForm">
        <v-text-field
          v-model="postForm.title"
          label="Title"
          variant="underlined"
        ></v-text-field>

        <v-text-field
          v-model="postForm.content"
          label="Content"
          variant="underlined"
        ></v-text-field>

        <v-text-field
          v-model="postForm.creator"
          label="Creator"
          variant="underlined"
        ></v-text-field>
        <v-spacer></v-spacer>
        <v-btn
          class="mt-2 pa-2"
          block
          color="black"
          size="large"
          type="submit"
          variant="elevated"
        >
          Submit
        </v-btn>
      </v-form>
    </v-container>
  </v-card>
</template>

<script lang="ts">
import CrudModels from "../../models/CrudModels";
import { defineComponent, PropType } from "@vue/runtime-core";

export default defineComponent({
  props: {
    submitForm: {},
    post: {
      type: Object as PropType<CrudModels>,
      required: true,
    },
  },
  computed: {
    postForm: {
      get() {
        return this.post;
      },
      set(value: Event) {
        this.$emit("sendPost", value);
      },
    },
  },
});
</script>
