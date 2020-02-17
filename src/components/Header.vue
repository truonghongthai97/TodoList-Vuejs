<template>
  <header>
    <div @click="handleClickSelectAll">
      <font-awesome-icon
        icon="chevron-down"
        :class="{'switch-selection': selectAll, 'hidden-icon': isNotItem, 'select-all': leastOneCompletedItem}"
      />
    </div>
    <input
      type="text"
      placeholder="What needs to be done?"
      v-model="textInput"
      @keyup.enter="handleAddItem"
    />
  </header>
</template>

<script>
export default {
  name: "Header",
  props: {
    isNotItem: {
      default: false
    },
    leastOneCompletedItem: {
      default: false
    }
  },
  data: function() {
    return { isSelectAll: false, textInput: "", lengthItem: Number };
  },
  methods: {
    handleClickSelectAll() {
      this.isSelectAll = !this.isSelectAll;
      this.$emit("onSelectAll", this.isSelectAll);
    },
    handleAddItem(event) {
      console.log("TCL: handleAddItem -> this._uid", this._uid);
      this.$emit("onAddItem", event.target.value);
      this.textInput = "";
    }
  },
  computed: {
    selectAll: function() {
      return this.isSelectAll;
    }
  }
};
</script>

<style scoped>
header {
  display: flex;
  align-items: center;
  background: white;
  padding: 5px 16px;
}

.switch-selection {
  color: #bbbbbb;
  font-size: 20px;
}
.switch-selection:hover {
  cursor: pointer;
}

.select-all {
  color: black;
}

input {
  display: block;
  width: 100%;
  padding: 5px 16px;
  border: none;
  font-size: 20px;
}

input:focus {
  outline: none;
}

.hidden-icon {
  visibility: hidden;
}
</style>


