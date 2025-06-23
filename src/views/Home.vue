<template>
  <div class="home">
    <div class="hero" @click="goToContact">
      <h1>{{ $t('home.title') }}</h1>
      <p>{{ $t('home.description') }}</p>
    </div>
    
    <div class="commitment-section">
      <div class="container">
        <h2>{{ $t('home.commitment.title') }}</h2>
        <div class="commitment-content">
          <p>{{ $t('home.commitment.paragraph1') }}</p>
          <p>{{ $t('home.commitment.paragraph2') }}</p>
        </div>
        <router-link to="/service" class="service-button">
          {{ $t('home.commitment.serviceButton') }}
        </router-link>
      </div>
    </div>

    <div class="why-choose-us-section">
      <div class="container">
        <div class="statements-grid">
          <div class="statement-item" v-for="(statement, index) in statements" :key="index">
            <div class="statement-icon">
              <i :class="statement.icon"></i>
            </div>
            <p>{{ statement.text }}</p>
          </div>
        </div>
      </div>
    </div>

    <div class="partners-section">
      <div class="container">
        <h2>{{ $t('home.partners.title') }}</h2>
        <div class="partners-grid">
          <div class="partner-item" v-for="(partner, index) in partners" :key="index">
            <div class="partner-image" :class="{ 'partner-image-cover': index === 2 }">
              <img :src="partner.image" :alt="partner.name">
            </div>
            <h4>{{ partner.name }}</h4>
          </div>
        </div>
      </div>
    </div>

    <div class="testimonials-section">
      <div class="container">
        <h2>{{ $t('home.testimonials.title') }}</h2>
        <div class="testimonials-grid">
          <div class="testimonial-item" v-for="(testimonial, index) in testimonials" :key="index">
            <div class="testimonial-content">
              <p>{{ testimonial.content }}</p>
              <div class="testimonial-author">
                <span class="guest-info">{{ testimonial.author }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="slogan-section">
      <div class="slogan-inner">
        <div class="slogan-line"></div>
        <h2>{{ $t('home.slogan.title') }}</h2>
        <p>{{ $t('home.slogan.content') }}</p>
        <div class="slogan-line"></div>
        <div class="footer-nav">
          <router-link to="/" exact>{{ $t('nav.home') }}</router-link>
          <router-link to="/about">{{ $t('nav.about') }}</router-link>
          <router-link to="/service">{{ $t('nav.service') }}</router-link>
          <router-link to="/team">{{ $t('nav.team') }}</router-link>
          <router-link to="/contact">{{ $t('nav.contact') }}</router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      statements: [
        {
          icon: 'fas fa-shield-alt',
          text: this.$t('home.whyChooseUs.statement1')
        },
        {
          icon: 'fas fa-heart',
          text: this.$t('home.whyChooseUs.statement2')
        },
        {
          icon: 'fas fa-handshake',
          text: this.$t('home.whyChooseUs.statement3')
        },
        {
          icon: 'fas fa-leaf',
          text: this.$t('home.whyChooseUs.statement4')
        },
        {
          icon: 'fas fa-star',
          text: this.$t('home.whyChooseUs.statement5')
        }
      ],
      partners: [
        {
          image: require('../assets/1.jpg'),
          name: 'NZ Transport Agency'
        },
        {
          image: require('../assets/2.jpg'),
          name: 'Bus and Coach Association'
        },
        {
          image: require('../assets/3.jpg'),
          name: 'VTNZ'
        }
      ],
      testimonials: [
        {
          content: this.$t('home.testimonials.testimonial1.content'),
          author: this.$t('home.testimonials.testimonial1.author')
        },
        {
          content: this.$t('home.testimonials.testimonial2.content'),
          author: this.$t('home.testimonials.testimonial2.author')
        }
      ],
      logoClickCount: 0,
      logoClickTimer: null
    }
  },
  watch: {
    '$i18n.locale'() {
      this.updateTranslations()
    }
  },
  methods: {
    goToContact() {
      this.$router.push('/contact')
    },
    updateTranslations() {
      this.statements = [
        {
          icon: 'fas fa-shield-alt',
          text: this.$t('home.whyChooseUs.statement1')
        },
        {
          icon: 'fas fa-heart',
          text: this.$t('home.whyChooseUs.statement2')
        },
        {
          icon: 'fas fa-handshake',
          text: this.$t('home.whyChooseUs.statement3')
        },
        {
          icon: 'fas fa-leaf',
          text: this.$t('home.whyChooseUs.statement4')
        },
        {
          icon: 'fas fa-star',
          text: this.$t('home.whyChooseUs.statement5')
        }
      ]
      this.partners = [
        {
          image: require('../assets/1.jpg'),
          name: 'NZ Transport Agency'
        },
        {
          image: require('../assets/2.jpg'),
          name: 'Bus and Coach Association'
        },
        {
          image: require('../assets/3.jpg'),
          name: 'VTNZ'
        }
      ]
      this.testimonials = [
        {
          content: this.$t('home.testimonials.testimonial1.content'),
          author: this.$t('home.testimonials.testimonial1.author')
        },
        {
          content: this.$t('home.testimonials.testimonial2.content'),
          author: this.$t('home.testimonials.testimonial2.author')
        }
      ]
    },
    handleLogoClick() {
      if (this.logoClickTimer) clearTimeout(this.logoClickTimer)
      this.logoClickCount++
      if (this.logoClickCount >= 5) {
        this.logoClickCount = 0
        const pwd = prompt('请输入管理员口令：')
        if (pwd === 'admin2024') {
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
  }
}
</script>

<style lang="scss" scoped>
.home {
  .hero {
    background-image: url('../assets/nz-hero.webp');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    color: white;
    text-align: center;
    padding: 2rem;
    margin-bottom: 2rem;
    position: relative;
    margin: auto;
    cursor: pointer;

    &::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      z-index: 1;
    }

    h1 {
      font-size: 4rem;
      margin-bottom: 1.5rem;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
      position: relative;
      z-index: 2;
    }

    p {
      font-size: 1.8rem;
      text-shadow: 1px 1px 2px rgba(0,0,0,0.5);
      max-width: 800px;
      position: relative;
      z-index: 2;
    }
  }

  .commitment-section {
    padding: 4rem 2rem;
    background-color: #fff;

    .container {
      max-width: 1200px;
      margin: 0 auto;
      text-align: center;

      h2 {
        color: #2c3e50;
        font-size: 2.5rem;
        margin-bottom: 2rem;
        position: relative;
        padding-bottom: 1rem;

        &::after {
          content: '';
          position: absolute;
          bottom: 0;
          left: 50%;
          transform: translateX(-50%);
          width: 100px;
          height: 3px;
          background-color: #667eea;
        }
      }

      .commitment-content {
        max-width: 900px;
        margin: 0 auto 3rem;

        p {
          color: #666;
          font-size: 1.1rem;
          line-height: 1.8;
          margin-bottom: 1.5rem;
          text-align: left;

          &:last-child {
            margin-bottom: 0;
          }
        }
      }

      .service-button {
        display: inline-block;
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        color: white;
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
  }

  .why-choose-us-section {
    padding: 4rem 2rem;
    background-color: #fff;

    .container {
      max-width: 1200px;
      margin: 0 auto;
      text-align: center;

      .statements-grid {
        display: flex;
        flex-wrap: nowrap;
        justify-content: space-between;
        gap: 1rem;
        max-width: 1200px;
        margin: 0 auto;

        .statement-item {
          flex: 1;
          min-width: 0;
          text-align: center;
          padding: 1.5rem 1rem;
          background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
          border-radius: 15px;
          border: 1px solid #e9ecef;
          transition: all 0.3s ease;
          box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);

          &:hover {
            transform: translateY(-8px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
            background: linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%);
          }

          .statement-icon {
            width: 60px;
            height: 60px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 1rem;

            i {
              font-size: 1.5rem;
              color: white;
            }
          }

          p {
            color: #495057;
            font-size: 0.95rem;
            line-height: 1.5;
            margin: 0;
            font-weight: 500;
          }
        }
      }
    }
  }

  .partners-section {
    padding: 4rem 2rem;
    background-color: #fff;

    .container {
      max-width: 1200px;
      margin: 0 auto;
      text-align: center;

      h2 {
        color: #2c3e50;
        font-size: 2.5rem;
        margin-bottom: 2rem;
        position: relative;
        padding-bottom: 1rem;

        &::after {
          content: '';
          position: absolute;
          bottom: 0;
          left: 50%;
          transform: translateX(-50%);
          width: 100px;
          height: 3px;
          background-color: #667eea;
        }
      }

      .partners-grid {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-around;
        gap: 2rem;
        max-width: 1200px;
        margin: 0 auto;

        .partner-item {
          flex: 1;
          min-width: 0;
          text-align: center;
          padding: 1.5rem 1rem;
          background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
          border-radius: 15px;
          border: 1px solid #e9ecef;
          transition: all 0.3s ease;
          box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);

          &:hover {
            transform: translateY(-8px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
            background: linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%);
          }

          .partner-image {
            width: 200px;
            height: 120px;
            margin: 0 auto 1rem;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);

            img {
              width: 100%;
              height: 100%;
              object-fit: contain;
              background-color: white;
            }

            &.partner-image-cover img {
              object-fit: cover;
            }
          }

          h4 {
            color: #495057;
            font-size: 0.95rem;
            margin: 0;
            font-weight: 500;
          }
        }
      }
    }
  }

  .testimonials-section {
    padding: 4rem 2rem;
    background-color: #fff;

    .container {
      max-width: 1200px;
      margin: 0 auto;
      text-align: center;

      h2 {
        color: #2c3e50;
        font-size: 2.5rem;
        margin-bottom: 2rem;
        position: relative;
        padding-bottom: 1rem;

        &::after {
          content: '';
          position: absolute;
          bottom: 0;
          left: 50%;
          transform: translateX(-50%);
          width: 100px;
          height: 3px;
          background-color: #667eea;
        }
      }

      .testimonials-grid {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-around;
        gap: 2rem;
        max-width: 1200px;
        margin: 0 auto;

        .testimonial-item {
          flex: 1;
          min-width: 0;
          text-align: center;
          padding: 1.5rem 1rem;
          background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
          border-radius: 15px;
          border: 1px solid #e9ecef;
          transition: all 0.3s ease;
          box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);

          &:hover {
            transform: translateY(-8px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
            background: linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%);
          }

          .testimonial-content {
            max-width: 900px;
            margin: 0 auto 1rem;

            p {
              color: #666;
              font-size: 1.1rem;
              line-height: 1.8;
              margin-bottom: 1rem;
              text-align: left;
            }
          }

          .testimonial-author {
            color: #495057;
            font-size: 0.95rem;
            font-weight: 500;
          }
        }
      }
    }
  }

  .slogan-section {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    text-align: center;
    padding: 3rem 1.5rem;

    .slogan-inner {
      position: relative;

      .slogan-line {
        width: 100%;
        height: 2px;
        background-color: white;
        margin-bottom: 25px;
      }

      h2 {
        font-size: 2.2rem;
        margin-bottom: 25px;
        font-weight: 700;
        color: white;
        position: relative;
        padding-bottom: 1rem;
      }

      p {
        font-size: 1.05rem;
        line-height: 1.7;
        margin-bottom: 40px;
        opacity: 0.9;
        max-width: 600px;
        margin-left: auto;
        margin-right: auto;
        color: white;
      }
    }
  }

  .footer-nav {
    margin-top: 2rem;
    text-align: center;

    a {
      color: #fff;
      text-decoration: none;
      margin: 0 1.2rem;
      font-weight: 500;
      font-size: 1.1rem;
      letter-spacing: 1px;
      transition: color 0.2s;
      padding: 0.3em 0.8em;
      border-radius: 20px;
      display: inline-block;
    }
    a.router-link-exact-active,
    a:hover {
      background: rgba(255,255,255,0.18);
      color: #ffe082;
      text-decoration: none;
    }
  }

  @keyframes pulse {
    0% {
      transform: scale(1);
      opacity: 0.8;
    }
    50% {
      transform: scale(1.05);
      opacity: 1;
    }
    100% {
      transform: scale(1);
      opacity: 0.8;
    }
  }

  @keyframes bounce {
    0%, 20%, 50%, 80%, 100% {
      transform: translateY(0);
    }
    40% {
      transform: translateY(-10px);
    }
    60% {
      transform: translateY(-5px);
    }
  }
}

// 移动端样式
@media screen and (max-width: 768px) {
  .home {
    .hero {
      height: 60vh;
      padding: 1rem;
      background-position: 85% center;

      h1 {
        font-size: 2.5rem;
        margin-bottom: 1rem;
      }

      p {
        font-size: 1.2rem;
        padding: 0 1rem;
      }
    }

    .commitment-section {
      padding: 2rem 1rem;

      .container {
        h2 {
          font-size: 2rem;
          margin-bottom: 1.5rem;
        }

        .commitment-content {
          margin-bottom: 2rem;

          p {
            font-size: 1rem;
            line-height: 1.6;
            margin-bottom: 1rem;
          }
        }

        .service-button {
          padding: 12px 30px;
          font-size: 1rem;
        }
      }
    }

    .why-choose-us-section {
      padding: 2rem 1rem;

      .container {
        .statements-grid {
          flex-direction: column;
          gap: 1rem;

          .statement-item {
            min-width: auto;
            padding: 1.5rem 1rem;
            
            .statement-icon {
              width: 50px;
              height: 50px;
              background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
              border-radius: 50%;
              display: flex;
              align-items: center;
              justify-content: center;
              margin: 0 auto 1rem;

              i {
                font-size: 1.3rem;
                color: white;
              }
            }
            
            p {
              font-size: 1rem;
              line-height: 1.6;
            }
          }
        }
      }
    }

    .partners-section {
      padding: 2rem 1rem;

      .container {
        h2 {
          font-size: 2rem;
          margin-bottom: 1.5rem;
        }

        .partners-grid {
          flex-direction: column;
          gap: 1rem;

          .partner-item {
            min-width: auto;
            padding: 1.5rem 1rem;
            
            .partner-image {
              width: 180px;
              height: 100px;
              margin: 0 auto 0.8rem;
              border-radius: 10px;
              overflow: hidden;
              box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);

              img {
                width: 100%;
                height: 100%;
                object-fit: contain;
                background-color: white;
              }

              &.partner-image-cover img {
                object-fit: cover;
              }
            }
            
            h4 {
              font-size: 0.95rem;
            }
          }
        }
      }
    }

    .testimonials-section {
      padding: 2rem 1rem;

      .container {
        h2 {
          font-size: 2rem;
          margin-bottom: 1.5rem;
        }

        .testimonials-grid {
          flex-direction: column;
          gap: 1rem;

          .testimonial-item {
            min-width: auto;
            padding: 1.5rem 1rem;
            
            .testimonial-content {
              max-width: 900px;
              margin: 0 auto 1rem;

              p {
                font-size: 1rem;
                line-height: 1.6;
              }
            }
            
            .testimonial-author {
              font-size: 0.95rem;
            }
          }
        }
      }
    }

    .slogan-section {
      padding: 60px 20px;

      .slogan-inner {
        .slogan-line {
          width: 40px;
          height: 2px;
          margin-bottom: 20px;
        }

        h2 {
          font-size: 2rem;
          margin-bottom: 20px;
        }

        p {
          font-size: 1rem;
          line-height: 1.6;
        }
      }
    }

    .footer-nav {
      a {
        margin: 0 0.3rem;
        font-size: 1rem;
        padding: 0.3em 0.5em;
      }
    }
  }
}

// 平板样式
@media screen and (min-width: 769px) and (max-width: 1024px) {
  .home {
    .hero {
      height: 70vh;

      h1 {
        font-size: 3rem;
      }

      p {
        font-size: 1.5rem;
      }
    }

    .commitment-section {
      padding: 3rem 1.5rem;

      .container {
        h2 {
          font-size: 2.2rem;
        }

        .commitment-content {
          p {
            font-size: 1.05rem;
          }
        }

        .service-button {
          padding: 14px 35px;
          font-size: 1.05rem;
        }
      }
    }

    .why-choose-us-section {
      padding: 3rem 1.5rem;

      .container {
        .statements-grid {
          gap: 0.8rem;

          .statement-item {
            padding: 1.2rem 0.8rem;
            
            .statement-icon {
              width: 55px;
              height: 55px;
              background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
              border-radius: 50%;
              display: flex;
              align-items: center;
              justify-content: center;
              margin: 0 auto 0.8rem;

              i {
                font-size: 1.4rem;
                color: white;
              }
            }
            
            p {
              font-size: 0.9rem;
              line-height: 1.4;
            }
          }
        }
      }
    }

    .partners-section {
      padding: 3rem 1.5rem;

      .container {
        h2 {
          font-size: 2.2rem;
        }

        .partners-grid {
          gap: 0.8rem;

          .partner-item {
            padding: 1.2rem 0.8rem;
            
            .partner-image {
              width: 180px;
              height: 100px;
              margin: 0 auto 0.8rem;
              border-radius: 10px;
              overflow: hidden;
              box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);

              img {
                width: 100%;
                height: 100%;
                object-fit: contain;
                background-color: white;
              }

              &.partner-image-cover img {
                object-fit: cover;
              }
            }
            
            h4 {
              font-size: 0.95rem;
            }
          }
        }
      }
    }

    .testimonials-section {
      padding: 3rem 1.5rem;

      .container {
        h2 {
          font-size: 2.2rem;
        }

        .testimonials-grid {
          gap: 0.8rem;

          .testimonial-item {
            padding: 1.2rem 0.8rem;
            
            .testimonial-content {
              max-width: 900px;
              margin: 0 auto 1rem;

              p {
                font-size: 1rem;
                line-height: 1.6;
              }
            }
            
            .testimonial-author {
              font-size: 0.95rem;
            }
          }
        }
      }
    }

    .slogan-section {
      padding: 3rem 1.5rem;

      .slogan-inner {
        .slogan-line {
          width: 50px;
          height: 2.5px;
          margin-bottom: 25px;
        }

        h2 {
          font-size: 2.2rem;
        }

        p {
          font-size: 1.05rem;
          line-height: 1.7;
        }
      }
    }
  }
}

// 大屏幕样式
@media screen and (min-width: 1025px) {
  .home {
    .hero {
      height: 100vh;
      background-size: cover;
      background-position: center center;
    }
  }
}
</style> 