<template>
  <section @click="explosion" :style="cssProps">
    <div v-for="particle in particles" :key="particle[0]" class="particle"></div>
    <slot/>
  </section>
</template>

<script>
import anime from 'animejs';

export default {
  name: 'AVPE',
  props: {
    amount: Number,
    color: String,
    duration: Number,
    ease: String,
    size: String,
    radius: Number
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
      const duration = this.duration ? this.duration : 500;
      const ease = this.ease ? this.ease : 'easeInBounce';
      const radius = this.radius ? this.radius : 50;

      const particles = this.particles;

      for (let i = 0; i < amount; i++) {
        this.particles.push([ Math.random() * Math.PI * 2, Math.sqrt(Math.random()) * radius ]);
      }

      this.$nextTick(() => {
        anime({
          targets: '.particle',
          duration: duration,
          easing: ease,
          translateX: (el, i) => {
            return [
              event.pageX,
              event.pageX + (Math.cos(particles[i][0]) * particles[i][1])
            ]
          },
          translateY: (el, i) => {
            return [
              event.pageY,
              event.pageY + (Math.sin(particles[i][0]) * particles[i][1])
            ]
          },
          complete: () => {
            particles.splice(0, amount);
          },
          opacity: 0
        });
      });
    }
  },
  computed: {
    cssProps() {
      return {
        '--particle-color': this.color ? this.color : 'red',
        '--particle-size': this.size ? this.size : '2px'
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  .particle {
    background-color: var(--particle-color);
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
