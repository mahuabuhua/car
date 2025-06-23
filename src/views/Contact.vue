<template>
  <div class="contact-page">
    <div class="hero-section">
      <h1>{{ $t('contact.title') }}</h1>
      <p>{{ $t('contact.content') }}</p>
    </div>

    <div class="contact-container">
      <div class="contact-cards">
        <div class="contact-card">
          <div class="contact-icon">
            <i class="fas fa-phone"></i>
          </div>
          <h3>{{ $t('contact.phone.label') }}</h3>
          <p>{{ $t('contact.phone.number') }}</p>
        </div>
        <div class="contact-card">
          <div class="contact-icon">
            <i class="fas fa-envelope"></i>
          </div>
          <h3>{{ $t('contact.email.label') }}</h3>
          <p>{{ $t('contact.email.address') }}</p>
        </div>
      </div>
    </div>

    <div class="contact-form-section">
      <h2>{{ $t('contact.form.title') }}</h2>
      <div class="form-container">
        <form @submit.prevent="submitForm" class="contact-form">
          <div class="form-group">
            <label for="name">{{ $t('contact.form.name') }}</label>
            <input 
              type="text" 
              id="name" 
              v-model="form.name" 
              :placeholder="$t('contact.form.namePlaceholder')"
              required
            >
          </div>
          <div class="form-group">
            <label for="email">{{ $t('contact.form.email') }}</label>
            <input 
              type="email" 
              id="email" 
              v-model="form.email" 
              :placeholder="$t('contact.form.emailPlaceholder')"
              required
            >
          </div>
          <div class="form-group">
            <label for="tittle">{{ $t('contact.form.tittle') }}</label>
            <input 
              type="text" 
              id="tittle" 
              v-model="form.tittle" 
              :placeholder="$t('contact.form.tittlePlaceholder')"
            >
          </div>
          <div class="form-group">
            <label for="message">{{ $t('contact.form.message') }}</label>
            <textarea 
              id="message" 
              v-model="form.message" 
              :placeholder="$t('contact.form.messagePlaceholder')"
              rows="5"
              required
            ></textarea>
          </div>
          <button type="submit" class="submit-button">
            {{ $t('contact.form.submit') }}
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Contact',
  mounted() {
    // 确保页面加载时滚动到顶部
    window.scrollTo(0, 0)
  },
  data() {
    return {
      form: {
        name: '',
        email: '',
        tittle: '',
        message: ''
      }
    }
  },
  methods: {
    submitForm() {
      // 获取当前时间，格式为"2024-05-01T12:00:00"
      const now = new Date()
      const time = now.toISOString().slice(0, 19)
      const payload = {
        ...this.form,
        time
      }
      this.$axios.post('/api/user-contacts/save', payload)
        .then(() => {
          this.$message
            ? this.$message.success(this.$t('contact.form.success'))
            : alert(this.$t('contact.form.success'))
          this.form = { name: '', email: '', tittle: '', message: '' }
        })
        .catch(() => {
          this.$message
            ? this.$message.error(this.$t('contact.form.fail'))
            : alert(this.$t('contact.form.fail'))
        })
    }
  }
}
</script>

<style lang="scss" scoped>
.contact-page {
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

.contact-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  margin-bottom: 80px;
}

.contact-cards {
  display: flex;
  justify-content: center;
  gap: 40px;
  flex-wrap: wrap;
}

.contact-card {
  flex: 1 1 300px;
  max-width: 400px;
  min-width: 220px;
  background: white;
  border-radius: 15px;
  padding: 40px 30px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  text-align: center;
  transition: transform 0.3s, box-shadow 0.3s;
  margin-bottom: 0;

  &:hover {
    transform: translateY(-10px);
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
  }

  .contact-icon {
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
    color: #667eea;
    font-size: 1.1rem;
    font-weight: 500;
    word-break: break-all;
  }
}

.contact-form-section {
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

.form-container {
  max-width: 600px;
  margin: 0 auto;
}

.contact-form {
  .form-group {
    margin-bottom: 25px;

    label {
      display: block;
      color: #2c3e50;
      font-weight: 600;
      margin-bottom: 8px;
      font-size: 1rem;
    }

    input, textarea {
      width: 100%;
      padding: 15px;
      border: 2px solid #e1e5e9;
      border-radius: 10px;
      font-size: 1rem;
      transition: border-color 0.3s ease;
      background: #f8f9fa;

      &:focus {
        outline: none;
        border-color: #667eea;
        background: white;
      }

      &::placeholder {
        color: #999;
      }
    }

    textarea {
      resize: vertical;
      min-height: 120px;
    }
  }

  .submit-button {
    width: 100%;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 15px;
    border: none;
    border-radius: 10px;
    font-size: 1.1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);

    &:hover {
      transform: translateY(-3px);
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
    }
  }
}

@media (max-width: 900px) {
  .contact-cards {
    flex-direction: column;
    gap: 20px;
    align-items: stretch;
  }
  .contact-card {
    max-width: 100%;
    margin-bottom: 0;
  }
  .form-container {
    max-width: 100vw;
    padding: 0 8px;
  }
  .contact-form .form-group input,
  .contact-form .form-group textarea {
    max-width: 100%;
    min-width: 0;
    box-sizing: border-box;
    margin: 0 auto;
    font-size: 1rem;
  }
}
</style> 