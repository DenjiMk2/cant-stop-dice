<template>
  <div class="MainPage">
    <div class="InputDice">
      <ul>
        <li v-for="dice in dices" v-bind:key="dice.faceNumber">
          <button v-on:click="selectDice(dice)">
            {{dice.faceNumber}}
          </button>
        </li>
      </ul>
      <button v-on:click="placedDices=[]">
        リセット
      </button>
    </div>
    <div class="PlacedDice">
      <ul>
        <li v-for="dice in placedDices" v-bind:key="dice.faceNumber">
          {{dice.faceNumber}}
        </li>
      </ul>
    </div>
    <div class="CombinationDices">
      <ul>
        <li v-for="combination in combinationDices" v-bind:key="combination[0][0]">
          ({{combination[0].reduce((a,b)=>a+b)}},{{combination[1].reduce((a,b)=>a+b)}})
        </li>
      </ul>
    </div>
    <div class="GoMap">
      <ul>
        <li v-for="i in [2,3,4,5,6,7,8,9,10,11,12]" v-bind:key="i">
          <div v-bind:class="{active:this.isCanGoNumber(i)}">{{i}}</div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MainPage',
  data() {
    return {
      dices: [
        { faceNumber: 1 },
        { faceNumber: 2 },
        { faceNumber: 3 },
        { faceNumber: 4 },
        { faceNumber: 5 },
        { faceNumber: 6 },
      ],
      placedDices: [
        { faceNumber: 3 },
        { faceNumber: 4 },
        { faceNumber: 2 },
        { faceNumber: 5 },
      ],
      combinationDices: [
        [[3, 4], [2, 5]],
        [[3, 2], [4, 5]],
        [[3, 5], [4, 2]],
      ],
    };
  },
  methods: {
    selectDice(dice) {
      if (this.placedDices.length >= 4) return;
      this.placedDices.push(dice);
      if (this.placedDices.length >= 4) this.combination();
    },
  },
  combination() {

  },
  isCanGoNumber(num) {
    const numberSet = new Set();
    this.combinationDices.forEach((a) => {
      this.numberSet.add(a[0]);
      this.numberSet.add(a[1]);
    });
    return numberSet.has(num);
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.active {
  color:red;
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
