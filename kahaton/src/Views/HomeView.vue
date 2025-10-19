<template>
    <body :class="{'high-contrast-mode': isHighContrast}">
        <!-- Кнопка доступности -->
        <div class="accessibility-toggle">
            <button 
                @click="toggleHighContrast" 
                class="accessibility-btn"
                :title="isHighContrast ? 'Обычный режим' : 'Режим для слабовидящих'"
            >
                <span class="btn-icon">👁️</span>
                {{ isHighContrast ? 'Обычный вид' : 'Для слабовидящих' }}
            </button>
        </div>

       

        <!-- Основной контент -->
        <div class="main-content">
            <div class="sidebar">
                <h3 class="sidebar-title">Последние запросы</h3>
                <ul class="history-list" id="historyList">
                    <!-- История запросов -->
                </ul>
            </div>

            <div class="search-container">
                <h1 class="search-title">Введите ваш запрос</h1>
                <div class="query-type-selector">
                    <label for="queryType" class="query-type-label">Роль:</label>
                    <select 
                        id="queryType" 
                        class="query-type-select" 
                        v-model="selectedQueryType"
                        @change="onQueryTypeChange"
                    >
                        <option value="student">Пользователь</option>
                        <option value="programmist">Программист</option>
                        <option value="kolhoznik">Глава сельского поселения</option>

                    </select>
                </div>

                <form class="search-form" id="searchForm">
                    <input type="text" class="search-input" placeholder="Введите запрос" required id="searchInput">
                    <div class="button-group">
                        <button type="submit" class="search-button">Найти</button>
                        <button type="button" class="search-button" id="uploadButton">Загрузить файл</button>
                        <button type="button" class="search-button_new" id="newRequestButton">Новый запрос</button>
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
    transition: background-color 0.3s ease, color 0.3s ease, border-color 0.3s ease, font-family 0.3s ease;
}

@font-face {
    font-family: 'LucidaSansUnicode';
    src: url('../assets/fonts/lucidasansunicode.ttf') format('truetype');
    font-weight: normal;
    font-style: normal;
    font-display: swap;
}

body {
    background: linear-gradient(135deg, #e6f2ff 0%, #ffffff 100%);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    position: relative;
}

/* Контейнер для селектора ролей */
.role-selector-container {
    width: 100%;
    background: linear-gradient(135deg, #f8fbff 0%, #e6f2ff 100%);
    border-bottom: 2px solid #e6f2ff;
    padding: 15px 0;
    margin-top: 80px; /* Отступ для кнопки доступности */
}

.role-selector-wrapper {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
    margin-top: -5%;
    margin-right: 3%;
}

.role-selector {
    display: flex;
    align-items: center;
    gap: 15px;
    background: white;
    padding: 15px 20px;
    border-radius: 12px;
    box-shadow: 0 4px 15px rgba(0, 100, 200, 0.1);
    border: 2px solid #e6f2ff;
    max-width: 400px;
    margin: 0 auto;
}

.role-label {
    font-weight: 600;
    color: #2c5aa0;
    font-size: 16px;
    white-space: nowrap;
    font-family: 'Arial', sans-serif;
}

.role-select {
    flex: 1;
    padding: 10px 15px;
    border: 2px solid #e6f2ff;
    border-radius: 8px;
    font-size: 15px;
    background: white;
    color: #333;
    cursor: pointer;
    outline: none;
    transition: all 0.3s ease;
    font-family: 'Arial', sans-serif;
}

.role-select:focus {
    border-color: #2c5aa0;
    box-shadow: 0 0 0 3px rgba(44, 90, 160, 0.1);
}

.role-select:hover {
    border-color: #2c5aa0;
}

/* Новый селектор типа запроса */
.query-type-selector {
    display: flex;
    align-items: center;
    gap: 15px;
    background: white;
    padding: 15px 20px;
    border-radius: 12px;
    box-shadow: 0 4px 15px rgba(0, 100, 200, 0.1);
    border: 2px solid #e6f2ff;
    max-width: 400px;
    margin: 0 auto 25px auto;
    justify-content: center;
}

.query-type-label {
    font-weight: 600;
    color: #2c5aa0;
    font-size: 16px;
    white-space: nowrap;
    font-family: 'Arial', sans-serif;
}

.query-type-select {
    flex: 1;
    padding: 10px 15px;
    border: 2px solid #e6f2ff;
    border-radius: 8px;
    font-size: 15px;
    background: white;
    color: #333;
    cursor: pointer;
    outline: none;
    transition: all 0.3s ease;
    font-family: 'Arial', sans-serif;
    min-width: 200px;
}

.query-type-select:focus {
    border-color: #2c5aa0;
    box-shadow: 0 0 0 3px rgba(44, 90, 160, 0.1);
}

.query-type-select:hover {
    border-color: #2c5aa0;
}

/* Стили для режима высокой контрастности */
body.high-contrast-mode .role-selector-container {
    background: #000000 !important;
    border-bottom: 3px solid #ffffff !important;
}

body.high-contrast-mode .role-selector {
    background: #000000 !important;
    border: 3px solid #ffffff !important;
    color: #ffffff !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

body.high-contrast-mode .role-label {
    color: #ffffff !important;
    font-size: 18px !important;
    font-weight: bold !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

body.high-contrast-mode .role-select {
    background: #000000 !important;
    border: 2px solid #ffffff !important;
    color: #ffffff !important;
    font-size: 16px !important;
    font-weight: bold !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

body.high-contrast-mode .role-select option {
    background: #000000 !important;
    color: #ffffff !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

/* Стили для селектора типа запроса в режиме высокой контрастности */
body.high-contrast-mode .query-type-selector {
    background: #000000 !important;
    border: 3px solid #ffffff !important;
    color: #ffffff !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

body.high-contrast-mode .query-type-label {
    color: #ffffff !important;
    font-size: 18px !important;
    font-weight: bold !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

body.high-contrast-mode .query-type-select {
    background: #000000 !important;
    border: 2px solid #ffffff !important;
    color: #ffffff !important;
    font-size: 16px !important;
    font-weight: bold !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

body.high-contrast-mode .query-type-select option {
    background: #000000 !important;
    color: #ffffff !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

/* Остальные стили остаются такими же, но с небольшими корректировками */
body.high-contrast-mode {
    background: #000000 !important;
    color: #ffffff !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

body.high-contrast-mode .main-content {
    background: transparent;
}

body.high-contrast-mode .sidebar {
    background: #000000 !important;
    border: 3px solid #ffffff !important;
    color: #ffffff !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

body.high-contrast-mode .sidebar-title {
    color: #ffffff !important;
    border-bottom: 3px solid #ffffff !important;
    font-size: 22px !important;
    font-weight: bold !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

body.high-contrast-mode .history-item {
    background: #000000 !important;
    border: 2px solid #ffffff !important;
    color: #ffffff !important;
    font-size: 16px !important;
    font-weight: bold !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

body.high-contrast-mode .history-item:hover {
    background: #333333 !important;
    border-color: #cccccc !important;
}

body.high-contrast-mode .search-container {
    background: #000000 !important;
    border: 3px solid #ffffff !important;
    color: #ffffff !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

body.high-contrast-mode .search-title {
    color: #ffffff !important;
    font-size: 28px !important;
    font-weight: bold !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

body.high-contrast-mode .search-input {
    background: #000000 !important;
    border: 3px solid #ffffff !important;
    color: #ffffff !important;
    font-size: 18px !important;
    font-weight: bold !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

body.high-contrast-mode .search-input::placeholder {
    color: #cccccc !important;
    font-size: 18px !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

body.high-contrast-mode .search-input:focus {
    border-color: #ffffff !important;
    box-shadow: 0 0 0 3px rgba(255, 255, 255, 0.3) !important;
    background: #1a1a1a !important;
}

body.high-contrast-mode .search-button {
    background: #ffffff !important;
    color: #000000 !important;
    border: 2px solid #ffffff !important;
    font-size: 18px !important;
    font-weight: bold !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

body.high-contrast-mode .search-button:hover {
    background: #cccccc !important;
    color: #000000 !important;
    border-color: #cccccc !important;
}

.accessibility-toggle {
    position: fixed;
    top: 20px;
    right: 20px;
    z-index: 1000;
}

.accessibility-btn {
    background: #2c5aa0;
    color: white;
    border: none;
    padding: 12px 20px;
    border-radius: 25px;
    font-size: 14px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    gap: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
    font-family: 'Arial', sans-serif;
}

.accessibility-btn:hover {
    background: #1e3d6f;
    transform: translateY(-2px);
}

body.high-contrast-mode .accessibility-btn {
    background: #ffffff !important;
    color: #000000 !important;
    border: 2px solid #ffffff !important;
    font-weight: bold !important;
    font-family: 'LucidaSansUnicode', 'Arial', sans-serif !important;
}

body.high-contrast-mode .accessibility-btn:hover {
    background: #cccccc !important;
    color: #000000 !important;
    border-color: #cccccc !important;
}

.btn-icon {
    font-size: 16px;
}

.main-content {
    flex: 1;
    display: flex;
    max-width: 1200px;
    margin: 20px auto 0;
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
    font-family: 'Arial', sans-serif;
}

.sidebar-title {
    color: #2c5aa0;
    font-size: 18px;
    font-weight: 600;
    margin-bottom: 20px;
    padding-bottom: 10px;
    border-bottom: 2px solid #e6f2ff;
    font-family: 'Arial', sans-serif;
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
    font-family: 'Arial', sans-serif;
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
    font-family: 'Arial', sans-serif;
}

.search-container {
    background: white;
    padding: 40px;
    border-radius: 20px;
    box-shadow: 0 10px 30px rgba(0, 100, 200, 0.1);
    flex: 1;
    text-align: center;
    font-family: 'Arial', sans-serif;
}

.search-title {
    color: #2c5aa0;
    font-size: 24px;
    margin-bottom: 30px;
    font-weight: 600;
    font-family: 'Arial', sans-serif;
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
    font-family: 'Arial', sans-serif;
}

.search-input:focus {
    border-color: #2c5aa0;
    box-shadow: 0 0 0 3px rgba(44, 90, 160, 0.1);
}

.search-input::placeholder {
    color: #999;
    font-family: 'Arial', sans-serif;
}

.search-button_new {
    background: #ea3263;
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
    font-family: 'Arial', sans-serif;
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
    font-family: 'Arial', sans-serif;
}

.search-button:hover {
    background: #1e3d6f;
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(44, 90, 160, 0.3);
}

.search-button_new:hover {
    background: #d12a55;
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(234, 50, 99, 0.3);
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
    .accessibility-toggle {
        position: relative;
        top: auto;
        right: auto;
        text-align: center;
        margin-bottom: 20px;
    }
    
    .accessibility-btn {
        padding: 10px 16px;
        font-size: 13px;
    }

    .role-selector-container {
        margin-top: 0;
        padding: 10px 0;
    }

    .role-selector {
        flex-direction: column;
        align-items: stretch;
        gap: 10px;
        max-width: 100%;
    }

    .role-label {
        text-align: center;
    }

    .query-type-selector {
        flex-direction: column;
        align-items: stretch;
        gap: 10px;
        max-width: 100%;
        margin-bottom: 20px;
    }

    .query-type-label {
        text-align: center;
    }

    .main-content {
        flex-direction: column;
        padding: 20px;
        margin-top: 10px;
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
    .role-selector {
        padding: 12px 15px;
    }

    .role-label {
        font-size: 14px;
    }

    .role-select {
        padding: 8px 12px;
        font-size: 14px;
    }

    .query-type-selector {
        padding: 12px 15px;
    }

    .query-type-label {
        font-size: 14px;
    }

    .query-type-select {
        padding: 8px 12px;
        font-size: 14px;
        min-width: 150px;
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

export default {
    name: 'App',
    data() {
        return {
            isHighContrast: false,
            selectedRole: 'user',
            selectedQueryType: 'general'
        }
    },
    methods: {
        toggleHighContrast() {
            this.isHighContrast = !this.isHighContrast;
            localStorage.setItem('highContrastMode', this.isHighContrast);
        },
        onRoleChange() {
            console.log('Выбрана роль:', this.selectedRole);
        },
        onQueryTypeChange() {
            console.log('Выбран тип запроса:', this.selectedQueryType);
        },
        async GetWorkers() {
            try {
                const response = await axios.get("http://localhost:5027/api/Workers/GetAllWorkers");
                if (response.status === 200) {
                    
                }
            } catch (error) {
                console.log(error);
            } 
        }
    },
    mounted() {   
        const savedMode = localStorage.getItem('highContrastMode');
        if (savedMode !== null) {
            this.isHighContrast = savedMode === 'true';
        }
    }
}
</script>