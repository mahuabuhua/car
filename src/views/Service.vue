<template>
  <div class="service-page">
    <div class="hero-section">
      <h1>{{ $t('service.title') }}</h1>
      <p>{{ $t('service.subtitle') }}</p>
    </div>

    <div class="services-container">
      <div class="service-card" v-for="(service, index) in services" :key="index">
        <div class="service-icon">
          <i :class="service.icon"></i>
        </div>
        <h3>{{ service.title }}</h3>
        <p>{{ service.description }}</p>
        <ul>
          <li v-for="(feature, featureIndex) in service.features" :key="featureIndex">
            {{ feature }}
          </li>
        </ul>
      </div>
    </div>

    <div class="why-choose-us">
      <h2>{{ $t('service.whyChooseUs.title') }}</h2>
      <div class="features-grid">
        <div class="feature-item" v-for="(feature, index) in whyChooseUs" :key="index">
          <div class="feature-icon">
            <i :class="feature.icon"></i>
          </div>
          <h4>{{ feature.title }}</h4>
        </div>
      </div>
    </div>

    <div class="cta-section">
      <h2>{{ $t('service.cta.title') }}</h2>
      <p>{{ $t('service.cta.description') }}</p>
      <router-link to="/contact" class="cta-button">
        {{ $t('service.cta.button') }}
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Service',
  mounted() {
    // 确保页面加载时滚动到顶部
    window.scrollTo(0, 0)
  },
  data() {
    return {
      services: [
        {
          icon: 'fas fa-car',
          title: this.$t('service.services.individual.title'),
          description: this.$t('service.services.individual.description'),
          features: this.$t('service.services.individual.features')
        },
        {
          icon: 'fas fa-building',
          title: this.$t('service.services.travelAgents.title'),
          description: this.$t('service.services.travelAgents.description'),
          features: this.$t('service.services.travelAgents.features')
        },
        {
          icon: 'fas fa-map-marked-alt',
          title: this.$t('service.services.guidedTour.title'),
          description: this.$t('service.services.guidedTour.description'),
          features: this.$t('service.services.guidedTour.features')
        },
        {
          icon: 'fas fa-star',
          title: this.$t('service.services.quality.title'),
          description: this.$t('service.services.quality.description'),
          features: this.$t('service.services.quality.features')
        }
      ],
      whyChooseUs: [
        {
          icon: 'fas fa-shield-alt',
          title: this.$t('home.whyChooseUs.statement1'),
          description: ''
        },
        {
          icon: 'fas fa-heart',
          title: this.$t('home.whyChooseUs.statement2'),
          description: ''
        },
        {
          icon: 'fas fa-handshake',
          title: this.$t('home.whyChooseUs.statement3'),
          description: ''
        },
        {
          icon: 'fas fa-leaf',
          title: this.$t('home.whyChooseUs.statement4'),
          description: ''
        },
        {
          icon: 'fas fa-star',
          title: this.$t('home.whyChooseUs.statement5'),
          description: ''
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
      this.services = [
        {
          icon: 'fas fa-car',
          title: this.$t('service.services.individual.title'),
          description: this.$t('service.services.individual.description'),
          features: this.$t('service.services.individual.features')
        },
        {
          icon: 'fas fa-building',
          title: this.$t('service.services.travelAgents.title'),
          description: this.$t('service.services.travelAgents.description'),
          features: this.$t('service.services.travelAgents.features')
        },
        {
          icon: 'fas fa-map-marked-alt',
          title: this.$t('service.services.guidedTour.title'),
          description: this.$t('service.services.guidedTour.description'),
          features: this.$t('service.services.guidedTour.features')
        },
        {
          icon: 'fas fa-star',
          title: this.$t('service.services.quality.title'),
          description: this.$t('service.services.quality.description'),
          features: this.$t('service.services.quality.features')
        }
      ]
      this.whyChooseUs = [
        {
          icon: 'fas fa-shield-alt',
          title: this.$t('home.whyChooseUs.statement1'),
          description: ''
        },
        {
          icon: 'fas fa-heart',
          title: this.$t('home.whyChooseUs.statement2'),
          description: ''
        },
        {
          icon: 'fas fa-handshake',
          title: this.$t('home.whyChooseUs.statement3'),
          description: ''
        },
        {
          icon: 'fas fa-leaf',
          title: this.$t('home.whyChooseUs.statement4'),
          description: ''
        },
        {
          icon: 'fas fa-star',
          title: this.$t('home.whyChooseUs.statement5'),
          description: ''
        }
      ]
    }
  }
}
</script>

<style lang="scss" scoped>
.service-page {
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

.services-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 30px;
  margin-bottom: 80px;
}

.service-card {
  background: white;
  border-radius: 15px;
  padding: 30px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  text-align: center;

  &:hover {
    transform: translateY(-10px);
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
  }

  .service-icon {
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

  h3 {
    color: #2c3e50;
    font-size: 1.5rem;
    margin-bottom: 15px;
    font-weight: 600;
  }

  p {
    color: #666;
    line-height: 1.6;
    margin-bottom: 20px;
  }

  ul {
    list-style: none;
    padding: 0;
    text-align: left;

    li {
      color: #555;
      padding: 8px 0;
      position: relative;
      padding-left: 25px;

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

.why-choose-us {
  background: white;
  padding: 80px 20px;
  margin-bottom: 60px;

  h2 {
    text-align: center;
    font-size: 2.5rem;
    color: #2c3e50;
    margin-bottom: 50px;
    font-weight: 700;
  }
}

.features-grid {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 30px;
}

.feature-item {
  text-align: center;
  padding: 20px;

  .feature-icon {
    width: 60px;
    height: 60px;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto 20px;

    i {
      font-size: 1.5rem;
      color: white;
    }
  }

  h4 {
    color: #2c3e50;
    font-size: 1.1rem;
    margin-bottom: 0;
    font-weight: 600;
    line-height: 1.5;
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

  .services-container {
    grid-template-columns: 1fr;
    gap: 20px;
    padding: 0 15px;
  }

  .service-card {
    padding: 25px;
  }

  .features-grid {
    grid-template-columns: 1fr;
    gap: 30px;
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
}
</style> 