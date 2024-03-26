<template>
  <div class="navigation-collapse" :class="{ active: activeIndex === index }">
    <div v-if="isMobile" class="navigation-collapse__header" @click="toggleAccordion(index)">
      <Arrow class="navigation-collapse__arrow" />
      <h3 class="navigation-collapse__title">{{ secondaryItem.text }}</h3>
    </div>
    <div v-else class="navigation-collapse__header" @mouseover="toggleAccordion(index)">
      <Arrow class="navigation-collapse__arrow" />
      <h3 class="navigation-collapse__title">{{ secondaryItem.text }}</h3>
    </div>
    <div
      v-show="activeIndex === index"
      class="navigation-collapse__content"
      v-for="content in secondaryItem.navContent"
      :key="content.text"
    >
      <div class="navigation-collapse__block navigation-collapse__block--50">
        <h3>{{ content.title }}</h3>
        <p>{{ content.body }}</p>
        <div class="navigation-collapse__link" v-for="link in content.links" :key="link.text">
          <a :href="link.url">
            <img class="navigation-collapse__icon" :src="link.icon.url" :alt="link.icon.alt" />
            <span>{{ link.text }}</span>
            <Open class="navigation-collapse__open-icon" />
          </a>
        </div>
      </div>
      <div
        class="navigation-collapse__block navigation-collapse__block--25"
        v-if="content.capabilities"
      >
        <div class="navigation-collapse__capabilities">
          <h4>Platform Capabilities</h4>
          <span v-for="capability in content.capabilities" :key="capability.text">
            {{ capability.text }}
          </span>
        </div>
      </div>
      <div class="navigation-collapse__block navigation-collapse__block--25" v-if="content.article">
        <div class="navigation-collapse__article">
          <a :href="content.article.link">
            <img
              class="navigation-collapse__image"
              :src="content.article.image.url"
              :alt="content.article.image.alt"
            />
            <h4>{{ content.article.text }}</h4>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Arrow from '@/assets/icons/arrow.svg'
import Open from '@/assets/icons/open.svg'

export default {
  components: {
    Arrow,
    Open
  },

  props: {
    secondaryItem: {
      type: Object
    },
    isMobile: {
      type: Boolean
    },
    index: {
      type: Number
    },
    activeIndex: {
      type: Number
    }
  },
  methods: {
    toggleAccordion() {
      this.$emit('toggle-accordion', this.index)
    }
  }
}
</script>