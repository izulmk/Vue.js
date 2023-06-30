<template>
  <transition name="fade">
    <div v-if="sliderStatus">
      <div class="align-items-center" :class="sliderState">
        <label for="" class="font-weight-bold mr-2">Max</label>
        <!-- eslint-disable-next-line -->
        <input type="text" class="form-control mx-2" style="width: 60px; text-align: center" v-model="maxAmount" @change="$emit('update:maximum', maxAmount)" />
        <!-- eslint-disable-next-line -->
        <input type="range" class="custom-range" min="0" max="200" v-model="maxAmount" @input="updateMaximum" />
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "price-slider",
  data: function () {
    return {
      maxAmount: 50,
    };
  },
  props: ["sliderStatus", "maximum"],
  computed: {
    sliderState: function () {
      return this.sliderStatus ? "d-flex" : "d-none";
    },
  },
  methods: {
    updateMaximum() {
      this.$emit("update:maximum", this.maxAmount);
    },
  },
};
</script>

<style>
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 1s ease-in-out;
}
</style>
