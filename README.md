<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>GitHub Stats - Dark Layout</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="github-stats-container">
    <div class="profile-header">
      <img src="https://via.placeholder.com/150" alt="Profile Picture" class="profile-image">
      <h1 class="username">GitHub Username</h1>
    </div>

    <div class="stats-grid">
      <div class="stat-card total-repos">
        <h3>Total Repositories</h3>
        <div class="stat-value">45</div>
      </div>

      <div class="stat-card total-commits">
        <h3>Total Commits</h3>
        <div class="stat-value">1,234</div>
      </div>

      <div class="stat-card followers">
        <h3>Followers</h3>
        <div class="stat-value">256</div>
      </div>

      <div class="stat-card contributions">
        <h3>Contributions</h3>
        <div class="stat-value">3,456</div>
      </div>
    </div>

    <div class="language-stats">
      <h2>Language Distribution</h2>
      <div class="language-bars">
        <div class="language-bar" style="--percent: 45%; --color: #f1e05a;">
          <span class="lang-name">JavaScript</span>
          <span class="lang-percent">45%</span>
        </div>
        <div class="language-bar" style="--percent: 30%; --color: #3572A5;">
          <span class="lang-name">Python</span>
          <span class="lang-percent">30%</span>
        </div>
        <div class="language-bar" style="--percent: 15%; --color: #e34c26;">
          <span class="lang-name">HTML</span>
          <span class="lang-percent">15%</span>
        </div>
        <div class="language-bar" style="--percent: 10%; --color: #563d7c;">
          <span class="lang-name">CSS</span>
          <span class="lang-percent">10%</span>
        </div>
      </div>
    </div>
  </div>

  <script src="script.js"></script>
</body>
</html>

// Optional: Add dynamic fetching of GitHub stats
async function fetchGitHubStats(username) {
  try {
    const response = await fetch(`https://api.github.com/users/${username}`);
    const userData = await response.json();

    document.querySelector('.username').textContent = userData.login;
    document.querySelector('.profile-image').src = userData.avatar_url;

    // You would need additional API calls or GitHub GraphQL API 
    // to fetch more detailed stats like total commits, languages, etc.
  } catch (error) {
    console.error('Error fetching GitHub stats:', error);
  }
}

// Uncomment and replace 'yourusername' with actual GitHub username
// fetchGitHubStats('yourusername');

// Optional: Add animations or interactions
document.addEventListener('DOMContentLoaded', () => {
  const languageBars = document.querySelectorAll('.language-bar');

  languageBars.forEach(bar => {
    bar.addEventListener('mouseenter', () => {
      bar.style.transform = 'scale(1.05)';
    });

    bar.addEventListener('mouseleave', () => {
      bar.style.transform = 'scale(1)';
    });
  });
});

:root {
  --bg-dark: #121212;
  --card-dark: #1e1e1e;
  --text-primary: #e0e0e0;
  --accent-color: #bb86fc;
  --accent-variant: #3700b3;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Arial', sans-serif;
  background-color: var(--bg-dark);
  color: var(--text-primary);
  line-height: 1.6;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 20px;
}

.github-stats-container {
  background-color: var(--card-dark);
  border-radius: 12px;
  padding: 30px;
  width: 100%;
  max-width: 800px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
}

.profile-header {
  display: flex;
  align-items: center;
  margin-bottom: 30px;
}

.profile-image {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  margin-right: 20px;
  border: 3px solid var(--accent-color);
}

.username {
  font-size: 2rem;
  color: var(--accent-color);
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
  margin-bottom: 30px;
}

.stat-card {
  background-color: var(--bg-dark);
  border-radius: 8px;
  padding: 20px;
  text-align: center;
  border: 1px solid var(--accent-variant);
}

.stat-card h3 {
  color: var(--accent-color);
  margin-bottom: 10px;
}

.stat-value {
  font-size: 2rem;
  font-weight: bold;
  color: var(--text-primary);
}

.language-stats {
  background-color: var(--bg-dark);
  border-radius: 8px;
  padding: 20px;
  border: 1px solid var(--accent-variant);
}

.language-stats h2 {
  color: var(--accent-color);
  margin-bottom: 15px;
  text-align: center;
}

.language-bars {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.language-bar {
  background-color: var(--card-dark);
  border-radius: 5px;
  overflow: hidden;
  position: relative;
  height: 30px;
}

.language-bar::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: var(--percent, 0%);
  background-color: var(--color);
  transition: width 1s ease-in-out;
}

.language-bar span {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 1;
  color: white;
  padding: 0 10px;
}

.lang-name {
  left: 0;
}

.lang-percent {
  right: 0;
}

@media (max-width: 600px) {
  .stats-grid {
    grid-template-columns: 1fr;
  }
}

