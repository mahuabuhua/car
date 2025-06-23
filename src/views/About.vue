<template>
  <div class="about-page">
    <div class="hero-section">
      <h1>{{ $t('about.title') }}</h1>
      <p>{{ $t('about.content') }}</p>
    </div>

    <div class="about-container">
      <div class="about-card">
        <div class="about-icon">
          <i class="fas fa-building"></i>
        </div>
        <h2>{{ $t('about.business.title') }}</h2>
        <p>{{ $t('about.business.description') }}</p>
      </div>
    </div>

    <div class="mission-section">
      <h2>{{ $t('about.mission.title') }}</h2>
      <p class="mission-subtitle">{{ $t('about.mission.subtitle') }}</p>
      <div class="mission-grid">
        <div class="mission-item" v-for="(mission, index) in missions" :key="index">
          <div class="mission-icon">
            <i :class="mission.icon"></i>
          </div>
          <h4 class="mission-title">{{ mission.title }}</h4>
          <p class="mission-description">{{ mission.description }}</p>
          <ul class="mission-features">
            <li v-for="(feature, featureIndex) in mission.features" :key="featureIndex">
              {{ feature }}
            </li>
          </ul>
        </div>
      </div>
    </div>

    <div class="cta-section">
      <h2>{{ $t('about.cta.title') }}</h2>
      <p>{{ $t('about.cta.description') }}</p>
      <router-link to="/service" class="cta-button">
        {{ $t('about.cta.button') }}
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'About',
  mounted() {
    // 确保页面加载时滚动到顶部
    window.scrollTo(0, 0)
  },
  data() {
    return {
      missions: [
        {
          icon: 'fas fa-leaf',
          title: this.$t('about.mission.sustainability.title'),
          description: this.$t('about.mission.sustainability.description'),
          features: this.$t('about.mission.sustainability.features')
        },
        {
          icon: 'fas fa-shield-alt',
          title: this.$t('about.mission.cultural.title'),
          description: this.$t('about.mission.cultural.description'),
          features: this.$t('about.mission.cultural.features')
        },
        {
          icon: 'fas fa-hands-helping',
          title: this.$t('about.mission.community.title'),
          description: this.$t('about.mission.community.description'),
          features: this.$t('about.mission.community.features')
        },
        {
          icon: 'fas fa-chart-line',
          title: this.$t('about.mission.quality.title'),
          description: this.$t('about.mission.quality.description'),
          features: this.$t('about.mission.quality.features')
        }
      ]
    }
  },
  watch: {
    '$i18n.locale'() {
      this.updateTranslations()
    }
  },
  methods: {
    updateTranslations() {
      this.missions = [
        {
          icon: 'fas fa-leaf',
          title: this.$t('about.mission.sustainability.title'),
          description: this.$t('about.mission.sustainability.description'),
          features: this.$t('about.mission.sustainability.features')
        },
        {
          icon: 'fas fa-shield-alt',
          title: this.$t('about.mission.cultural.title'),
          description: this.$t('about.mission.cultural.description'),
          features: this.$t('about.mission.cultural.features')
        },
        {
          icon: 'fas fa-hands-helping',
          title: this.$t('about.mission.community.title'),
          description: this.$t('about.mission.community.description'),
          features: this.$t('about.mission.community.features')
        },
        {
          icon: 'fas fa-chart-line',
          title: this.$t('about.mission.quality.title'),
          description: this.$t('about.mission.quality.description'),
          features: this.$t('about.mission.quality.features')
        }
      ]
    }
  }
}
</script>

<style lang="scss" scoped>
.about-page {
  min-height: 100vh;
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
}

.hero-section {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  text-align: center;
  padding: 80px 20px;
  margin-bottom: 60px;

  h1 {
    font-size: 3rem;
    margin-bottom: 20px;
    font-weight: 700;
  }

  p {
    font-size: 1.2rem;
    opacity: 0.9;
    max-width: 600px;
    margin: 0 auto;
  }
}

.about-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  margin-bottom: 80px;
}

.about-card {
  background: white;
  border-radius: 15px;
  padding: 40px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  text-align: center;
  max-width: 900px;
  margin: 0 auto;

  .about-icon {
    width: 80px;
    height: 80px;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto 30px;

    i {
      font-size: 2rem;
      color: white;
    }
  }

  h2 {
    color: #2c3e50;
    font-size: 2.5rem;
    margin-bottom: 20px;
    font-weight: 700;
  }

  p {
    color: #666;
    line-height: 1.8;
    font-size: 1.1rem;
  }
}

.mission-section {
  background: white;
  padding: 80px 20px;
  margin-bottom: 60px;

  h2 {
    text-align: center;
    font-size: 2.5rem;
    color: #2c3e50;
    margin-bottom: 20px;
    font-weight: 700;
  }

  .mission-subtitle {
    text-align: center;
    color: #666;
    font-size: 1.1rem;
    line-height: 1.6;
    max-width: 800px;
    margin: 0 auto 50px;
  }
}

.mission-grid {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 30px;
}

.mission-item {
  background: white;
  border-radius: 15px;
  padding: 40px 30px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  text-align: center;
  transition: transform 0.3s ease, box-shadow 0.3s ease;

  &:hover {
    transform: translateY(-10px);
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
  }

  .mission-icon {
    width: 80px;
    height: 80px;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto 20px;

    i {
      font-size: 2rem;
      color: white;
    }
  }

  .mission-title {
    color: #2c3e50;
    font-size: 1.5rem;
    margin-bottom: 15px;
    font-weight: 700;
  }

  .mission-description {
    color: #2c3e50;
    line-height: 1.6;
    margin-bottom: 20px;
    font-weight: 600;
    font-size: 1rem;
  }

  .mission-features {
    list-style: none;
    padding: 0;
    margin: 0;
    text-align: left;

    li {
      color: #666;
      padding: 8px 0;
      position: relative;
      padding-left: 20px;
      line-height: 1.5;
      font-size: 0.9rem;

      &:before {
        content: '✓';
        position: absolute;
        left: 0;
        color: #42b983;
        font-weight: bold;
      }
    }
  }
}

.cta-section {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  text-align: center;
  padding: 60px 20px;

  h2 {
    font-size: 2rem;
    margin-bottom: 20px;
    font-weight: 700;
  }

  p {
    font-size: 1rem;
    margin-bottom: 40px;
    opacity: 0.9;
  }

  .cta-button {
    display: inline-block;
    background: white;
    color: #667eea;
    padding: 15px 40px;
    border-radius: 50px;
    text-decoration: none;
    font-weight: 600;
    font-size: 1.1rem;
    transition: all 0.3s ease;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);

    &:hover {
      transform: translateY(-3px);
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
    }
  }
}

@media (max-width: 768px) {
  .hero-section {
    padding: 60px 20px;

    h1 {
      font-size: 2.5rem;
    }

    p {
      font-size: 1rem;
    }
  }

  .about-card {
    padding: 30px 20px;

    h2 {
      font-size: 2rem;
    }

    p {
      font-size: 1rem;
    }
  }

  .mission-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }

  .mission-section {
    padding: 60px 20px;

    h2 {
      font-size: 2rem;
    }

    .mission-subtitle {
      font-size: 1rem;
      margin-bottom: 40px;
    }
  }

  .cta-section {
    padding: 60px 20px;

    h2 {
      font-size: 2rem;
    }

    p {
      font-size: 1rem;
    }
  }

  .mission-item {
    padding: 30px 20px;

    .mission-icon {
      width: 70px;
      height: 70px;

      i {
        font-size: 1.8rem;
      }
    }

    .mission-title {
      font-size: 1.3rem;
    }

    .mission-description {
      font-size: 0.95rem;
    }

    .mission-features li {
      font-size: 0.9rem;
    }
  }
}
</style> 