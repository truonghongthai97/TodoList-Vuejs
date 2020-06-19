<template>
  <div class="wrapper-item">
    <div class="item-left">
      <div
        :class="['wrapper-check', { 'wrapper-check__checked': item.completed }]"
        @click="handleCheck(item.id)"
      >
        <font-awesome-icon
          icon="check"
          :class="{ 'ic-check': true, 'ic-visable': item.completed }"
        />
      </div>
      <p>{{ item.value }}</p>
    </div>
    <div>
      <font-awesome-icon
        icon="times"
        class="ic-delete"
        @click="handleDeleteItem(item.id)"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "Item",
  props: {
    item: Object
  },
  data: function() {
    return {};
  },
  methods: {
    handleCheck(itemId) {
      this.$emit("onSelectItem", itemId);
    },
    handleDeleteItem(itemId) {
      this.$emit("onDeleteItem", itemId);
    }
  }
};
</script>

<style>
.wrapper-item {
  display: flex;
  align-items: center;
  padding: 0px 15px;
}

.wrapper-check {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 5px;
  margin-right: 20px;
  border-radius: 50%;
  border: 0.5px solid #bbbbbb;
  width: 30px;
  height: 30px;
  cursor: pointer;
}

.wrapper-check__checked {
  border-color: #26b90059;
}

.ic-check {
  visibility: hidden;
}

.ic-visable {
  color: #26b90073;
  visibility: visible;
}
.item-left {
  flex-grow: 1;
  display: flex;
  align-items: center;
}

.ic-delete {
  color: #cc9a9a;
  display: none;
  cursor: pointer;
  font-size: 20px;
}

.wrapper-item:hover .ic-delete {
  display: block;
}
</style>
