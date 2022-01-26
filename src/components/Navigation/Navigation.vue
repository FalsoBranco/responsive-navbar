<script setup>
import { ref, onMounted } from "vue";

const scrolledNav = ref(null);
const mobile = ref(null);
const mobileNav = ref(null);
const windowWidth = ref(null);

const routes = [
  { path: "Home", text: "Home" },
  { path: "", text: "About" },
  { path: "", text: "Portfolio" },
  { path: "", text: "Contact" },
];

function toggleMobileNav() {
  mobileNav.value = !mobileNav.value;
}

function updateScroll() {
  const scrollPosition = window.scrollY;
  if (scrollPosition > 50) {
    scrolledNav.value = true;
    return;
  }
  scrolledNav.value = false;
}

function checkScreen() {
  windowWidth.value = window.innerWidth;
  if (windowWidth.value <= 750) {
    mobile.value = true;
    return;
  }
  mobile.value = false;
  mobileNav.value = false;
}

window.addEventListener("resize", checkScreen);
checkScreen();

onMounted(() => {
  window.addEventListener("scroll", updateScroll);
});
</script>

<template>
  <header :class="{ 'scrolled-nav': scrolledNav }">
    <nav>
      <div class="branding">
        <img src="../../assets/logo.png" alt="" />
      </div>
      <ul v-show="!mobile" class="navigation">
        <template v-for="(route, index) in routes" :key="index">
          <li>
            <router-link class="link" :to="{ name: route.path }">
              {{ route.text }}
            </router-link>
          </li>
        </template>
      </ul>
      <div class="icon">
        <i
          @click="toggleMobileNav"
          v-show="mobile"
          class="far fa-bars"
          :class="{ 'icon-active': mobileNav }"
        ></i>
      </div>
      <transition name="mobile-nav">
        <ul v-show="mobileNav" class="dropdown-nav">
          <li v-for="(route, index) in routes" :key="index">
            <router-link class="link" :to="{ name: route.path }">
              {{ route.text }}
            </router-link>
          </li>
        </ul>
      </transition>
    </nav>
  </header>
</template>
<style lang="scss" scoped>
header {
  background-color: rgba(0, 0, 0, 0.8);
  z-index: 99;
  width: 100%;
  position: fixed;
  transition: 0.5s ease all;
  color: #fff;

  nav {
    position: relative;
    display: flex;
    flex-direction: row;
    padding: 12px 0;
    transition: 0.5s ease all;
    width: 90%;
    margin: 0 auto;

    @media (min-width: 1144px) {
      max-width: 1140px;
    }
    ul,
    .link {
      font-weight: 500;
      color: #fff;
      list-style: none;
      text-decoration: none;
    }
    li {
      text-transform: uppercase;
      padding: 16px;
      margin-left: 16px;
    }
    .link {
      font-size: 14px;
      transition: 0.5s ease all;
      padding-bottom: 4px;
      border-bottom: 1 px solid transparent;
      &:hover {
        color: #00efea;
        border-color: #00efea;
      }
    }
    .branding {
      display: flex;
      align-items: center;

      img {
        width: 50px;
        transition: 0.5s ease all;
      }
    }
    .navigation {
      display: flex;
      align-items: center;
      flex: 1;
      justify-content: flex-end;
    }
    .icon {
      display: flex;
      align-items: center;
      position: absolute;
      top: 0;
      right: 24px;
      height: 100%;
      i {
        cursor: pointer;
        font-size: 24px;
        transition: 0.8s ease all;
      }
    }
    .icon-active {
      transform: rotate(180deg);
    }
    .dropdown-nav {
      display: flex;
      flex-direction: column;
      position: fixed;
      min-width: 250px;
      height: 100%;
      background-color: #fff;
      top: 0;
      left: 0;
      li {
        margin-left: 0;
        .link {
          color: #000;
          &:hover {
            color: crimson;
          }
        }
      }
    }
    .mobile-nav-enter-active,
    .mobile-nav-leave-active {
      transition: 1s ease all;
    }
    .mobile-nav-enter-from,
    .mobile-nav-leave-to {
      transform: translateX(-250px);
    }
    .mobile-nav-enter-to {
      transform: translateX(0);
    }
  }
}
.scrolled-nav {
  background-color: #000;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
    0 2px 4px -1px rgba(0, 0, 0, 0.1);

  nav {
    padding: 8px 0;
    .branding {
      img {
        width: 40px;
        box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
          0 2px 4px -1px rgba(0, 0, 0, 0.1);
      }
    }
  }
}
</style>
