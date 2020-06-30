<template>
  <div >
    <v-navigation-drawer app v-model="drawer">
      <form >
        <v-slider
            v-model="width"
            min="500"
            max="960"
            label="Background Width"
            hide-details
        ></v-slider>
        <v-slider
            v-model="faceRadius"
            min="240"
            max="250"
            label="Face Radius"
            hide-details
        ></v-slider>
        <v-slider
            v-model="eyeSpacing"
            min="50"
            max="150"
            label="Eye Spacing"
            hide-details
        ></v-slider>
        <v-slider
            v-model="eyeYOffset"
            min="50"
            max="240"
            label="Eye Elevation"
            hide-details
        ></v-slider>
        <v-slider
            v-model="eyeRadius"
            min="10"
            max="60"
            label="Eye Radius"
            hide-details
        ></v-slider>
        <v-slider
            v-model="eyebrowWidth"
            min="0"
            max="100"
            label="Eyebrow Width"
            hide-details
        ></v-slider>
        <v-slider
            v-model="eyebrowHeight"
            min="0"
            max="30"
            label="Eyebrow Height"
            hide-details
        ></v-slider>
        <v-slider
            v-model="eyebrowYOffset"
            min="0"
            max="100"
            label="Eyebrow Elevation"
            hide-details
        ></v-slider>
        <v-slider
            v-model="mouthInnerRadius"
            min="0"
            max="110"
            label="Mouth Inner Radius"
            hide-details
        ></v-slider>
        <v-slider
            v-model="mouthOuterRadius"
            min="0"
            max="120"
            label="Mouth Outer Radius"
            hide-details
        ></v-slider>
        <v-slider
            v-model="mouthStartAngle"
            :min="Math.PI / 4"
            :max="Math.PI"
            label="Mouth Start Angle"
            hide-details
        ></v-slider>
        <v-slider
            v-model="mouthEndAngle"
            :min="Math.PI"
            :max="Math.PI * 7/4"
            label="Mouth End Angle"
            hide-details
        ></v-slider>
        <v-slider
            v-model="mouthXOffset"
            min="0"
            max="20"
            label="Mouth X"
            hide-details
        ></v-slider>
        <v-slider
            v-model="mouthYOffset"
            min="0"
            max="20"
            label="Mouth Y"
            hide-details
        ></v-slider>
        <p>Face Color</p>
        <v-color-picker 
            v-model="faceColor"
            hide-inputs
        ></v-color-picker>
        <p>Eye Color</p>
        <v-color-picker 
            v-model="eyeColor"
            hide-inputs
        ></v-color-picker>
        <p>Background Color</p>
        <v-color-picker 
            v-model="backgroundColor"
            hide-inputs
        ></v-color-picker>
      </form>
    </v-navigation-drawer>

    <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = !drawer" class="grey--text" ></v-app-bar-nav-icon>
      <v-tool-bar-title>The Emoji Maker</v-tool-bar-title>
      <v-spacer></v-spacer>
      <v-btn @click="exportEmoji">Export Emoji</v-btn>
    </v-app-bar>

    
    <v-content class=" ml-4 my-4">
      
      <v-container fluid>
          <Emoji 
            :width="width"
            :height="height"
            :backgroundColor="backgroundColor"
            :faceColor="faceColor"
            :faceRadius="faceRadius"
            :eyeColor="eyeColor"
            :eyeSpacing="eyeSpacing"
            :eyeYOffset="eyeYOffset"
            :eyeRadius="eyeRadius"
            :eyebrowWidth="eyebrowWidth"
            :eyebrowHeight="eyebrowHeight"
            :eyebrowYOffset="eyebrowYOffset"
            :mouthInnerRadius="mouthInnerRadius"
            :mouthOuterRadius="mouthOuterRadius"
            :mouthStartAngle="mouthStartAngle"
            :mouthEndAngle="mouthEndAngle"
            :mouthYOffset="mouthYOffset"
            :mouthXOffset="mouthXOffset"
            @element="setEmoji"
          />
      </v-container>
    </v-content>

    <v-footer app>
      <p>Made by <a href="https://github.com/ahmed-com">Ahmed-com</a></p>
    </v-footer>
  </div>
</template>

<script>
import Emoji from './components/Emoji';

export default {
  name: 'App',

  components: {
    Emoji
  },

  data: () => ({
    width : 960,
    height : 500,
    backgroundColor : 'red',
    faceColor : 'yellow',
    faceRadius : 240,
    eyeColor : 'black',
    eyeSpacing : 100,
    eyeYOffset : 70,
    eyeRadius : 30,
    eyebrowWidth : 70,
    eyebrowHeight : 15,
    eyebrowYOffset : 70,
    mouthInnerRadius : 100,
    mouthOuterRadius : 120,
    mouthStartAngle : Math.PI /2 ,
    mouthEndAngle : Math.PI * 5/8,
    mouthYOffset : 0,
    mouthXOffset : 0,
    emoji : null,
    drawer: true
  }),
  methods : {
    exportEmoji(){
      const emoji = this.emoji;
      // convert svg to string
      let source = new XMLSerializer().serializeToString(emoji);
      // convert svg string into a url
      source = '<?xml version="1.0" standalone="no"?>\r\n' + source;
      const url = "data:image/svg+xml;charset=utf-8,"+encodeURIComponent(source);
      this.download('Emoji.svg',url);
    },
    setEmoji(element){
      this.emoji = element;
    },
    download(fileName,url){
      const element = document.createElement('a');
      element.setAttribute('href', url);
      element.setAttribute('download', fileName);
      element.style.display = 'none';
      document.body.appendChild(element);
      element.click();
      document.body.removeChild(element);
    }
  }
};
</script>
