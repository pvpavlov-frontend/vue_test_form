<template>
  <div>
    <div class="wrapper">
      <div
        v-for="(value, index) in arrayOfValues"
        :key="index"
        class="wrapper-fraction"
      >
        <fraction-component
          @onValue="onValue($event, index)"
          @onRemove="onRemove(index)"
          @valueInput="setData($event, index)"
          :numeratorValue="Number(value.numerator)"
          :denominatorValue="Number(value.denominator)"
        />
        <span
          v-if="index < arrayOfValues.length-1"
          class="symbol"
        >
        +
        </span>
        <span
          class="symbol resalt"
          v-else
        >
        = {{ getSum }}
        </span>
      </div>
    </div>
  <button 
    @click="onAddElement"
    title="создать новый элемент"
  >
    add new element
  </button>
  </div>
</template>

<script>
import FractionComponent from './components/FractionComponent'

export default {
  components: { FractionComponent },
  data () {
    return {
      arrayOfValues: [
        {
          numerator: null,
          denominator: null,
          total: null
        },
        {
          numerator: null,
          denominator: null,
          total: null
        }
      ]
    }
  },
  computed: {
    getSum() {
      return this.arrayOfValues.reduce((a, { total }) => a + total, 0, 2).toFixed(2)
    }
  },
  methods: {
    onValue(value, index) {
      this.arrayOfValues[index].total = value
    },
    setData (value, index) {
      Object.assign(this.arrayOfValues[index], value)
    },
    onAddElement () {
      if (this.arrayOfValues.length < 5) {
        this.arrayOfValues.push(
          {
            numerator: null,
            denominator: null,
            total: null
          }
        )
      }
    },
    onRemove (index) {
      if(this.arrayOfValues.length > 2) {
        this.arrayOfValues.splice(index, 1)
      }
    }
  }
}
</script>

<style scoped lang="scss">
  .wrapper {
    display: flex;
    justify-content: center;
    margin: 140px auto 0;
    &-fraction {
      display: flex;
      align-items: center;
    }
    .symbol {
      margin: 5px;
      color: #484848;
      font-size: 40px;
      &.resalt{
        font-size: 20px;
      }
    }
  }
  button {
    display: flex;
    margin: 20px auto 0; 
    border: 1px solid #bcbcb9;
    color: #747878;
    border-radius: 3px;
    font-family: 'Times New Roman', Times, serif;
    font-size: 20px;
    padding: 10px 20px;
    cursor: pointer;
  }
</style>