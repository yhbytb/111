# 111
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>施工交底协同平台 - 吊顶截面对比分析</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body, html {
            height: 100%;
            font-family: "Microsoft YaHei", sans-serif;
            background-color: #f5f5f5;
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #2c3e50 0%, #34495e 100%);
            color: #ffffff;
            padding: 15px 0;
            text-align: center;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 2px 15px rgba(0,0,0,0.1);
        }
        
        .header h1 {
            font-size: 24px;
            margin-bottom: 5px;
        }
        
        .header p {
            font-size: 16px;
            opacity: 0.9;
        }
        
        .main-container {
            display: flex;
            height: calc(100vh - 60px);
            width: 100%;
        }
        
        .comparison-section {
            flex: 3;
            display: flex;
            flex-direction: column;
        }
        
        .comparison-wrapper {
            flex: 1;
            display: flex;
            position: relative;
        }
        
        .comparison-item {
            flex: 1;
            display: flex;
            flex-direction: column;
            border-right: 2px solid #e74c3c;
            position: relative;
            transition: all 0.3s ease;
        }
        
        .comparison-item:hover {
            box-shadow: inset 0 0 0 2px rgba(231, 76, 60, 0.1);
        }
        
        .comparison-item:last-child {
            border-right: none;
        }
        
        .item-label {
            background: linear-gradient(to right, #2c3e50, #34495e);
            color: white;
            padding: 12px 15px;
            font-size: 16px;
            font-weight: bold;
            text-align: center;
            border-bottom: 1px solid #2c3e50;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        
        .item-content {
            flex: 1;
            position: relative;
            overflow: hidden;
        }
        
        .model-container, .image-container {
            width: 100%;
            height: 100%;
        }
        
        .image-container {
            display: flex;
            align-items: center;
            justify-content: center;
            background: linear-gradient(45deg, #ecf0f1 25%, #bdc3c7 25%, #bdc3c7 50%, #ecf0f1 50%, #ecf0f1 75%, #bdc3c7 75%, #bdc3c7);
            background-size: 30px 30px;
        }
        
        .image-container img {
            max-width: 95%;
            max-height: 95%;
            object-fit: contain;
            box-shadow: 0 5px 25px rgba(0,0,0,0.2);
            background-color: white;
            border-radius: 4px;
        }
        
        .modelo-wrapper {
            width: 100%;
            height: 100%;
            position: relative;
        }
        
        .modelo-wrapper iframe {
            width: 100%;
            height: 100%;
            border: none;
        }
        
        .notes-section {
            flex: 1;
            min-width: 350px;
            max-width: 450px;
            background: linear-gradient(to bottom, #ffffff, #f8f9fa);
            border-left: 3px solid #e74c3c;
            display: flex;
            flex-direction: column;
            overflow: hidden;
            box-shadow: -5px 0 15px rgba(0,0,0,0.05);
        }
        
        .notes-tabs {
            display: flex;
            background: linear-gradient(to right, #2c3e50, #34495e);
            border-bottom: 2px solid #e74c3c;
        }
        
        .tab-btn {
            flex: 1;
            background: none;
            border: none;
            color: #ecf0f1;
            padding: 14px 0;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
        }
        
        .tab-btn::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            width: 0;
            height: 3px;
            background-color: #3498db;
            transition: all 0.3s;
            transform: translateX(-50%);
        }
        
        .tab-btn.active {
            background-color: rgba(52, 152, 219, 0.2);
            color: white;
        }
        
        .tab-btn.active::after {
            width: 80%;
        }
        
        .tab-btn:hover {
            background-color: rgba(52, 152, 219, 0.1);
        }
        
        .tab-content {
            flex: 1;
            padding: 25px;
            overflow-y: auto;
            display: none;
            animation: fadeIn 0.3s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .tab-content.active {
            display: block;
        }
        
        .notes-title {
            color: #2c3e50;
            font-size: 20px;
            font-weight: bold;
            margin-bottom: 20px;
            padding-bottom: 12px;
            border-bottom: 3px solid #e74c3c;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .note-item {
            margin-bottom: 20px;
            padding: 18px;
            background: white;
            border-radius: 8px;
            border-left: 5px solid #3498db;
            box-shadow: 0 3px 10px rgba(0,0,0,0.08);
            transition: transform 0.2s;
        }
        
        .note-item:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .note-item.warning {
            border-left-color: #e74c3c;
            background: linear-gradient(to right, #fff5f5, #ffeaea);
        }
        
        .note-item.important {
            border-left-color: #f39c12;
            background: linear-gradient(to right, #fef9e7, #fef3cd);
        }
        
        .note-item.success {
            border-left-color: #27ae60;
            background: linear-gradient(to right, #eafaf1, #d5f5e3);
        }
        
        .note-title {
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 16px;
        }
        
        .note-content {
            color: #555;
            line-height: 1.7;
            font-size: 14px;
        }
        
        .materials-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            gap: 12px;
            margin-top: 20px;
        }
        
        .material-item {
            padding: 15px;
            background: white;
            border-radius: 6px;
            text-align: center;
            border: 1px solid #ddd;
            transition: all 0.3s;
            cursor: pointer;
        }
        
        .material-item:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            border-color: #3498db;
        }
        
        .material-name {
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 8px;
            font-size: 15px;
        }
        
        .material-spec {
            color: #7f8c8d;
            font-size: 13px;
            line-height: 1.4;
        }
        
        .comparison-controls {
            position: absolute;
            bottom: 25px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(44, 62, 80, 0.95);
            padding: 12px 25px;
            border-radius: 35px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.25);
            z-index: 20;
            display: flex;
            gap: 12px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255,255,255,0.1);
        }
        
        .control-btn {
            background: linear-gradient(to right, #3498db, #2980b9);
            color: white;
            border: none;
            padding: 10px 18px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 14px;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 8px;
            min-width: 120px;
            justify-content: center;
        }
        
        .control-btn:hover {
            background: linear-gradient(to right, #2980b9, #21618c);
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(41, 128, 185, 0.3);
        }
        
        .control-btn.secondary {
            background: linear-gradient(to right, #95a5a6, #7f8c8d);
        }
        
        .control-btn.secondary:hover {
            background: linear-gradient(to right, #7f8c8d, #6c7b7d);
        }
        
        .divider-line {
            position: absolute;
            top: 0;
            bottom: 0;
            left: 50%;
            width: 3px;
            background: linear-gradient(to bottom, #e74c3c, #3498db);
            z-index: 10;
            box-shadow: 0 0 10px rgba(231, 76, 60, 0.3);
        }
        
        .legend {
            position: absolute;
            top: 15px;
            right: 15px;
            background: rgba(255, 255, 255, 0.98);
            padding: 15px 20px;
            border-radius: 8px;
            font-size: 13px;
            box-shadow: 0 3px 15px rgba(0,0,0,0.15);
            border-left: 4px solid #e74c3c;
            max-width: 220px;
            backdrop-filter: blur(5px);
        }
        
        .dimension-display {
            position: absolute;
            bottom: 15px;
            right: 15px;
            background: rgba(44, 62, 80, 0.9);
            color: white;
            padding: 12px 18px;
            border-radius: 6px;
            font-size: 13px;
            font-family: 'Courier New', monospace;
        }
        
        @media (max-width: 1200px) {
            .notes-section {
                min-width: 300px;
            }
            
            .control-btn {
                min-width: 100px;
                padding: 8px 15px;
            }
        }
        
        @media (max-width: 900px) {
            .main-container {
                flex-direction: column;
            }
            
            .notes-section {
                max-width: 100%;
                border-left: none;
                border-top: 3px solid #e74c3c;
            }
            
            .comparison-controls {
                bottom: 15px;
                flex-wrap: wrap;
                justify-content: center;
                max-width: 95%;
            }
        }
    </style>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
</head>
<body>
    <!-- 标题区域 -->
    <div class="header">
        <h1>施工交底协同平台 - 吊顶截面对比分析</h1>
        <p>上传时间：2025年11月31日 | 模型名称：吊顶截面模型</p>
    </div>

    <!-- 主容器 -->
    <div class="main-container">
        <!-- 左侧对比区域 -->
        <div class="comparison-section">
            <div class="comparison-wrapper">
                <!-- 三维模型 -->
                <div class="comparison-item">
                    <div class="item-label">
                        <i class="fas fa-cube"></i> 吊顶截面三维模型
                    </div>
                    <div class="item-content">
                        <div class="model-container">
                            <div class="modelo-wrapper">
                                <iframe src="https://www.modelo.io/embedded/2005168417823895553?viewport=false&autoplay=false&autorotate=false&hideTools=false&showBIM=false&showBBoxSize=false&showKooRender=false&showSettings=false&showFullScreen=true&showLogo=true&showUploadModels=true" 
                                        frameborder="0" 
                                        allowfullscreen
                                        title="吊顶截面三维模型">
                                </iframe>
                            </div>
                        </div>
                    </div>
                </div>
                
                <!-- 施工图纸 -->
                <div class="comparison-item">
                    <div class="item-label">
                        <i class="fas fa-drafting-compass"></i> 吊顶施工详图
                    </div>
                    <div class="item-content">
                        <div class="image-container">
                            <img src="https://image2url.com/r2/bucket1/images/1767664489060-50c09e13-f0d0-4971-bf87-6b490999f517.jpg" 
                                 alt="吊顶截面施工详图" 
                                 title="吊顶截面施工详图">
                        </div>
                    </div>
                </div>
                
                <!-- 分割线 -->
                <div class="divider-line"></div>
                
                <!-- 图例 -->
                <div class="legend">
                    <strong><i class="fas fa-info-circle"></i> 图例说明：</strong><br>
                    • 左侧：吊顶截面三维BIM模型<br>
                    • 右侧：吊顶施工CAD详图<br>
                    • 下方：对比控制工具<br>
                    • 右侧：施工要点与材料信息
                </div>
                
                <!-- 尺寸显示 -->
                <div class="dimension-display">
                    <i class="fas fa-ruler-combined"></i> 参考尺寸：层高2800mm | 吊顶下净高2400mm
                </div>
            </div>
            
            <!-- 对比控制按钮 -->
            <div class="comparison-controls">
                <button class="control-btn" onclick="swapViews()">
                    <i class="fas fa-exchange-alt"></i> 交换位置
                </button>
                <button class="control-btn" onclick="toggleFullScreen(0)">
                    <i class="fas fa-expand"></i> 全屏模型
                </button>
                <button class="control-btn" onclick="toggleFullScreen(1)">
                    <i class="fas fa-expand"></i> 全屏图纸
                </button>
                <button class="control-btn secondary" onclick="showMeasurements()">
                    <i class="fas fa-ruler"></i> 显示尺寸
                </button>
            </div>
        </div>
        
        <!-- 右侧注意事项和材料标注区域 -->
        <div class="notes-section">
            <!-- 选项卡 -->
            <div class="notes-tabs">
                <button class="tab-btn active" onclick="showTab('notes')">
                    <i class="fas fa-exclamation-circle"></i> 施工要点
                </button>
                <button class="tab-btn" onclick="showTab('materials')">
                    <i class="fas fa-clipboard-list"></i> 吊顶材料
                </button>
                <button class="tab-btn" onclick="showTab('install')">
                    <i class="fas fa-tools"></i> 安装规范
                </button>
            </div>
            
            <!-- 施工要点内容 -->
            <div id="notes-tab" class="tab-content active">
                <div class="notes-title">
                    <i class="fas fa-exclamation-triangle"></i> 吊顶施工关键要点
                </div>
                
                <div class="note-item warning">
                    <div class="note-title">
                        <i class="fas fa-arrow-up"></i> 标高控制
                    </div>
                    <div class="note-content">
                        1. 吊顶完成面标高必须准确（设计标高±2mm）<br>
                        2. 周边标高线必须水平，误差≤3mm<br>
                        3. 灯具孔位提前定位，避免与龙骨冲突<br>
                        4. 考虑设备管线高度，预留足够空间
                    </div>
                </div>
                
                <div class="note-item important">
                    <div class="note-title">
                        <i class="fas fa-layer-group"></i> 龙骨安装
                    </div>
                    <div class="note-content">
                        1. 主龙骨间距≤1200mm，副龙骨间距≤400mm<br>
                        2. 吊杆间距≤1200mm，距墙≤300mm<br>
                        3. 边龙骨必须固定牢固，使用膨胀螺栓<br>
                        4. 龙骨必须调平，平整度≤2mm/2m
                    </div>
                </div>
                
                <div class="note-item success">
                    <div class="note-title">
                        <i class="fas fa-th"></i> 板材安装
                    </div>
                    <div class="note-content">
                        1. 石膏板长边必须与副龙骨垂直<br>
                        2. 板缝必须错开，错缝距离≥300mm<br>
                        3. 自攻螺丝间距：边部≤200mm，中部≤300mm<br>
                        4. 螺丝陷入板面0.5-1mm，不得破坏纸面
                    </div>
                </div>
                
                <div class="note-item">
                    <div class="note-title">
                        <i class="fas fa-compress-arrows-alt"></i> 伸缩缝处理
                    </div>
                    <div class="note-content">
                        1. 大面积吊顶必须设置伸缩缝（间距≤12m）<br>
                        2. 伸缩缝宽度20-30mm，深度贯通<br>
                        3. 采用专用伸缩缝材料填充<br>
                        4. 转角处必须做L型整板，避免裂缝
                    </div>
                </div>
            </div>
            
            <!-- 吊顶材料内容 -->
            <div id="materials-tab" class="tab-content">
                <div class="notes-title">
                    <i class="fas fa-boxes"></i> 吊顶材料清单
                </div>
                
                <div class="materials-grid">
                    <div class="material-item">
                        <div class="material-name">轻钢龙骨</div>
                        <div class="material-spec">主龙骨38×12<br>副龙骨50×19<br>边龙骨50×20</div>
                    </div>
                    <div class="material-item">
                        <div class="material-name">石膏板</div>
                        <div class="material-spec">9.5mm/12mm厚<br>防火/防潮型<br>1200×2400mm</div>
                    </div>
                    <div class="material-item">
                        <div class="material-name">吊杆</div>
                        <div class="material-spec">Φ8全牙吊杆<br>L=按需<br>配套螺母垫片</div>
                    </div>
                    <div class="material-item">
                        <div class="material-name">自攻螺丝</div>
                        <div class="material-spec">黑色磷化<br>25mm/35mm<br>十字槽沉头</div>
                    </div>
                    <div class="material-item">
                        <div class="material-name">膨胀螺栓</div>
                        <div class="material-spec">M8/M10<br>长度80-100mm<br>重型</div>
                    </div>
                    <div class="material-item">
                        <div class="material-name">接缝材料</div>
                        <div class="material-spec">嵌缝石膏<br>接缝纸带<br>网格带</div>
                    </div>
                </div>
                
                <div class="note-item" style="margin-top: 25px;">
                    <div class="note-title">
                        <i class="fas fa-clipboard-check"></i> 材料验收标准
                    </div>
                    <div class="note-content">
                        • 龙骨：镀锌量≥120g/m²，厚度达标<br>
                        • 石膏板：品牌认证，无破损变形<br>
                        • 吊杆：丝牙完整，无锈蚀<br>
                        • 所有材料需有合格证、检测报告<br>
                        • 防火材料需有防火等级证明
                    </div>
                </div>
            </div>
            
            <!-- 安装规范内容 -->
            <div id="install-tab" class="tab-content">
                <div class="notes-title">
                    <i class="fas fa-cogs"></i> 安装技术规范
                </div>
                
                <div class="note-item">
                    <div class="note-title">
                        <i class="fas fa-ruler"></i> 尺寸要求
                    </div>
                    <div class="note-content">
                        <strong>吊顶下净高：</strong>≥2400mm（主要空间）<br>
                        <strong>主龙骨间距：</strong>900-1200mm<br>
                        <strong>副龙骨间距：</strong>300-400mm<br>
                        <strong>吊杆间距：</strong>≤1200mm<br>
                        <strong>距墙距离：</strong>≤300mm
                    </div>
                </div>
                
                <div class="note-item">
                    <div class="note-title">
                        <i class="fas fa-bolt"></i> 电气配合
                    </div>
                    <div class="note-content">
                        <strong>灯具开孔：</strong>提前定位，避开龙骨<br>
                        <strong>线管敷设：</strong>固定牢固，不干扰吊顶<br>
                        <strong>检修口：</strong>600×600mm，位置合理<br>
                        <strong>消防设施：</strong>烟感、喷淋按规范安装<br>
                        <strong>通风设备：</strong>预留风口，协调安装
                    </div>
                </div>
                
                <div class="note-item">
                    <div class="note-title">
                        <i class="fas fa-check-double"></i> 质量验收
                    </div>
                    <div class="note-content">
                        <strong>平整度：</strong>≤2mm/2m<br>
                        <strong>接缝：</strong>平直均匀，宽度3-5mm<br>
                        <strong>牢固度：</strong>无松动、下坠<br>
                        <strong>观感：</strong>无裂缝、起泡、污染<br>
                        <strong>完成面：</strong>洁净无破损
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // 显示对应的选项卡
        function showTab(tabName) {
            // 隐藏所有选项卡内容
            document.querySelectorAll('.tab-content').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // 移除所有选项卡按钮的活动状态
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // 显示选中的选项卡内容
            document.getElementById(tabName + '-tab').classList.add('active');
            
            // 设置选中的选项卡按钮为活动状态
            event.currentTarget.classList.add('active');
        }
        
        // 交换左右视图位置
        function swapViews() {
            const container = document.querySelector('.comparison-wrapper');
            const items = document.querySelectorAll('.comparison-item');
            
            if (items.length >= 2) {
                container.insertBefore(items[1], items[0]);
                
                // 更新图例文字
                const legend = document.querySelector('.legend');
                if (legend.innerHTML.includes('左侧：吊顶截面三维BIM模型')) {
                    legend.innerHTML = legend.innerHTML
                        .replace('左侧：吊顶截面三维BIM模型', '左侧：吊顶施工CAD详图')
                        .replace('右侧：吊顶施工CAD详图', '右侧：吊顶截面三维BIM模型');
                } else {
                    legend.innerHTML = legend.innerHTML
                        .replace('左侧：吊顶施工CAD详图', '左侧：吊顶截面三维BIM模型')
                        .replace('右侧：吊顶截面三维BIM模型', '右侧：吊顶施工CAD详图');
                }
            }
        }
        
        // 全屏查看功能
        function toggleFullScreen(itemIndex) {
            const items = document.querySelectorAll('.comparison-item');
            if (itemIndex >= items.length) return;
            
            const item = items[itemIndex];
            
            if (!document.fullscreenElement) {
                if (item.requestFullscreen) {
                    item.requestFullscreen();
                } else if (item.webkitRequestFullscreen) {
                    item.webkitRequestFullscreen();
                } else if (item.msRequestFullscreen) {
                    item.msRequestFullscreen();
                }
            } else {
                if (document.exitFullscreen) {
                    document.exitFullscreen();
                } else if (document.webkitExitFullscreen) {
                    document.webkitExitFullscreen();
                } else if (document.msExitFullscreen) {
                    document.msExitFullscreen();
                }
            }
        }
        
        // 显示尺寸测量功能
        function showMeasurements() {
            const dimensionDisplay = document.querySelector('.dimension-display');
            if (dimensionDisplay.style.display === 'none') {
                dimensionDisplay.style.display = 'block';
                alert('尺寸显示已开启\n层高：2800mm\n吊顶下净高：2400mm\n吊顶厚度：150mm');
            } else {
                dimensionDisplay.style.display = 'none';
            }
        }
        
        // 初始化显示尺寸
        window.addEventListener('load', function() {
            // 设置初始尺寸显示
            const dimensionDisplay = document.querySelector('.dimension-display');
            dimensionDisplay.innerHTML = `<i class="fas fa-ruler-combined"></i> 参考尺寸：层高2800mm | 吊顶下净高2400mm`;
            
            // 添加点击事件显示详细尺寸
            dimensionDisplay.addEventListener('click', function() {
                alert('详细尺寸信息：\n\n' +
                      '1. 建筑层高：2800mm\n' +
                      '2. 吊顶下净高：2400mm\n' +
                      '3. 吊顶结构厚度：150mm\n' +
                      '4. 主龙骨高度：38mm\n' +
                      '5. 副龙骨高度：50mm\n' +
                      '6. 石膏板厚度：12mm');
            });
            
            console.log('吊顶截面对比分析系统加载完成');
            console.log('三维模型：吊顶截面模型');
            console.log('施工图纸：吊顶施工详图');
            console.log('上传时间：2025年11月31日');
        });
        
        // 监听全屏变化
        document.addEventListener('fullscreenchange', handleFullScreenChange);
        document.addEventListener('webkitfullscreenchange', handleFullScreenChange);
        document.addEventListener('msfullscreenchange', handleFullScreenChange);
        
        function handleFullScreenChange() {
            const isFullScreen = document.fullscreenElement || 
                                document.webkitFullscreenElement || 
                                document.msFullscreenElement;
            
            if (isFullScreen) {
                document.body.style.overflow = 'hidden';
            } else {
                document.body.style.overflow = '';
            }
        }
    </script>
</body>
</html>
