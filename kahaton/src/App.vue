<template>
  <div>
    <div class="top-bar">
        <div class="top-bar-content">
            <div class="logo">
                <img class="image_logo" src="../src/components/icons/photo_2025-10-08_19-36-59.jpg" alt="Логотип команды">
            </div>
            <div class="nav-links">
                <router-link to="/" exact>Главная</router-link>
                <router-link to="/info">О нас</router-link>
            </div>
        </div>
    </div>
  <div id="app">
    <router-view></router-view>
  </div>
  </div>
  
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

body {
  background: linear-gradient(135deg, #ffffff 0%, #ffffff 100%);
  min-height: 100vh;
}

.top-bar {
    background: linear-gradient(135deg, #2c5aa0 0%, #1e3d6f 100%);
    color: white;
    padding: 15px 0;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.top-bar-content {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.logo {
    font-size: 24px;
    font-weight: bold;
    color: white;
}

.image_logo {
    height: 60px;
    width: auto;
    border-radius: 5px;
}

.nav-links {
    display: flex;
    gap: 20px;
}

.nav-links a {
    color: white;
    text-decoration: none;
    font-weight: 500;
    transition: all 0.5s;
}

.nav-links a:hover {
    opacity: 0.8;
    transform: scale(120%) translateY(-3.5px);
}
</style>