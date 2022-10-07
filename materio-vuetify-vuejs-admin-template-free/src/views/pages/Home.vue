<script>
import axios from 'axios'
import { ref } from '@vue/composition-api'
import {
  mdiChevronUp,
  mdiChevronDown,
  mdiCartPlus,
  mdiShareVariantOutline,
  mdiLockOpenOutline,
  mdiStarOutline,
  mdiAccountOutline,
  mdiTrendingUp,
  mdiHelpCircleOutline,
} from '@mdi/js'
export default {
  data() {
    return {
      products: [],
    }
  },
  methods: {
    async fetchData() {
      try {
        const { data } = await axios.get('https://dummyjson.com/products')
        this.products = data.products
        console.log(this.products)
      } catch (error) {
        console.log(error)
      }
    },
  },
  created() {
    this.fetchData()
  },
  setup() {
    const isCardDetailsVisible = false
    const rating = ref(5)

    return {
      isCardDetailsVisible,
      rating,

      // icons
      icons: {
        mdiChevronUp,
        mdiChevronDown,
        mdiCartPlus,
        mdiShareVariantOutline,
        mdiLockOpenOutline,
        mdiStarOutline,
        mdiAccountOutline,
        mdiTrendingUp,
        mdiHelpCircleOutline,
      },
    }
  },
}
</script>
<template>
  <div class="d-flex flex-wrap">
    <v-card :loading="loading" class="mx-1 my-3 card" max-width="280" v-for="product in products">
      <template slot="progress">
        <v-progress-linear color="deep-purple" height="10" indeterminate></v-progress-linear>
      </template>
      <v-img :aspect-ratio="9 / 7" :src="product.images[2]"></v-img>

      <v-card-title>{{ product.title }}</v-card-title>
      <v-divider class=""></v-divider>

      <div class="content my-4">
        <div>
          <v-card-text>
            <div>{{ product.description }}</div>
          </v-card-text>
        </div>
        <div>
          <v-card-text class="text--primary text-base">
            <span>Price :</span> <span class="font-weight-bold">${{ product.price }}</span>
          </v-card-text>
          <v-card-actions class="d-flex justify-space-between dense">
            <v-btn text color="primary" dark>
              <v-icon>{{ icons.mdiCartPlus }}</v-icon>
              <span class="ms-2">Add to cart</span>
            </v-btn>
            <v-btn icon>
              <v-icon>{{ icons.mdiShareVariantOutline }}</v-icon>
            </v-btn>
          </v-card-actions>
        </div>
      </div>
    </v-card>
  </div>
</template>
<style>
.img-item {
}

.items {
  align-items: stretch;
}

.content {
  height: 200px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
</style>
