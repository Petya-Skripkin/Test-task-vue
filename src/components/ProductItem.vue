<template>
  <div class="item" :class="active && 'active' || isCard && 'card'" @click="ClickHandler">
    {{data.name}}
  </div>
</template>

<script>

export default {
  name: 'ProductItem',
  props: ['active','data', 'isCard'],
  methods: {
    ClickHandler() {
      this.$emit('getItem', this.data.id)
    }
  }
}
</script>

<style scoped>
.item {
  /* width: calc(100% / 5 - 10px); */
  padding: 10px 15px;
  border: 1.5px solid #00b419;
  border-radius: 5px;
  cursor: pointer;
}

.item.card {
  width: calc(100% / 6 - 10px);
}

.item.active {
  border-color: rgb(255, 183, 0);
}
</style>
