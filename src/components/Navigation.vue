<template>
  <nav class="navigation">
    <div class="navigation__wrapper">
      <!-- Logo -->
      <router-link to="/">
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
        <!-- Primary nav - Platform, Resources, About us  -->
        <ul class="navigation__primary">
          <li
            class="navigation__item"
            v-for="primaryItem in navPrimaryItems"
            :key="primaryItem.text"
          >
            <!-- If nav item has submenu, display a button to expand submenu -->
            <a
              v-if="primaryItem.navSecondaryItems"
              aria-haspopup="true"
              aria-expanded="false"
              :aria-controls="primaryItem.text"
              @click.prevent="event.preventDefault()"
              :href="primaryItem.link"
              class="navigation__link"
            >
              {{ primaryItem.text }}
            </a>
            <!-- Else display link -->
            <router-link
              v-else
              to="primaryItem.link"
              :target="primaryItem.target"
              class="navigation__link"
            >
              {{ primaryItem.text }}
            </router-link>
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
import navigationData from '../../public/data/navigation.json'

export default {
  components: {
    Logo,
    Hamburger,
    Close
  },

  data() {
    return {
      showMobileMenu: false,
      navPrimaryItems: navigationData.navPrimaryItems
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
    }
  }
}
</script>


