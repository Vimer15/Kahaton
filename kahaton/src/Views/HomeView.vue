<template>
    <body>
    <div class="main-content">
        <div class="sidebar">
            <h3 class="sidebar-title">Последние запросы</h3>
            <ul class="history-list" id="historyList">
            </ul>
        </div>

        <div class="search-container">
            <h1 class="search-title">Введите ваш запрос</h1>
            <form class="search-form" id="searchForm">
                <input type="text" class="search-input" placeholder="Введите запрос" required id="searchInput">
                <div class="button-group">
                    <button type="submit" class="search-button">Найти</button>
                    <button type="button" class="search-button" id="uploadButton">Загрузить файл</button>
                </div>
            </form>
        </div>
    </div>
</body>
</template>
<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Arial', sans-serif;
}

body {
    background: linear-gradient(135deg, #e6f2ff 0%, #ffffff 100%);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
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
    transition: all 0.5s;
}

.nav-links a:hover {
    opacity: 0.8;
    transform: scale(120%) translateY(-3.5px);
}

.main-content {
    flex: 1;
    display: flex;
    max-width: 1200px;
    margin: 0 auto;
    width: 100%;
    padding: 40px 20px;
    gap: 30px;
}

.sidebar {
    width: 300px;
    background: white;
    border-radius: 15px;
    box-shadow: 0 5px 20px rgba(0, 100, 200, 0.1);
    padding: 25px;
    height: fit-content;
}

.sidebar-title {
    color: #2c5aa0;
    font-size: 18px;
    font-weight: 600;
    margin-bottom: 20px;
    padding-bottom: 10px;
    border-bottom: 2px solid #e6f2ff;
}

.history-list {
    list-style: none;
}

.history-item {
    padding: 12px 15px;
    margin-bottom: 8px;
    background: #f8fbff;
    border: 1px solid #e6f2ff;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.3s ease;
    color: #333;
    font-size: 14px;
}

.history-item:hover {
    background: #e6f2ff;
    border-color: #2c5aa0;
    transform: translateX(5px);
}

.history-item:last-child {
    margin-bottom: 0;
}

.empty-history {
    color: #999;
    font-style: italic;
    text-align: center;
    padding: 20px 0;
}

.search-container {
    background: white;
    padding: 40px;
    border-radius: 20px;
    box-shadow: 0 10px 30px rgba(0, 100, 200, 0.1);
    flex: 1;
    text-align: center;
}

.search-title {
    color: #2c5aa0;
    font-size: 24px;
    margin-bottom: 30px;
    font-weight: 600;
}

.search-form {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.search-input {
    padding: 15px 20px;
    border: 2px solid #e6f2ff;
    border-radius: 12px;
    font-size: 16px;
    outline: none;
    transition: all 0.3s ease;
    color: #333;
}

.search-input:focus {
    border-color: #2c5aa0;
    box-shadow: 0 0 0 3px rgba(44, 90, 160, 0.1);
}

.search-input::placeholder {
    color: #999;
}

.search-button {
    background: #2c5aa0;
    color: white;
    border: none;
    padding: 15px 30px;
    border-radius: 12px;
    font-size: 16px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    text-transform: uppercase;
    letter-spacing: 0.5px;
}

.search-button:hover {
    background: #1e3d6f;
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(44, 90, 160, 0.3);
}

.search-button:active {
    transform: translateY(0);
}

.button-group {
    display: flex;
    gap: 15px;
}

.button-group .search-button {
    flex: 1;
}

/* Адаптивность */
@media (max-width: 768px) {
    .top-bar-content {
        flex-direction: column;
        gap: 10px;
        text-align: center;
    }

    .nav-links {
        gap: 15px;
    }

    .main-content {
        flex-direction: column;
        padding: 20px;
    }

    .sidebar {
        width: 100%;
        order: 2;
    }

    .search-container {
        order: 1;
        padding: 30px 25px;
    }

    .search-title {
        font-size: 20px;
        margin-bottom: 25px;
    }

    .search-input {
        padding: 12px 18px;
        font-size: 15px;
    }

    .search-button {
        padding: 12px 25px;
        font-size: 15px;
    }

    .button-group {
        flex-direction: column;
    }
}

@media (max-width: 480px) {
    .top-bar {
        padding: 12px 0;
    }

    .logo {
        font-size: 20px;
    }

    .nav-links {
        flex-wrap: wrap;
        justify-content: center;
        gap: 10px;
    }

    .search-container {
        padding: 25px 20px;
    }

    .search-title {
        font-size: 18px;
        margin-bottom: 20px;
    }

    .search-form {
        gap: 15px;
    }

    .sidebar {
        padding: 20px;
    }
}
</style>

<script>
import axios from "axios";

async function GetWorkers() {
  try {
    const response = await axios.get("http://localhost:5027/api/Workers/GetAllWorkers");
    if (response.status === 200) {
      listWorker.value = response.data;
      listWorkerFind.value = response.data;
    }
  } catch (error) {
    console.log(error);
  } 
}
</script>

