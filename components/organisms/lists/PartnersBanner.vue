<template>
  <div class="partners__slider">
    <ul class="partners__slide-track">
      <li
        v-for="(partner, index) in partners"
        :key="`${partner.alt}-${index}`"
        class="flex items-center partners__slide"
      >
        <a :href="partner.link" class="opacity-75 hover:opacity-100 w-28" rel="noopener sponsored" target="_blank">
          <img
            loading="lazy"
            :src="partner.logoFull"
            :alt="partner.title"
            :title="partner.title"
            :class="partner.logoSize || 'h-full w-full'"
          />
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
import { defineComponent, computed } from '@nuxtjs/composition-api'

export default defineComponent({
  props: {
    partnersLogo: {
      type: Array,
      required: true,
      default: () => []
    }
  },
  setup(props) {
    // double array values
    const partners = computed(() => props.partnersLogo.concat(props.partnersLogo))

    return {
      partners
    }
  }
})
</script>

<style lang="postcss">
@-webkit-keyframes scroll {
  0% {
    -webkit-transform: translateX(0);
    transform: translateX(0);
  }
  100% {
    -webkit-transform: translateX(calc(-250px * 8));
    transform: translateX(calc(-250px * 8));
  }
}

@keyframes scroll {
  0% {
    -webkit-transform: translateX(0);
    transform: translateX(0);
  }
  100% {
    -webkit-transform: translateX(calc(-250px * 8));
    transform: translateX(calc(-250px * 8));
  }
}

.partners__slider {
  @apply relative pb-8 h-40 overflow-hidden w-full;
}

.partners__slider::before,
.partners__slider::after {
  @apply absolute h-24 w-48 z-10;
  background: linear-gradient(to right, rgba(229, 249, 255, 0) 0%, rgba(255, 255, 255, 0) 20%);
  content: '';
  pointer-events: none;
}
@screen sm {
  .partners__slider::before,
  .partners__slider::after {
    background: linear-gradient(to right, rgba(229, 249, 255, 0) 0%, rgba(255, 255, 255, 0) 50%);
  }
}

@screen md {
  .partners__slider::before,
  .partners__slider::after {
    background: linear-gradient(to right, rgba(229, 249, 255, 0) 0%, rgba(255, 255, 255, 0) 100%);
  }
}

.partners__slider::after {
  @apply right-0 top-0 transform rotate-180;
}

.partners__slider::before {
  @apply left-0 top-0;
}

.partners__slider .partners__slide-track {
  @apply flex;
  -webkit-animation: scroll 30s linear infinite;
  animation: scroll 30s linear infinite;
  width: calc(250px * 16);
}

.partners__slider .partners__slide {
  @apply h-24 w-64;
}
.partners__slide-track:hover {
  animation-play-state: paused;
}
</style>
