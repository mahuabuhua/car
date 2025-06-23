<template>
  <div id="app">
    <nav class="navbar" :class="{ 'navbar-scrolled': isScrolled }">
      <div class="logo">
        <img src="./assets/logo.png" alt="Logo" @click="handleLogoClick">
      </div>
      <div class="nav-links" :class="{ 'nav-active': isMenuOpen }">
        <router-link to="/" @click="closeMenu">{{ $t('nav.home') }}</router-link>
        <router-link to="/about" @click="closeMenu">{{ $t('nav.about') }}</router-link>
        <router-link to="/service" @click="closeMenu">{{ $t('nav.service') }}</router-link>
        <router-link to="/contact" @click="closeMenu">{{ $t('nav.contact') }}</router-link>
        <!-- <router-link to="/team" @click="closeMenu">{{ $t('nav.team') }}</router-link> -->
        <select v-model="$i18n.locale" @change="closeMenu">
          <option value="en">English</option>
          <option value="zh">中文</option>
        </select>
      </div>
      <div class="menu-toggle" @click="toggleMenu" :class="{ 'active': isMenuOpen }">
        <span></span>
        <span></span>
        <span></span>
      </div>
    </nav>
    <router-view />
  </div>
</template>

<script>
export default {
  data() {
    return {
      isMenuOpen: false,
      isScrolled: false,
      logoClickCount: 0,
      logoClickTimer: null
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll)
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen
    },
    closeMenu() {
      this.isMenuOpen = false
    },
    handleScroll() {
      this.isScrolled = window.scrollY > 50
    },
    handleLogoClick() {
      if (this.logoClickTimer) clearTimeout(this.logoClickTimer)
      this.logoClickCount++
      if (this.logoClickCount >= 5) {
        this.logoClickCount = 0
        const pwd = prompt('请输入管理员口令：')
        if (pwd === 'kl2025') {
          localStorage.setItem('customer_authed', '1');
          this.$router.push('/customer')
        } else if (pwd !== null) {
          alert('口令错误！')
        }
      } else {
        this.logoClickTimer = setTimeout(() => {
          this.logoClickCount = 0
        }, 1500)
      }
    }
  },
  watch: {
    $route() {
      this.closeMenu()
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 10vh;
}

.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  background-color: white;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  height: 10vh;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  transition: all 0.3s ease;

  &.navbar-scrolled {
    height: 8vh;
    padding: 0.5rem 2rem;
    background-color: white;

    .logo img {
      height: 140px;
      margin-left: -3rem;
    }
  }

  .logo {
    background: transparent;

    img {
      margin-left: -4rem;
      height: 180px;
      width: auto;
      object-fit: contain;
      transition: all 0.3s ease;
    }
  }

  .nav-links {
    display: flex;
    gap: 2rem;
    align-items: center;
    margin-left: 2rem;

    a {
      color: #2c3e50;
      text-decoration: none;
      font-weight: bold;
      font-size: 1.1rem;
      transition: color 0.3s ease;

      &:hover {
        color: #667eea;
      }

      &.router-link-exact-active {
        color: #667eea;
      }
    }

    select {
      margin-left: 1rem;
      padding: 0.5rem;
      border: 1px solid #ddd;
      border-radius: 4px;
      font-size: 1rem;
      background-color: white;
      cursor: pointer;
      transition: border-color 0.3s ease;

      &:focus {
        outline: none;
        border-color: #667eea;
      }
    }
  }

  .menu-toggle {
    display: none;
    flex-direction: column;
    gap: 5px;
    cursor: pointer;
    padding: 5px;
    z-index: 1000;

    span {
      display: block;
      width: 22px;
      height: 2px;
      background-color: #2c3e50;
      transition: all 0.3s ease;
      border-radius: 2px;
    }

    &.active {
      span {
        &:first-child {
          transform: translateY(7px) rotate(45deg);
        }

        &:nth-child(2) {
          opacity: 0;
        }

        &:last-child {
          transform: translateY(-7px) rotate(-45deg);
        }
      }
    }
  }
}

// 移动端样式
@media screen and (max-width: 768px) {
  .navbar {
    height: 9vh;
    padding: 0.5rem 1rem;
    transition: none;
    background-color: white;


    &.navbar-scrolled {
      height: 5vh;
      padding: 0.5rem 1rem;
      transition: none;
      background-color: white;

      .logo img {
        height: 120px;
        margin-left: -2.5rem;
        transition: none;
      }

    }



    .logo img {
      height: 150px;
      margin-left: -3rem;
      transition: none;
    }

    .menu-toggle {
      display: flex;
      padding: 3px;

      span {
        width: 20px;
        height: 2px;
      }
    }

    .nav-links {
      position: fixed;
      top: 0;
      right: -100%;
      width: 45%;
      height: auto;
      max-height: 80vh;
      background-color: rgba(255, 255, 255, 0.98);
      flex-direction: column;
      padding: 60px 15px 15px;
      transition: all 0.3s ease;
      box-shadow: -2px 0 8px rgba(0, 0, 0, 0.1);
      backdrop-filter: blur(10px);
      z-index: 999;
      border-radius: 0 0 0 15px;

      &.nav-active {
        right: 0;
      }

      a {
        font-size: 0.9rem;
        padding: 10px 0;
        width: 100%;
        text-align: center;
        border-bottom: 1px solid rgba(0, 0, 0, 0.05);

        &:last-of-type {
          border-bottom: none;
        }
      }

      select {
        margin: 12px 0;
        width: 90%;
        padding: 6px;
        border-radius: 15px;
        border: 1px solid #ddd;
        background-color: white;
        font-size: 0.85rem;
      }
    }
  }
}
</style>