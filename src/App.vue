<template>
  <div class="main-wrap">
    <div class="item-list">
      <div class="item" v-for="item in itemList" :key="item" @click="updateCart(item)" :class="{ selected: item.isSelected === true }">
        <div>{{ item.name }}</div>
        <div>${{ item.amount }}</div>
      </div>
    </div>
    <div class="cart">
      <div class="item" v-for="item in cartNewOrder" :key="item">
        <div class="item-wrap" v-if="item.isSelected === true">
          <div>{{ item.name }}</div>
          <div>@ &nbsp; {{ item.quantity }} x</div>
          <div>${{ item.amount }}</div>
          <div>${{ item.amount * item.quantity }}</div>
          <div class="control-wrap">
            <div @click="updateItemQty('subract', item)">-</div>
            <div @click="updateItemQty('add', item)">+</div>
            <div @click="removeItem(item)">x</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      itemList: [
        { name: "Milk", amount: 10, isSelected: false, quantity: 0 }, // 0
        { name: "Fish", amount: 20, isSelected: false, quantity: 0 }, // 1
        { name: "Lettuce", amount: 30, isSelected: false, quantity: 0 }, // 2
        { name: "Rice", amount: 5, isSelected: false, quantity: 0 } // 3
      ],

      cartNewOrder: []
    }
  },

  methods: {
    updateCart(item) {
      if (item.isSelected == false) {
        this.cartNewOrder.unshift(item)
      } else {
        let missingItemIndex = this.cartNewOrder.findIndex((missingItem) => missingItem.name == item.name)
        this.cartNewOrder.splice(missingItemIndex, 1)
      }
      item.isSelected = !item.isSelected
    },

    updateItemQty(mode, item) {
      if (mode === "add") {
        item.quantity++
      } else {
        if (item.quantity > 0) {
          item.quantity--
        } else {
          item.isSelected = false
        }
      }
    }
  }
}
</script>

<style lang="scss">
body {
  font-family: Source Sans Pro, sans-serif;
}

.main-wrap {
  display: flex;
  justify-content: space-between;

  .item-list {
    .item {
      display: flex;
      justify-content: space-between;
      background-color: rgba(#ddd, 1);
      margin: 0.5rem;
      padding: 1rem;
      border-radius: 0.5rem;
      width: 10rem;
      cursor: pointer;
    }

    .selected {
      background-color: rgba(#eee, 1);
      color: rgba(#a3a3a3, 1);
    }
  }

  .cart {
    .item {
      display: flex;
      width: 20rem;

      .item-wrap {
        display: flex;
        flex: 1;
        justify-content: space-between;
        background-color: rgba(#ddd, 1);
        margin: 0.25rem;
        height: 1.5rem;
        padding: 1rem;
        border-radius: 0.5rem;
        align-items: center;

        &:hover {
          .control-wrap {
            display: flex;
          }
        }

        .control-wrap {
          display: none;

          div {
            padding: 0.5rem 1rem;
            margin: 0 0.25rem;
            background-color: rgba(#ff9200, 1);
            border-radius: 0.5rem;
            cursor: pointer;
          }
        }
      }
    }

    .total {
      display: flex;
      justify-content: space-between;
      background-color: rgba(#111, 1);
      color: rgba(#fff, 1);
      padding: 1rem;
      margin: 0.25rem;
      border-radius: 0.5rem;
    }
  }
}
</style>

this.cartNewOrder.findIndex((removeItem) => removeItem.name == item.name)) let missingItemIndex = this.cartNewOrder.findIndex((removeItem) => removeItem.name == item.name))
this.cartNewOrder.splice(missingItemIndex, 1)
