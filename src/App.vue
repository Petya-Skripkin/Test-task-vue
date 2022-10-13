<template>
  <div class="main">
    <div class="block head">
      <MainSelect v-if="multiSelect.length > 0" :count="multiSelect.length" :maxCount="maxCountMultiSelect" :isCard="true">
        <ProductItem v-for="data in multiSelect" :key="data.id" :data="data" @getItem="getLeftItems" :isCard="true" />
      </MainSelect>
      <MainSelect v-else :count="0" :maxCount="maxCountMultiSelect">
        Ничего не выбрано
      </MainSelect>
      <MainSelect v-if="selectOne.length > 0">
        <ProductItem v-for="data in selectOne" :key="data.id" :data="data" @getItem="getRightItem" />
      </MainSelect>
      <MainSelect v-else>
        Ничего не выбрано
      </MainSelect>
    </div>
    <div class="block">
      <MainSelect>
        <ProductItem v-for="data in leftBlockData" :key="data.id" :data="data" :active="isActive(multiSelect, data)"
          @getItem="getLeftItems" />
      </MainSelect>
      <MainSelect>
        <ProductItem v-for="data in rightBlockdata" :key="data.id" :data="data" :active="isActive(selectOne, data)"
          @getItem="getRightItem" />
      </MainSelect>
    </div>
  </div>
</template>

<script>
import ProductItem from "@/components/ProductItem.vue";
import MainSelect from "@/components/MainSelect.vue";
import * as data from "@/mock"

export default {
  name: "App",
  components: { ProductItem, MainSelect },
  data() {
    return {
      leftBlockData: data.LeftBlock,
      rightBlockdata: data.RightBlock,
      multiSelect: [],
      selectOne: [],
      maxCountMultiSelect: 6
    }
  },
  methods: {
    getLeftItems(e) {
      if (this.multiSelect.length < this.maxCountMultiSelect && !this.multiSelect.find(el => el.id === e)) {
        this.multiSelect.push(this.leftBlockData.find(el => el.id === e))
      } else {
        this.multiSelect = this.multiSelect.filter(el => el.id !== e)
      }
    },
    getRightItem(e) {
      if (!this.selectOne.find(el => el.id === e)) {
        this.selectOne.push(this.rightBlockdata.find(el => el.id === e))
        this.selectOne = this.selectOne.filter(el => el.id === e)
      } else {
        this.selectOne.pop()
      }
    },
    isActive(el, item) {
      return el.some(el => el.id === item.id)
    }
  },
}
</script>

<style>
* {
  margin: 0;
  border: 0;
  padding: 0;
  box-sizing: border-box;
}

.main {
  height: 100vh;
  padding: 20px;
}

.block {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 20px;
}

.head {
  height: 30%;
  margin-bottom: 20px;
}

.content {
  display: inline-block;
  width: 100%;
  height: 100%;
}
</style>
