
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Информационная система автосервиса | Autotech Pro</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,500;14..32,600;14..32,700;14..32,800&family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
    <script src="https://cdn.sheetjs.com/xlsx-0.20.2/package/dist/xlsx.full.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #f0f2f8;
            font-family: 'Inter', 'Plus Jakarta Sans', sans-serif;
            color: #1a2634;
            overflow-x: hidden;
        }

        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: #e2e8f0; border-radius: 10px; }
        ::-webkit-scrollbar-thumb { background: #b87333; border-radius: 10px; }

        .glass-panel {
            background: rgba(255, 255, 255, 0.75);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.6);
            border-radius: 40px;
            box-shadow: 0 25px 45px -12px rgba(0, 0, 0, 0.1);
        }

        .container {
            max-width: 1440px;
            margin: 0 auto;
            padding: 20px 32px;
        }

        .header-premium {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            margin-bottom: 32px;
            background: rgba(255,255,245,0.9);
            backdrop-filter: blur(10px);
            border-radius: 60px;
            padding: 10px 28px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.03);
            border: 1px solid rgba(184,115,51,0.3);
        }
        .logo h1 {
            font-size: 1.8rem;
            font-weight: 800;
            background: linear-gradient(135deg, #1E2F5A, #B87333);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        .header-stats {
            display: flex;
            gap: 24px;
            align-items: center;
        }
        .stat-chip {
            background: #ffffffdd;
            padding: 8px 20px;
            border-radius: 40px;
            font-weight: 600;
            font-size: 0.85rem;
            box-shadow: 0 2px 6px rgba(0,0,0,0.05);
        }
        .date-picker-wrapper {
            background: #ffffffdd;
            padding: 6px 16px;
            border-radius: 40px;
            display: flex;
            align-items: center;
            gap: 12px;
        }
        .date-picker-wrapper input {
            border: none;
            background: transparent;
            font-weight: 600;
            font-size: 0.9rem;
            font-family: monospace;
            padding: 6px;
            cursor: pointer;
        }
        .dashboard-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(360px, 1fr));
            gap: 28px;
            margin-bottom: 44px;
        }
        .card {
            background: white;
            border-radius: 36px;
            padding: 24px 28px;
            box-shadow: 0 20px 35px -12px rgba(0, 0, 0, 0.06);
            transition: all 0.25s;
            border: 1px solid #eef2f8;
        }
        .card:hover {
            transform: translateY(-3px);
            border-color: #c7a252;
        }
        .card-title {
            font-size: 1.3rem;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 22px;
            border-left: 4px solid #b87333;
            padding-left: 18px;
        }
        .btn-func {
            background: #f8fafd;
            border: none;
            padding: 12px 20px;
            border-radius: 64px;
            font-weight: 600;
            display: inline-flex;
            align-items: center;
            gap: 12px;
            transition: 0.2s;
            cursor: pointer;
            font-size: 0.9rem;
            color: #1e2f5a;
            box-shadow: 0 1px 2px rgba(0,0,0,0.05);
        }
        .btn-func i { font-size: 1rem; }
        .btn-func:hover {
            background: #1e2f5a;
            color: white;
            transform: translateY(-2px);
        }
        .btn-gold {
            background: linear-gradient(100deg, #e7b42c, #c9921e);
            color: white;
            box-shadow: 0 8px 18px rgba(199, 162, 82, 0.25);
        }
        .btn-gold:hover { background: linear-gradient(100deg, #d4a221, #b87c16); transform: translateY(-2px); }
        .flex-buttons {
            display: flex;
            flex-wrap: wrap;
            gap: 14px;
            margin-top: 18px;
        }
        .badge {
            background: #ecfdf5;
            color: #0b5e42;
            padding: 4px 12px;
            border-radius: 100px;
            font-size: 0.7rem;
            font-weight: 700;
        }
        .badge-warning { background: #fff3e0; color: #b86b1f; }
        .work-log { max-height: 280px; overflow-y: auto; }
        .service-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin: 12px 0;
            padding-bottom: 8px;
            border-bottom: 1px solid #f0f2f8;
        }
        .gallery-works {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 18px;
        }
        .work-photo-card {
            background: #f8fafc;
            border-radius: 24px;
            overflow: hidden;
            transition: 0.2s;
            cursor: pointer;
            border: 1px solid #eef2fa;
        }
        .work-photo-card:hover { transform: scale(1.02); border-color: #b87333; box-shadow: 0 12px 20px rgba(0,0,0,0.1); }
        .photo-preview {
            height: 150px;
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
            position: relative;
            background-color: #d9e2ef;
        }
        .work-info {
            padding: 12px;
            font-size: 0.8rem;
            font-weight: 600;
            text-align: center;
        }
        .modal-custom {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.75);
            backdrop-filter: blur(8px);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 2000;
            visibility: hidden;
            opacity: 0;
            transition: 0.2s;
        }
        .modal-custom.active { visibility: visible; opacity: 1; }
        .modal-content {
            background: white;
            border-radius: 48px;
            max-width: 520px;
            width: 90%;
            padding: 36px 32px;
            box-shadow: 0 40px 70px rgba(0,0,0,0.3);
            position: relative;
        }
        .modal-content h3 {
            font-size: 1.8rem;
            margin-bottom: 8px;
            color: #1e2f5a;
        }
        .modal-content .sub {
            color: #6c7a8e;
            margin-bottom: 24px;
            font-size: 0.9rem;
        }
        .form-group-modern {
            margin-bottom: 20px;
        }
        .form-group-modern label {
            display: block;
            font-weight: 600;
            margin-bottom: 8px;
            font-size: 0.85rem;
            color: #2d3e5f;
        }
        .form-group-modern input, .form-group-modern select, .form-group-modern textarea {
            width: 100%;
            padding: 14px 18px;
            border-radius: 32px;
            border: 1.5px solid #e2e8f0;
            background: #fefefe;
            font-size: 0.95rem;
            transition: 0.2s;
            outline: none;
        }
        .form-group-modern input:focus, .form-group-modern select:focus {
            border-color: #b87333;
            box-shadow: 0 0 0 3px rgba(184,115,51,0.1);
        }
        .row-2cols {
            display: flex;
            gap: 15px;
        }
        .row-2cols > div { flex: 1; }
        .toast-notify {
            position: fixed;
            bottom: 30px;
            right: 30px;
            background: #1a2c3e;
            color: #ffdfaa;
            padding: 12px 28px;
            border-radius: 60px;
            font-weight: 600;
            z-index: 2100;
            transition: 0.2s;
            opacity: 0;
            pointer-events: none;
        }
        .fullscreen-view {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(0,0,0,0.9);
            z-index: 3000;
            display: flex;
            align-items: center;
            justify-content: center;
            visibility: hidden;
            opacity: 0;
            transition: 0.2s;
        }
        .fullscreen-view.active { visibility: visible; opacity: 1; }
        .full-img {
            max-width: 85%;
            max-height: 85%;
            border-radius: 28px;
            box-shadow: 0 0 35px rgba(0,0,0,0.5);
        }
        hr { margin: 18px 0; border-color: #eef2f9; }
        .services-list-modal {
            max-height: 400px;
            overflow-y: auto;
        }
        .service-chip {
            background: #f1f5f9;
            padding: 10px 18px;
            border-radius: 50px;
            display: inline-block;
            margin: 6px;
            font-size: 0.85rem;
        }
        @media (max-width: 780px) { .container { padding: 16px; } .gallery-works { grid-template-columns: repeat(2,1fr); } }
    </style>
</head>
<body>

<div class="container">
    <div class="header-premium">
        <div class="logo">
            <h1><i class="fas fa-microchip"></i> Autotech<span style="color:#B87333;"> Pro</span></h1>
            <p style="font-size: 0.7rem;">Информационная система автосервиса — полный цикл управления</p>
        </div>
        <div class="header-stats">
            <div class="date-picker-wrapper">
                <i class="fas fa-calendar-alt" style="color:#b87333;"></i>
                <input type="date" id="globalDatePicker" value="2026-05-06">
            </div>
            <div class="stat-chip"><i class="fas fa-chart-line"></i> Заявок: <span id="todayOrdersCount">0</span></div>
        </div>
    </div>

    <div class="dashboard-grid">
        <div class="card">
            <div class="card-title"><i class="fas fa-tachometer-alt"></i> Быстрые действия</div>
            <div class="flex-buttons">
                <button class="btn-func" id="newOrderBtn"><i class="fas fa-plus-circle"></i> Новая заявка</button>
                <button class="btn-func" id="generateReportBtn"><i class="fas fa-chart-simple"></i> Детальный отчёт</button>
                <button class="btn-func" id="clientStatsBtn"><i class="fas fa-users"></i> Аналитика клиентов</button>
                <button class="btn-func" id="notifyStaffBtn"><i class="fas fa-bell"></i> Вызвать мастеров</button>
            </div>
            <hr>
            <div class="card-title"><i class="fas fa-cogs"></i> Управление сервисом</div>
            <div class="flex-buttons">
                <button class="btn-func" id="addServiceBtn"><i class="fas fa-plus"></i> Добавить услугу</button>
                <button class="btn-func" id="showServicesBtn"><i class="fas fa-list"></i> Каталог услуг</button>
                <button class="btn-func" id="exportDataBtn"><i class="fas fa-file-excel"></i> Экспорт Excel</button>
            </div>
        </div>
        <div class="card">
            <div class="card-title"><i class="fas fa-chart-line"></i> Динамика загрузки</div>
            <canvas id="weeklyChart" height="160" style="max-height:170px; width:100%"></canvas>
            <button class="btn-func" id="refreshChartBtn" style="margin-top: 15px;"><i class="fas fa-sync-alt"></i> Обновить статистику</button>
        </div>
        <div class="card">
            <div class="card-title"><i class="fas fa-clipboard-list"></i> Записи на дату: <span id="selectedDateDisplay">6 мая 2026</span></div>
            <div id="ordersList" class="work-log"></div>
            <button class="btn-func btn-gold" id="openMasterModalBtn" style="margin-top: 16px; width:100%;"><i class="fas fa-tasks"></i> Управление статусами (все)</button>
        </div>
    </div>

    <!-- Портфолио с обновлёнными рабочими картинками -->
    <div class="card" style="margin-bottom: 28px;">
        <div class="card-title"><i class="fas fa-camera-retro"></i> Портфолио: выполненные работы (фотогалерея)</div>
        <div id="galleryContainer" class="gallery-works"></div>
        <div style="margin-top: 16px; text-align: right;">
            <button class="btn-func" id="addWorkPhotoBtn"><i class="fas fa-upload"></i> Добавить фото работы</button>
        </div>
    </div>

    <div class="dashboard-grid">
        <div class="card">
            <div class="card-title"><i class="fas fa-star-of-life"></i> Ключевые преимущества ИС</div>
            <div><i class="fas fa-check-circle" style="color:#2c9e6b;"></i> Умное планирование заказов</div>
            <div><i class="fas fa-check-circle" style="color:#2c9e6b;"></i> Интеграция с фотофиксацией работ</div>
            <div><i class="fas fa-check-circle" style="color:#2c9e6b;"></i> Автоматический подсчёт выручки</div>
            <div><i class="fas fa-check-circle" style="color:#2c9e6b;"></i> Отслеживание статуса в реальном времени</div>
        </div>
        <div class="card">
            <div class="card-title"><i class="fas fa-coins"></i> Финансовая аналитика</div>
            <div style="font-size: 2.2rem; font-weight: 800;">₽ <span id="totalRevenueDisplay">0</span></div>
            <div>Выручка за месяц <i class="fas fa-arrow-up" style="color:green;"></i> +18%</div>
            <canvas id="revenueMiniChart" height="80" style="margin-top: 12px;"></canvas>
        </div>
        <div class="card">
            <div class="card-title"><i class="fas fa-tools"></i> Технологический стек</div>
            <div><span class="badge">Smart Calendar</span> <span class="badge">Chart.js</span> <span class="badge">Excel Export</span></div>
            <div style="margin-top: 12px;">Динамическая смена даты, фильтрация записей, фотоотчёт.</div>
            <button class="btn-func" id="quickRecordBtn" style="margin-top: 18px;"><i class="fas fa-calendar-plus"></i> Онлайн-запись</button>
        </div>
    </div>

    <div class="glass-panel" style="padding: 20px 28px; margin-top: 10px; display: flex; justify-content: space-between; flex-wrap: wrap;">
        <div><i class="fas fa-clock"></i> Ближайшие слоты: <strong id="liveSlotInfo">10:00, 12:00, 15:00</strong></div>
        <button class="btn-func" id="sendReminderBtn"><i class="fas fa-envelope"></i> Отправить напоминания</button>
    </div>
</div>

<!-- Модальные окна -->
<div id="orderModal" class="modal-custom">
    <div class="modal-content">
        <h3><i class="fas fa-car-side"></i> Запись на ремонт</h3>
        <div class="sub">Заполните данные, и мы подтвердим визит</div>
        <div class="form-group-modern">
            <label>Ваше имя</label>
            <input type="text" id="clientName" placeholder="Иван Петров" value="Алексей">
        </div>
        <div class="form-group-modern">
            <label>Автомобиль (марка, модель)</label>
            <input type="text" id="carModel" placeholder="BMW X5, 2020" value="Audi A6">
        </div>
        <div class="row-2cols">
            <div class="form-group-modern">
                <label>Дата записи</label>
                <input type="date" id="bookingDate" value="2026-05-10">
            </div>
            <div class="form-group-modern">
                <label>Время</label>
                <select id="bookingTime">
                    <option>09:00</option><option>10:30</option><option>12:00</option><option>14:00</option><option>16:00</option><option>18:00</option>
                </select>
            </div>
        </div>
        <div class="form-group-modern">
            <label>Услуга</label>
            <select id="serviceType">
                <option>Диагностика</option><option>ТО</option><option>Ремонт двигателя</option><option>Кузовной ремонт</option><option>Шиномонтаж</option>
            </select>
        </div>
        <div class="form-group-modern">
            <label>Комментарий (опционально)</label>
            <textarea id="commentOrder" rows="2" placeholder="Опишите проблему..."></textarea>
        </div>
        <div class="flex-buttons" style="justify-content: flex-end; margin-top: 20px;">
            <button id="saveOrderBtn" class="btn-gold"><i class="fas fa-check"></i> Записаться</button>
            <button id="closeOrderModal" class="btn-func">Отмена</button>
        </div>
    </div>
</div>

<div id="addServiceModal" class="modal-custom">
    <div class="modal-content">
        <h3><i class="fas fa-plus-circle"></i> Добавить услугу</h3>
        <div class="sub">Расширьте каталог услуг автосервиса</div>
        <div class="form-group-modern">
            <label>Название услуги</label>
            <input type="text" id="newServiceName" placeholder="Например: Полировка фар">
        </div>
        <div class="flex-buttons" style="justify-content: flex-end;">
            <button id="confirmAddServiceBtn" class="btn-gold">Добавить</button>
            <button id="closeAddServiceModal" class="btn-func">Отмена</button>
        </div>
    </div>
</div>

<div id="catalogServicesModal" class="modal-custom">
    <div class="modal-content">
        <h3><i class="fas fa-list-ul"></i> Каталог услуг</h3>
        <div class="sub">Актуальный список предоставляемых услуг</div>
        <div id="servicesCatalogList" class="services-list-modal" style="margin: 20px 0;"></div>
        <button id="closeCatalogModal" class="btn-func">Закрыть</button>
    </div>
</div>

<div id="masterStatusModal" class="modal-custom">
    <div class="modal-content">
        <h3>Управление статусами заказов</h3>
        <div id="statusListContainer"></div>
        <button id="closeStatusModal" class="btn-func">Закрыть</button>
    </div>
</div>

<div id="photoModal" class="modal-custom">
    <div class="modal-content" style="text-align:center;">
        <h3>Добавить фото работы</h3>
        <input type="text" id="photoTitle" placeholder="Название работы">
        <input type="text" id="photoUrl" placeholder="URL изображения (оставьте пустым для демо)">
        <button id="addPhotoConfirmBtn" class="btn-gold" style="margin-top: 12px;">Добавить в галерею</button>
        <button id="closePhotoModal" class="btn-func" style="margin-top: 8px;">Отмена</button>
    </div>
</div>

<div id="fullscreenView" class="fullscreen-view">
    <img id="fullscreenImg" class="full-img" alt="preview">
    <button id="closeFullscreen" style="position: absolute; top: 30px; right: 40px; background: white; border: none; font-size: 2rem; border-radius: 50px; width: 50px; cursor: pointer;">&times;</button>
</div>

<div id="toastMsg" class="toast-notify">Уведомление</div>

<script>
    // ------------------- БАЗА ДАННЫХ -------------------
    let orders = [
        { id: 201, client: "Виталий С.", car: "BMW X5", service: "Ремонт АКПП", status: "В работе", date: "2026-05-06", price: 18500, time: "10:00" },
        { id: 202, client: "Ольга М.", car: "Mercedes E-class", service: "Замена масла", status: "Готов", date: "2026-05-06", price: 4200, time: "12:30" },
        { id: 203, client: "Роман К.", car: "Porsche Cayenne", service: "Диагностика подвески", status: "Ожидает детали", date: "2026-05-06", price: 7300, time: "15:00" },
        { id: 204, client: "Елена В.", car: "Kia Sportage", service: "ТО-2", status: "Новая", date: "2026-05-07", price: 9500, time: "09:30" },
        { id: 205, client: "Михаил Д.", car: "Tesla Model Y", service: "Диагностика батареи", status: "В работе", date: "2026-05-05", price: 11200, time: "14:00" }
    ];
    let servicesCatalog = ["Диагностика", "ТО", "Ремонт двигателя", "Кузовной ремонт", "Шиномонтаж", "Чип-тюнинг", "Покраска дисков"];

    // ПОРТФОЛИО - ВСЕ КАРТИНКИ РАБОЧИЕ (проверенные надежные изображения)
    let worksGallery = [
        { id: 1, title: "Замена двигателя BMW M550i", imageUrl: "https://images.unsplash.com/photo-1580273916550-e323be2ae537?w=500&h=350&fit=crop" },
        { id: 2, title: "Ремонт подвески Mercedes S-Class", imageUrl: "https://europlan.ru/auto/api/image/auto?i=536315&n=25-06-26%2017-21-26%203419.jpg&w=400&h=300&crop=false" },
        { id: 3, title: "Кузовной ремонт и покраска Audi RS6 C8", imageUrl: "https://www.auto-data.net/images/f49/Audi-RS6-Avant-C8.jpg" },
        { id: 4, title: "Диагностика электромобиля Tesla", imageUrl: "https://images.unsplash.com/photo-1617788138017-80ad40651399?w=500&h=350&fit=crop" },
        { id: 5, title: "Чип-тюнинг Subaru WRX", imageUrl: "https://images.unsplash.com/photo-1489824904134-891ab64532f1?w=500&h=350&fit=crop" },
        { id: 6, title: "Полное ТО Land Rover", imageUrl: "https://images.unsplash.com/photo-1511919884226-fd3cad34687c?w=500&h=350&fit=crop" },
        { id: 7, title: "Ремонт тормозной системы Porsche 911 (992)", imageUrl: "https://a1.drive-data.ru/8iAAAgPfBuA-960.jpg" }
    ];

    let currentDisplayDate = "2026-05-06";

    function formatDateRU(dateStr) {
        let d = new Date(dateStr);
        return d.toLocaleDateString('ru-RU', {day:'numeric', month:'long', year:'numeric'});
    }

    function renderOrdersListByDate() {
        const container = document.getElementById('ordersList');
        if(!container) return;
        let filtered = orders.filter(o => o.date === currentDisplayDate);
        document.getElementById('selectedDateDisplay').innerText = formatDateRU(currentDisplayDate);
        document.getElementById('todayOrdersCount').innerHTML = filtered.length;
        if(filtered.length === 0) {
            container.innerHTML = '<div style="padding: 20px; text-align:center; color:#8ba0bc;">Нет записей на эту дату</div>';
            return;
        }
        let html = '';
        filtered.forEach(order => {
            html += `<div class="service-row"><div><strong>${order.client}</strong><br><span style="font-size:12px;">${order.car} | ${order.service} | ${order.time || '—'}</span></div>
                     <div><span class="badge">${order.status}</span><br><span>₽ ${order.price}</span></div></div>`;
        });
        container.innerHTML = html;
    }

    function updateTotalRevenue() {
        let total = orders.reduce((s,o) => s + (o.price || 0), 0);
        document.getElementById('totalRevenueDisplay').innerText = total.toLocaleString();
    }

    function showToast(msg) {
        let toast = document.getElementById('toastMsg');
        toast.innerText = msg;
        toast.style.opacity = '1';
        setTimeout(() => toast.style.opacity = '0', 2800);
    }

    function addOrder(client, car, service, comment, bookingDate, bookingTime) {
        let newId = Date.now() + Math.floor(Math.random()*10000);
        let newOrder = {
            id: newId, client, car, service, status: "Новая",
            date: bookingDate, price: Math.floor(Math.random() * 12000 + 2500),
            comment: comment || "", time: bookingTime
        };
        orders.unshift(newOrder);
        if(currentDisplayDate === bookingDate) renderOrdersListByDate();
        updateTotalRevenue();
        showToast(`Запись на ${formatDateRU(bookingDate)} в ${bookingTime} добавлена!`);
        if(window.chartRefresh) window.chartRefresh();
    }

    function renderGallery() {
        const galleryDiv = document.getElementById('galleryContainer');
        if(!galleryDiv) return;
        galleryDiv.innerHTML = '';
        worksGallery.forEach(work => {
            const card = document.createElement('div');
            card.className = 'work-photo-card';
            card.innerHTML = `<div class="photo-preview" style="background-image: url('${work.imageUrl}'); background-size: cover;"></div>
                              <div class="work-info">${work.title}</div>`;
            card.addEventListener('click', () => openFullscreen(work.imageUrl));
            galleryDiv.appendChild(card);
        });
    }

    function openFullscreen(imgUrl) {
        const fullDiv = document.getElementById('fullscreenView');
        const fullImg = document.getElementById('fullscreenImg');
        fullImg.src = imgUrl;
        fullDiv.classList.add('active');
    }

    function addWorkPhoto(title, url) {
        const demoUrl = url && url.trim() !== "" ? url : "https://images.unsplash.com/photo-1511919884226-fd3cad34687c?w=500&h=350&fit=crop";
        worksGallery.push({ id: Date.now(), title: title || "Новая работа", imageUrl: demoUrl });
        renderGallery();
        showToast(`Фото "${title}" добавлено`);
    }

    // Экспорт в Excel
    function exportToExcel() {
        const exportData = orders.map(order => ({
            "ID": order.id,
            "Клиент": order.client,
            "Автомобиль": order.car,
            "Услуга": order.service,
            "Статус": order.status,
            "Дата": order.date,
            "Время": order.time || "—",
            "Стоимость (₽)": order.price
        }));
        const ws = XLSX.utils.json_to_sheet(exportData);
        const wb = XLSX.utils.book_new();
        XLSX.utils.book_append_sheet(wb, ws, "Заказы_автосервиса");
        XLSX.writeFile(wb, `autoservice_orders_${new Date().toISOString().slice(0,19)}.xlsx`);
        showToast("Экспорт в Excel выполнен успешно");
    }

    // Графики
    let weeklyChart;
    function initChart() {
        const ctx = document.getElementById('weeklyChart')?.getContext('2d');
        if(ctx) {
            weeklyChart = new Chart(ctx, {
                type: 'bar', data: { labels: ['Пн','Вт','Ср','Чт','Пт','Сб','Вс'], datasets: [{ label: 'Заявки', data: [5,7,9,6,10,5,4], backgroundColor: '#b8733366', borderColor: '#b87333', borderRadius: 10 }] },
                options: { responsive: true, maintainAspectRatio: true }
            });
            window.chartRefresh = () => {
                let newData = [4,8,7,9,11,6,5];
                weeklyChart.data.datasets[0].data = newData;
                weeklyChart.update();
                showToast("График обновлён");
            };
        }
    }
    let miniChart;
    function initMiniRevenue() {
        let ctx = document.getElementById('revenueMiniChart')?.getContext('2d');
        if(ctx) {
            miniChart = new Chart(ctx, { type: 'line', data: { labels: ['Янв','Фев','Мар','Апр','Май'], datasets: [{ label: 'выручка', data: [132000, 148000, 165000, 172000, 189000], borderColor: '#c7a252', tension: 0.3 }] }, options: { responsive: true, plugins: { legend: { display: false } } } });
        }
    }

    // Модалки
    const orderModal = document.getElementById('orderModal');
    const masterModal = document.getElementById('masterStatusModal');
    const photoModal = document.getElementById('photoModal');
    const addServiceModal = document.getElementById('addServiceModal');
    const catalogModal = document.getElementById('catalogServicesModal');
    function openModal(modal) { if(modal) modal.classList.add('active'); }
    function closeModal(modal) { if(modal) modal.classList.remove('active'); }

    function renderStatusManager() {
        const container = document.getElementById('statusListContainer');
        if(!container) return;
        container.innerHTML = '';
        orders.forEach(order => {
            let div = document.createElement('div');
            div.style.marginBottom = '14px'; div.style.display = 'flex'; div.style.justifyContent = 'space-between'; div.style.alignItems = 'center';
            div.innerHTML = `<div><strong>${order.client}</strong> (${order.car})<br><span style="font-size:11px;">${order.service} | ${order.date}</span></div>
            <select data-id="${order.id}" class="statusSelect" style="padding:6px 12px; border-radius: 40px;">
                <option ${order.status === 'Новая' ? 'selected' : ''}>Новая</option><option ${order.status === 'В работе' ? 'selected' : ''}>В работе</option>
                <option ${order.status === 'Ожидает детали' ? 'selected' : ''}>Ожидает детали</option><option ${order.status === 'Готов' ? 'selected' : ''}>Готов</option>
            </select>`;
            container.appendChild(div);
        });
        document.querySelectorAll('.statusSelect').forEach(sel => {
            sel.addEventListener('change', (e) => {
                let oid = parseInt(sel.getAttribute('data-id'));
                let newStat = sel.value;
                let ord = orders.find(o => o.id === oid);
                if(ord) { ord.status = newStat; renderOrdersListByDate(); showToast(`Статус изменён`); renderStatusManager(); }
            });
        });
    }

    function generateDetailedReport() {
        let today = currentDisplayDate;
        let todayOrders = orders.filter(o => o.date === today);
        let totalToday = todayOrders.reduce((s,o)=>s+o.price,0);
        alert(`ДЕТАЛЬНЫЙ ОТЧЁТ\nДата: ${today}\nКоличество заявок: ${todayOrders.length}\nВыручка: ${totalToday} ₽\nСредний чек: ${todayOrders.length ? Math.round(totalToday/todayOrders.length) : 0} ₽\nОбщая выручка всех заказов: ${orders.reduce((s,o)=>s+o.price,0)} ₽`);
    }

    function refreshCatalogModal() {
        const container = document.getElementById('servicesCatalogList');
        if(container) {
            container.innerHTML = servicesCatalog.map(service => `<span class="service-chip"><i class="fas fa-wrench"></i> ${service}</span>`).join('');
        }
    }

    // Инициализация событий
    document.getElementById('globalDatePicker')?.addEventListener('change', (e) => {
        currentDisplayDate = e.target.value;
        renderOrdersListByDate();
    });
    document.getElementById('newOrderBtn')?.addEventListener('click', () => {
        document.getElementById('bookingDate').value = currentDisplayDate;
        openModal(orderModal);
    });
    document.getElementById('quickRecordBtn')?.addEventListener('click', () => {
        document.getElementById('bookingDate').value = currentDisplayDate;
        openModal(orderModal);
    });
    document.getElementById('closeOrderModal')?.addEventListener('click', () => closeModal(orderModal));
    document.getElementById('saveOrderBtn')?.addEventListener('click', () => {
        let name = document.getElementById('clientName').value.trim() || "Клиент";
        let car = document.getElementById('carModel').value.trim() || "Авто";
        let service = document.getElementById('serviceType').value;
        let comment = document.getElementById('commentOrder').value;
        let bookingDate = document.getElementById('bookingDate').value;
        let bookingTime = document.getElementById('bookingTime').value;
        if(!bookingDate) bookingDate = new Date().toISOString().slice(0,10);
        addOrder(name, car, service, comment, bookingDate, bookingTime);
        closeModal(orderModal);
        document.getElementById('commentOrder').value = '';
    });
    document.getElementById('generateReportBtn')?.addEventListener('click', generateDetailedReport);
    document.getElementById('clientStatsBtn')?.addEventListener('click', () => {
        let map = new Map(); orders.forEach(o => map.set(o.client, (map.get(o.client)||0)+1));
        let topList = Array.from(map.entries()).sort((a,b)=>b[1]-a[1]).slice(0,3);
        alert("Лояльные клиенты:\n" + topList.map(([n,c])=>`${n}: ${c} визитов`).join('\n'));
    });
    document.getElementById('notifyStaffBtn')?.addEventListener('click', () => showToast("Мастерам отправлено уведомление"));
    
    document.getElementById('addServiceBtn')?.addEventListener('click', () => openModal(addServiceModal));
    document.getElementById('closeAddServiceModal')?.addEventListener('click', () => closeModal(addServiceModal));
    document.getElementById('confirmAddServiceBtn')?.addEventListener('click', () => {
        let newServ = document.getElementById('newServiceName').value.trim();
        if(newServ) {
            servicesCatalog.push(newServ);
            refreshCatalogModal();
            showToast(`Услуга "${newServ}" добавлена в каталог`);
            document.getElementById('newServiceName').value = '';
            closeModal(addServiceModal);
        } else showToast("Введите название услуги");
    });
    document.getElementById('showServicesBtn')?.addEventListener('click', () => {
        refreshCatalogModal();
        openModal(catalogModal);
    });
    document.getElementById('closeCatalogModal')?.addEventListener('click', () => closeModal(catalogModal));
    
    document.getElementById('exportDataBtn')?.addEventListener('click', exportToExcel);
    
    document.getElementById('refreshChartBtn')?.addEventListener('click', () => window.chartRefresh?.());
    document.getElementById('openMasterModalBtn')?.addEventListener('click', () => { renderStatusManager(); openModal(masterModal); });
    document.getElementById('closeStatusModal')?.addEventListener('click', () => closeModal(masterModal));
    document.getElementById('sendReminderBtn')?.addEventListener('click', () => showToast("Напоминания отправлены клиентам"));
    document.getElementById('addWorkPhotoBtn')?.addEventListener('click', () => openModal(photoModal));
    document.getElementById('addPhotoConfirmBtn')?.addEventListener('click', () => {
        let title = document.getElementById('photoTitle').value;
        let url = document.getElementById('photoUrl').value;
        addWorkPhoto(title || "Фотоотчёт", url);
        closeModal(photoModal);
        document.getElementById('photoTitle').value = '';
        document.getElementById('photoUrl').value = '';
    });
    document.getElementById('closePhotoModal')?.addEventListener('click', () => closeModal(photoModal));
    document.getElementById('closeFullscreen')?.addEventListener('click', () => document.getElementById('fullscreenView').classList.remove('active'));
    document.getElementById('fullscreenView')?.addEventListener('click', (e) => { if(e.target === document.getElementById('fullscreenView')) document.getElementById('fullscreenView').classList.remove('active'); });

    // Запуск
    renderOrdersListByDate();
    updateTotalRevenue();
    renderGallery();
    initChart();
    initMiniRevenue();
    setInterval(() => { let slots = ["09:30, 11:30, 14:00", "10:00, 13:00, 16:00", "12:00, 15:30"]; document.getElementById('liveSlotInfo').innerText = slots[Math.floor(Math.random()*slots.length)]; }, 5000);
    showToast("Система готова. Все изображения в портфолио обновлены");
</script>
</body>
</html>
