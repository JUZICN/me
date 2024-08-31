<template>
  <div id="app">
    <button class="mode-selector" id="modeSelector">
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-sun">
        <circle cx="12" cy="12" r="4"></circle>
        <path d="M12 2v2"></path>
        <path d="M12 20v2"></path>
        <path d="m4.93 4.93 1.41 1.41"></path>
        <path d="m17.66 17.66 1.41 1.41"></path>
        <path d="M2 12h2"></path>
        <path d="M20 12h2"></path>
        <path d="m6.34 17.66-1.41 1.41"></path>
        <path d="m19.07 4.93-1.41 1.41"></path>
      </svg>
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-moon">
        <path d="M12 3a6 6 0 0 0 9 9 9 9 0 1 1-9-9Z"></path>
      </svg>
    </button>
    <div class="dropdown-menu" id="dropdownMenu">
      <button data-mode="light">Light</button>
      <button data-mode="dark">Dark</button>
      <button data-mode="system">System</button>
    </div>
    <AboutMe />
  </div>
</template>

<script>
import AboutMe from './components/AboutMe.vue';

export default {
  components: {
    AboutMe
  },
  mounted() {
    this.initMode();
    this.addEventListeners();
  },
  methods: {
    setMode(mode) {
      const modeSelector = document.getElementById('modeSelector');
      if (mode === 'dark') {
        document.body.classList.add('dark-mode');
        document.body.classList.remove('light-mode');
        modeSelector.querySelector('.lucide-sun').style.display = 'none';
        modeSelector.querySelector('.lucide-moon').style.display = 'block';
      } else if (mode === 'light') {
        document.body.classList.remove('dark-mode');
        document.body.classList.add('light-mode');
        modeSelector.querySelector('.lucide-sun').style.display = 'block';
        modeSelector.querySelector('.lucide-moon').style.display = 'none';
      } else {
        document.body.classList.remove('dark-mode', 'light-mode');
        const detectedMode = this.detectColorScheme();
        if (detectedMode === 'dark') {
          document.body.classList.add('dark-mode');
        } else {
          document.body.classList.add('light-mode');
        }
        modeSelector.querySelector('.lucide-sun').style.display = document.body.classList.contains('dark-mode') ? 'none' : 'block';
        modeSelector.querySelector('.lucide-moon').style.display = document.body.classList.contains('dark-mode') ? 'block' : 'none';
      }
    },
    detectColorScheme() {
      return window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light';
    },
    initMode() {
      const savedMode = localStorage.getItem('color-mode');
      if (savedMode) {
        this.setMode(savedMode);
      } else {
        this.setMode('system');
      }
    },
    addEventListeners() {
      const modeSelector = document.getElementById('modeSelector');
      const dropdownMenu = document.getElementById('dropdownMenu');
      
      modeSelector.addEventListener('click', (event) => {
        event.stopPropagation();
        dropdownMenu.classList.toggle('show');
        dropdownMenu.classList.toggle('dark-mode', document.body.classList.contains('dark-mode'));
      });
      
      dropdownMenu.addEventListener('click', (e) => {
        if (e.target.tagName === 'BUTTON') {
          const selectedMode = e.target.getAttribute('data-mode');
          this.setMode(selectedMode);
          localStorage.setItem('color-mode', selectedMode);
          dropdownMenu.classList.remove('show');
        }
      });
      
      window.addEventListener('click', (e) => {
        if (!modeSelector.contains(e.target) && !dropdownMenu.contains(e.target)) {
          dropdownMenu.classList.remove('show');
        }
      });
      
      window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', () => {
        if (!localStorage.getItem('color-mode')) {
          this.setMode(this.detectColorScheme());
        }
      });
    }
  }
};
</script>

<style>
body {
  font-family: 'Inter', sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f9f9f9;
  color: #333;
  transition: background-color 0.5s, color 0.5s;
}
footer {
    text-align: center; /* 使文字水平居中 */
    display: flex;
    flex-direction: column; /* 使文字按列排列 */
    justify-content: center; /* 垂直居中 */
    align-items: center; /* 水平居中 */
    font-size: 14px;
}

footer p {
    margin: 0; /* 移除段落之间的默认间距 */
}
footer a {
    color: #000;
}
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 20px;
}

[data-theme='dark'] {
  background-color: #1a1a1a;
  color: #f9f9f9;
}

[data-theme='dark'] .about-me {
  background-color: #262626;
}

.light-mode {
  background-color: #ffffff;
  color: #000000;
}

.dark-mode {
  background-color: #000000;
  color: #ffffff;
}

.dark-mode *:not(a) {
  color: #ffffff;
}

.dark-mode .contact a {
  color: #fff;
}
.dark-mode .projects a {
  color: #fff;
}

.dark-mode .project-item{
  background-color: #000;
}
.dark-mode .education-item {
  background-color: #000;
}
.dark-mode .project-item p {
  color: #ddd;
}
.dark-mode .education-item p {
  color: #ddd;
}
.dark-mode .project-header h4 {
  color: #fff;
}
.dark-mode .edu-header h4 {
  color: #fff;
}
/* Adjust text colors for dark mode */
.dark-mode .info h1 {
  color: #ffffff; /* White color for name */
}

.dark-mode .info h2 {
  color: #e0e0e0; /* Light gray color for profession */
}

.dark-mode .info p {
  color: #b0b0b0; /* Lighter gray color for location */
}

.mode-selector {
  position: fixed;
  top: 20px;
  right: 20px;
  width: 40px;
  height: 40px;
  background: transparent;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background-color 0.3s;
}

.mode-selector:hover {
  background-color: rgba(0, 0, 0, 0.1);
}

.dropdown-menu {
  position: absolute;
  top: 60px;
  right: 20px;
  width: 100px;
  background-color: #ffffff;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  opacity: 0;
  transform: translateY(-10px);
  visibility: hidden;
  transition: opacity 0.3s, transform 0.3s, visibility 0.3s, border-color 0.3s;
}

.dropdown-menu.dark-mode {
  background-color: #333;
  border-color: #333;
  color: #ffffff;
}

.dropdown-menu.show {
  opacity: 1;
  transform: translateY(0);
  visibility: visible;
}

.dropdown-menu button {
  width: 100%;
  padding: 10px 15px;
  background: transparent;
  border: none;
  text-align: left;
  cursor: pointer;
  color: #000000;
  transition: background-color 0.3s;
}

.dropdown-menu button:hover {
  background-color: rgba(0, 0, 0, 0.1);
}

.dark-mode .dropdown-menu button {
  color: #ffffff;
}

.lucide {
  fill: none;
  stroke: currentColor;
}

.lucide-sun, .lucide-moon {
  transition: opacity 0.3s;
}

.dark-mode .lucide-sun {
  opacity: 0;
}

.dark-mode .lucide-moon {
  opacity: 1;
  stroke: #ffffff;
}

.light-mode .lucide-sun {
  opacity: 1;
  stroke: #000000;
}

.light-mode .lucide-moon {
  opacity: 0;
}
::selection {
  color: #000;
  background-color: #DCDCDC;
}
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap');

* {
    font-family: 'Inter', sans-serif;
}

::-webkit-scrollbar {
    width: 0px;
    background: transparent;
}

html {
    overflow: -moz-scrollbars-none;
}

body {
    overflow: auto;
}
</style>

