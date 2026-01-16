<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="white">
    <title>Jo·Ra的小窝 ❤️</title>
    <style>
        /* 全局样式 - 轻量化 + iPhone适配 + 可爱字体 */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "幼圆", "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", sans-serif;
        }
        
        body {
            background-color: #ffffff;
            color: #333333;
            padding: 10px;
            max-width: 428px;
            margin: 0 auto;
            line-height: 1.4;
            font-size: 13px;
        }
        
        /* 顶部时间天气区域 */
        .header {
            text-align: center;
            padding: 12px 0;
            border-bottom: 1px solid #f0f0f0;
            margin-bottom: 12px;
        }
        
        .time-date {
            font-size: 18px;
            font-weight: bold;
            margin-bottom: 4px;
            color: #ff6b8b;
            letter-spacing: 2px;
            text-shadow: 0 1px 2px rgba(255,107,139,0.1);
        }
        
        .weather {
            font-size: 13px;
            color: #666666;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 5px;
        }
        
        /* 分类模块区域 */
        .categories {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
            margin-bottom: 15px;
        }
        
        .category-card {
            background-color: #f8f9fa;
            border-radius: 8px;
            padding: 12px;
            text-align: center;
            box-shadow: 0 1px 4px rgba(0,0,0,0.02);
            transition: all 0.2s;
            cursor: pointer;
        }
        
        .category-card:hover {
            transform: translateY(-1px);
            background-color: #fff0f3;
        }
        
        .category-icon {
            font-size: 22px;
            margin-bottom: 6px;
        }
        
        .category-title {
            font-size: 14px;
            font-weight: 600;
            margin-bottom: 3px;
        }
        
        .category-desc {
            font-size: 11px;
            color: #888888;
        }
        
        /* 代办事项区域 */
        .todo-section {
            margin-bottom: 15px;
            border-bottom: 1px solid #f0f0f0;
            padding-bottom: 15px;
        }
        
        .todo-title {
            font-size: 14px;
            font-weight: 600;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 5px;
            color: #ff6b8b;
        }
        
        .todo-input-container {
            display: flex;
            gap: 5px;
            margin-bottom: 10px;
        }
        
        #todo-input {
            flex: 1;
            padding: 8px 10px;
            border: 1px solid #e0e0e0;
            border-radius: 5px;
            font-size: 13px;
        }
        
        #add-todo {
            background-color: #ff6b8b;
            color: white;
            border: none;
            border-radius: 5px;
            padding: 0 10px;
            cursor: pointer;
            font-size: 13px;
        }
        
        .todo-list-container {
            max-height: calc(3 * 38px);
            overflow-y: auto;
            -webkit-overflow-scrolling: touch;
        }
        
        #todo-list {
            list-style: none;
        }
        
        .todo-item {
            display: flex;
            align-items: center;
            padding: 6px 0;
            border-bottom: 1px solid #f5f5f5;
            height: 38px;
        }
        
        .todo-checkbox {
            width: 16px;
            height: 16px;
            margin-right: 8px;
            accent-color: #ff6b8b;
        }
        
        .todo-text {
            flex: 1;
            font-size: 13px;
        }
        
        .todo-text.completed {
            text-decoration: line-through;
            color: #aaaaaa;
        }
        
        .todo-delete {
            color: #ff6b8b;
            background: none;
            border: none;
            cursor: pointer;
            font-size: 11px;
            opacity: 0.7;
        }
        
        /* 图片展示区域 */
        .photo-section {
            margin-bottom: 12px;
        }
        
        .photo-title {
            font-size: 14px;
            font-weight: 600;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 5px;
            color: #ff6b8b;
        }
        
        .photo-container {
            position: relative;
            width: 100%;
            padding-top: 56.25%;
            background-color: #f8f9fa;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 1px 4px rgba(0,0,0,0.02);
        }
        
        #photo-display {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: none;
        }
        
        .photo-placeholder {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            color: #999999;
            font-size: 13px;
        }
        
        .photo-placeholder-icon {
            font-size: 36px;
            margin-bottom: 6px;
        }
        
        #photo-upload {
            display: none;
        }
        
        .photo-upload-btn {
            margin-top: 10px;
            padding: 7px 14px;
            background-color: #f0f0f0;
            border: none;
            border-radius: 5px;
            color: #666666;
            cursor: pointer;
            font-size: 11px;
        }
        
        /* 分类详情弹窗 */
        .detail-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            padding: 15px;
        }
        
        .detail-content {
            background-color: white;
            border-radius: 10px;
            width: 100%;
            max-width: 360px;
            max-height: 90vh;
            overflow-y: auto;
            -webkit-overflow-scrolling: touch;
            padding: 15px;
        }
        
        .detail-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
            padding-bottom: 8px;
            border-bottom: 1px solid #f0f0f0;
        }
        
        .detail-title {
            font-size: 16px;
            font-weight: 600;
            color: #ff6b8b;
        }
        
        .close-btn {
            background: none;
            border: none;
            font-size: 18px;
            cursor: pointer;
            color: #666;
        }
        
        .detail-form {
            margin-bottom: 12px;
        }
        
        .detail-input {
            width: 100%;
            padding: 8px 10px;
            border: 1px solid #e0e0e0;
            border-radius: 5px;
            margin-bottom: 8px;
            font-size: 13px;
        }
        
        .detail-textarea {
            width: 100%;
            padding: 8px 10px;
            border: 1px solid #e0e0e0;
            border-radius: 5px;
            margin-bottom: 8px;
            font-size: 13px;
            min-height: 70px;
            resize: none;
        }
        
        .upload-img-btn {
            padding: 7px 14px;
            background-color: #f0f0f0;
            border: none;
            border-radius: 5px;
            color: #666;
            cursor: pointer;
            font-size: 11px;
            margin-bottom: 8px;
        }
        
        .crop-btn {
            padding: 7px 14px;
            background-color: #ff6b8b;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 11px;
            margin-bottom: 8px;
            display: none;
        }
        
        .save-btn {
            background-color: #ff6b8b;
            color: white;
            border: none;
            border-radius: 5px;
            padding: 8px 18px;
            cursor: pointer;
            font-size: 13px;
        }
        
        /* 图片裁剪弹窗 */
        .crop-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.8);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 2000;
            padding: 20px;
        }
        
        .crop-content {
            width: 100%;
            max-width: 320px;
            background-color: white;
            border-radius: 10px;
            padding: 15px;
        }
        
        .crop-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .crop-title {
            font-size: 14px;
            font-weight: 600;
            color: #ff6b8b;
        }
        
        .crop-close-btn {
            background: none;
            border: none;
            font-size: 18px;
            cursor: pointer;
            color: #666;
        }
        
        .crop-container {
            position: relative;
            width: 100%;
            height: 280px;
            background-color: #f0f0f0;
            margin-bottom: 10px;
            overflow: hidden;
        }
        
        .crop-img {
            position: absolute;
            top: 0;
            left: 0;
            transform-origin: center center;
        }
        
        .crop-box {
            position: absolute;
            border: 2px solid #ff6b8b;
            background-color: rgba(255,255,255,0.2);
            cursor: move;
            box-sizing: border-box;
        }
        
        .crop-confirm-btn {
            width: 100%;
            padding: 8px 0;
            background-color: #ff6b8b;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 13px;
        }
        
        /* 图片+可爱文字预览 */
        .img-note-preview {
            position: relative;
            width: 100%;
            border-radius: 8px;
            overflow: hidden;
            margin-bottom: 8px;
            display: none;
            aspect-ratio: 1/1; /* 正方形预览 */
        }
        
        .preview-img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block;
        }
        
        .cute-text-overlay {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: white;
            font-size: 16px;
            font-weight: bold;
            text-shadow: 0 2px 4px rgba(0,0,0,0.5);
            text-align: center;
            padding: 0 10px;
            letter-spacing: 1px;
            font-family: "幼圆", sans-serif;
        }
        
        .detail-list {
            margin-top: 12px;
        }
        
        .detail-item {
            margin-bottom: 12px;
            border-bottom: 1px solid #f5f5f5;
            padding-bottom: 8px;
            position: relative;
        }
        
        .detail-item-delete {
            position: absolute;
            top: 0;
            right: 0;
            background-color: #ff4444;
            color: white;
            border: none;
            border-radius: 4px;
            padding: 2px 6px;
            font-size: 10px;
            cursor: pointer;
            opacity: 0.7;
        }
        
        .detail-item-delete:hover {
            opacity: 1;
        }
        
        .detail-item-img-container {
            position: relative;
            width: 100%;
            border-radius: 8px;
            overflow: hidden;
            margin-bottom: 6px;
            aspect-ratio: 1/1; /* 正方形显示 */
        }
        
        .detail-item-img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block;
        }
        
        .detail-item-text-overlay {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: white;
            font-size: 14px;
            font-weight: bold;
            text-shadow: 0 2px 4px rgba(0,0,0,0.5);
            text-align: center;
            padding: 0 8px;
            letter-spacing: 1px;
            font-family: "幼圆", sans-serif;
        }
        
        .detail-item-text {
            font-size: 13px;
            color: #333;
            margin-bottom: 3px;
        }
        
        .detail-item-note {
            font-size: 11px;
            color: #888;
        }
        
        /* 隐藏滚动条 */
        ::-webkit-scrollbar {
            width: 0;
            height: 0;
        }
    </style>
</head>
<body>
    <!-- 顶部：时间日期天气 -->
    <div class="header">
        <div class="time-date" id="time-date">2026-01-16 Fri 14:30</div>
        <div class="weather" id="weather">
            <span>☀️</span>
            <span>加载中...</span>
        </div>
    </div>

    <!-- 中上：分类模块 -->
    <div class="categories">
        <div class="category-card" data-type="eat">
            <div class="category-icon">🍽️</div>
            <div class="category-title">吃</div>
            <div class="category-desc">吃过&收藏小食堂</div>
        </div>
        <div class="category-card" data-type="drink">
            <div class="category-icon">☕</div>
            <div class="category-title">喝</div>
            <div class="category-desc">咖啡店 & 小酒馆</div>
        </div>
        <div class="category-card" data-type="play">
            <div class="category-icon">🚶</div>
            <div class="category-title">逛</div>
            <div class="category-desc">去过的美好地方</div>
        </div>
        <div class="category-card" data-type="good">
            <div class="category-icon">🎁</div>
            <div class="category-title">好物分享</div>
            <div class="category-desc">喜欢的小玩意儿</div>
        </div>
    </div>

    <!-- 中间：代办事项 -->
    <div class="todo-section">
        <div class="todo-title">
            <span>📝</span>
            <span>小Jo的待办事项</span>
        </div>
        <div class="todo-input-container">
            <input type="text" id="todo-input" placeholder="添加新的代办事项...">
            <button id="add-todo">添加</button>
        </div>
        <div class="todo-list-container">
            <ul id="todo-list"></ul>
        </div>
    </div>

    <!-- 下半部分：自定义图片区域 -->
    <div class="photo-section">
        <div class="photo-title">
            <span>🖼️</span>
            <span>Jo·Ra大冒险plog</span>
        </div>
        <div class="photo-container">
            <img id="photo-display" src="" alt="自定义图片">
            <div class="photo-placeholder" id="photo-placeholder">
                <div class="photo-placeholder-icon">🖼️</div>
                <div>点击上传我们的合照吧</div>
            </div>
        </div>
        <input type="file" id="photo-upload" accept="image/*">
        <button class="photo-upload-btn" onclick="document.getElementById('photo-upload').click()">选择图片</button>
    </div>

    <!-- 分类详情弹窗 -->
    <div class="detail-modal" id="detail-modal">
        <div class="detail-content">
            <div class="detail-header">
                <div class="detail-title" id="detail-modal-title">吃</div>
                <button class="close-btn" id="close-modal">×</button>
            </div>
            <div class="detail-form">
                <input type="text" class="detail-input" id="item-name" placeholder="输入名称（如：XX餐厅）">
                <textarea class="detail-textarea" id="item-note" placeholder="输入可爱小文字（会显示在图片中间）"></textarea>
                <input type="file" id="item-photo-upload" accept="image/*" style="display: none;">
                <button class="upload-img-btn" onclick="document.getElementById('item-photo-upload').click()">上传图片</button>
                <button class="crop-btn" id="crop-btn" onclick="openCropModal()">裁剪为正方形</button>
                
                <!-- 图片+可爱文字预览（正方形） -->
                <div class="img-note-preview" id="img-note-preview">
                    <img class="preview-img" id="item-photo-preview" src="" alt="预览">
                    <div class="cute-text-overlay" id="cute-text-preview">可爱小文字</div>
                </div>
                
                <button class="save-btn" id="save-item">保存</button>
            </div>
            <div class="detail-list" id="detail-list"></div>
        </div>
    </div>

    <!-- 图片裁剪弹窗 -->
    <div class="crop-modal" id="crop-modal">
        <div class="crop-content">
            <div class="crop-header">
                <div class="crop-title">裁剪为正方形</div>
                <button class="crop-close-btn" id="crop-close-btn">×</button>
            </div>
            <div class="crop-container" id="crop-container">
                <img class="crop-img" id="crop-img" src="" alt="裁剪图片">
                <div class="crop-box" id="crop-box"></div>
            </div>
            <button class="crop-confirm-btn" id="crop-confirm-btn">确认裁剪</button>
        </div>
    </div>

    <script>
        // 全局变量
        let currentCategory = '';
        let itemPhotoBase64 = '';
        let cropImgOriginal = '';
        let cropScale = 1;
        let cropOffsetX = 0;
        let cropOffsetY = 0;
        let isDragging = false;
        let startX, startY;

        // 1. 实时更新时间日期（英文星期缩写）
        function updateDateTime() {
            const now = new Date();
            const year = now.getFullYear();
            const month = String(now.getMonth() + 1).padStart(2, '0');
            const day = String(now.getDate()).padStart(2, '0');
            const hours = String(now.getHours()).padStart(2, '0');
            const minutes = String(now.getMinutes()).padStart(2, '0');
            const weekdays = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'];
            const weekday = weekdays[now.getDay()];
            const timeStr = `${year}-${month}-${day} ${weekday} ${hours}:${minutes}`;
            document.getElementById('time-date').textContent = timeStr;
        }
        setInterval(updateDateTime, 1000);
        updateDateTime();

        // 2. 获取天气（适配iPhone/微信环境）
        async function getWeather() {
            try {
                const response = await fetch('https://api.weatherapi.com/v1/current.json?key=7e9e0e9999d8469d8c6142406241601&q=auto:ip', {
                    mode: 'cors',
                    cache: 'no-cache'
                });
                if (!response.ok) throw new Error('天气接口请求失败');
                const data = await response.json();
                const weatherIcons = {
                    'Sunny': '☀️',
                    'Partly cloudy': '⛅',
                    'Cloudy': '☁️',
                    'Rain': '🌧️',
                    'Light rain': '🌦️',
                    'Snow': '❄️',
                    'Clear': '🌙',
                    'Mist': '🌫️',
                    'Fog': '🌫️'
                };
                const icon = weatherIcons[data.current.condition.text] || '☀️';
                const temp = data.current.temp_c;
                const city = data.location.name;
                const desc = data.current.condition.text;
                document.getElementById('weather').innerHTML = `
                    <span>${icon}</span>
                    <span>${city} ${temp}°C ${desc}</span>
                `;
            } catch (error) {
                console.error('获取天气失败:', error);
                document.getElementById('weather').innerHTML = `
                    <span>☀️</span>
                    <span>本地 22°C 晴</span>
                `;
            }
        }
        getWeather();
        setInterval(getWeather, 30 * 60 * 1000);

        // 3. 代办事项功能
        const todoInput = document.getElementById('todo-input');
        const addTodoBtn = document.getElementById('add-todo');
        const todoList = document.getElementById('todo-list');

        function loadTodos() {
            const todos = JSON.parse(localStorage.getItem('couple-todos') || '[]');
            todos.forEach(todo => addTodoToDOM(todo.text, todo.completed));
        }

        function addTodoToDOM(text, completed = false) {
            const li = document.createElement('li');
            li.className = 'todo-item';
            li.innerHTML = `
                <input type="checkbox" class="todo-checkbox" ${completed ? 'checked' : ''}>
                <span class="todo-text ${completed ? 'completed' : ''}">${text}</span>
                <button class="todo-delete">删除</button>
            `;
            const checkbox = li.querySelector('.todo-checkbox');
            checkbox.addEventListener('change', () => {
                const textSpan = li.querySelector('.todo-text');
                textSpan.classList.toggle('completed');
                saveTodos();
            });
            const deleteBtn = li.querySelector('.todo-delete');
            deleteBtn.addEventListener('click', () => {
                li.remove();
                saveTodos();
            });
            todoList.appendChild(li);
        }

        function saveTodos() {
            const todos = [];
            document.querySelectorAll('.todo-item').forEach(item => {
                const text = item.querySelector('.todo-text').textContent;
                const completed = item.querySelector('.todo-checkbox').checked;
                todos.push({ text, completed });
            });
            localStorage.setItem('couple-todos', JSON.stringify(todos));
        }

        addTodoBtn.addEventListener('click', () => {
            const text = todoInput.value.trim();
            if (text) {
                addTodoToDOM(text);
                todoInput.value = '';
                saveTodos();
            }
        });

        todoInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') addTodoBtn.click();
        });

        // 4. 主图片上传功能
        const photoUpload = document.getElementById('photo-upload');
        const photoDisplay = document.getElementById('photo-display');
        const photoPlaceholder = document.getElementById('photo-placeholder');

        photoUpload.addEventListener('change', (e) => {
            const file = e.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = (event) => {
                    photoDisplay.src = event.target.result;
                    photoDisplay.style.display = 'block';
                    photoPlaceholder.style.display = 'none';
                    localStorage.setItem('couple-photo', event.target.result);
                };
                reader.readAsDataURL(file);
            }
        });

        function loadPhoto() {
            const savedPhoto = localStorage.getItem('couple-photo');
            if (savedPhoto) {
                photoDisplay.src = savedPhoto;
                photoDisplay.style.display = 'block';
                photoPlaceholder.style.display = 'none';
            }
        }

        // 5. 分类详情功能（核心：图片裁剪+可爱文字+删除）
        const categoryCards = document.querySelectorAll('.category-card');
        const detailModal = document.getElementById('detail-modal');
        const closeModal = document.getElementById('close-modal');
        const detailModalTitle = document.getElementById('detail-modal-title');
        const itemPhotoUpload = document.getElementById('item-photo-upload');
        const itemPhotoPreview = document.getElementById('item-photo-preview');
        const cuteTextPreview = document.getElementById('cute-text-preview');
        const imgNotePreview = document.getElementById('img-note-preview');
        const cropBtn = document.getElementById('crop-btn');
        const itemNameInput = document.getElementById('item-name');
        const itemNoteInput = document.getElementById('item-note');
        const saveItemBtn = document.getElementById('save-item');
        const detailList = document.getElementById('detail-list');

        // 裁剪相关元素
        const cropModal = document.getElementById('crop-modal');
        const cropCloseBtn = document.getElementById('crop-close-btn');
        const cropImg = document.getElementById('crop-img');
        const cropContainer = document.getElementById('crop-container');
        const cropBox = document.getElementById('crop-box');
        const cropConfirmBtn = document.getElementById('crop-confirm-btn');

        // 分类标题映射
        const categoryTitles = {
            'eat': '吃',
            'drink': '喝',
            'play': '逛',
            'good': '好物分享'
        };

        // 打开详情弹窗
        categoryCards.forEach(card => {
            card.addEventListener('click', () => {
                currentCategory = card.dataset.type;
                detailModalTitle.textContent = categoryTitles[currentCategory];
                detailModal.style.display = 'flex';
                loadCategoryItems();
                // 重置表单
                itemPhotoPreview.src = '';
                imgNotePreview.style.display = 'none';
                cropBtn.style.display = 'none';
                itemPhotoBase64 = '';
                itemNameInput.value = '';
                itemNoteInput.value = '';
            });
        });

        // 关闭详情弹窗
        closeModal.addEventListener('click', () => {
            detailModal.style.display = 'none';
        });

        detailModal.addEventListener('click', (e) => {
            if (e.target === detailModal) closeModal.click();
        });

        // 实时预览可爱文字
        itemNoteInput.addEventListener('input', () => {
            const noteText = itemNoteInput.value.trim() || '可爱小文字';
            cuteTextPreview.textContent = noteText;
        });

        // 上传分类图片
        itemPhotoUpload.addEventListener('change', (e) => {
            const file = e.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = (event) => {
                    itemPhotoBase64 = event.target.result;
                    cropImgOriginal = event.target.result;
                    itemPhotoPreview.src = itemPhotoBase64;
                    imgNotePreview.style.display = 'block';
                    cropBtn.style.display = 'inline-block';
                    // 同步文字预览
                    const noteText = itemNoteInput.value.trim() || '可爱小文字';
                    cuteTextPreview.textContent = noteText;
                };
                reader.readAsDataURL(file);
            }
        });

        // 打开裁剪弹窗
        function openCropModal() {
            if (!cropImgOriginal) return;
            cropModal.style.display = 'flex';
            cropImg.src = cropImgOriginal;
            
            // 初始化裁剪框
            setTimeout(() => {
                const containerRect = cropContainer.getBoundingClientRect();
                const img = new Image();
                img.src = cropImgOriginal;
                
                img.onload = () => {
                    // 计算缩放比例，让图片适应容器
                    const scaleX = containerRect.width / img.width;
                    const scaleY = containerRect.height / img.height;
                    cropScale = Math.min(scaleX, scaleY);
                    
                    // 设置图片尺寸和位置
                    cropImg.style.width = `${img.width * cropScale}px`;
                    cropImg.style.height = `${img.height * cropScale}px`;
                    cropImg.style.top = `${(containerRect.height - img.height * cropScale) / 2}px`;
                    cropImg.style.left = `${(containerRect.width - img.width * cropScale) / 2}px`;
                    
                    // 设置正方形裁剪框
                    const cropSize = Math.min(containerRect.width, containerRect.height) * 0.8;
                    cropBox.style.width = `${cropSize}px`;
                    cropBox.style.height = `${cropSize}px`;
                    cropBox.style.top = `${(containerRect.height - cropSize) / 2}px`;
                    cropBox.style.left = `${(containerRect.width - cropSize) / 2}px`;
                    
                    cropOffsetX = parseInt(cropBox.style.left);
                    cropOffsetY = parseInt(cropBox.style.top);
                };
            }, 100);
        }

        // 关闭裁剪弹窗
        cropCloseBtn.addEventListener('click', () => {
            cropModal.style.display = 'none';
        });

        // 裁剪框拖拽功能
        cropBox.addEventListener('mousedown', (e) => {
            isDragging = true;
            startX = e.clientX - cropOffsetX;
            startY = e.clientY - cropOffsetY;
            e.preventDefault();
        });

        document.addEventListener('mousemove', (e) => {
            if (!isDragging) return;
            const containerRect = cropContainer.getBoundingClientRect();
            const newX = e.clientX - startX;
            const newY = e.clientY - startY;
            
            // 限制裁剪框在容器内
            cropOffsetX = Math.max(0, Math.min(newX, containerRect.width - parseInt(cropBox.style.width)));
            cropOffsetY = Math.max(0, Math.min(newY, containerRect.height - parseInt(cropBox.style.height)));
            
            cropBox.style.left = `${cropOffsetX}px`;
            cropBox.style.top = `${cropOffsetY}px`;
        });

        document.addEventListener('mouseup', () => {
            isDragging = false;
        });

        // 移动端触摸拖拽
        cropBox.addEventListener('touchstart', (e) => {
            isDragging = true;
            startX = e.touches[0].clientX - cropOffsetX;
            startY = e.touches[0].clientY - cropOffsetY;
            e.preventDefault();
        });

        document.addEventListener('touchmove', (e) => {
            if (!isDragging) return;
            const containerRect = cropContainer.getBoundingClientRect();
            const newX = e.touches[0].clientX - startX;
            const newY = e.touches[0].clientY - startY;
            
            cropOffsetX = Math.max(0, Math.min(newX, containerRect.width - parseInt(cropBox.style.width)));
            cropOffsetY = Math.max(0, Math.min(newY, containerRect.height - parseInt(cropBox.style.height)));
            
            cropBox.style.left = `${cropOffsetX}px`;
            cropBox.style.top = `${cropOffsetY}px`;
        });

        document.addEventListener('touchend', () => {
            isDragging = false;
        });

        // 确认裁剪
        cropConfirmBtn.addEventListener('click', () => {
            const canvas = document.createElement('canvas');
            const ctx = canvas.getContext('2d');
            const cropSize = parseInt(cropBox.style.width);
            
            // 设置canvas为正方形
            canvas.width = cropSize;
            canvas.height = cropSize;
            
            const img = new Image();
            img.src = cropImgOriginal;
            
            img.onload = () => {
                // 计算裁剪区域
                const containerRect = cropContainer.getBoundingClientRect();
                const imgRect = cropImg.getBoundingClientRect();
                
                const imgScaleX = img.width / imgRect.width;
                const imgScaleY = img.height / imgRect.height;
                
                const cropX = (cropOffsetX - (imgRect.left - containerRect.left)) * imgScaleX;
                const cropY = (cropOffsetY - (imgRect.top - containerRect.top)) * imgScaleY;
                const cropWidth = cropSize * imgScaleX;
                const cropHeight = cropSize * imgScaleY;
                
                // 绘制裁剪后的图片
                ctx.drawImage(img, cropX, cropY, cropWidth, cropHeight, 0, 0, cropSize, cropSize);
                
                // 转换为base64
                const croppedBase64 = canvas.toDataURL('image/jpeg', 0.9);
                itemPhotoBase64 = croppedBase64;
                itemPhotoPreview.src = croppedBase64;
                
                // 关闭裁剪弹窗
                cropModal.style.display = 'none';
            };
        });

        // 保存分类项
        saveItemBtn.addEventListener('click', () => {
            const name = itemNameInput.value.trim();
            const note = itemNoteInput.value.trim() || '无可爱备注～';
            
            if (!name) {
                alert('请输入名称哦～');
                return;
            }
            
            const item = {
                id: Date.now().toString(),
                name: name,
                note: note,
                photo: itemPhotoBase64,
                time: new Date().toLocaleString()
            };
            
            const items = JSON.parse(localStorage.getItem(`category-${currentCategory}`) || '[]');
            items.push(item);
            localStorage.setItem(`category-${currentCategory}`, JSON.stringify(items));
            
            loadCategoryItems();
            
            // 重置表单
            itemNameInput.value = '';
            itemNoteInput.value = '';
            itemPhotoPreview.src = '';
            imgNotePreview.style.display = 'none';
            cropBtn.style.display = 'none';
            itemPhotoBase64 = '';
            
            alert('保存成功啦～');
        });

        // 加载分类项（支持删除）
        function loadCategoryItems() {
            const items = JSON.parse(localStorage.getItem(`category-${currentCategory}`) || '[]');
            detailList.innerHTML = '';
            
            if (items.length === 0) {
                detailList.innerHTML = '<div style="text-align: center; color: #999; padding: 15px 0;">还没有记录哦，添加第一个吧～</div>';
                return;
            }
            
            items.forEach(item => {
                const itemDiv = document.createElement('div');
                itemDiv.className = 'detail-item';
                itemDiv.dataset.id = item.id;
                
                // 构建带删除按钮的HTML
                itemDiv.innerHTML = `
                    <button class="detail-item-delete" data-id="${item.id}">删除</button>
                    ${item.photo ? `
                        <div class="detail-item-img-container">
                            <img src="${item.photo}" class="detail-item-img" alt="${item.name}">
                            <div class="detail-item-text-overlay">${item.note}</div>
                        </div>
                    ` : ''}
                    <div class="detail-item-text">${item.name}</div>
                    <div style="font-size: 10px; color: #bbb; margin-top: 3px;">${item.time}</div>
                `;
                
                detailList.appendChild(itemDiv);
                
                // 添加删除事件
                const deleteBtn = itemDiv.querySelector('.detail-item-delete');
                deleteBtn.addEventListener('click', () => {
                    if (confirm('确定要删除这条记录吗？')) {
                        // 过滤掉要删除的项
                        const newItems = items.filter(i => i.id !== item.id);
                        localStorage.setItem(`category-${currentCategory}`, JSON.stringify(newItems));
                        loadCategoryItems(); // 刷新列表
                    }
                });
            });
        }

        // 初始化
        loadTodos();
        loadPhoto();
    </script>
</body>
</html>
