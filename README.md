<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>스마트 신발 시스템 대시보드</title>
    <style>
        :root {
            --primary: #3498db;
            --secondary: #2ecc71;
            --dark: #2c3e50;
            --light: #ecf0f1;
            --danger: #e74c3c;
            --warning: #f39c12;
            --info: #1abc9c;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f7fa;
            color: #333;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 0;
            border-bottom: 1px solid #ddd;
            margin-bottom: 2rem;
        }
        
        .logo {
            display: flex;
            align-items: center;
        }
        
        .logo img {
            width: 40px;
            margin-right: 10px;
        }
        
        .logo h1 {
            font-size: 1.5rem;
            color: var(--dark);
        }
        
        nav ul {
            display: flex;
            list-style: none;
        }
        
        nav ul li {
            margin-left: 20px;
        }
        
        nav ul li a {
            text-decoration: none;
            color: var(--dark);
            font-weight: 500;
            transition: color 0.3s;
        }
        
        nav ul li a:hover {
            color: var(--primary);
        }
        
        .user-info {
            display: flex;
            align-items: center;
        }
        
        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background-color: var(--primary);
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;
            font-weight: bold;
            margin-right: 10px;
        }
        
        .dashboard {
            display: grid;
            grid-template-columns: repeat(12, 1fr);
            gap: 20px;
        }
        
        .card {
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
            padding: 20px;
            transition: transform 0.3s, box-shadow 0.3s;
        }
        
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }
        
        .card-title {
            font-size: 1.1rem;
            font-weight: 600;
            color: var(--dark);
        }
        
        .overview {
            grid-column: span 12;
        }
        
        .stats-container {
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 15px;
        }
        
        .stat-card {
            flex: 1;
            min-width: 200px;
            padding: 15px;
            border-radius: 8px;
            display: flex;
            flex-direction: column;
            color: white;
        }
        
        .stat-card.steps {
            background: linear-gradient(135deg, #3498db, #2980b9);
        }
        
        .stat-card.distance {
            background: linear-gradient(135deg, #2ecc71, #27ae60);
        }
        
        .stat-card.calories {
            background: linear-gradient(135deg, #e74c3c, #c0392b);
        }
        
        .stat-card.time {
            background: linear-gradient(135deg, #f39c12, #d35400);
        }
        
        .stat-label {
            font-size: 0.9rem;
            opacity: 0.9;
        }
        
        .stat-value {
            font-size: 1.8rem;
            font-weight: bold;
            margin: 5px 0;
        }
        
        .stat-subtext {
            font-size: 0.8rem;
            opacity: 0.8;
        }
        
        .walking-data {
            grid-column: span 8;
        }
        
        .shoe-control {
            grid-column: span 4;
        }
        
        .gps-tracking {
            grid-column: span 8;
            height: 400px;
        }
        
        .heel-control {
            grid-column: span 4;
        }
        
        .battery-status {
            grid-column: span 4;
        }
        
        .system-status {
            grid-column: span 8;
        }
        
        .chart-container {
            height: 250px;
            position: relative;
        }
        
        #map {
            height: 350px;
            width: 100%;
            border-radius: 8px;
        }
        
        .control-group {
            margin-bottom: 20px;
        }
        
        .control-label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
        }
        
        .slider-container {
            display: flex;
            align-items: center;
        }
        
        .slider {
            flex: 1;
            height: 5px;
            border-radius: 5px;
            background: #ddd;
            outline: none;
            -webkit-appearance: none;
        }
        
        .slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background: var(--primary);
            cursor: pointer;
        }
        
        .slider-value {
            width: 40px;
            text-align: center;
            margin-left: 10px;
        }
        
        .toggle-switch {
            position: relative;
            display: inline-block;
            width: 60px;
            height: 34px;
        }
        
        .toggle-switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }
        
        .toggle-slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: #ccc;
            transition: .4s;
            border-radius: 34px;
        }
        
        .toggle-slider:before {
            position: absolute;
            content: "";
            height: 26px;
            width: 26px;
            left: 4px;
            bottom: 4px;
            background-color: white;
            transition: .4s;
            border-radius: 50%;
        }
        
        input:checked + .toggle-slider {
            background-color: var(--primary);
        }
        
        input:checked + .toggle-slider:before {
            transform: translateX(26px);
        }
        
        .toggle-label {
            margin-left: 10px;
        }
        
        .battery-indicator {
            height: 100px;
            width: 50px;
            border: 3px solid #333;
            border-radius: 5px;
            position: relative;
            margin: 30px auto;
        }
        
        .battery-level {
            position: absolute;
            bottom: 0;
            width: 100%;
            background-color: var(--primary);
            transition: height 0.5s;
        }
        
        .battery-cap {
            position: absolute;
            height: 10px;
            width: 20px;
            background: #333;
            top: -10px;
            left: 50%;
            transform: translateX(-50%);
            border-radius: 5px 5px 0 0;
        }
        
        .battery-percentage {
            text-align: center;
            font-size: 1.5rem;
            font-weight: bold;
            margin-top: 10px;
        }
        
        .status-circle {
            display: inline-block;
            width: 12px;
            height: 12px;
            border-radius: 50%;
            margin-right: 8px;
        }
        
        .status-active {
            background-color: var(--secondary);
        }
        
        .status-inactive {
            background-color: var(--danger);
        }
        
        .status-warning {
            background-color: var(--warning);
        }
        
        .status-item {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .status-text {
            flex: 1;
        }
        
        .status-value {
            font-weight: 500;
        }
        
        .btn {
            padding: 8px 16px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: 500;
            transition: background-color 0.3s;
        }
        
        .btn-primary {
            background-color: var(--primary);
            color: white;
        }
        
        .btn-primary:hover {
            background-color: #2980b9;
        }
        
        .btn-secondary {
            background-color: var(--secondary);
            color: white;
        }
        
        .btn-secondary:hover {
            background-color: #27ae60;
        }
        
        .btn-danger {
            background-color: var(--danger);
            color: white;
        }
        
        .btn-danger:hover {
            background-color: #c0392b;
        }
        
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
        }
        
        .modal-content {
            background-color: white;
            margin: 10% auto;
            padding: 20px;
            border-radius: 8px;
            width: 80%;
            max-width: 500px;
        }
        
        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
        }
        
        .close:hover {
            color: black;
        }
        
        @media (max-width: 768px) {
            .dashboard {
                grid-template-columns: repeat(1, 1fr);
            }
            
            .walking-data, .shoe-control, .gps-tracking, .heel-control, .battery-status, .system-status {
                grid-column: span 1;
            }
            
            nav {
                display: none;
            }
            
            .stats-container {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="logo">
                <img src="/api/placeholder/40/40" alt="스마트 신발 로고">
                <h1>스마트 신발 대시보드</h1>
            </div>
            <nav>
                <ul>
                    <li><a href="#" class="active">대시보드</a></li>
                    <li><a href="#">통계</a></li>
                    <li><a href="#">설정</a></li>
                    <li><a href="#">도움말</a></li>
                </ul>
            </nav>
            <div class="user-info">
                <div class="user-avatar">U</div>
                <span>사용자</span>
            </div>
        </header>
        
        <main class="dashboard">
            <section class="card overview">
                <div class="card-header">
                    <h2 class="card-title">오늘의 활동 정보</h2>
                    <span id="current-date">2025년 4월 9일</span>
                </div>
                <div class="stats-container">
                    <div class="stat-card steps">
                        <span class="stat-label">걸음 수</span>
                        <span class="stat-value" id="step-count">7,428</span>
                        <span class="stat-subtext">목표의 74%</span>
                    </div>
                    <div class="stat-card distance">
                        <span class="stat-label">이동 거리</span>
                        <span class="stat-value" id="distance">5.2 km</span>
                        <span class="stat-subtext">어제보다 1.3km 증가</span>
                    </div>
                    <div class="stat-card calories">
                        <span class="stat-label">소모 칼로리</span>
                        <span class="stat-value" id="calories">342 kcal</span>
                        <span class="stat-subtext">목표의 45%</span>
                    </div>
                    <div class="stat-card time">
                        <span class="stat-label">활동 시간</span>
                        <span class="stat-value" id="active-time">1h 12m</span>
                        <span class="stat-subtext">평균보다 25분 증가</span>
                    </div>
                </div>
            </section>
            
            <section class="card walking-data">
                <div class="card-header">
                    <h2 class="card-title">보폭 분석</h2>
                    <button class="btn btn-primary" id="refresh-data">새로고침</button>
                </div>
                <div class="chart-container">
                    <canvas id="stride-chart"></canvas>
                </div>
            </section>
            
            <section class="card shoe-control">
                <div class="card-header">
                    <h2 class="card-title">신발 제어</h2>
                    <div class="status-circle status-active"></div>
                </div>
                <div class="control-group">
                    <label class="control-label">자동 높이 조절</label>
                    <div style="display: flex; align-items: center;">
                        <label class="toggle-switch">
                            <input type="checkbox" id="auto-height-toggle" checked>
                            <span class="toggle-slider"></span>
                        </label>
                        <span class="toggle-label">활성화됨</span>
                    </div>
                </div>
                <div class="control-group">
                    <label class="control-label">왼쪽 굽 높이 (mm)</label>
                    <div class="slider-container">
                        <input type="range" min="0" max="30" value="15" class="slider" id="left-heel-slider">
                        <span class="slider-value" id="left-heel-value">15</span>
                    </div>
                </div>
                <div class="control-group">
                    <label class="control-label">오른쪽 굽 높이 (mm)</label>
                    <div class="slider-container">
                        <input type="range" min="0" max="30" value="15" class="slider" id="right-heel-slider">
                        <span class="slider-value" id="right-heel-value">15</span>
                    </div>
                </div>
                <button class="btn btn-secondary" style="width: 100%;">설정 적용</button>
            </section>
            
            <section class="card gps-tracking">
                <div class="card-header">
                    <h2 class="card-title">실시간 위치 추적</h2>
                    <div>
                        <span id="gps-status"><span class="status-circle status-active"></span> 신호 양호</span>
                    </div>
                </div>
                <div id="map"></div>
                <div style="margin-top: 15px; display: flex; justify-content: space-between;">
                    <div>
                        <strong>현재 속도:</strong> <span id="current-speed">4.2 km/h</span>
                    </div>
                    <div>
                        <strong>예상 도착 시간:</strong> <span id="eta">17:45</span>
                    </div>
                </div>
            </section>
            
            <section class="card heel-control">
                <div class="card-header">
                    <h2 class="card-title">굽 조절 모드</h2>
                </div>
                <div style="display: flex; flex-direction: column; gap: 10px;">
                    <button class="btn btn-primary" style="width: 100%;">편안함 모드</button>
                    <button class="btn btn-secondary" style="width: 100%;">스포츠 모드</button>
                    <button class="btn btn-danger" style="width: 100%;">자세 교정 모드</button>
                </div>
                <div style="margin-top: 20px;">
                    <label class="control-label">지형 적응 민감도</label>
                    <div class="slider-container">
                        <input type="range" min="0" max="100" value="70" class="slider" id="sensitivity-slider">
                        <span class="slider-value" id="sensitivity-value">70%</span>
                    </div>
                </div>
                <div style="margin-top: 20px;">
                    <label class="control-label">반응 속도</label>
                    <div class="slider-container">
                        <input type="range" min="0" max="100" value="50" class="slider" id="response-slider">
                        <span class="slider-value" id="response-value">50%</span>
                    </div>
                </div>
            </section>
            
            <section class="card battery-status">
                <div class="card-header">
                    <h2 class="card-title">배터리 상태</h2>
                </div>
                <div class="battery-indicator">
                    <div class="battery-cap"></div>
                    <div class="battery-level" style="height: 65%;"></div>
                </div>
                <div class="battery-percentage">65%</div>
                <div style="text-align: center; margin-top: 10px;">
                    <span>남은 시간: 약 4시간 30분</span>
                </div>
                <div style="margin-top: 20px;">
                    <div class="status-item">
                        <div class="status-text">절전 모드</div>
                        <label class="toggle-switch">
                            <input type="checkbox" id="power-save-toggle">
                            <span class="toggle-slider"></span>
                        </label>
                    </div>
                </div>
            </section>
            
            <section class="card system-status">
                <div class="card-header">
                    <h2 class="card-title">시스템 상태</h2>
                    <button class="btn btn-primary" id="system-check-btn">상태 점검</button>
                </div>
                <div style="margin-top: 10px;">
                    <div class="status-item">
                        <span class="status-circle status-active"></span>
                        <div class="status-text">Raspberry Pi Zero 2 W</div>
                        <div class="status-value">온라인</div>
                    </div>
                    <div class="status-item">
                        <span class="status-circle status-active"></span>
                        <div class="status-text">MPU-6050 센서</div>
                        <div class="status-value">정상 작동 중</div>
                    </div>
                    <div class="status-item">
                        <span class="status-circle status-active"></span>
                        <div class="status-text">GPS 모듈 (NEO-6M)</div>
                        <div class="status-value">신호 양호</div>
                    </div>
                    <div class="status-item">
                        <span class="status-circle status-warning"></span>
                        <div class="status-text">리니어 액추에이터 (왼쪽)</div>
                        <div class="status-value">주의 필요</div>
                    </div>
                    <div class="status-item">
                        <span class="status-circle status-active"></span>
                        <div class="status-text">리니어 액추에이터 (오른쪽)</div>
                        <div class="status-value">정상 작동 중</div>
                    </div>
                    <div class="status-item">
                        <span class="status-circle status-active"></span>
                        <div class="status-text">모터 드라이버</div>
                        <div class="status-value">정상 작동 중</div>
                    </div>
                    <div class="status-item">
                        <span class="status-circle status-active"></span>
                        <div class="status-text">인터넷 연결</div>
                        <div class="status-value">연결됨</div>
                    </div>
                </div>
                <div style="margin-top: 20px; display: flex; justify-content: space-between;">
                    <button class="btn btn-secondary" id="update-firmware-btn">펌웨어 업데이트</button>
                    <button class="btn btn-danger" id="reset-system-btn">시스템 초기화</button>
                </div>
            </section>
        </main>
    </div>
    
    <div id="system-modal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2>시스템 진단 결과</h2>
            <p style="margin: 20px 0;">모든 시스템이 정상적으로 작동 중입니다. 다음 문제가 발견되었습니다:</p>
            <ul style="margin-left: 20px; margin-bottom: 20px;">
                <li>왼쪽 리니어 액추에이터의 반응 속도가 약간 느립니다. 점검이 필요할 수 있습니다.</li>
            </ul>
            <button class="btn btn-primary" style="width: 100%;">자세한 보고서 보기</button>
        </div>
    </div>
    
    <script src="https://maps.googleapis.com/maps/api/js?key=AIzaSyDUTPxDi7pFFMyJaN3GR_iX0Y85vJG0ciE&callback=initMap" async defer></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>

    <!-- 실시간 추적 버튼 추가 -->
<button id="toggle-tracking-btn" style="margin: 10px;">실시간 위치 추적 시작</button>

<script>
    // 현재 날짜 표시
    document.getElementById('current-date').textContent = new Date().toLocaleDateString('ko-KR', {
        year: 'numeric',
        month: 'long',
        day: 'numeric'
    });

    // 보폭 차트 생성
    const strideChart = new Chart(document.getElementById('stride-chart'), {
        type: 'line',
        data: {
            labels: ['08:00', '09:00', '10:00', '11:00', '12:00', '13:00', '14:00', '15:00'],
            datasets: [
                {
                    label: '보폭 길이 (cm)',
                    backgroundColor: 'rgba(52, 152, 219, 0.2)',
                    borderColor: 'rgba(52, 152, 219, 1)',
                    data: [65, 68, 70, 72, 68, 65, 67, 69],
                    tension: 0.4
                },
                {
                    label: '보행 속도 (km/h)',
                    backgroundColor: 'rgba(46, 204, 113, 0.2)',
                    borderColor: 'rgba(46, 204, 113, 1)',
                    data: [3.8, 4.2, 4.5, 4.8, 4.3, 3.9, 4.1, 4.2],
                    tension: 0.4
                }
            ]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
                legend: { position: 'top' },
                tooltip: { mode: 'index', intersect: false }
            },
            scales: {
                y: {
                    beginAtZero: false,
                    ticks: {
                        callback: function(value) { return value; }
                    }
                }
            }
        }
    });

    // Google Maps 초기화
    let map;
    let marker;
    let path;
    let trackingMode = false;

    function initMap() {
    const defaultLocation = { lat: 37.5665, lng: 126.9780 }; // fallback 위치

    map = new google.maps.Map(document.getElementById("map"), {
        zoom: 15,
        center: defaultLocation,
        mapTypeId: google.maps.MapTypeId.ROADMAP,
        streetViewControl: false,
        zoomControl: true,
        mapTypeControl: false
    });

    // 임시 마커 (초기 위치는 defaultLocation)
    marker = new google.maps.Marker({
        position: defaultLocation,
        map: map,
        title: "현재 위치",
        icon: {
            path: google.maps.SymbolPath.CIRCLE,
            scale: 10,
            fillColor: "#3498db",
            fillOpacity: 1,
            strokeColor: "#ffffff",
            strokeWeight: 2,
        }
    });

    // 실제 현재 위치 반영
    if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(
            (position) => {
                const currentPos = {
                    lat: position.coords.latitude,
                    lng: position.coords.longitude
                };
                map.setCenter(currentPos);
                marker.setPosition(currentPos);
            },
            () => {
                console.warn("⚠️ 위치 권한이 거부되었거나 위치를 가져올 수 없습니다.");
            }
        );
    }

    // 경로 라인 (가상 경로)
    const routeCoordinates = [
        { lat: 37.5665, lng: 126.9780 },
        { lat: 37.5668, lng: 126.9785 },
        { lat: 37.5672, lng: 126.9790 },
        { lat: 37.5678, lng: 126.9795 },
        { lat: 37.5683, lng: 126.9800 },
        { lat: 37.5688, lng: 126.9805 }
    ];

    path = new google.maps.Polyline({
        path: routeCoordinates,
        geodesic: true,
        strokeColor: "#3498db",
        strokeOpacity: 1.0,
        strokeWeight: 4
    });
    path.setMap(map);

    // 목적지 마커
    const destination = new google.maps.Marker({
        position: { lat: 37.5700, lng: 126.9820 },
        map: map,
        title: "목적지",
        icon: {
            url: "https://maps.google.com/mapfiles/ms/icons/red-dot.png"
        }
    });

    // 정보창
    const infoWindow = new google.maps.InfoWindow({ content: "현재 위치" });
    marker.addListener("click", () => {
        infoWindow.open(map, marker);
    });

    

    // 실시간 추적 버튼 이벤트
    document.getElementById('toggle-tracking-btn').addEventListener('click', () => {
        trackingMode = !trackingMode;
        if (trackingMode) {
            startTracking();
            alert("실시간 위치 추적이 시작되었습니다.");
        } else {
            alert("실시간 위치 추적이 중단되었습니다. (중단하려면 새로고침하세요)");
        }
    });
}


    function simulateMovement(coordinates) {
        let currentIndex = 0;
        setInterval(() => {
            if (!trackingMode && currentIndex < coordinates.length - 1) {
                currentIndex++;
                marker.setPosition(coordinates[currentIndex]);
                map.panTo(coordinates[currentIndex]);
                updateMovementData();
            }
        }, 5000);
    }

    function startTracking() {
    if (navigator.geolocation) {
        navigator.geolocation.watchPosition(
            (position) => {
                const pos = {
                    lat: position.coords.latitude,
                    lng: position.coords.longitude
                };
                marker.setPosition(pos);
                map.panTo(pos);
                updateMovementData();

                // ✅ 정확도 표시 (단위: 미터)
                const accuracy = position.coords.accuracy;
                document.getElementById('accuracy').textContent = `정확도: ±${Math.round(accuracy)} m`;
            },
            (error) => {
                console.error("실시간 위치 추적 실패:", error);
                alert("위치 추적에 실패했습니다.");
            },
            {
                enableHighAccuracy: true,
                maximumAge: 0,
                timeout: 10000
            }
        );
    } else {
        alert("이 브라우저는 위치 정보를 지원하지 않습니다.");
    }
}

    function updateMovementData() {
        const newSpeed = (4 + Math.random()).toFixed(1);
        document.getElementById('current-speed').textContent = `${newSpeed} km/h`;

        const now = new Date();
        const etaMinutes = 15 + Math.floor(Math.random() * 10);
        now.setMinutes(now.getMinutes() + etaMinutes);
        document.getElementById('eta').textContent = now.toLocaleTimeString('ko-KR', {
            hour: '2-digit',
            minute: '2-digit',
            hour12: false
        });
    }


        
        // 슬라이더 이벤트 핸들러
        document.getElementById('left-heel-slider').addEventListener('input', function() {
            document.getElementById('left-heel-value').textContent = this.value;
        });
        document.getElementById('right-heel-slider').addEventListener('input', function() {
            document.getElementById('right-heel-value').textContent = this.value;
        });
        
        document.getElementById('sensitivity-slider').addEventListener('input', function() {
            document.getElementById('sensitivity-value').textContent = this.value + '%';
        });
        
        document.getElementById('response-slider').addEventListener('input', function() {
            document.getElementById('response-value').textContent = this.value + '%';
        });
        
        // 모달 관련 스크립트
        const modal = document.getElementById('system-modal');
        const btn = document.getElementById('system-check-btn');
        const span = document.getElementsByClassName('close')[0];
        
        btn.onclick = function() {
            modal.style.display = 'block';
        }
        
        span.onclick = function() {
            modal.style.display = 'none';
        }
        
        window.onclick = function(event) {
            if (event.target == modal) {
                modal.style.display = 'none';
            }
        }
        
        // 데이터 자동 업데이트 시뮬레이션
        function updateData() {
            // 걸음 수 업데이트
            const stepCount = document.getElementById('step-count');
            let currentSteps = parseInt(stepCount.textContent.replace(',', ''));
            currentSteps += Math.floor(Math.random() * 10);
            stepCount.textContent = currentSteps.toLocaleString();
            
            // 거리 업데이트
            const distance = document.getElementById('distance');
            let currentDistance = parseFloat(distance.textContent);
            currentDistance += parseFloat((Math.random() * 0.01).toFixed(2));
            distance.textContent = currentDistance.toFixed(1) + ' km';
            
            // 칼로리 업데이트
            const calories = document.getElementById('calories');
            let currentCalories = parseInt(calories.textContent);
            currentCalories += Math.floor(Math.random() * 3);
            calories.textContent = currentCalories + ' kcal';
            
            // 활동 시간 업데이트
            const activeTime = document.getElementById('active-time');
            let [hours, minutes] = activeTime.textContent.split('h ');
            hours = parseInt(hours);
            minutes = parseInt(minutes);
            minutes += 1;
            if (minutes >= 60) {
                hours += 1;
                minutes -= 60;
            }
            activeTime.textContent = hours + 'h ' + minutes + 'm';
        }
        
        // 배터리 상태 업데이트
        function updateBatteryStatus() {
            const batteryLevel = document.querySelector('.battery-level');
            const batteryPercentage = document.querySelector('.battery-percentage');
            let currentPercentage = parseInt(batteryPercentage.textContent);
            
            // 5분마다 1% 감소 시뮬레이션
            setInterval(() => {
                if (currentPercentage > 0) {
                    currentPercentage -= 1;
                    batteryPercentage.textContent = currentPercentage + '%';
                    batteryLevel.style.height = currentPercentage + '%';
                    
                    // 배터리 잔량에 따른 색상 변경
                    if (currentPercentage < 20) {
                        batteryLevel.style.backgroundColor = 'var(--danger)';
                    } else if (currentPercentage < 50) {
                        batteryLevel.style.backgroundColor = 'var(--warning)';
                    }
                    
                    // 남은 시간 업데이트
                    const remainingTime = document.querySelector('.battery-status div:nth-child(4) span');
                    const hours = Math.floor((currentPercentage / 100) * 7);
                    const minutes = Math.floor(((currentPercentage / 100) * 7 - hours) * 60);
                    remainingTime.textContent = `남은 시간: 약 ${hours}시간 ${minutes}분`;
                }
            }, 30000); // 실제론 30초마다 업데이트 (데모 목적)
        }
        
        // 자동 높이 조절 토글 이벤트
        document.getElementById('auto-height-toggle').addEventListener('change', function() {
            const leftHeelSlider = document.getElementById('left-heel-slider');
            const rightHeelSlider = document.getElementById('right-heel-slider');
            const toggleLabel = this.parentNode.nextElementSibling;
            
            if (this.checked) {
                toggleLabel.textContent = '활성화됨';
                leftHeelSlider.disabled = true;
                rightHeelSlider.disabled = true;
                // 자동 모드에서는 시스템이 최적의 높이를 계산
                setTimeout(() => {
                    leftHeelSlider.value = 18;
                    rightHeelSlider.value = 18;
                    document.getElementById('left-heel-value').textContent = '18';
                    document.getElementById('right-heel-value').textContent = '18';
                }, 1000);
            } else {
                toggleLabel.textContent = '비활성화됨';
                leftHeelSlider.disabled = false;
                rightHeelSlider.disabled = false;
            }
        });
        
        // 절전 모드 토글 이벤트
        document.getElementById('power-save-toggle').addEventListener('change', function() {
            if (this.checked) {
                // 절전 모드 활성화 로직
                document.querySelector('.battery-percentage').style.color = 'var(--secondary)';
                // 배터리 소모 속도 감소 시뮬레이션
            } else {
                // 절전 모드 비활성화 로직
                document.querySelector('.battery-percentage').style.color = '';
            }
        });
        
        // 굽 조절 모드 버튼 이벤트
        const modeButtons = document.querySelectorAll('.heel-control button');
        modeButtons.forEach(button => {
            button.addEventListener('click', function() {
                // 이전에 선택된 버튼의 강조 표시 제거
                modeButtons.forEach(btn => btn.style.opacity = '1');
                
                // 현재 버튼 강조 표시
                this.style.opacity = '0.8';
                
                // 선택된 모드에 따른 설정 변경
                const mode = this.textContent;
                const sensitivitySlider = document.getElementById('sensitivity-slider');
                const responseSlider = document.getElementById('response-slider');
                
                switch(mode) {
                    case '편안함 모드':
                        sensitivitySlider.value = 70;
                        responseSlider.value = 30;
                        break;
                    case '스포츠 모드':
                        sensitivitySlider.value = 90;
                        responseSlider.value = 80;
                        break;
                    case '자세 교정 모드':
                        sensitivitySlider.value = 50;
                        responseSlider.value = 60;
                        break;
                }
                
                // 화면에 표시되는 값 업데이트
                document.getElementById('sensitivity-value').textContent = sensitivitySlider.value + '%';
                document.getElementById('response-value').textContent = responseSlider.value + '%';
            });
        });
        
        // 시스템 초기화 버튼 이벤트
        document.getElementById('reset-system-btn').addEventListener('click', function() {
            if (confirm('정말로 시스템을 초기화하시겠습니까? 모든 설정이 기본값으로 돌아갑니다.')) {
                // 초기화 애니메이션 및 로직
                const statusItems = document.querySelectorAll('.status-item .status-value');
                statusItems.forEach(item => {
                    item.textContent = '초기화 중...';
                });
                
                setTimeout(() => {
                    statusItems.forEach(item => {
                        item.textContent = '정상 작동 중';
                    });
                    alert('시스템이 성공적으로 초기화되었습니다.');
                }, 3000);
            }
        });
        
        // 펌웨어 업데이트 버튼 이벤트
        document.getElementById('update-firmware-btn').addEventListener('click', function() {
            // 펌웨어 업데이트 모달 또는 알림
            const updateProgress = document.createElement('div');
            updateProgress.style.width = '100%';
            updateProgress.style.height = '20px';
            updateProgress.style.backgroundColor = '#f1f1f1';
            updateProgress.style.borderRadius = '5px';
            updateProgress.style.margin = '10px 0';
            updateProgress.style.overflow = 'hidden';
            updateProgress.innerHTML = '<div style="width: 0%; height: 100%; background-color: var(--primary); transition: width 3s linear;"></div>';
            
            this.parentNode.insertBefore(updateProgress, this);
            this.disabled = true;
            this.textContent = '업데이트 중...';
            
            // 프로그레스 바 애니메이션
            setTimeout(() => {
                updateProgress.querySelector('div').style.width = '100%';
            }, 100);
            
            // 업데이트 완료 시뮬레이션
            setTimeout(() => {
                this.disabled = false;
                this.textContent = '펌웨어 업데이트';
                updateProgress.remove();
                alert('펌웨어가 성공적으로 업데이트되었습니다.');
            }, 3500);
        });
        
        // 새로고침 버튼 이벤트
        document.getElementById('refresh-data').addEventListener('click', function() {
            // 데이터 새로고침 애니메이션
            this.disabled = true;
            this.innerHTML = '<span style="display: inline-block; animation: spin 1s linear infinite;">↻</span>';
            
            setTimeout(() => {
                // 차트 데이터 업데이트
                strideChart.data.datasets[0].data = Array.from({length: 8}, () => Math.floor(Math.random() * 10) + 65);
                strideChart.data.datasets[1].data = Array.from({length: 8}, () => (Math.random() * 1.5 + 3.5).toFixed(1));
                strideChart.update();
                
                this.disabled = false;
                this.textContent = '새로고침';
            }, 1500);
        });
        
        // 주기적 데이터 업데이트
        setInterval(updateData, 10000); // 10초마다 데이터 업데이트
        
        // 배터리 상태 시뮬레이션 시작
        updateBatteryStatus();
        
        // 애니메이션 키프레임 추가
        const style = document.createElement('style');
        style.innerHTML = `
            @keyframes spin {
                0% { transform: rotate(0deg); }
                100% { transform: rotate(360deg); }
            }
        `;
        document.head.appendChild(style);
    </script>
</body>
</html>
