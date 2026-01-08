<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Админ-панель дня рождения Миши</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #0c0c2e 0%, #1a1a3e 100%);
            color: #fff;
            min-height: 100vh;
            overflow-x: hidden;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            position: relative;
            z-index: 1;
        }
        
        /* Стили для основной части сайта */
        .main-content {
            flex: 1;
        }
        
        header {
            text-align: center;
            margin-bottom: 40px;
            width: 100%;
        }
        
        h1 {
            font-size: 2.8rem;
            margin-bottom: 10px;
            background: linear-gradient(to right, #ff7eb3, #ff758c, #ff7eb3);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 0 5px 15px rgba(255, 118, 140, 0.2);
        }
        
        .subtitle {
            font-size: 1.4rem;
            color: #a8b2d1;
            margin-bottom: 20px;
        }
        
        .birthday-info {
            background: rgba(255, 255, 255, 0.08);
            border-radius: 15px;
            padding: 20px 30px;
            margin: 20px auto 30px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            max-width: 800px;
            text-align: center;
        }
        
        .countdown-container {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 20px;
            padding: 40px 30px;
            margin: 30px auto;
            width: 100%;
            max-width: 1000px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
        }
        
        .countdown-title {
            text-align: center;
            font-size: 1.8rem;
            margin-bottom: 30px;
            color: #64ffda;
        }
        
        .countdown {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 25px;
        }
        
        .countdown-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            background: rgba(10, 25, 47, 0.8);
            border-radius: 15px;
            padding: 25px 15px;
            min-width: 150px;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(100, 255, 218, 0.2);
            transition: transform 0.3s ease;
        }
        
        .countdown-item:hover {
            transform: translateY(-10px);
        }
        
        .countdown-value {
            font-size: 3.5rem;
            font-weight: 700;
            color: #ff758c;
            text-shadow: 0 0 10px rgba(255, 118, 140, 0.5);
            line-height: 1;
        }
        
        .countdown-label {
            font-size: 1.1rem;
            color: #a8b2d1;
            margin-top: 10px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        
        /* Стили для админ-панели */
        .admin-panel {
            position: fixed;
            top: 0;
            right: -400px;
            width: 380px;
            height: 100vh;
            background: rgba(10, 25, 47, 0.95);
            backdrop-filter: blur(10px);
            border-left: 1px solid rgba(100, 255, 218, 0.2);
            box-shadow: -5px 0 25px rgba(0, 0, 0, 0.5);
            transition: right 0.4s ease;
            z-index: 1000;
            overflow-y: auto;
            padding: 20px;
        }
        
        .admin-panel.open {
            right: 0;
        }
        
        .admin-toggle {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #ff758c;
            color: white;
            border: none;
            border-radius: 50%;
            width: 60px;
            height: 60px;
            font-size: 24px;
            cursor: pointer;
            box-shadow: 0 5px 15px rgba(255, 118, 140, 0.4);
            z-index: 999;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s ease;
        }
        
        .admin-toggle:hover {
            background: #ff6582;
            transform: scale(1.1);
        }
        
        .admin-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            padding-bottom: 15px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .admin-header h2 {
            color: #64ffda;
            font-size: 1.8rem;
        }
        
        .admin-close {
            background: none;
            border: none;
            color: #ff758c;
            font-size: 24px;
            cursor: pointer;
        }
        
        .admin-section {
            margin-bottom: 25px;
            padding-bottom: 20px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
        }
        
        .admin-section h3 {
            color: #a8b2d1;
            margin-bottom: 15px;
            font-size: 1.3rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .admin-section h3 i {
            color: #ff758c;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: #8892b0;
            font-size: 0.95rem;
        }
        
        .form-control {
            width: 100%;
            padding: 12px 15px;
            background: rgba(255, 255, 255, 0.07);
            border: 1px solid rgba(100, 255, 218, 0.2);
            border-radius: 8px;
            color: white;
            font-size: 1rem;
            transition: all 0.3s ease;
        }
        
        .form-control:focus {
            outline: none;
            border-color: #64ffda;
            box-shadow: 0 0 0 2px rgba(100, 255, 218, 0.2);
        }
        
        .btn {
            padding: 12px 20px;
            background: #64ffda;
            color: #0a192f;
            border: none;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            width: 100%;
            margin-top: 10px;
        }
        
        .btn:hover {
            background: #52d7b7;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(100, 255, 218, 0.4);
        }
        
        .btn-danger {
            background: #ff758c;
        }
        
        .btn-danger:hover {
            background: #ff6582;
            box-shadow: 0 5px 15px rgba(255, 118, 140, 0.4);
        }
        
        .btn-secondary {
            background: #8892b0;
            margin-top: 5px;
        }
        
        .btn-secondary:hover {
            background: #767f9c;
            box-shadow: 0 5px 15px rgba(136, 146, 176, 0.4);
        }
        
        .admin-status {
            background: rgba(255, 117, 140, 0.1);
            border: 1px solid rgba(255, 117, 140, 0.3);
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 20px;
            text-align: center;
        }
        
        .admin-status h4 {
            color: #ff758c;
            margin-bottom: 5px;
        }
        
        .admin-status p {
            color: #a8b2d1;
            font-size: 0.9rem;
        }
        
        .messages-list {
            max-height: 200px;
            overflow-y: auto;
            margin-bottom: 15px;
        }
        
        .message-item {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 6px;
            padding: 10px;
            margin-bottom: 8px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .message-text {
            color: #a8b2d1;
            font-size: 0.9rem;
        }
        
        .message-delete {
            background: rgba(255, 117, 140, 0.2);
            color: #ff758c;
            border: none;
            border-radius: 4px;
            width: 25px;
            height: 25px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .celebrate-container {
            display: none;
            text-align: center;
            margin-top: 40px;
            animation: fadeIn 1.5s ease-out;
        }
        
        .celebrate-title {
            font-size: 4.5rem;
            color: #ffd700;
            margin-bottom: 30px;
            text-shadow: 0 0 20px rgba(255, 215, 0, 0.7);
            animation: pulse 1.5s infinite alternate;
        }
        
        .message {
            font-size: 2.2rem;
            color: #64ffda;
            max-width: 800px;
            margin: 0 auto 40px;
            line-height: 1.4;
        }
        
        .birthday-cake {
            font-size: 5rem;
            margin: 30px 0;
            animation: bounce 2s infinite;
        }
        
        .custom-messages {
            margin-top: 30px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 20px;
            max-width: 800px;
            margin-left: auto;
            margin-right: auto;
        }
        
        .custom-messages h3 {
            color: #64ffda;
            margin-bottom: 15px;
            text-align: center;
        }
        
        .custom-message-item {
            background: rgba(100, 255, 218, 0.1);
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 15px;
            border-left: 4px solid #64ffda;
        }
        
        .footer {
            margin-top: 50px;
            text-align: center;
            color: #8892b0;
            font-size: 1rem;
            padding-top: 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            width: 100%;
        }
        
        /* Стили для салюта */
        .firework {
            position: absolute;
            width: 5px;
            height: 5px;
            border-radius: 50%;
            z-index: 0;
        }
        
        /* Анимации */
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        @keyframes pulse {
            from { transform: scale(1); }
            to { transform: scale(1.05); }
        }
        
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }
        
        /* Адаптивность */
        @media (max-width: 768px) {
            h1 {
                font-size: 2.2rem;
            }
            
            .subtitle {
                font-size: 1.1rem;
            }
            
            .countdown {
                gap: 15px;
            }
            
            .countdown-item {
                min-width: 120px;
                padding: 20px 10px;
            }
            
            .countdown-value {
                font-size: 2.8rem;
            }
            
            .admin-panel {
                width: 100%;
                right: -100%;
            }
            
            .admin-toggle {
                width: 50px;
                height: 50px;
                font-size: 20px;
            }
            
            .celebrate-title {
                font-size: 3.5rem;
            }
            
            .message {
                font-size: 1.8rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Кнопка открытия админ-панели -->
        <button class="admin-toggle" id="adminToggle">
            <i class="fas fa-cog"></i>
        </button>
        
        <!-- Основное содержание сайта -->
        <div class="main-content">
            <header>
                <h1>Обратный отсчет до дня рождения Миши</h1>
                <div class="subtitle" id="subtitle">9 января 2026 года, 00:00 по Калининградскому времени</div>
                
                <div class="birthday-info">
                    <p><i class="fas fa-birthday-cake"></i>У Миши день рождения 9 января</p>
                    <p><i class="fas fa-clock"></i>Таймер показывает время до праздника</p>
                    <p><i class="fas fa-fireworks"></i>Когда время истечет - будет праздничный салют!</p>
                </div>
            </header>
            
            <div class="countdown-container">
                <h2 class="countdown-title" id="countdownTitle">До дня рождения Миши осталось:</h2>
                <div class="countdown">
                    <div class="countdown-item">
                        <div class="countdown-value" id="days">00</div>
                        <div class="countdown-label">Дней</div>
                    </div>
                    <div class="countdown-item">
                        <div class="countdown-value" id="hours">00</div>
                        <div class="countdown-label">Часов</div>
                    </div>
                    <div class="countdown-item">
                        <div class="countdown-value" id="minutes">00</div>
                        <div class="countdown-label">Минут</div>
                    </div>
                    <div class="countdown-item">
                        <div class="countdown-value" id="seconds">00</div>
                        <div class="countdown-label">Секунд</div>
                    </div>
                </div>
            </div>
            
            <!-- Область для пользовательских сообщений -->
            <div class="custom-messages" id="customMessages">
                <h3>Поздравления для Миши:</h3>
                <!-- Сообщения будут добавляться сюда -->
            </div>
            
            <div class="celebrate-container" id="celebrate">
                <h1 class="celebrate-title" id="birthdayTitle">С ДНЕМ РОЖДЕНИЯ!</h1>
                <div class="message" id="birthdayMessage">Дорогой Миша! Поздравляем тебя с днем рождения! Желаем счастья, здоровья и исполнения всех желаний!</div>
                <div class="birthday-cake">🎂🎉🥳</div>
                <div class="message">Пусть этот год принесет тебе много радостных моментов и новых достижений!</div>
            </div>
            
            <div class="footer">
                <p>Таймер обновляется в реальном времени | Калининградское время (UTC+2)</p>
                <p>Сайт создан специально для дня рождения Миши 9 января 2026 года</p>
            </div>
        </div>
        
        <!-- Админ-панель -->
        <div class="admin-panel" id="adminPanel">
            <div class="admin-header">
                <h2><i class="fas fa-user-shield"></i> Админ-панель</h2>
                <button class="admin-close" id="adminClose">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            
            <!-- Статус админ-доступа -->
            <div class="admin-status" id="adminStatus">
                <h4>Статус доступа: <span id="accessStatus">Проверка...</span></h4>
                <p id="ipInfo">IP: загрузка...</p>
            </div>
            
            <!-- Раздел управления таймером -->
            <div class="admin-section">
                <h3><i class="fas fa-clock"></i> Управление таймером</h3>
                <div class="form-group">
                    <label for="targetDate">Дата и время события:</label>
                    <input type="datetime-local" id="targetDate" class="form-control">
                </div>
                <div class="form-group">
                    <label for="timezone">Часовой пояс:</label>
                    <select id="timezone" class="form-control">
                        <option value="+02:00">Калининград (UTC+2)</option>
                        <option value="+03:00">Москва (UTC+3)</option>
                        <option value="+04:00">Самара (UTC+4)</option>
                        <option value="+05:00">Екатеринбург (UTC+5)</option>
                    </select>
                </div>
                <button class="btn" id="updateTimer">
                    <i class="fas fa-sync-alt"></i> Обновить таймер
                </button>
            </div>
            
            <!-- Раздел управления текстом -->
            <div class="admin-section">
                <h3><i class="fas fa-font"></i> Тексты на сайте</h3>
                <div class="form-group">
                    <label for="mainTitle">Заголовок сайта:</label>
                    <input type="text" id="mainTitle" class="form-control" value="Обратный отсчет до дня рождения Миши">
                </div>
                <div class="form-group">
                    <label for="subtitleText">Подзаголовок:</label>
                    <input type="text" id="subtitleText" class="form-control" value="9 января 2026 года, 00:00 по Калининградскому времени">
                </div>
                <div class="form-group">
                    <label for="countdownText">Текст над таймером:</label>
                    <input type="text" id="countdownText" class="form-control" value="До дня рождения Миши осталось:">
                </div>
                <div class="form-group">
                    <label for="birthdayTitleText">Заголовок поздравления:</label>
                    <input type="text" id="birthdayTitleText" class="form-control" value="С ДНЕМ РОЖДЕНИЯ!">
                </div>
                <div class="form-group">
                    <label for="birthdayMessageText">Текст поздравления:</label>
                    <textarea id="birthdayMessageText" class="form-control" rows="3">Дорогой Миша! Поздравляем тебя с днем рождения! Желаем счастья, здоровья и исполнения всех желаний!</textarea>
                </div>
                <button class="btn" id="updateTexts">
                    <i class="fas fa-check"></i> Обновить тексты
                </button>
            </div>
            
            <!-- Раздел управления сообщениями -->
            <div class="admin-section">
                <h3><i class="fas fa-comments"></i> Управление сообщениями</h3>
                <div class="form-group">
                    <label for="newMessage">Добавить новое сообщение:</label>
                    <textarea id="newMessage" class="form-control" rows="3" placeholder="Введите текст сообщения для отображения на сайте"></textarea>
                </div>
                <button class="btn" id="addMessage">
                    <i class="fas fa-plus"></i> Добавить сообщение
                </button>
                
                <div class="form-group">
                    <label>Список сообщений:</label>
                    <div class="messages-list" id="messagesList">
                        <!-- Сообщения будут добавляться сюда -->
                    </div>
                </div>
            </div>
            
            <!-- Раздел управления внешним видом -->
            <div class="admin-section">
                <h3><i class="fas fa-palette"></i> Внешний вид</h3>
                <div class="form-group">
                    <label for="themeColor">Цветовая тема:</label>
                    <select id="themeColor" class="form-control">
                        <option value="default">Стандартная (синяя)</option>
                        <option value="purple">Фиолетовая</option>
                        <option value="green">Зеленая</option>
                        <option value="red">Красная</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="fireworksEnabled">Салют после отсчета:</label>
                    <select id="fireworksEnabled" class="form-control">
                        <option value="true">Включен</option>
                        <option value="false">Выключен</option>
                    </select>
                </div>
                <button class="btn" id="updateAppearance">
                    <i class="fas fa-paint-brush"></i> Применить настройки
                </button>
            </div>
            
            <!-- Раздел управления данными -->
            <div class="admin-section">
                <h3><i class="fas fa-database"></i> Управление данными</h3>
                <button class="btn btn-secondary" id="exportData">
                    <i class="fas fa-download"></i> Экспорт настроек
                </button>
                <button class="btn btn-secondary" id="importData">
                    <i class="fas fa-upload"></i> Импорт настроек
                </button>
                <button class="btn btn-danger" id="resetAll">
                    <i class="fas fa-trash-alt"></i> Сбросить все настройки
                </button>
            </div>
            
            <!-- Раздел информации -->
            <div class="admin-section">
                <h3><i class="fas fa-info-circle"></i> Информация</h3>
                <p style="color: #a8b2d1; font-size: 0.9rem; margin-bottom: 10px;">
                    Админ-панель доступна только с вашего IP-адреса.
                    Все изменения сохраняются в локальном хранилище браузера.
                </p>
                <p style="color: #8892b0; font-size: 0.8rem;">
                    Текущая версия: 1.0 | Последнее обновление: <span id="lastUpdated">-</span>
                </p>
            </div>
        </div>
    </div>

    <script>
        // ========================
        // ОСНОВНАЯ ЛОГИКА САЙТА
        // ========================
        
        // Настройки по умолчанию
        const defaultSettings = {
            targetDate: '2026-01-09T00:00:00+02:00',
            mainTitle: 'Обратный отсчет до дня рождения Миши',
            subtitle: '9 января 2026 года, 00:00 по Калининградскому времени',
            countdownText: 'До дня рождения Миши осталось:',
            birthdayTitle: 'С ДНЕМ РОЖДЕНИЯ!',
            birthdayMessage: 'Дорогой Миша! Поздравляем тебя с днем рождения! Желаем счастья, здоровья и исполнения всех желаний!',
            theme: 'default',
            fireworksEnabled: true,
            customMessages: [
                'С днём рождения, Миша! Желаю всего самого наилучшего!',
                'Пусть сбываются все мечты! Удачи во всем!',
                'Здоровья, счастья и успехов в новом году жизни!'
            ],
            lastUpdated: new Date().toLocaleString('ru-RU')
        };
        
        // Текущие настройки
        let settings = {...defaultSettings};
        
        // Загрузка сохраненных настроек
        function loadSettings() {
            const saved = localStorage.getItem('birthdayTimerSettings');
            if (saved) {
                try {
                    const parsed = JSON.parse(saved);
                    settings = {...defaultSettings, ...parsed};
                    
                    // Восстанавливаем дату в правильном формате
                    if (parsed.targetDate) {
                        settings.targetDate = parsed.targetDate;
                    }
                } catch (e) {
                    console.error('Ошибка загрузки настроек:', e);
                }
            }
        }
        
        // Сохранение настроек
        function saveSettings() {
            settings.lastUpdated = new Date().toLocaleString('ru-RU');
            localStorage.setItem('birthdayTimerSettings', JSON.stringify(settings));
        }
        
        // ========================
        // АДМИН-ПАНЕЛЬ И ДОСТУП
        // ========================
        
        // Получение IP пользователя
        async function getUserIP() {
            try {
                const response = await fetch('https://api.ipify.org?format=json');
                const data = await response.json();
                return data.ip;
            } catch (error) {
                console.error('Ошибка получения IP:', error);
                return 'unknown';
            }
        }
        
        // Проверка доступа к админ-панели
        async function checkAdminAccess() {
            const userIP = await getUserIP();
            const adminIPs = localStorage.getItem('adminIPs') || '';
            
            // Показываем IP пользователя
            document.getElementById('ipInfo').textContent = `IP: ${userIP}`;
            
            // Проверяем, есть ли IP в списке админов
            const isAdmin = adminIPs.includes(userIP) || adminIPs === '';
            
            if (isAdmin) {
                document.getElementById('accessStatus').textContent = 'Доступ разрешен';
                document.getElementById('accessStatus').style.color = '#64ffda';
                return true;
            } else {
                document.getElementById('accessStatus').textContent = 'Доступ запрещен';
                document.getElementById('accessStatus').style.color = '#ff758c';
                
                // Скрываем кнопку админ-панели
                document.getElementById('adminToggle').style.display = 'none';
                return false;
            }
        }
        
        // Добавление текущего IP в список админов
        async function addCurrentIPAsAdmin() {
            const userIP = await getUserIP();
            let adminIPs = localStorage.getItem('adminIPs') || '';
            
            if (!adminIPs.includes(userIP)) {
                adminIPs = adminIPs ? `${adminIPs},${userIP}` : userIP;
                localStorage.setItem('adminIPs', adminIPs);
                alert(`Ваш IP (${userIP}) добавлен в список администраторов.`);
                checkAdminAccess();
            }
        }
        
        // ========================
        // УПРАВЛЕНИЕ ТАЙМЕРОМ
        // ========================
        
        // Элементы DOM
        const daysElement = document.getElementById('days');
        const hoursElement = document.getElementById('hours');
        const minutesElement = document.getElementById('minutes');
        const secondsElement = document.getElementById('seconds');
        const celebrateElement = document.getElementById('celebrate');
        const countdownContainer = document.querySelector('.countdown-container');
        const countdownTitle = document.querySelector('.countdown-title');
        
        // Функция обновления таймера
        function updateCountdown() {
            const now = new Date();
            const targetDate = new Date(settings.targetDate);
            const timeDifference = targetDate - now;
            
            // Если время истекло
            if (timeDifference <= 0) {
                daysElement.textContent = '00';
                hoursElement.textContent = '00';
                minutesElement.textContent = '00';
                secondsElement.textContent = '00';
                
                // Показываем праздничное сообщение
                celebrateElement.style.display = 'block';
                countdownContainer.style.display = 'none';
                countdownTitle.style.display = 'none';
                
                // Запускаем салют если включен
                if (settings.fireworksEnabled) {
                    startFireworks();
                }
                return;
            }
            
            // Расчет времени
            const days = Math.floor(timeDifference / (1000 * 60 * 60 * 24));
            const hours = Math.floor((timeDifference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((timeDifference % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((timeDifference % (1000 * 60)) / 1000);
            
            // Обновление элементов DOM
            daysElement.textContent = days.toString().padStart(2, '0');
            hoursElement.textContent = hours.toString().padStart(2, '0');
            minutesElement.textContent = minutes.toString().padStart(2, '0');
            secondsElement.textContent = seconds.toString().padStart(2, '0');
        }
        
        // ========================
        // УПРАВЛЕНИЕ ИНТЕРФЕЙСОМ
        // ========================
        
        // Применение настроек к интерфейсу
        function applySettingsToUI() {
            // Обновляем тексты
            document.getElementById('subtitle').textContent = settings.subtitle;
            document.getElementById('countdownTitle').textContent = settings.countdownText;
            document.getElementById('birthdayTitle').textContent = settings.birthdayTitle;
            document.getElementById('birthdayMessage').textContent = settings.birthdayMessage;
            document.querySelector('h1').textContent = settings.mainTitle;
            
            // Обновляем дату в админ-панели
            const dateInput = document.getElementById('targetDate');
            const dateObj = new Date(settings.targetDate);
            const localDate = new Date(dateObj.getTime() - dateObj.getTimezoneOffset() * 60000);
            dateInput.value = localDate.toISOString().slice(0, 16);
            
            // Обновляем остальные поля в админ-панели
            document.getElementById('mainTitle').value = settings.mainTitle;
            document.getElementById('subtitleText').value = settings.subtitle;
            document.getElementById('countdownText').value = settings.countdownText;
            document.getElementById('birthdayTitleText').value = settings.birthdayTitle;
            document.getElementById('birthdayMessageText').value = settings.birthdayMessage;
            document.getElementById('themeColor').value = settings.theme;
            document.getElementById('fireworksEnabled').value = settings.fireworksEnabled.toString();
            
            // Обновляем список сообщений
            updateMessagesList();
            updateCustomMessagesDisplay();
            
            // Обновляем тему
            applyTheme(settings.theme);
            
            // Обновляем информацию о последнем обновлении
            document.getElementById('lastUpdated').textContent = settings.lastUpdated;
        }
        
        // Обновление списка сообщений в админ-панели
        function updateMessagesList() {
            const messagesList = document.getElementById('messagesList');
            messagesList.innerHTML = '';
            
            settings.customMessages.forEach((message, index) => {
                const messageItem = document.createElement('div');
                messageItem.className = 'message-item';
                messageItem.innerHTML = `
                    <div class="message-text">${message.substring(0, 50)}${message.length > 50 ? '...' : ''}</div>
                    <button class="message-delete" data-index="${index}">
                        <i class="fas fa-trash"></i>
                    </button>
                `;
                messagesList.appendChild(messageItem);
            });
            
            // Добавляем обработчики для кнопок удаления
            document.querySelectorAll('.message-delete').forEach(button => {
                button.addEventListener('click', function() {
                    const index = parseInt(this.getAttribute('data-index'));
                    deleteMessage(index);
                });
            });
        }
        
        // Обновление отображения пользовательских сообщений на сайте
        function updateCustomMessagesDisplay() {
            const customMessagesContainer = document.getElementById('customMessages');
            customMessagesContainer.innerHTML = '<h3>Поздравления для Миши:</h3>';
            
            if (settings.customMessages.length === 0) {
                customMessagesContainer.innerHTML += '<p style="text-align: center; color: #8892b0;">Пока нет поздравлений. Будьте первым!</p>';
                return;
            }
            
            settings.customMessages.forEach(message => {
                const messageElement = document.createElement('div');
                messageElement.className = 'custom-message-item';
                messageElement.textContent = message;
                customMessagesContainer.appendChild(messageElement);
            });
        }
        
        // Добавление нового сообщения
        function addNewMessage() {
            const newMessageInput = document.getElementById('newMessage');
            const message = newMessageInput.value.trim();
            
            if (message) {
                settings.customMessages.push(message);
                saveSettings();
                updateMessagesList();
                updateCustomMessagesDisplay();
                newMessageInput.value = '';
                
                // Показываем уведомление
                showNotification('Сообщение добавлено!');
            }
        }
        
        // Удаление сообщения
        function deleteMessage(index) {
            settings.customMessages.splice(index, 1);
            saveSettings();
            updateMessagesList();
            updateCustomMessagesDisplay();
            
            // Показываем уведомление
            showNotification('Сообщение удалено!');
        }
        
        // Применение цветовой темы
        function applyTheme(theme) {
            const body = document.body;
            
            // Удаляем предыдущие классы тем
            body.classList.remove('theme-purple', 'theme-green', 'theme-red');
            
            // Применяем новую тему
            if (theme !== 'default') {
                body.classList.add(`theme-${theme}`);
            }
            
            // Обновляем CSS переменные в зависимости от темы
            let primaryColor, secondaryColor;
            
            switch(theme) {
                case 'purple':
                    primaryColor = '#9d4edd';
                    secondaryColor = '#c77dff';
                    break;
                case 'green':
                    primaryColor = '#2d6a4f';
                    secondaryColor = '#52b788';
                    break;
                case 'red':
                    primaryColor = '#c1121f';
                    secondaryColor = '#ff758c';
                    break;
                default: // default blue
                    primaryColor = '#64ffda';
                    secondaryColor = '#ff758c';
            }
            
            // Применяем CSS переменные
            document.documentElement.style.setProperty('--primary-color', primaryColor);
            document.documentElement.style.setProperty('--secondary-color', secondaryColor);
        }
        
        // Показать уведомление
        function showNotification(message) {
            // Создаем элемент уведомления
            const notification = document.createElement('div');
            notification.style.cssText = `
                position: fixed;
                top: 20px;
                right: 20px;
                background: rgba(100, 255, 218, 0.9);
                color: #0a192f;
                padding: 15px 20px;
                border-radius: 8px;
                box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
                z-index: 9999;
                font-weight: 600;
                animation: slideIn 0.3s ease;
            `;
            notification.textContent = message;
            
            document.body.appendChild(notification);
            
            // Удаляем уведомление через 3 секунды
            setTimeout(() => {
                notification.style.animation = 'slideOut 0.3s ease';
                setTimeout(() => {
                    document.body.removeChild(notification);
                }, 300);
            }, 3000);
        }
        
        // ========================
        // ФЕЙЕРВЕРКИ
        // ========================
        
        // Функция создания салюта
        function startFireworks() {
            const colors = ['#ff0000', '#00ff00', '#0000ff', '#ffff00', '#ff00ff', '#00ffff', '#ffa500', '#ff1493'];
            const container = document.querySelector('.container');
            
            // Создаем множество фейерверков
            for (let i = 0; i < 150; i++) {
                setTimeout(() => {
                    createFirework(container, colors);
                }, i * 100);
            }
            
            // Продолжаем запускать фейерверки
            const intervalId = setInterval(() => {
                for (let i = 0; i < 5; i++) {
                    createFirework(container, colors);
                }
            }, 2000);
            
            // Останавливаем фейерверки через 30 секунд
            setTimeout(() => {
                clearInterval(intervalId);
            }, 30000);
        }
        
        // Функция создания одного фейерверка
        function createFirework(container, colors) {
            const firework = document.createElement('div');
            firework.className = 'firework';
            
            // Случайные начальные позиции
            const startX = Math.random() * window.innerWidth;
            const startY = window.innerHeight;
            
            // Случайный цвет
            const color = colors[Math.floor(Math.random() * colors.length)];
            
            // Настройка фейерверка
            firework.style.left = `${startX}px`;
            firework.style.top = `${startY}px`;
            firework.style.backgroundColor = color;
            firework.style.boxShadow = `0 0 10px ${color}`;
            
            container.appendChild(firework);
            
            // Анимация фейерверка
            const animationDuration = 1500 + Math.random() * 1000;
            const burstX = startX + (Math.random() * 200 - 100);
            const burstY = startY - 100 - Math.random() * 300;
            
            // Ключевые кадры анимации
            const keyframes = [
                { 
                    transform: `translate(0, 0)`, 
                    opacity: 1 
                },
                { 
                    transform: `translate(${burstX - startX}px, ${burstY - startY}px)`, 
                    opacity: 1 
                },
                { 
                    transform: `translate(${burstX - startX + (Math.random() * 100 - 50)}px, ${burstY - startY + (Math.random() * 100 - 50)}px)`, 
                    opacity: 0,
                    width: '15px',
                    height: '15px'
                }
            ];
            
            // Запуск анимации
            firework.animate(keyframes, {
                duration: animationDuration,
                easing: 'cubic-bezier(0.1, 0.8, 0.2, 1)'
            });
            
            // Удаление элемента после анимации
            setTimeout(() => {
                if (firework.parentNode) {
                    firework.parentNode.removeChild(firework);
                }
            }, animationDuration);
        }
        
        // ========================
        // ЭКСПОРТ/ИМПОРТ НАСТРОЕК
        // ========================
        
        // Экспорт настроек
        function exportSettings() {
            const dataStr = JSON.stringify(settings, null, 2);
            const dataUri = 'data:application/json;charset=utf-8,'+ encodeURIComponent(dataStr);
            
            const exportFileDefaultName = 'birthday-timer-settings.json';
            
            const linkElement = document.createElement('a');
            linkElement.setAttribute('href', dataUri);
            linkElement.setAttribute('download', exportFileDefaultName);
            linkElement.click();
            
            showNotification('Настройки экспортированы!');
        }
        
        // Импорт настроек
        function importSettings() {
            const input = document.createElement('input');
            input.type = 'file';
            input.accept = 'application/json';
            
            input.onchange = function(event) {
                const file = event.target.files[0];
                const reader = new FileReader();
                
                reader.onload = function(e) {
                    try {
                        const importedSettings = JSON.parse(e.target.result);
                        settings = {...defaultSettings, ...importedSettings};
                        saveSettings();
                        applySettingsToUI();
                        showNotification('Настройки импортированы!');
                    } catch (error) {
                        alert('Ошибка при импорте настроек. Проверьте файл.');
                    }
                };
                
                reader.readAsText(file);
            };
            
            input.click();
        }
        
        // Сброс всех настроек
        function resetAllSettings() {
            if (confirm('Вы уверены, что хотите сбросить все настройки к значениям по умолчанию?')) {
                settings = {...defaultSettings};
                saveSettings();
                applySettingsToUI();
                showNotification('Все настройки сброшены!');
            }
        }
        
        // ========================
        // ИНИЦИАЛИЗАЦИЯ
        // ========================
        
        // Инициализация при загрузке страницы
        document.addEventListener('DOMContentLoaded', async function() {
            // Загружаем настройки
            loadSettings();
            
            // Проверяем доступ к админ-панели
            const hasAccess = await checkAdminAccess();
            
            // Если у пользователя нет доступа, останавливаем дальнейшую инициализацию админ-панели
            if (!hasAccess) {
                return;
            }
            
            // Применяем настройки к интерфейсу
            applySettingsToUI();
            
            // Обновляем таймер каждую секунду
            updateCountdown();
            setInterval(updateCountdown, 1000);
            
            // Добавляем обработчики для админ-панели
            document.getElementById('adminToggle').addEventListener('click', function() {
                document.getElementById('adminPanel').classList.add('open');
            });
            
            document.getElementById('adminClose').addEventListener('click', function() {
                document.getElementById('adminPanel').classList.remove('open');
            });
            
            // Добавляем текущий IP в админы при двойном клике на кнопку админ-панели
            let clickCount = 0;
            document.getElementById('adminToggle').addEventListener('click', function(e) {
                clickCount++;
                if (clickCount === 2) {
                    addCurrentIPAsAdmin();
                    clickCount = 0;
                }
                setTimeout(() => { clickCount = 0; }, 500);
            });
            
            // Обработчики для обновления таймера
            document.getElementById('updateTimer').addEventListener('click', function() {
                const dateInput = document.getElementById('targetDate').value;
                const timezone = document.getElementById('timezone').value;
                
                if (dateInput) {
                    // Преобразуем локальную дату в строку с правильным часовым поясом
                    const localDate = new Date(dateInput);
                    const dateString = localDate.toISOString().replace('Z', timezone);
                    
                    settings.targetDate = dateString;
                    saveSettings();
                    applySettingsToUI();
                    showNotification('Таймер обновлен!');
                }
            });
            
            // Обработчики для обновления текстов
            document.getElementById('updateTexts').addEventListener('click', function() {
                settings.mainTitle = document.getElementById('mainTitle').value;
                settings.subtitle = document.getElementById('subtitleText').value;
                settings.countdownText = document.getElementById('countdownText').value;
                settings.birthdayTitle = document.getElementById('birthdayTitleText').value;
                settings.birthdayMessage = document.getElementById('birthdayMessageText').value;
                
                saveSettings();
                applySettingsToUI();
                showNotification('Тексты обновлены!');
            });
            
            // Обработчики для управления сообщениями
            document.getElementById('addMessage').addEventListener('click', addNewMessage);
            
            // Обработчики для внешнего вида
            document.getElementById('updateAppearance').addEventListener('click', function() {
                settings.theme = document.getElementById('themeColor').value;
                settings.fireworksEnabled = document.getElementById('fireworksEnabled').value === 'true';
                
                saveSettings();
                applySettingsToUI();
                showNotification('Внешний вид обновлен!');
            });
            
            // Обработчики для управления данными
            document.getElementById('exportData').addEventListener('click', exportSettings);
            document.getElementById('importData').addEventListener('click', importSettings);
            document.getElementById('resetAll').addEventListener('click', resetAllSettings);
            
            // Добавляем CSS для анимаций уведомлений
            const style = document.createElement('style');
            style.textContent = `
                @keyframes slideIn {
                    from { transform: translateX(100%); opacity: 0; }
                    to { transform: translateX(0); opacity: 1; }
                }
                @keyframes slideOut {
                    from { transform: translateX(0); opacity: 1; }
                    to { transform: translateX(100%); opacity: 0; }
                }
                .theme-purple { --primary-color: #9d4edd; --secondary-color: #c77dff; }
                .theme-green { --primary-color: #2d6a4f; --secondary-color: #52b788; }
                .theme-red { --primary-color: #c1121f; --secondary-color: #ff758c; }
            `;
            document.head.appendChild(style);
        });
        
        // Адаптация под изменение размера окна
        window.addEventListener('resize', function() {
            // При изменении размера окна удаляем все фейерверки
            const fireworks = document.querySelectorAll('.firework');
            fireworks.forEach(firework => {
                if (firework.parentNode) {
                    firework.parentNode.removeChild(firework);
                }
            });
        });
    </script>
</body>
</html>
