<template>
  <form class="stack-small" @submit.prevent="onSubmit">
    <div class="button-wrapper">
      <div>
        <label class="edit-label"></label>
        <input :id="id" type="text" autocomplete="off" v-model.lazy.trim="newLabel" />
      </div>
      <div class="btn-group">
        <button type="button" class="btn cancel-button" @click="onCancel">
          <!-- Cancel
          <span class="visually-hidden">editing {{label}}</span>
          </-->
        </button>
        <button type="submit" class="btn btn__primary commit-button">
          <!-- Save
          <span class="visually-hidden">edit for {{label}}</span>
          </-->
        </button>
      </div>
    </div>
  </form>
</template>
<script>
export default {
  props: {
    label: {
      type: String,
      required: true
    },
    id: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      newLabel: this.label
    };
  },
  methods: {
    onSubmit() {
      if (this.newLabel && this.newLabel !== this.label) {
        this.$emit("item-edited", this.newLabel);
      }
    },
    onCancel() {
      this.$emit("edit-cancelled");
    }
  }
};
</script>
<style>
  .button-wrapper {
    display: flex;
    padding: 2px;
  }
  .cancel-button {
    width: 20px;
    height: 20px;
    background-image: url("https://img.icons8.com/ios-glyphs/30/000000/cancel.png");
    background-size: contain;
  }
  .commit-button {
    width: 20px;
    height: 20px;
    background-image: url("https://img.icons8.com/external-royyan-wijaya-detailed-outline-royyan-wijaya/24/000000/external-tick-interface-royyan-wijaya-detailed-outline-royyan-wijaya-4.png");
    background-size: contain;
  }
</style>
