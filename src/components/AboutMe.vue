<template>
    <div class="about-me">
      <button class="mode-selector" @click="toggleDropdown">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        </svg>
        <div class="dropdown-menu" v-show="dropdownVisible">
          <button @click="changeMode('light')">Light Mode</button>
          <button @click="changeMode('dark')">Dark Mode</button>
        </div>
      </button>
      
      <div class="header animate-enter staggered">
        <a href="https://juz1.cn" target="_blank"><img :src="profileImage" alt="Juzi" class="profile-image" /></a>
        <div class="info">
          <h1>{{ name }}</h1>
          <h2>{{ profession }}</h2>
          <p>{{ location }}</p>
        </div>
      </div>
  
      <div class="content">
        <section class="projects">
          <h3>Projects</h3>
          <div v-for="(project, index) in projects" :key="index" class="project-item animate-enter staggered">
            <div class="project-header">
              <h4>{{ project.name }}</h4>
              <a :href="project.link" target="_blank">View Project</a>
            </div>
            <p>{{ project.description }}</p>
          </div>
        </section>
  
        <section class="education">
          <h3>Education</h3>
          <div v-for="(edu, index) in education" :key="index" class="education-item animate-enter staggered">
            <div class="edu-header">
              <h4>{{ edu.institution }}</h4>
              <p>{{ edu.years }}</p>
            </div>
            <p>{{ edu.degree }}</p>
          </div>
        </section>
  
        <section class="contact">
          <h3>Contact</h3>
          <p>Email: <a :href="'mailto:' + contact.email">{{ contact.email }}</a></p>
          <p>Blog: <a :href="contact.blog" target="_blank">{{ contact.blog }}</a></p>
          <p>GitHub: <a :href="contact.github" target="_blank">{{ contact.github }}</a></p>
        </section>
        <footer class="footer">
      <p>&copy; 2023-2024 <a href="https://juz1.cn" target="_blank">Juzi</a> Made with ❤</p>
      <a href="https://beian.miit.gov.cn/" target="_blank">鄂ICP备2024068469号-1</a>
  </footer>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        name: "Juzi",
        profession: "Student",
        location: "Shandong",
        profileImage: "https://juz1.cn/_next/image?url=%2Favatar.png&w=96&q=75", // Replace with your image URL
        projects: [
          {
            name: "Personal Website",
            description: "The website to introduce me",
            link: "https://juz1.cn"
          },
          {
            name: "Sponsor Site",
            description: "Sponsor me",
            link: "https://sponsor.juz1.cn"
          }
        ],
        education: [
          {
            institution: "AnZhou Primary School",
            degree: "XianJu,Taizhou,Zhejiang",
            years: "2016 - 2022"
          },
          {
            institution: "YuXin School",
            degree: "Changyi,Weifang,Shandong",
            years: "2022 - NOW"
          }
        ],
        contact: {
          email: "i@juz1.cn",
          blog: "https://juz1.cn/blog",
          github: "https://github.com/JUZICN"
        },
        dropdownVisible: false,
      };
    },
    methods: {
      toggleDropdown() {
        this.dropdownVisible = !this.dropdownVisible;
      },
      changeMode(mode) {
        document.documentElement.setAttribute('data-theme', mode);
        this.dropdownVisible = false;
      }
    }
  };
  </script>
  
  <style scoped lang="scss">
  .about-me {
    max-width: 800px;
    margin: 0 auto;
    padding: 50px 20px;
    font-family: 'Inter', sans-serif;
    color: #1a1a1a;
  }
  
  .header {
    display: flex;
    align-items: center;
    margin-bottom: 60px;
  }
  
  .profile-image {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    margin-right: 40px;
  }
  
  .info h1 {
    margin: 0;
    font-size: 2rem;
    font-weight: 600;
    color: #333;
  }
  
  .info h2 {
    margin-top: 5px;
    font-size: 1.2rem;
    font-weight: 400;
    color: #555;
  }
  
  .info p {
    margin-top: 5px;
    font-size: 0.9rem;
    font-weight: 300;
    color: #777;
  }
  
  .content {
    margin-top: 30px;
  }
  
  section {
    margin-bottom: 50px;
  }
  
  h3 {
    font-size: 1.5rem;
    margin-bottom: 15px;
    color: #333;
    font-weight: 500;
  }
  
  .project-item, .education-item {
    margin-bottom: 30px;
    padding: 10px;
    border-radius: 8px;
    background-color: #fff;
    transition: background-color 0.3s ease, transform 0.3s ease;
  }
  
  .project-item:hover, .education-item:hover {
    background-color: #ebebeb;
    transform: translateY(-3px);
  }
  
  .project-header, .edu-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  .project-header h4, .edu-header h4 {
    font-size: 1.1rem;
    margin: 0;
    color: #444;
  }
  
  .project-header a, .edu-header p {
    font-size: 0.9rem;
    color: #000;
    text-decoration: none;
  }
  
  .project-header a:hover, .edu-header p:hover {
    text-decoration: underline;
  }
  
  .project-item p, .education-item p {
    margin-top: 8px;
    font-size: 0.9rem;
    color: #555;
  }
  
  .contact p {
    font-size: 0.9rem;
    margin-bottom: 8px;
    transition: all 0.3s ease;
  }
  
  .contact a {
    color: #000;
    text-decoration: none;
  }
  
  .contact a:hover {
    text-decoration: underline;
  }
  
  /* Keyframes and animations */
  @keyframes enter {
    from {
      opacity: 0;
      transform: translateY(10px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  
  .animate-enter {
    animation: enter 0.3s ease both;
    animation-delay: var(--delay, 120ms);
  }
  
  .staggered {
    --delay: calc(var(--stagger) * 100ms);
  }
  
  .staggered:nth-child(1) {
    --stagger: 0.5;
  }
  .staggered:nth-child(2) {
    --stagger: 1;
  }
  .staggered:nth-child(3) {
    --stagger: 1.5;
  }
  
  /* Mode selector styles */
  .mode-selector {
    background: transparent;
    border: none;
    cursor: pointer;
    position: fixed;
    top: 16px;
    right: 16px;
    z-index: 1000;
  }
  
  .mode-selector svg {
    display: block;
    transition: opacity 0.3s ease;
  }
  
  .dropdown-menu {
    display: none;
    position: absolute;
    top: 50px;
    right: 0;
    background: white;
    border: 1px solid #ddd;
    border-radius: 4px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    z-index: 1000;
  }
  
  .dropdown-menu button {
    display: block;
    background: none;
    border: none;
    padding: 8px 16px;
    cursor: pointer;
    width: 100%;
    text-align: left;
  }
  
  .dropdown-menu button:hover {
    background: #f0f0f0;
  }
  </style>
  
  