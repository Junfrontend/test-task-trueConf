<template>
  <div class="wrapper">
    <h1>{{ msg }}</h1>
    <div class="traffic-light">
      <svg
        version="1.1"
        id="Capa_1"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        x="0px"
        y="0px"
        viewBox="0 0 452.8 452.8"
        style="enable-background: new 0 0 452.8 452.8"
        xml:space="preserve"
      >
        <path
          style="fill: #676d79"
          d="M315.8,354.4c0,17.2-14.4,31.6-31.6,31.6h-116c-17.2,0-31.6-14.4-31.6-31.6V38
	c0-17.2,14.4-31.6,31.6-31.6h116c17.2,0,31.6,14.4,31.6,31.6V354.4z"
        />
        <path
          style="fill: #898989"
          d="M163.8,354.4V38c0-17.2,14.4-31.6,31.6-31.6h-27.6c-17.2,0-31.6,14.4-31.6,31.6v316.4
	c0,17.2,14.4,31.6,31.6,31.6h27.6C178.2,386,163.8,371.6,163.8,354.4z"
        />
        <circle v-bind:style="colors.redPlace" cx="226.2" cy="86.4" r="44.4" />
        <circle
          v-bind:style="colors.yellowPlace"
          cx="226.2"
          cy="197.2"
          r="44.4"
        />
        <circle v-bind:style="colors.greenPlace" cx="226.2" cy="308" r="44.4" />
        <g>
          <path
            style="fill: #424953"
            d="M284.2,0h-116c-20.8,0-38,17.2-38,38v316.4c0,20.8,17.2,38,38,38h24.4v54c0,3.6,2.8,6.4,6.4,6.4
		c3.6,0,6.4-2.8,6.4-6.4V392h44.4v54.4c0,3.6,2.8,6.4,6.4,6.4c3.6,0,6.4-2.8,6.4-6.4V392h22c20.8,0,38-17.2,38-38V38
		C322.2,17.2,305,0,284.2,0z M309.4,354.4c0,14-11.2,25.2-25.2,25.2h-116c-14,0-25.2-11.2-25.2-25.2V38c0-14,11.2-25.2,25.2-25.2
		h116c14,0,25.2,11.2,25.2,25.2V354.4z"
          />
          <path
            style="fill: #424953"
            d="M226.2,36c-28,0-50.8,22.8-50.8,50.8s22.8,50.8,50.8,50.8S277,114.8,277,86.8
		C277,58.4,254.2,36,226.2,36z M226.2,124.4c-20.8,0-38-17.2-38-38s17.2-38,38-38s38,17.2,38,38S247,124.4,226.2,124.4z"
          />
          <path
            style="fill: #424953"
            d="M226.2,146.4c-28,0-50.8,22.8-50.8,50.8s22.8,50.8,50.8,50.8s50.8-22.8,50.8-50.8
		S254.2,146.4,226.2,146.4z M226.2,235.2c-20.8,0-38-17.2-38-38s17.2-38,38-38s38,17.2,38,38S247,235.2,226.2,235.2z"
          />
          <path
            style="fill: #424953"
            d="M226.2,257.2c-28,0-50.8,22.8-50.8,50.8c0,28,22.8,50.4,50.8,50.4s50.8-22.8,50.8-50.8
		C277,280,254.2,257.2,226.2,257.2z M226.2,346c-20.8,0-38-17.2-38-38s17.2-38,38-38s38,17.2,38,38S247,346,226.2,346z"
          />
        </g>
      </svg>
    </div>
    <div class="time">До смены синала осталось {{ timeCounter }} секунд</div>
    <div class="control-buttons">
      <button class="control-buttons__turn-off" @click.prevent="turnLightOff">
        Выключить светофор
      </button>
      <button class="control-buttons__start" @click.prevent="colorsLoop">
        Включить светофор
      </button>
    </div>
  </div>
</template>

<script>
let timeId;
export default {
  name: "trafficLight",
  props: {
    msg: String,
  },

  data() {
    return {
      colors: {
        red: "fill:#EE6E55;",
        yellow: "fill:#FFCE57;",
        green: "fill:#A1C969;",
        basic: "fill:#dddddd;",
        redPlace: "fill:#dddddd",
        yellowPlace: "fill:#dddddd",
        greenPlace: "fill:#dddddd",
      },
      timer: {
        //time in ms
        redLight: 10000,
        yellowLight: 3000,
        greenLight: 15000,
      },
      timeCounter: "",
    };
  },

  methods: {
    turnLightOff() {
      (this.colors.redPlace = this.colors.basic),
        (this.colors.yellowPlace = this.colors.basic),
        (this.colors.greenPlace = this.colors.basic);
      clearInterval(timeId);
      this.timeCounter = "";
    },
    timeChecker(currentTimer, color) {
      this.timeCounter = currentTimer / 1000;
      timeId = setInterval(() => {
        this.timeCounter--;
        if (this.timeCounter < 4) {
          if (color === this.colors.red) {
            this.colors.redPlace = this.colors.basic;
            setTimeout(() => {
              this.colors.redPlace = this.colors.red;
            }, 500);
          }
          if (color === this.colors.yellow) {
            this.colors.yellowPlace = this.colors.basic;
            setTimeout(() => {
              this.colors.yellowPlace = this.colors.yellow;
            }, 500);
          }
          if (color === this.colors.green) {
            this.colors.greenPlace = this.colors.basic;
            setTimeout(() => {
              this.colors.greenPlace = this.colors.green;
            }, 500);
          }
        }
      }, 1000);

      setTimeout(() => {
        clearInterval(timeId);
      }, currentTimer - 1000);
    },
    turnRed() {
      this.colors.redPlace = this.colors.red;
      this.timeChecker(this.timer.redLight, this.colors.redPlace);
      setTimeout(() => {
        this.colors.redPlace = this.colors.basic;
      }, this.timer.redLight);
    },
    turnYellow() {
      this.colors.yellowPlace = this.colors.yellow;
      this.timeChecker(this.timer.yellowLight, this.colors.yellow);
      setTimeout(() => {
        this.colors.yellowPlace = this.colors.basic;
      }, this.timer.yellowLight);
    },
    turnGreen() {
      this.colors.greenPlace = this.colors.green;
      this.timeChecker(this.timer.greenLight, this.colors.green);
      setTimeout(() => {
        this.colors.greenPlace = this.colors.basic;
      }, this.timer.greenLight);
    },
    colorsLoop() {
      this.turnLightOff();
      this.turnRed();
      setTimeout(() => {
        this.turnYellow();
      }, this.timer.redLight);
      setTimeout(() => {
        this.turnGreen();
      }, this.timer.redLight + this.timer.yellowLight);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.traffic-light {
  height: 500px;
  width: auto;
}

svg {
  height: 100%;
}

.time {
  margin-top: 20px;
}

.control-buttons {
  margin-top: 30px;
}

.control-buttons__turn-off {
  color: #ffffff;
  padding: 10px;
  background: #f06161;
  border: none;
  margin-right: 20px;
}

.control-buttons__start {
  color: #ffffff;
  padding: 10px;
  background: #68bd4e;
  border: none;
}
</style>
