<template>
  <div id="app">
    <h1>Pig Ground</h1>
    <add-pig @pig-add="addPig"></add-pig>
    <h2 id="list-eatting">{{listEatting}}</h2>
    <ul aria-labelledby="list-finished" class="stack-large">
      <li v-for="littlePig in Pigs" :key="littlePig.id">
        <one-pig :selfIntroduce=littlePig.selfIntroduce :eat=littlePig.eat :id=littlePig.id @checkbox-changed="updateEatStatus(littlePig.id)"></one-pig> 
        <button class="btn" @click="Pigs.pop(littlePig)">Sell</button>
      </li>
    </ul>
  </div>
</template>

<script>
import OnePig from './components/OnePig'
import AddPig from './components/AddPig'
import uniqueId from "lodash.uniqueid";

export default {
  name: 'App',
  components: {
    OnePig,
    AddPig
  },
  data() {
    return {
      Pigs: [
        { id: uniqueId("pig-"), selfIntroduce: "I'm a happy little pig", eat: false },
        {
          id: uniqueId("pig-"),
          selfIntroduce: "I'm a strong little pig",
          eat: true,
        },
        { id: uniqueId("pig-"), selfIntroduce: "I'm a fat little pig", eat: true },
        { id: uniqueId("pig-"), selfIntroduce: "I'm a beautiful little pig", eat: false },
      ],
    }
  },
  methods: {
    addPig(selfIntroduce) {
      this.Pigs.push({id:uniqueId('pig-'), eat: true, selfIntroduce: selfIntroduce})
    }, 
    updateEatStatus(pigId) {
      const pigUpdate = this.Pigs.find((littlePig) => littlePig.id === pigId)
      pigUpdate.eat = !pigUpdate.eat
    }
  },
  //实时计算正在吃饭的小猪数量
  computed: {
      listEatting() {
        const eattingPigs = this.Pigs.filter((pig) => pig.eat).length
        return `${eattingPigs} out of ${this.Pigs.length} pigs is eatting.`
      }
    }
}
</script>

<style>
  /* 全局样式 */
  .btn {
    padding: 0.8rem 1rem 0.7rem;
    border: 0.2rem solid #4d4d4d;
    cursor: pointer;
    text-transform: capitalize;
  }
  .btn__danger {
    color: #fff;
    background-color: #ca3c3c;
    border-color: #bd2130;
  }
  .btn__filter {
    border-color: lightgrey;
  }
  .btn__danger:focus {
    outline-color: #c82333;
  }
  .btn__primary {
    color: #fff;
    background-color: #000;
  }
  .btn-group {
    display: flex;
    justify-content: space-between;
  }
  .btn-group > * {
    flex: 1 1 auto;
  }
  .btn-group > * + * {
    margin-left: 0.8rem;
  }
  .label-wrapper {
    margin: 0;
    flex: 0 0 100%;
    text-align: center;
  }
  [class*="__lg"] {
    display: inline-block;
    width: 100%;
    font-size: 1.9rem;
  }
  [class*="__lg"]:not(:last-child) {
    margin-bottom: 1rem;
  }
  @media screen and (min-width: 620px) {
    [class*="__lg"] {
      font-size: 2.4rem;
    }
  }
  .visually-hidden {
    position: absolute;
    height: 1px;
    width: 1px;
    overflow: hidden;
    clip: rect(1px 1px 1px 1px);
    clip: rect(1px, 1px, 1px, 1px);
    clip-path: rect(1px, 1px, 1px, 1px);
    white-space: nowrap;
  }
  [class*="stack"] > * {
    margin-top: 0;
    margin-bottom: 0;
  }
  .stack-small > * + * {
    margin-top: 1.25rem;
  }
  .stack-large > * + * {
    margin-top: 2.5rem;
  }
  @media screen and (min-width: 550px) {
    .stack-small > * + * {
      margin-top: 1.4rem;
    }
    .stack-large > * + * {
      margin-top: 2.8rem;
    }
  }
  /* 全局样式结束 */
  #app {
    background: #fff;
    margin: 2rem 0 4rem 0;
    padding: 1rem;
    padding-top: 0;
    position: relative;
    box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 2.5rem 5rem 0 rgba(0, 0, 0, 0.1);
  }
  @media screen and (min-width: 550px) {
    #app {
      padding: 4rem;
    }
  }
  #app > * {
    max-width: 50rem;
    margin-left: auto;
    margin-right: auto;
  }
  #app > form {
    max-width: 100%;
  }
  #app h1 {
    display: block;
    min-width: 100%;
    width: 100%;
    text-align: center;
    margin: 0;
    margin-bottom: 1rem;
  }
</style>

