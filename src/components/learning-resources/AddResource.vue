<template>
  <base-dialog v-if="inputInvalid" title="Invalid Input" @close="confirmError">
    <template #default>
      <p>Unfortunately, at least one input is invalid.</p>
      <p>
        Please check all inputs and make sure you enter at least a few
        characters for each input.
      </p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Ok</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form>
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <input
          id="description"
          name="description"
          type="text"
          ref="descInput"
        />
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" ref="linkInput" />
      </div>
      <base-button type="submit" @click.prevent="submitData"
        >Add Resource</base-button
      >
    </form>
  </base-card>
</template>

<script>
export default {
  inject: ["addResource"],
  data() {
    return {
      inputInvalid: false,
    };
  },
  methods: {
    submitData() {
      const title = this.$refs.titleInput.value;
      const description = this.$refs.descInput.value;
      const url = this.$refs.linkInput.value;

      if (!title.trim() || !description.trim() || !url.trim()) {
        this.inputInvalid = true;
        return;
      } else {
        this.addResource(title, description, url);
      }
    },

    confirmError() {
      this.inputInvalid = false;
    },
  },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
