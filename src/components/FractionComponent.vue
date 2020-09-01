<template>
  <div class="fraction">
    <div
      class="fraction-remove"
      @click="$emit('onRemove')"
      title="удалить текущий элемент"
    >
      &times;
    </div>
    <input
      type="text"
      class="fraction-field"
      v-model="numerator"
      @input="onInput($event.target.value, 'numerator')"
      maxlength="2"
    >
    <div class="fraction-line"></div>
    <input
      type="text"
      class="fraction-field"
      v-model="denominator"
      @input="onInput($event.target.value, 'denominator')"
      maxlength="2"
    >
  </div>
</template>

<script>
  export default {
    props: {
        numeratorValue: {
            type: Number,
            default: 0
        },
        denominatorValue: {
            type: Number,
            default: 0
        },
    },
    data() {
      return {
        numerator: null,
        denominator: null
      }
    },
    computed: {
      getValue() {
        if(this.numerator > 0 && this.denominator > 0 ) {
            return Number((this.numerator / this.denominator).toFixed(3))
        } else return 0
      }
    },
    watch: {
      getValue: {
        handler(value) {
            this.$emit('onValue', value)
        }
      },
      numeratorValue: {
        handler(value) {
            this.numerator = value
        }
      },
      denominatorValue: {
        handler(value) {
            this.denominator = value
        }
      },
    },
    methods: {
      onInput(interValue, field) {
        this[field] = interValue.replace(/[^\d]/g,'')
        this.$emit('valueInput', { 
            [field]: this[field]
        });
      }
    }
  }
</script>

<style scoped lang="scss">
.fraction {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 40px;
  margin: 10px;
  position: relative;
  &-field {
    padding: 5px;
    width: 23px;
    display: block;
    text-align: center;
    background: #f5f0f5;
    border: 1px solid #b6b5b6;
    line-height: 20px;
  }
  &-line {
    margin: 5px;
    width: 60px;
    height: 2px;
    background: #484848;
  }
  &-remove {
    cursor: pointer;
    position: absolute;
    right: -11px;
    top: -14px;
    background: #ff4d4d;
    color: white;
    border-radius: 50%;
    width: 15px;
    height: 15px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
}

</style>