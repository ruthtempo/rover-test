
<template>
  <div id="app">
    <div>
      <table>
        <tr v-for="row in rowArray" :key="row">
          <td v-for="col in columnArray" :key="col">
            <p v-if="parseInt(x) === col && parseInt(y) === row">
              ({{ x }}, {{ y }}), {{ orientation }}
            </p>
          </td>
        </tr>
      </table>
    </div>
    <div>
      <div>
        <div>
          <h4>Modify Grid</h4>
          <label for="width">cols</label>
          <input type="number" id="width" v-model="columns" />
          <label for="length">rows</label>
          <input type="number" id="length" v-model="rows" />
        </div>
        <div>
          <h4>current position</h4>
          <div :style="{ color: this.isvalid ? 'green' : 'red' }">
            ({{ x }}, {{ y }}), {{ orientation }}
            {{ valid }}
            {{ columnArray }}
          </div>
        </div>
        <h4>Commands</h4>
        <ul>
          <li>L : turn left</li>
          <li>R : turn right</li>
          <li>A : move foward</li>
        </ul>
      </div>
      <h4>Enter Coordinates</h4>
      <label for="x"> x</label>
      <input type="number" id="x" placeholder="enter number" v-model="x" />
      <label for="y">y</label>
      <input type="number" id="y" placeholder="enter number" v-model="y" />
      <label for="coord">Orientation</label>
      <input
        type="text"
        id="coord"
        placeholder="N, S, W or E"
        v-model="orientation"
      />
      <input type="text" placeholder="enter command" v-model="input" />

      <button @click="move(input)">click</button>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      columns: 6,
      rows: 5,
      orientation: "N",
      x: 1,
      y: 1,
      isvalid: true,
      input: "",
      dynamicrows: [],
      dynamiccolumns: [],
    };
  },
  computed: {
    columnArray: function () {
      this.dynamiccolumns = [];
      for (let i = 0; i < this.columns; i++) {
        this.dynamiccolumns.push(i);
      }
      return this.dynamiccolumns;
    },
    rowArray: function () {
      this.dynamicrows = [];
      for (let j = 0; j < this.rows; j++) {
        this.dynamicrows.push(j);
      }
      return this.dynamicrows;
    },
    valid: function () {
      if (
        this.x > this.columns - 1 ||
        this.x < 0 ||
        this.y > this.rows - 1 ||
        this.y < 0
      ) {
        return (this.isvalid = false);
      } else {
        return (this.isvalid = true);
      }
    },
  },
  methods: {
    checkIfValid() {
      if (
        this.x > this.columns - 1 ||
        this.x < 0 ||
        this.y > this.rows - 1 ||
        this.y < 0
      ) {
        this.isvalid = false;
      } else {
        this.isvalid = true;
      }
    },
    move(commands) {
      commands.split("").forEach((command) => {
        if (command === "A") {
          this.moveFoward();
        } else if (command === "L") {
          this.turnLeft();
        } else {
          this.turnRight();
        }
      });
      // this.checkIfValid();
    },
    turnLeft() {
      if (this.orientation === "N") {
        this.orientation = "W";
      } else if (this.orientation === "W") {
        this.orientation = "S";
      } else if (this.orientation === "S") {
        this.orientation = "E";
      } else if (this.orientation === "E") {
        this.orientation = "N";
      }
    },
    turnRight() {
      if (this.orientation === "N") {
        this.orientation = "E";
      } else if (this.orientation === "W") {
        this.orientation = "N";
      } else if (this.orientation === "S") {
        this.orientation = "W";
      } else if (this.orientation === "E") {
        this.orientation = "S";
      }
    },
    moveFoward() {
      if (this.orientation === "N") {
        this.y = this.y + 1;
      } else if (this.orientation === "S") {
        this.y = this.y - 1;
      } else if (this.orientation === "E") {
        this.x = this.x + 1;
      } else if (this.orientation === "W") {
        this.x = this.x - 1;
      }
    },
  },
};
</script>
<style scoped>
td {
  border: 1px solid black;
  height: 50px;
  width: 80px;
}
</style>


