<template>
  <section @click="explosion" :style="cssProps">
    <div v-for="particle in particles" :key="particle[1]" :class="'particle group' + particle[0]"></div>
    <slot/>
  </section>
</template>

<script>
import anime from 'animejs';

export default {
  name: 'AVPE',
  props: {
    amount: Number,
    borderRadius: String,
    color: String,
    colorEnd: String,
    duration: Number,
    ease: String,
    size: String,
    radius: Number,
    startingOpacity: Number,
    endingOpacity: Number
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
      const colorEnd = this.colorEnd ? this.colorEnd : '#000000';
      const duration = this.duration ? this.duration : 500;
      const ease = this.ease ? this.ease : 'easeInBounce';
      const radius = this.radius ? this.radius : 50;
      const startingOpacity = this.startingOpacity ? this.startingOpacity : 1;
      const endingOpacity = this.endingOpacity ? this.endingOpacity : 0;

      const particles = this.particles;

      const key = Date.now();

      for (let i = 0; i < amount; i++) {
        this.particles.push([ key, Math.random() * Math.PI * 2, Math.sqrt(Math.random()) * radius ]);
      }

      this.$nextTick(() => {
        anime({
          targets: '.group' + key,
          duration: duration,
          easing: ease,
          translateX: (el, i) => {
            return [
              event.pageX,
              event.pageX + (Math.cos(particles[i][1]) * particles[i][2])
            ]
          },
          translateY: (el, i) => {
            return [
              event.pageY,
              event.pageY + (Math.sin(particles[i][1]) * particles[i][2])
            ]
          },
          complete: () => {
            particles.splice(0, amount);
          },
          backgroundColor: colorEnd,
          opacity: [ startingOpacity, endingOpacity ]
        });
      });
    }
  },
  computed: {
    cssProps() {
      return {
        '--particle-border-radius': this.borderRadius ? this.borderRadius : '0',
        '--particle-color': this.color ? this.color : '#FF0000',
        '--particle-size': this.size ? this.size : '2px'
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  .particle {
    background-color: var(--particle-color);
    border-radius: var(--particle-border-radius);
    display: inline;
    overflow: hidden;
    position: fixed;
    left: 0;
    top: 0;
    width: var(--particle-size);
    height: var(--particle-size);
    z-index: -1;
  }
</style>
