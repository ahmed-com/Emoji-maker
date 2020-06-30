<template>
  <svg :width="width" :height="height" :style="{backgroundColor}">
    <g 
      :transform="emojiPosition"
      >
        <circle 
          :r="faceRadius"
          :fill="faceColor"
          stroke="black"
        ></circle>
        <path :transform="mouthPosition" :d="mouthPath" ></path>
        <g
          :transform="eyesPosition"
          >
            <g
              :transform="eyebrowsPosition"
              >
                <rect
                  :width="eyebrowWidth"
                  :height="eyebrowHeight"
                  :x="eyeSpacing-(eyebrowWidth/2)"
                ></rect>
                <rect
                  :width="eyebrowWidth"
                  :height="eyebrowHeight"
                  :x="-eyeSpacing-(eyebrowWidth/2)"
                ></rect>
            </g>
            <circle
              :r="eyeRadius"
              :cx="-eyeSpacing"
              :fill="eyeColor"
            ></circle>
            <circle
              :r="eyeRadius"
              :cx="eyeSpacing"
              :fill="eyeColor"
            ></circle>
        </g>
    </g>
  </svg>
</template>

<script>
  import * as d3 from "d3";
  const arc = d3.arc();

  export default {
    name: 'Emoji',

    props: [
      "width",
      "height",
      "backgroundColor",
      "faceColor",
      "faceRadius",
      "eyeColor",
      "eyeSpacing",
      "eyeYOffset",
      "eyeRadius",
      "eyebrowWidth",
      "eyebrowHeight",
      "eyebrowYOffset",
      "mouthInnerRadius",
      "mouthOuterRadius",
      "mouthStartAngle",
      "mouthEndAngle",
      "mouthYOffset",
      "mouthXOffset"
    ],
    computed : {
      emojiPosition(){
        return `translate(${this.width / 2} , ${this.height / 2})`;
      },
      mouthPosition(){
        return `translate(${this.mouthXOffset}, ${this.mouthYOffset})`;
      },
      eyesPosition(){
        return `translate(${0}, ${-this.eyeYOffset})`;
      },
      eyebrowsPosition(){
        return `translate(${0}, ${-this.eyebrowYOffset})`;
      },
      mouthPath(){
        const vm = this;
        return arc({
          innerRadius: vm.mouthInnerRadius,
          outerRadius: vm.mouthOuterRadius,
          startAngle: vm.mouthStartAngle,
          endAngle: vm.mouthEndAngle,
        });
      }
    }
  }
</script>
