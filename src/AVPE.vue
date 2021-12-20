<template>
  <section @click="explosion" :style="cssProps">
    <div v-for="particle in particles" :key="particle[1]" :class="'particle group' + particle[0]"></div>
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
    borderRadiusStart: String,
    borderRadiusEnd: String,
    colorStart: String,
    colorEnd: String,
    durationMax: Number,
    durationMin: Number,
    ease: String,
    easeBorderRadius: String,
    easeHeight: String,
    easeWidth: String,
    easeOpacity: String,
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
      const amountMax = this.amountMax ? this.amount : 100;
      const amountMin = this.amountMin ? this.amountMin : amountMax;
      const borderRadiusStart = this.borderRadiusStart ? this.borderRadiusStart : '0';
      const borderRadiusEnd = this.borderRadiusEnd ? this.borderRadiusEnd : '1px';
      const colorStart = this.colorStart ? this.colorStart : 'random';
      const colorEnd = this.colorEnd ? this.colorEnd : 'random';
      const durationMax = this.durationMax ? this.durationMax : 500;
      const durationMin = this.durationMin ? this.durationMin : durationMax;
      const ease = this.ease ? this.ease : 'easeInBounce';
      const easeBorderRadius = this.easeBorderRadius ? this.easeBorderRadius : this.ease;
      const easeHeight = this.easeHeight ? this.easeHeight : this.ease;
      const easeWidth = this.easeWidth ? this.easeWidth : this.ease;
      const easeOpacity = this.easeOpacity ? this.easeOpacity : this.ease;
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

      this.$nextTick(() => {
        anime({
          targets: '.group' + key,
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
          rotate: randomRange(rotateMin, rotateMax),
          backgroundColor: () => [
            colorStartLogic(),
            colorEndLogic()
          ],
          translateX: (el, i) => [
            event.pageX,
            event.pageX + (Math.cos(particles[i][1]) * particles[i][2])
          ],
          translateY: (el, i) => [
            event.pageY,
            event.pageY + (Math.sin(particles[i][1]) * particles[i][2])
          ],
          complete: () => particles.splice(0, amount)
        });
      });
    }
  },
  computed: {
    cssProps() {
      return {
        '--particle-z-index': this.zindex ? this.zindex : '-1'
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  .particle {
    display: inline;
    overflow: hidden;
    position: fixed;
    left: 0;
    top: 0;
    z-index: var(--particle-z-index);
  }
</style>
