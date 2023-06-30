<template>
  <transition-group
    name="fade"
    tag="div"
    @beforeEnter="before"
    @enter="enter"
    @leave="leave"
  >
    <div
      class="row d-none mb-3 align-items-center"
      v-for="(item, index) in showItem"
      :key="item.id"
      :data-index="index"
    >
      <div class="col-1 m-auto">
        <button class="btn btn-info" @click="$emit('add', item)">+</button>
      </div>
      <div class="col-sm-4">
        <img :src="item.image" :alt="item.name" class="img-fluid d-block" />
      </div>
      <div class="col">
        <h3 class="text-info">{{ item.name }}</h3>
        <p class="mb-0">{{ item.description }}</p>
        <div class="h5 float-right">
          <price-display :value="item.price"></price-display>
        </div>
      </div>
    </div>
  </transition-group>
</template>

<script>
import PriceDisplay from "./PriceDisplay.vue";

export default {
  name: "ProductList",
  components: {
    PriceDisplay,
  },
  props: {
    products: {
      type: Array,
      required: true,
    },
    maximum: {
      type: Number,
      required: true,
    },
  },
  computed: {
    showItem() {
      return this.products.filter((item) => item.price <= this.maximum);
    },
  },
  methods: {
    before(el) {
      el.className = "d-none";
    },
    enter(el) {
      const delay = el.dataset.index * 100;
      setTimeout(() => {
        el.className =
          "row d-flex mb-3 align-items-center animated fadeInRight";
      }, delay);
    },
    leave(el) {
      const delay = el.dataset.index * 100;
      setTimeout(() => {
        el.className =
          "row d-flex mb-3 align-items-center animated fadeOutRight";
      }, delay);
    },
  },
};
</script>
