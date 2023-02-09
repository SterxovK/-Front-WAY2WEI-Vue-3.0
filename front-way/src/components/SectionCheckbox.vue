<template>
  <div class="section-checkbox">
    <div class="checkbox-row">
      <label class="wrapper">
        Заполните информацию о компании
        <input
          class="checkbox"
          type="checkbox"
          :checked="isChecked"
          :value="value"
          @change="updateInput"
        />
        <span class="checkmark"></span>
      </label>
      <button class="button">Перейти</button>
    </div>
    <p class="checkbox-info">
      Это создаст более привлекательный образ компании и позволит вашим
      сотрудникам убедиться, что все идет как нужно
    </p>
    <div class="checkbox-row">
      <label class="wrapper">
        Создайте сотрудника
        <input
          class="checkbox"
          type="checkbox"
          :checked="isChecked"
          :value="value"
          @change="updateInput"
        />
        <span class="checkmark"></span>
      </label>
      <button class="button">Перейти</button>
    </div>
    <p class="checkbox-info">
      Сотрудник - это человек, который будет проходит обучение. Вы можете
      пропустить этот шаг если хотите протестировать систему самостоятельно
    </p>
  </div>
</template>

<script>

export default {
  name: 'SectionCheckbox',
  model: {
    prop: 'modelValue',
    event: 'change'
  },
  props: {
    value: { type: String },
    modelValue: { default: '' },
    label: { type: String, required: true },
    trueValue: { default: true },
    falseValue: { default: false }
  },
  computed: {
    isChecked () {
      if (this.modelValue instanceof Array) {
        return this.modelValue.includes(this.value)
      }
      // Note that `true-value` and `false-value` are camelCase in the JS
      return this.modelValue === this.trueValue
    }
  },
  methods: {
    updateInput (event) {
      const isChecked = event.target.checked
      if (this.modelValue instanceof Array) {
        const newValue = [...this.modelValue]
        if (isChecked) {
          newValue.push(this.value)
        } else {
          newValue.splice(newValue.indexOf(this.value), 1)
        }
        this.$emit('change', newValue)
      } else {
        this.$emit('change', isChecked ? this.trueValue : this.falseValue)
      }
    }
  }
}
</script>

<style>
/* Customize the label (the wrapper) */
.wrapper {
  display: block;
  position: relative;
  padding-left: 35px;
  margin-bottom: 6px;
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  font-size: 1rem;
  font-weight: 900;
}
/* Hide the browser's default checkbox */
.wrapper input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}
/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 21px;
  width: 21px;
  border-radius: 2px;
  background-color: #eee;
  border: 1px solid #ccc;
}
/* On mouse-over, add a grey background color */
.wrapper:hover input ~ .checkmark {
  background-color: #ccc;
}
/* When the checkbox is checked, add a blue background */
.wrapper input:checked ~ .checkmark {
  border-color: #42b983;
}
/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}
/* Show the checkmark when checked */
.wrapper input:checked ~ .checkmark:after {
  display: block;
}
/* Style the checkmark/indicator */
.wrapper .checkmark:after {
  left: 7px;
  top: 0px;
  width: 7px;
  height: 15px;
  border: solid #42b983;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
.section-checkbox {
  width: 90%;
  margin: auto;
  padding-top: 40px;
}

.checkbox-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 0 10px 0;
  border-top: 1px solid rgba(0, 0, 0, 0.1);
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
}

.label {
  font-size: 1rem;
  font-weight: 900;
  padding-left: 10px;
}

.checkbox-info {
  margin: 0;
  padding: 10px;
  font-size: 0.8rem;
  text-align: left;
  padding-left: 10px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
}

.button {
  font-size: 1rem;
  padding: 0.5rem 1rem;
  border: none;
  outline: none;
  cursor: pointer;
  background-color: #42b983;
  color: white;
}
</style>
