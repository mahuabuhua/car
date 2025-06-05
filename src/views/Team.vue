<template>
  <div class="team">
    <h1>{{ $t('team.title') }}</h1>
    <p>{{ $t('team.content') }}</p>
    <div class="team-grid">
      <div class="team-member">
        <img src="../assets/team1.jpg" alt="Team Member 1">
        <h3>John Smith</h3>
        <p>Tour Guide</p>
      </div>
      <div class="team-member">
        <img src="../assets/team2.jpg" alt="Team Member 2">
        <h3>Sarah Johnson</h3>
        <p>Travel Consultant</p>
      </div>
      <div class="team-member">
        <img src="../assets/team3.jpg" alt="Team Member 3">
        <h3>Mike Brown</h3>
        <p>Customer Service</p>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.team {
  padding: 2rem;
  max-width: 1200px;
  margin: 0 auto;

  h1 {
    color: #2c3e50;
    margin-bottom: 1rem;
    text-align: center;
  }

  p {
    text-align: center;
    color: #666;
    margin-bottom: 3rem;
  }

  .team-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
    padding: 1rem;

    .team-member {
      text-align: center;
      background: #f8f9fa;
      padding: 1rem;
      border-radius: 8px;
      transition: transform 0.3s ease;

      &:hover {
        transform: translateY(-5px);
      }

      img {
        width: 200px;
        height: 200px;
        border-radius: 50%;
        object-fit: cover;
        margin-bottom: 1rem;
      }

      h3 {
        color: #2c3e50;
        margin-bottom: 0.5rem;
      }

      p {
        color: #666;
        margin: 0;
      }
    }
  }
}
</style> 