<template>
  <div class="container">
    <div class="top-blocks">
      <div class="selected-user-items">
        <div class="items-counter">
          selected: {{ selectedUserItems.length }} / 6
        </div>
        <div class="items-container">
          <div v-for="item in selectedUserItems" :key="item.id" class="item">
            {{ item.name }}
          </div>
        </div>
      </div>

      <div class="selected-market-item">
        <div v-if="selectedMarketItem" class="item">
          {{ selectedMarketItem.name }}
        </div>
      </div>
    </div>

    <div class="bottom-blocks">
      <div class="user-items">
        <div class="items-container">
          <div
            v-for="item in userItems"
            :key="item.id"
            :class="['item', { selected: isUserItemSelected(item) }]"
            @click="toggleUserItem(item)"
          >
            {{ item.name }}
          </div>
        </div>
      </div>

      <div class="market-items">
        <div class="items-container">
          <div
            v-for="item in marketItems"
            :key="item.id"
            :class="['item', { selected: isMarketItemSelected(item) }]"
            @click="selectMarketItem(item)"
          >
            {{ item.name }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DvaPacana",
  data() {
    return {
      userItems: [
        { id: 1, name: "Shoes 1" },
        { id: 2, name: "Shoes 2" },
        { id: 3, name: "Shoes 3" },
        { id: 4, name: "Shoes 4" },
        { id: 5, name: "T-shirt 1" },
        { id: 6, name: "T-shirt 2" },
        { id: 7, name: "T-shirt 3" },
        { id: 8, name: "T-shirt 4" },
      ],
      marketItems: [
        { id: 11, name: "Jacket 1" },
        { id: 12, name: "Jacket 2" },
        { id: 13, name: "Jacket 3" },
        { id: 14, name: "Jacket 4" },
        { id: 15, name: "Hoodie 1" },
        { id: 16, name: "Hoodie 2" },
        { id: 17, name: "Hoodie 3" },
        { id: 18, name: "Hoodie 4" },
      ],
      selectedUserItems: [],
      selectedMarketItem: null,
    };
  },
  methods: {
    toggleUserItem(item) {
      const index = this.selectedUserItems.findIndex((i) => i.id === item.id);
      if (index === -1) {
        if (this.selectedUserItems.length < 6) {
          this.selectedUserItems.push(item);
        }
      } else {
        this.selectedUserItems.splice(index, 1);
      }
    },
    selectMarketItem(item) {
      this.selectedMarketItem =
        this.selectedMarketItem?.id === item.id ? null : item;
    },
    isUserItemSelected(item) {
      return this.selectedUserItems.some((i) => i.id === item.id);
    },
    isMarketItemSelected(item) {
      return this.selectedMarketItem?.id === item.id;
    },
  },
};
</script>

<style scoped>
.container {
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.top-blocks,
.bottom-blocks {
  display: flex;
  gap: 20px;
}

.selected-user-items,
.selected-market-item,
.user-items,
.market-items {
  border: 2px solid black;
  padding: 10px;
  flex: 1;
}

.items-container {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.item {
  border: 1px solid black;
  padding: 10px;
  cursor: pointer;
}

.item.selected {
  background-color: #e0e0e0;
}

.items-counter {
  margin-bottom: 10px;
}
</style>
