<template>
  <div
    class="modal"
    tabindex="-1"
    v-bind:class="{ openModal: openModal == true }"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">Luat choi</h5>
          <button
            v-on:click="closeModal"
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">
          <p>Modal body text goes here.</p>
        </div>
        <div class="modal-footer">
          <button
            type="button"
            class="btn btn-secondary"
            data-bs-dismiss="modal"
            v-on:click="closeModal"
          >
            Close
          </button>
          <button type="button" class="btn btn-primary" v-on:click="confirm">
            Save changes
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "rule",
  data() {
    return {};
  },
  props: {
    openModal: { type: Boolean, default: false },
  },
  methods: {
    confirm(){
       const close = !this.openModal;
      this.$emit('handleStart', close)
    },
    closeModal() {
      const close = !this.openModal;
      this.$emit("handleCloseModal", close);
    },
  },
};
</script>
<style>
.openModal {
  display: block;
  animation: ease 1s open;
}
@keyframes open {
  form {
    opacity: 0;
    transform: scale(0.5);
  }
  to {
    opacity: 1;
    transform: scale(1.2);
  }
}
</style>