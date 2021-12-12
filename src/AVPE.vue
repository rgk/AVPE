<template>
  <section @click="explosion" :style="cssProps">
    <div v-for="particle in particles" :key="particle[1]" :class="'particle group' + particle[0]"></div>
    <slot/>
  </section>
</template>

<script>
import anime from 'animejs';

const randomColor = () => '#' + Math.random().toString(16).slice(-6);

export default {
  name: 'AVPE',
  props: {
    amount: Number,
    borderRadiusStart: String,
    borderRadiusEnd: String,
    colorStart: String,
    colorEnd: String,
    duration: Number,
    ease: String,
    opacityStart: Number,
    opacityEnd: Number,
    radius: Number,
    rotate: Boolean,
    sizeStart: String,
    sizeEnd: String,
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
      const amount = this.amount ? this.amount : 100;
      const borderRadiusStart = this.borderRadiusStart ? this.borderRadiusStart : '0';
      const borderRadiusEnd = this.borderRadiusEnd ? this.borderRadiusEnd : '1px';
      const colorStart = this.colorStart ? this.colorStart : 'random';
      const colorEnd = this.colorEnd ? this.colorEnd : 'random';
      const duration = this.duration ? this.duration : 500;
      const ease = this.ease ? this.ease : 'easeInBounce';
      const opacityStart = this.opacityStart ? this.opacityStart : 1;
      const opacityEnd = this.opacityEnd ? this.opacityEnd : 0;
      const radius = this.radius ? this.radius : 50;
      const rotate = this.rotate ? true : false;
      const sizeStart = this.sizeStart ? this.sizeStart : '2px';
      const sizeEnd = this.sizeEnd ? this.sizeEnd : '1px';

      const particles = this.particles;

      const key = Date.now();

      for (let i = 0; i < amount; i++) {
        this.particles.push([ key, Math.random() * Math.PI * 2, Math.sqrt(Math.random()) * radius ]);
      }

      // This is so you do not need to check every element.
      const colorStartLogic = colorStart === 'random' ? () => randomColor() : () => colorEnd;
      const colorEndLogic = colorEnd === 'random' ? () => randomColor() : () => colorEnd;
      const rotateLogic = rotate ? () => Math.floor(Math.random() * (720)-360) : () => 0;

      this.$nextTick(() => {
        anime({
          targets: '.group' + key,
          duration: duration,
          easing: ease,
          borderRadius: [ borderRadiusStart, borderRadiusEnd ],
          height: [ sizeStart, sizeEnd ],
          width: [ sizeStart, sizeEnd ],
          opacity: [ opacityStart, opacityEnd ],
          rotate: rotateLogic(),
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
