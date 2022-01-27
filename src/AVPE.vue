<template>
  <section @click="explosion" :style="cssProps">
    <div v-for="particle in particles" :key="particle[1]" :class="'particle p' + particle[0]"></div>
    <slot/>
  </section>
</template>

<script>
import anime from 'animejs';

const randomColor = () => '#' + Math.random().toString(16).slice(-6);
const randomRange = (min, max) => Math.floor(Math.random() * (max - min) + min);

export default {
  name: 'AVPE',
  props: {
    amountMax: Number,
    blendMode: String,
    borderRadiusStart: String,
    borderRadiusEnd: String,
    boxShadow: String,
    colorStart: String,
    colorEnd: String,
    config: Object,
    defaults: Boolean,
    durationMax: Number,
    durationMin: Number,
    ease: String,
    easeBackgroundColor: String,
    easeBorderRadius: String,
    easeFilter: String,
    easeHeight: String,
    easeWidth: String,
    easeOpacity: String,
    easeRotate: String,
    easeX: String,
    easeY: String,
    filterStart: String,
    filterEnd: String,
    opacityStart: Number,
    opacityEnd: Number,
    radiusMax: Number,
    radiusMin: Number,
    rotateMax: Number,
    rotateMin: Number,
    sizeWidthStart: String,
    sizeHeightStart: String,
    sizeWidthEnd: String,
    sizeHeightEnd: String,
    zindex: Number
  },
  data() {
    return {
      particles: []
    }
  },
  methods: {
    explosion: function(event) {
      // Prop defaults.
      const amountMax = this.amountMax ? this.amountMax : 100;
      const amountMin = this.amountMin ? this.amountMin : amountMax;
      const borderRadiusStart = this.borderRadiusStart ? this.borderRadiusStart : '0';
      const borderRadiusEnd = this.borderRadiusEnd ? this.borderRadiusEnd : '1px';
      const colorStart = this.colorStart ? this.colorStart : 'random';
      const colorEnd = this.colorEnd ? this.colorEnd : 'random';
      const config = this.config ? this.config : {};
      const defaults = this.defaults ? this.defaults : TRUE;
      const durationMax = this.durationMax ? this.durationMax : 500;
      const durationMin = this.durationMin ? this.durationMin : durationMax;
      const ease = this.ease ? this.ease : 'easeInBounce';
      const easeBackgroundColor = this.easeBackgroundColor ? this.easeBackgroundColor : this.ease;
      const easeBorderRadius = this.easeBorderRadius ? this.easeBorderRadius : this.ease;
      const easeFilter = this.easeFilter ? this.easeFilter : this.ease;
      const easeHeight = this.easeHeight ? this.easeHeight : this.ease;
      const easeWidth = this.easeWidth ? this.easeWidth : this.ease;
      const easeOpacity = this.easeOpacity ? this.easeOpacity : this.ease;
      const easeRotate = this.easeRotate ? this.easeRotate : this.ease;
      const easeX = this.easeX ? this.easeX : this.ease;
      const easeY = this.easeY ? this.easeY : this.ease;
      const filterStart = this.filterStart ? this.filterStart : 'blur(1px)';
      const filterEnd = this.filterEnd ? this.filterEnd : 'blur(0px)';
      const opacityStart = this.opacityStart ? this.opacityStart : 1;
      const opacityEnd = this.opacityEnd ? this.opacityEnd : 0;
      const radiusMax = this.radiusMax ? this.radiusMax : 50;
      const radiusMin = this.radiusMin ? this.radiusMin : radiusMax;
      const rotateMax = this.rotateMax ? this.rotateMax : 0;
      const rotateMin = this.rotateMin ? this.rotateMin : rotateMax * -1;
      const sizeWidthStart = this.sizeWidthStart ? this.sizeWidthStart : '2px';
      const sizeHeightStart = this.sizeHeightStart ? this.sizeHeightStart : sizeWidthStart;
      const sizeWidthEnd = this.sizeWidthEnd ? this.sizeWidthEnd : '1px';
      const sizeHeightEnd = this.sizeHeightEnd ? this.sizeHeightEnd : sizeWidthEnd;

      const particles = this.particles;

      const key = Date.now();

      const amount = randomRange(amountMin, amountMax);

      for (let i = 0; i < amount; i++) {
        this.particles.push([
          key,
          Math.random() * Math.PI * 2,
          Math.sqrt(Math.random()) * randomRange(radiusMin, radiusMax)
        ]);
      }

      // This is so you do not need to check every element.
      const colorStartLogic = colorStart === 'random' ? () => randomColor() : () => colorStart;
      const colorEndLogic = colorEnd === 'random' ? () => randomColor() : () => colorEnd;

      let animeConfig = {
        targets: '.p' + key,
        translateX: {
          value: (el, i) => [
            event.pageX,
            event.pageX + (Math.cos(particles[i][1]) * particles[i][2])
          ],
          ease: easeX
        },
        translateY: {
          value: (el, i) => [
            event.pageY,
            event.pageY + (Math.sin(particles[i][1]) * particles[i][2])
          ],
          ease: easeY
        },
        complete: () => particles.splice(0, amount)
      };

      for (const [key, value] of Object.entries(config)) {
        switch (key) {
          case 'backgroundColor':
            let turnFunction = false;
            for (let i = 0; i < value['value].length; i++) {
              if (value['value][i] === 'random') value['value][i] = () => randomColor();
              turnFunction = true;
            }

            if (turnFunction) {
              value = () => {
              backgroundColor: () => {
                value: [
                  value['value'][0],
                  value['value'][1]
                ],
                easing: value['ease']
              }
            }

            break;
          case 'rotate':
            if (value.length > 1) value = () => randomRange(value[0], value[1]);

            break;
        }
      }

      if (defaults) {
        animeConfig = {
          ...animeConfig,
          duration: () => randomRange(durationMin, durationMax),
          easing: ease,
          borderRadius: {
            value: [ borderRadiusStart, borderRadiusEnd ],
            easing: easeBorderRadius
          },
          height: {
            value: [ sizeHeightStart, sizeHeightEnd ],
            easing: easeHeight
          },
          width: {
            value: [ sizeWidthStart, sizeWidthEnd ],
            easing: easeWidth
          },
          opacity: {
            value: [ opacityStart, opacityEnd ],
            easing: easeOpacity
          },
          rotate: {
            value: randomRange(rotateMin, rotateMax),
            easing: easeRotate
          },
          filter: {
            value: [ filterStart, filterEnd ],
            easing: easeFilter
          },
          backgroundColor: () => {
            value: [
              colorStartLogic(),
              colorEndLogic()
            ],
            easing: easeBackgroundColor
          }
        };
      }

      // Divs are not present on the DOM this tick.
      this.$nextTick(() => {
        anime({ ...animeConfig, ...config });
      });
    }
  },
  computed: {
    cssProps() {
      return {
        '--blend-mode': this.blendMode ? this.blendMode : 'hard-light',
        '--box-shadow': this.boxShadow ? this.boxShadow : '0 0 2px rgba(255, 255, 255, 0.123)',
        '--particle-z-index': this.zindex ? this.zindex : '-1'
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  .particle {
    box-shadow: var(--box-shadow);
    display: inline;
    mix-blend-mode: var(--blend-mode);
    overflow: hidden;
    position: fixed;
    left: 0;
    top: 0;
    z-index: var(--particle-z-index);
  }
</style>
