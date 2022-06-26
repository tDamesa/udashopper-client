<script lang="ts">
import { defineComponent } from "vue";
import { Api } from "../services/api";
import { AddListingModel } from "../types";
import Modal from "./Modal.vue";

export default defineComponent({
  data: () => {
    return {
      listing: {
        title: null,
        description: null,
        price: null,
        images: [],
      } as AddListingModel,
    };
  },
  methods: {
    save() {
      Api.saveListing(this.listing);
    },
    handleFileChange(event: any) {
      this.listing.images = Array.from(event.target.files);
    },
  },
  components: { Modal },
});
</script>

<template>
  <Modal>
    <template #title>Add Your Listing</template>
    <div class="add__body">
      <div>
        <label>Title</label>
        <input
          type="text"
          placeholder="Enter item title"
          v-model="listing.title"
        />
      </div>
      <div>
        <label>Price</label>
        <input
          type="number"
          placeholder="Enter item price"
          v-model="listing.price"
        />
      </div>
      <div>
        <label>Description</label>
        <textarea
          placeholder="Enter item description"
          v-model="listing.description"
        ></textarea>
      </div>
      <div>
        <label>Images</label>
        <input type="file" multiple @change="handleFileChange" />
      </div>
      <div>
        <button @click="save">Save</button>
      </div>
    </div>
  </Modal>
</template>

<style scoped lang="scss">
.add {
  &__body {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    padding: 1.5rem;
    width: 30rem;
  }
}
</style>
