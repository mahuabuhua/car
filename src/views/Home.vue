<template>
  <div class="home">
    <div class="hero">
      <h1>{{ $t('home.title') }}</h1>
      <p>{{ $t('home.description') }}</p>
    </div>
    <div class="services-section">
      <div class="container">
        <h2>{{ $t('home.services.title') }}</h2>
        <p class="services-intro">{{ $t('home.services.intro') }}</p>
        
        <div class="services-grid">
          <div class="service-card">
            <h3>{{ $t('home.services.sections.largeCoach.title') }}</h3>
            <ul>
              <li v-for="(feature, index) in $t('home.services.sections.largeCoach.features')" :key="index">
                {{ feature }}
              </li>
            </ul>
          </div>

          <div class="service-card">
            <h3>{{ $t('home.services.sections.smallCoach.title') }}</h3>
            <ul>
              <li v-for="(feature, index) in $t('home.services.sections.smallCoach.features')" :key="index">
                {{ feature }}
              </li>
            </ul>
          </div>

          <div class="service-card">
            <h3>{{ $t('home.services.sections.tourGuide.title') }}</h3>
            <ul>
              <li v-for="(feature, index) in $t('home.services.sections.tourGuide.features')" :key="index">
                {{ feature }}
              </li>
            </ul>
          </div>

          <div class="service-card">
            <h3>{{ $t('home.services.sections.cruiseShip.title') }}</h3>
            <ul>
              <li v-for="(feature, index) in $t('home.services.sections.cruiseShip.features')" :key="index">
                {{ feature }}
              </li>
            </ul>
          </div>
        </div>

        <div class="guided-tour-section">
          <p>{{ $t('home.services.guidedTour') }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.home {
  .hero {
    background-image: url('../assets/nz-hero.jpg');
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

  .services-section {
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
          background-color: #42b983;
        }
      }

      .services-intro {
        color: #666;
        font-size: 1.2rem;
        line-height: 1.8;
        max-width: 900px;
        margin: 0 auto 3rem;
      }

      .services-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
        gap: 2rem;
        padding: 1rem;

        .service-card {
          background: #f8f9fa;
          padding: 2rem;
          border-radius: 8px;
          text-align: left;
          transition: transform 0.3s ease, box-shadow 0.3s ease;
          box-shadow: 0 2px 4px rgba(0,0,0,0.1);

          &:hover {
            transform: translateY(-5px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
          }

          h3 {
            color: #2c3e50;
            font-size: 1.5rem;
            margin-bottom: 1.5rem;
            padding-bottom: 0.5rem;
            border-bottom: 2px solid #42b983;
          }

          ul {
            list-style: none;
            padding: 0;
            margin: 0;

            li {
              color: #666;
              font-size: 1rem;
              line-height: 1.6;
              margin-bottom: 1rem;
              padding-left: 1.5rem;
              position: relative;

              &::before {
                content: '•';
                color: #42b983;
                position: absolute;
                left: 0;
                font-size: 1.2rem;
              }

              &:last-child {
                margin-bottom: 0;
              }
            }
          }
        }
      }
    }
  }

  .gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
    padding: 2rem;
    max-width: 1400px;
    margin: 0 auto;

    img {
      width: 100%;
      height: 400px;
      object-fit: cover;
      border-radius: 12px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
      transition: transform 0.3s ease, box-shadow 0.3s ease;

      &:hover {
        transform: scale(1.05);
        box-shadow: 0 6px 12px rgba(0,0,0,0.2);
      }
    }
  }
}

.guided-tour-section {
  margin-top: 3rem;
  text-align: center;
  padding: 2rem;
  background-color: rgba(66, 185, 131, 0.1);
  border-radius: 8px;

  p {
    color: #2c3e50;
    font-size: 1.2rem;
    line-height: 1.6;
    margin: 0;
    font-style: italic;
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

    .services-section {
      padding: 2rem 1rem;

      .container {
        h2 {
          font-size: 2rem;
          margin-bottom: 1.5rem;
        }

        .services-intro {
          font-size: 1rem;
          line-height: 1.6;
          margin-bottom: 2rem;
          padding: 0 1rem;
        }

        .services-grid {
          grid-template-columns: 1fr;
          gap: 1.5rem;
          padding: 0.5rem;

          .service-card {
            padding: 1.5rem;

            h3 {
              font-size: 1.3rem;
              margin-bottom: 1rem;
            }

            ul li {
              font-size: 0.95rem;
              margin-bottom: 0.8rem;
            }
          }
        }
      }
    }

    .gallery {
      grid-template-columns: 1fr;
      gap: 1rem;
      padding: 1rem;

      img {
        height: 300px;
        border-radius: 8px;
      }
    }

    .guided-tour-section {
      margin-top: 2rem;
      padding: 1.5rem;

      p {
        font-size: 1rem;
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

    .services-section {
      padding: 3rem 1.5rem;

      .container {
        h2 {
          font-size: 2.2rem;
        }

        .services-intro {
          font-size: 1.1rem;
        }

        .services-grid {
          grid-template-columns: repeat(2, 1fr);
          gap: 1.5rem;
        }
      }
    }

    .gallery {
      grid-template-columns: repeat(2, 1fr);
      gap: 1.5rem;
      padding: 1.5rem;

      img {
        height: 350px;
      }
    }

    .guided-tour-section {
      margin-top: 2.5rem;
      padding: 1.8rem;

      p {
        font-size: 1.1rem;
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