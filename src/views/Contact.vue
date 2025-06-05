<template>
  <div class="contact">
    <div class="contact-header">
      <h1>{{ $t('contact.title') }}</h1>
      <p>{{ $t('contact.content') }}</p>
    </div>

    <div class="contact-info">
      <div class="info-card">
        <h2>{{ $t('contact.phone.label') }}</h2>
        <p>{{ $t('contact.phone.number') }}</p>
      </div>
      <div class="info-card">
        <h2>{{ $t('contact.email.label') }}</h2>
        <p>{{ $t('contact.email.address') }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: '',
        email: '',
        message: ''
      }
    }
  },
  methods: {
    submitForm() {
      // 这里添加表单提交逻辑
      console.log('Form submitted:', this.form)
    }
  }
}
</script>

<style lang="scss" scoped>
.contact {
  padding: 2rem;
  max-width: 800px;
  margin: 0 auto;

  .contact-header {
    text-align: center;
    margin-bottom: 3rem;

    h1 {
      color: #2c3e50;
      font-size: 2.5rem;
      margin-bottom: 1rem;
    }

    p {
      color: #666;
      font-size: 1.2rem;
      max-width: 600px;
      margin: 0 auto;
    }
  }

  .contact-info {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 2rem;

    .info-card {
      background-color: #f8f9fa;
      padding: 2rem;
      border-radius: 8px;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
      transition: transform 0.3s ease;
      text-align: center;

      &:hover {
        transform: translateY(-5px);
        background-color: #f8f9fa;
      }

      h2 {
        color: #2c3e50;
        font-size: 1.5rem;
        margin-bottom: 1rem;
        font-weight: 600;
      }

      p {
        color: #42b983;
        font-size: 1.2rem;
        word-break: break-all;
        font-weight: 500;
      }
    }
  }
}

@media (max-width: 768px) {
  .contact {
    padding: 1rem;

    .contact-header {
      margin-bottom: 2rem;

      h1 {
        font-size: 2rem;
      }

      p {
        font-size: 1rem;
      }
    }

    .contact-info {
      grid-template-columns: 1fr;
      gap: 1.5rem;

      .info-card {
        padding: 1.5rem;

        h2 {
          font-size: 1.3rem;
        }

        p {
          font-size: 1.1rem;
        }
      }
    }
  }
}
</style> 