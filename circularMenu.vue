<template>
  <div>
    <div :style="getStyle()">
      <transition v-for="(button, index) in buttonList"
                  :key="index"
                  name="myCircularOpen"
                  appear
                  before-appear="circle-spinal-circular-menucenter"
                  appear-class="circle-spinal-circular-menu"
                  appear-to-class="opencircle-spinal-circular-menu"
                  leave-to-class="closecircle-spinal-circular-menu"
                  :duration="{ enter: 500, leave: 800 }">
        <md-button :style="getButtonStyle(index)"
                   @click="button.action(options)"
                   style="margin: unset;pointer-events: auto; height: 40px"
                   class="md-icon-button"
                   v-tooltip="button.label">
          <md-icon :style="getIconColor(index)">{{button.buttonCfg.icon}}</md-icon>
        </md-button>
      </transition>
    </div>
    <!-- <md-button @click="activateMode"
               :style="color"
               class="myButton md-icon-button">
    </md-button> -->

  </div>
</template>


<script>
export default {
  name: "circularmenu",
  data() {
    return {
      buttonTab: [],
      data: {},
      color: {
        background: "#2D3D93"
      }
      // activateModeBool: true
    };
  },
  components: {},
  props: ["buttonList", "x", "y", "options"],
  methods: {
    // activateMode: function() {
    //   if (this.activateModeBool) {
    //     this.activateModeBool = false;
    //     this.color.background = "#F68204";
    //     this.data = {};
    //   } else {
    //     this.activateModeBool = true;
    //     this.color.background = "#2D3D93";
    //   }
    // },
    getStyle: function() {
      if (this.buttonList.length > 0) {
        return {
          position: "absolute",
          left: this.x - 75 + "px",
          top: this.y - 75 + "px",
          height: "150px",
          width: "150px",
          "pointer-events": "none",
          opacity: 1,
          "-webkit-transform": "scale(1)",
          "-moz-transform": "scale(1)",
          transform: "scale(1)",

          "-webkit-transition": "all 0.4s ease-out",
          "-moz-transition": "all 0.4s ease-out",
          transition: "all 0.4s ease-out"
        };
      } else {
        return {
          position: "absolute",
          opacity: 0,

          "-webkit-transform": "scale(0)",
          "-moz-transform": "scale(0)",
          transform: "scale(0)"
        };
      }
    },
    getButtonStyle: function(index) {
      let myStyle = {
        left: "",
        top: "",
        "background-color": this.buttonList[index].buttonCfg.backgroundColor,
        position: "absolute",
        "-webkit-transition": "all 0.4s ease-out",
        "-moz-transition": "all 0.4s ease-out",
        transition: "all 0.4s ease-out"
      };

      let nbrElement = this.buttonList.length;
      let radius = 60;
      let nbr = (2 * Math.PI) / nbrElement;
      if (nbrElement >= 7) {
        let result = nbrElement * 2 * 25;
        radius = result / (2 * Math.PI);
      }
      let axeX = (radius * Math.cos(nbr * index)).toFixed(1);
      let axeY = (radius * Math.sin(nbr * index)).toFixed(1);
      myStyle.left = "calc(50% + " + (axeX - 20) + "px)";
      myStyle.top = "calc(50% + " + (axeY - 20) + "px)";
      return myStyle;
    },
    getIconColor(index) {
      let color;
      try {
        color = this.buttonList[index].buttonCfg.fontColor;
      } catch (e) {
        color = "white";
      }
      return { color };
    }
  }
};
</script>

<style>
.myButton {
  margin: unset;
  pointer-events: auto;
  background: red;
  height: 20px;
  right: 38px;
  min-width: 20px;
  width: 20px;
  position: absolute;
  top: 68px;
}

.circle-spinal-circular-menu {
  opacity: 0;

  -webkit-transform: scale(0);
  -moz-transform: scale(0);
  transform: scale(0);

  -webkit-transition: all 0.4s ease-out;
  -moz-transition: all 0.4s ease-out;
  transition: all 0.4s ease-out;
}

.opencircle-spinal-circular-menu {
  opacity: 1;

  -webkit-transform: scale(1);
  -moz-transform: scale(1);
  transform: scale(1);
}

.closecircle-spinal-circular-menu {
  opacity: 0;

  -webkit-transform: scale(0);
  -moz-transform: scale(0);
  transform: scale(0);
}
.circle-spinal-circular-menucenter {
  left: "0";
  top: "0";
  position: "absolute";
}
</style>
