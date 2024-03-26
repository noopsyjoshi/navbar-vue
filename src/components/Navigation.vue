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
        <!-- Platform, Resources, About, Login -->
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
                  <NavigationMenu
                    :secondaryItem="secondaryItem"
                    :isMobile="isMobile"
                    :index="index"
                    :activeIndex="activeIndex"
                    @toggle-accordion="toggleAccordion"
                  />
                </li>
              </ul>
            </div>
          </li>
        </ul>

        <!-- TODO: Move login to end of Nav -->

        <router-link to="/" type="button" class="button navigation__button">
          Book a demo
        </router-link>
      </div>
    </div>
  </nav>
</template>

<script>
import NavigationMenu from './NavigationMenu.vue'
import Logo from '@/assets/icons/logo.svg'
import Hamburger from '@/assets/icons/hamburger.svg'
import Close from '@/assets/icons/close.svg'
import Chevron from '@/assets/icons/chevron.svg'
import navigationData from '/public/data/navigation.json'

export default {
  components: {
    NavigationMenu,
    Logo,
    Hamburger,
    Close,
    Chevron
  },

  data() {
    return {
      isMobile: false,
      showMobileMenu: false,
      navPrimaryItems: navigationData.navPrimaryItems,
      showSecondaryNav: false,
      activeIndex: 0
    }
  },

  created() {
    if (window.innerWidth < 992) {
      this.isMobile = true
    }
  },

  mounted() {
    // console.log('data', this.navPrimaryItems)
    window.addEventListener('resize', this.handleResize)
  },

  methods: {
    toggleMenu() {
      this.showMobileMenu = !this.showMobileMenu

      if (window.innerWidth < 992) {
        document.body.classList.toggle('overflow', this.showMobileMenu)
      }
    },

    toggleSecondaryNav() {
      this.showSecondaryNav = !this.showSecondaryNav
    },

    toggleAccordion(index) {
      this.activeIndex = index
    },

    handleResize() {
      if (window.innerWidth >= 992) {
        // Remove overflow class from body and close mobile menu on desktop
        if (document.body.classList.contains('overflow')) {
          document.body.classList.remove('overflow')
        }
        this.showMobileMenu = false
        this.isMobile = false
      } else {
        this.isMobile = true
      }
    }
  }
}
</script>


