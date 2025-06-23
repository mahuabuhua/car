<template>
  <div class="team-page">
    <div class="hero-section">
      <h1>{{ $t('team.title') }}</h1>
      <p>{{ $t('team.content') }}</p>
    </div>

    <div class="team-container">
      <div class="team-cards">
        <div class="team-card" v-for="(member, index) in teamMembers" :key="index">
          <div class="member-avatar">
            <i :class="member.icon"></i>
          </div>
          <h3>{{ member.name }}</h3>
          <p class="position">{{ member.position }}</p>
          <p class="description">{{ member.description }}</p>
          <div class="member-skills">
            <span v-for="(skill, skillIndex) in member.skills" :key="skillIndex" class="skill-tag">
              {{ skill }}
            </span>
          </div>
        </div>
      </div>
    </div>

    <div class="cta-section">
      <h2>{{ $t('team.cta.title') }}</h2>
      <p>{{ $t('team.cta.description') }}</p>
      <router-link to="/contact" class="cta-button">
        {{ $t('team.cta.button') }}
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Team',
  mounted() {
    // 确保页面加载时滚动到顶部
    window.scrollTo(0, 0)
  },
  data() {
    return {
      teamMembers: [
        {
          icon: 'fas fa-user-tie',
          name: this.$t('team.members.john.name'),
          position: this.$t('team.members.john.position'),
          description: this.$t('team.members.john.description'),
          skills: this.$t('team.members.john.skills')
        },
        {
          icon: 'fas fa-user-graduate',
          name: this.$t('team.members.sarah.name'),
          position: this.$t('team.members.sarah.position'),
          description: this.$t('team.members.sarah.description'),
          skills: this.$t('team.members.sarah.skills')
        },
        {
          icon: 'fas fa-headset',
          name: this.$t('team.members.mike.name'),
          position: this.$t('team.members.mike.position'),
          description: this.$t('team.members.mike.description'),
          skills: this.$t('team.members.mike.skills')
        }
      ],
      values: [
        {
          icon: 'fas fa-users',
          title: this.$t('team.values.collaboration.title'),
          description: this.$t('team.values.collaboration.description')
        },
        {
          icon: 'fas fa-lightbulb',
          title: this.$t('team.values.innovation.title'),
          description: this.$t('team.values.innovation.description')
        },
        {
          icon: 'fas fa-star',
          title: this.$t('team.values.excellence.title'),
          description: this.$t('team.values.excellence.description')
        },
        {
          icon: 'fas fa-heart',
          title: this.$t('team.values.passion.title'),
          description: this.$t('team.values.passion.description')
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
      this.teamMembers = [
        {
          icon: 'fas fa-user-tie',
          name: this.$t('team.members.john.name'),
          position: this.$t('team.members.john.position'),
          description: this.$t('team.members.john.description'),
          skills: this.$t('team.members.john.skills')
        },
        {
          icon: 'fas fa-user-graduate',
          name: this.$t('team.members.sarah.name'),
          position: this.$t('team.members.sarah.position'),
          description: this.$t('team.members.sarah.description'),
          skills: this.$t('team.members.sarah.skills')
        },
        {
          icon: 'fas fa-headset',
          name: this.$t('team.members.mike.name'),
          position: this.$t('team.members.mike.position'),
          description: this.$t('team.members.mike.description'),
          skills: this.$t('team.members.mike.skills')
        }
      ]
      this.values = [
        {
          icon: 'fas fa-users',
          title: this.$t('team.values.collaboration.title'),
          description: this.$t('team.values.collaboration.description')
        },
        {
          icon: 'fas fa-lightbulb',
          title: this.$t('team.values.innovation.title'),
          description: this.$t('team.values.innovation.description')
        },
        {
          icon: 'fas fa-star',
          title: this.$t('team.values.excellence.title'),
          description: this.$t('team.values.excellence.description')
        },
        {
          icon: 'fas fa-heart',
          title: this.$t('team.values.passion.title'),
          description: this.$t('team.values.passion.description')
        }
      ]
    }
  }
}
</script>

<style lang="scss" scoped>
.team-page {
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

.team-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  margin-bottom: 80px;
}

.team-cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 30px;
}

.team-card {
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

  .member-avatar {
    width: 100px;
    height: 100px;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto 20px;

    i {
      font-size: 2.5rem;
      color: white;
    }
  }

  h3 {
    color: #2c3e50;
    font-size: 1.8rem;
    margin-bottom: 10px;
    font-weight: 700;
  }

  .position {
    color: #667eea;
    font-size: 1.2rem;
    font-weight: 600;
    margin-bottom: 15px;
  }

  .description {
    color: #666;
    line-height: 1.6;
    margin-bottom: 20px;
    font-size: 1rem;
  }

  .member-skills {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    justify-content: center;

    .skill-tag {
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
      padding: 5px 12px;
      border-radius: 20px;
      font-size: 0.85rem;
      font-weight: 500;
    }
  }
}

.values-section {
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

.values-grid {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 40px;
}

.value-item {
  text-align: center;
  padding: 20px;

  .value-icon {
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
    font-size: 1.3rem;
    margin-bottom: 15px;
    font-weight: 600;
  }

  p {
    color: #666;
    line-height: 1.6;
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

  .team-cards {
    grid-template-columns: 1fr;
    gap: 20px;
  }

  .team-card {
    padding: 30px 20px;
  }

  .values-grid {
    grid-template-columns: 1fr;
    gap: 30px;
  }

  .values-section {
    padding: 60px 20px;

    h2 {
      font-size: 2rem;
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
}
</style> 