<template>
  <ul class="list">
    <li v-for="p in products" :key="p.id">
      {{ p.title }} - {{ p.price | currency }}
      <br>
      <el-button
        :disabled="!p.inventory"
        @click="addToCart(p)">
        Add to cart
      </el-button>
    </li>
  </ul>
</template>

<script lang="ts">
import Vue from 'vue'
import { mapGetters, mapActions } from 'vuex'
import { Button } from 'element-ui'

import { Product } from '../store'

Vue.use(Button)

// 以下是常规写法：

import { dispatchAddToCart } from '../store/dispatches'

export default Vue.extend({
  computed: {
    // ...mapGetters({
    //   products: 'allProducts'
    // })
    products(): Product[] {
      return this.$store.getters.allProducts
    },
  },
  methods: {
    // ...mapActions([
    //   'addToCart'
    // ])
    addToCart(p: Product) {
      dispatchAddToCart(p)
    },
  },
  created() {
    this.$store.dispatch('getAllProducts')
  },
})

// 以下是vue-property-decorator + vuex-class写法：

// import { Component } from 'vue-property-decorator'
// import { Getter, Action } from 'vuex-class'

// @Component
// export default class ProductList extends Vue {
//   @Getter('allProducts') public products!: Product[]
//   @Action('addToCart') public actionAddToCart!: any
//   @Action('getAllProducts') public getAllProducts!: any

//   public addToCart(p: Product) {
//     this.actionAddToCart(p)
//   }

//   public created() {
//     this.getAllProducts()
//   }
// }

</script>

<style lang="scss" scoped>
ul {
  list-style-type: none;
  padding-left: 0;
}

.list {
  li {
    padding: 5px 0;
  }
}
</style>

        