<template>
  <div id="app">
    <h1>todos</h1>
    <div class="wrapper">
      <Header
        @onSelectAll="handleSelectAll"
        @onAddItem="handleAddItem"
        :isNotItem="isNotItem"
        :selectAll="selectAll"
      />
      <section>
        <Item
          v-for="item in items"
          :key="item.id"
          :item="item"
          @onSelectItem="handleSelectItem"
          @onDeleteItem="handleDeleteItem"
        />
      </section>
      <Footer />
    </div>
  </div>
</template>

<script>
import Item from "./components/Item.vue";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "App",
  data: function() {
    return {
      items: [
        {
          id: 1,
          value: "123",
          completed: true
        },
        {
          id: 2,
          value: "123",
          completed: false
        }
      ]
    };
  },
  components: { Item, Header, Footer },
  methods: {
    handleSelectItem(id) {
      this.items = this.items.map(item => {
        if (item.id === id) {
          return { ...item, ...{ completed: !item.completed } };
        }
        return item;
      });
    },
    handleSelectAll(isSelectAll) {
      this.items = this.items.map(item => ({
        ...item,
        ...{ completed: isSelectAll }
      }));
    },
    handleDeleteItem(itemId) {
      this.items = this.items.filter(item => item.id !== itemId);
    },
    handleAddItem(value) {
      this.items.push({
        id: Math.random(),
        value,
        completed: false
      });
    }
  },
  computed: {
    isNotItem: function() {
      return this.items.length === 0;
    },
    selectAll: function() {
      return this.items.some(item => item.completed === true);
    }
  }
};
</script>

<style>
body {
  background: #f5f5f5;
}

html {
  box-sizing: border-box;
}
*,
*:before,
*:after {
  box-sizing: inherit;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  text-align: center;
}

.wrapper {
  background-color: white;
  max-width: 500px;
  margin: 0 auto;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);
}
</style>
