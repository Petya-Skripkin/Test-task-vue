<template>
  <div class="select" :class="isCard && 'cart'">
    <slot></slot>
    <span v-if="count !== undefined && maxCount" class="selected">
      selected: {{count}} / {{maxCount}}
    </span>
  </div>
</template>

<script>
export default {
  name: 'MainSelect',
  props: ['count', 'maxCount', 'isCard']
}
</script>

<style scoped>
.select {
  flex: 1;
  height: 100%;
  display: flex;
  flex-direction: column;
  /* justify-content: flex-start;
    flex-wrap: wrap; */
  gap: 10px;
  padding: 10px 15px;
  border: 1.5px solid #6a6a6a;
  border-radius: 5px;
}

.select.cart {
  align-items: center;
  flex-direction: row;
  flex-wrap: wrap;
}

.selected {
  width: 100%;
  display: inline-block;
  text-align: center;
  align-self: flex-end;
  justify-self: center;
  margin: 10px 0;
}
</style>

