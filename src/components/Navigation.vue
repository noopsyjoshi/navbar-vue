<template>
  <nav class="navigation">
    <div class="navigation__wrapper">
      <!-- Logo -->
      <router-link class="navigation__logo-wrapper" to="/">
        <Logo class="navigation__logo" alt="GuestXM Logo" />
      </router-link>

      <!-- Toggles to open/close navigation on mobile -->
      <div class="navigation__toggles" :class="this.showMobileMenu ? 'open' : ''">
        <button
          type="button"
          class="navigation__toggle"
          aria-label="Toggle mobile navigation"
          @click="toggleMenu"
        >
          <Hamburger class="navigation__hamburger" alt="Hamburger icon" />
          <Close class="navigation__close" alt="Close icon" />
        </button>
      </div>

      <div class="navigation__menu" :class="this.showMobileMenu ? 'open' : ''">
        <ul class="navigation__primary">
          <li
            class="navigation__item"
            v-for="primaryItem in navPrimaryItems"
            :key="primaryItem.text"
          >
            <a
              v-if="primaryItem.navSecondaryItems"
              aria-haspopup="true"
              aria-expanded="false"
              :aria-controls="primaryItem.text"
              :class="this.showSecondaryNav ? 'is-active' : ''"
              @click.prevent="toggleSecondaryNav()"
              href="/"
              class="navigation__link"
            >
              {{ primaryItem.text }}
              <Chevron class="navigation__chevron" alt="Down arrow" />
            </a>

            <router-link v-else to="" class="navigation__link">
              {{ primaryItem.text }}
            </router-link>

            <div
              v-if="primaryItem.navSecondaryItems"
              :class="this.showSecondaryNav ? 'is-active' : ''"
              class="navigation__secondary"
            >
              <ul>
                <li
                  class="navigation__secondary-item"
                  v-for="(secondaryItem, index) in primaryItem.navSecondaryItems"
                  :key="secondaryItem.text"
                >
                  <div class="navigation-collapse" :class="{ active: activeIndex === index }">
                    <div class="navigation-collapse__header" @click="toggleAccordion(index)">
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
                        <div
                          class="navigation-collapse__link"
                          v-for="link in content.links"
                          :key="link.text"
                        >
                          <router-link to="link.url">
                            <img
                              class="navigation-collapse__icon"
                              :src="link.icon.url"
                              :alt="link.icon.alt"
                            />
                            <span>{{ link.text }}</span>
                            <Open class="navigation-collapse__open-icon" />
                          </router-link>
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
                      <div
                        class="navigation-collapse__block navigation-collapse__block--25"
                        v-if="content.article"
                      >
                        <div class="navigation-collapse__article">
                          <img
                            class="navigation-collapse__image"
                            :src="content.article.image.url"
                            :alt="content.article.image.alt"
                          />
                          <h4>{{ content.article.text }}</h4>
                        </div>
                      </div>
                    </div>
                  </div>
                </li>
              </ul>
            </div>
          </li>
        </ul>

        <router-link to="/" type="button" class="button navigation__button">
          Book a demo
        </router-link>
      </div>
    </div>
  </nav>
</template>

<script>
import Logo from '@/assets/icons/logo.svg'
import Hamburger from '@/assets/icons/hamburger.svg'
import Close from '@/assets/icons/close.svg'
import Arrow from '@/assets/icons/arrow.svg'
import Open from '@/assets/icons/open.svg'
import Chevron from '@/assets/icons/chevron.svg'
import navigationData from '/public/data/navigation.json'

export default {
  components: {
    Logo,
    Hamburger,
    Close,
    Arrow,
    Open,
    Chevron
  },

  data() {
    return {
      showMobileMenu: false,
      navPrimaryItems: navigationData.navPrimaryItems,
      showSecondaryNav: false,
      expandedMenuSection: null,
      activeIndex: 0
    }
  },

  mounted() {
    console.log('data', this.navPrimaryItems)
  },

  methods: {
    toggleMenu() {
      this.showMobileMenu = !this.showMobileMenu

      // TODO: Move to watch?!
      this.showMobileMenu === true
        ? document.querySelector('body').classList.add('overflow')
        : document.querySelector('body').classList.remove('overflow')
    },

    toggleSecondaryNav() {
      this.showSecondaryNav = !this.showSecondaryNav
    },

    toggleAccordion(index) {
      console.log(this.activeIndex, index)

      this.activeIndex = this.activeIndex === index ? -1 : index
    }
  }
}
</script>


