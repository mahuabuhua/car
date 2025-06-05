<template>
  <div class="about">
    <div class="business-section">
      <div class="container">
        <h2>{{ $t('about.business.title') }}</h2>
        <p>{{ $t('about.business.description') }}</p>
      </div>
    </div>
  </div> 
</template>

<style lang="scss" scoped>
.about {
  .business-section {
    padding: 4rem 2rem;

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

      p {
        color: #666;
        font-size: 1.2rem;
        line-height: 1.8;
        max-width: 900px;
        margin: 0 auto;
      }
    }
  }
}

@media (max-width: 768px) {
  .about {
    .business-section {
      padding: 2rem 1rem;

      .container {
        h2 {
          font-size: 2rem;
          margin-bottom: 1.5rem;
        }

        p {
          font-size: 1rem;
          line-height: 1.6;
          padding: 0 1rem;
        }
      }
    }
  }
}

@media (min-width: 769px) and (max-width: 1024px) {
  .about {
    .business-section {
      padding: 3rem 1.5rem;

      .container {
        h2 {
          font-size: 2.2rem;
        }

        p {
          font-size: 1.1rem;
        }
      }
    }
  }
}
</style> 