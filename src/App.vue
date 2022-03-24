
<template>
  <div id="app">
    <div>
      <table>
        <tr v-for="row in rows" :key="row">
          <td v-for="col in columns" :key="col">
            <p v-if="x === col && y === row">
              ({{ x }}, {{ y }}), {{ orientation }}
            </p>
          </td>
        </tr>
      </table>
    </div>
    <div>
      <div>
        <div>
          <h4>current position</h4>
          <div :style="{ color: this.isvalid ? 'green' : 'red' }">
            ({{ x }}, {{ y }}), {{ orientation }}
            {{ isvalid }}
          </div>
        </div>
        <h4>Commands</h4>
        <ul>
          <li>L : turn left</li>
          <li>R : turn right</li>
          <li>A : move foward</li>
        </ul>
      </div>
      <input type="text" placeholder="enter command" v-model="input" />

      <button @click="move(input)">click</button>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      columns: [],
      rows: [],
      orientation: "N",
      x: 1,
      y: 2,
      isvalid: true,
      input: "",
    };
  },
  created: function () {
    this.createGrid();
  },
  methods: {
    checkIfValid() {
      if (this.x > 10 || this.x < 0 || this.y > 10 || this.y < 0) {
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
      this.checkIfValid();
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
    createGrid() {
      for (let i = 0; i < 10; i++) {
        this.rows.push(9 - i);
        this.columns.push(i);
      }
    },
    locateRover() {
      if (this.column === this.x && this.row === this.z) {
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


