<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>choose your options and click the "Find Names" button below</p>
    <div class="options-container">
      <Option v-for="option in optionArray" :key="option.title" :option="option" :options="options"/>
      <button class="select-btn" @click="showNames">Find Names</button>
    </div>
    <div class="result-box">
        <div v-for="(name,index) in selectedNames" :key="index">{{ name }}</div>
      </div>
  </div>
</template>

<script lang="ts" setup>
import { Gender, Popularity, Length, names } from '@/data'

interface OptionsState {
  gender: Gender,
  popularity: Popularity,
  length: Length
}
// options
const options = reactive<OptionsState>({
  gender: Gender.BOY,
  popularity: Popularity.TRENDY,
  length: Length.LONG
})

const selectedNames = ref<string[]>([])

const showNames = () => {
  const filterNames = names
    .filter((name) => name.gender === options.gender)
    .filter((name) => name.popularity === options.popularity)
    .filter((name) => {
      if(options.length === Length.ALL) return true
      else return name.length === options.length
    })
  selectedNames.value = filterNames.map(name => name.name)
}
// array of option
const optionArray = [
  {
    title: '1) Choose a gender',
    category: 'gender',
    buttons: [Gender.BOY, Gender.UNISEX, Gender.GIRL]
  },
  {
    title: '2) Choose the name popularity',
    category: 'popularity',
    buttons: [Popularity.TRENDY, Popularity.UNIQUE]
  },
  {
    title: "3) Choose name's length",
    category: 'length',
    buttons: [Length.SHORT, Length.ALL, Length.LONG]
  }
]

</script>

<style lang="scss" scoped>
.container {
  font-family: Arial, Helvetica, sans-serif;
  text-align: center;

  .options-container {
    background-color: rgb(223, 200, 200);
    width: 50%;
    margin: 25px auto 0;
    border-radius: 15px;
    padding: 15px 0 20px;

    .option-container {
      margin-bottom: 20px;

      button {
        background-color: #fff;
        outline: 2px solid rgb(233, 29, 29);
        border: 0;
        font-size: 16px;
        padding: 5px 20px;
        cursor: pointer;

        &:first-child {
          border-radius: 15px 0 0 15px;
        }

        &:last-child {
          border-radius: 0 15px 15px 0;
        }
        &.active {
          background-color: rgb(233, 29, 29);
          color: #fff;
        }
      }

    }
    .select-btn {
      margin: 15px 0;
      border-radius: 15px;
      padding: 8px 20px;
      font-size: 16px;
      border: none;
      color: #fff;
      background-color: rgb(233, 29, 29);
      cursor: pointer;
      &:hover {
        background-color: lighten(rgb(233, 29, 29), 10);
      }
    }
  }
  .result-box {
      width: 80%;
      display: flex;
      justify-content: center;
      margin: auto;
      > div {
        font-size: 16px;
        margin: 8px;
      }
    }
}
</style>