<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ตวงคนโปรด🐷(อนาคตที่ฝาก)</title>
    <style>
        body {
            background-color: #ffafbd;
            font-family: 'Arial', sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            overflow: hidden; /* กันหัวใจลอยทะลุหน้าจอ */
        }

        #shine {
            font-size: 2rem;
            color: white;
            text-shadow: 2px 2px 8px rgba(0,0,0,0.2);
            margin-bottom: 50px;
            text-align: center;
            z-index: 100;
        }

        .stack-container {
            position: relative;
            width: 250px;
            height: 320px;
            z-index: 10;
        }

        .stack-container img {
            position: absolute;
            width: 100%;
            height: 100%;
            object-fit: cover;
            border: 8px solid white;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            cursor: pointer;
            transition: transform 0.5s ease, opacity 0.5s ease;
        }

        .swiped {
            transform: translateX(200px) rotate(30deg) !important;
            opacity: 0;
        }

        /* --- ลูกเล่นใหม่: หัวใจลอย --- */
        .heart {
            position: fixed;
            font-size: 20px;
            color: #ff4d6d;
            pointer-events: none; /* ให้เมาส์ทะลุผ่านหัวใจได้ */
            animation: flyUp 1s ease-out forwards;
            z-index: 999;
        }

        @keyframes flyUp {
            0% { transform: translate(0, 0) scale(1); opacity: 1; }
            100% { transform: translate(var(--x), var(--y)) scale(1.5); opacity: 0; }
        }
    </style>
</head>
<body>

    <div id="shine"> 💕สุขสันต์วันวาเลนไทน์นะะะ💕<br><small style="font-size: 0.9rem;">(ลองกดที่รูปดูนะ)</small></div>

    <div class="stack-container" id="photoStack">
        <img src="https://i.postimg.cc/FKVHFYch/57428-0.jpg" alt="รูป 1">
        <img src="https://i.postimg.cc/Z5FSp1qd/57439-0.jpg" alt="รูป 2">
        <img src="https://i.postimg.cc/bvVNSKCf/57433-0.jpg" alt="รูป 3">
        <img src="https://i.postimg.cc/3wqYx2NQ/57427-0.jpg" alt="รูป 4">
        <img src="https://i.postimg.cc/QtDK0LQ2/57449-0.jpg" alt="รูป 5">
        <img src="https://i.postimg.cc/Z57hw6r3/57444-0.jpg" alt="รูป 6">
        <img src="https://i.postimg.cc/h4LWHkLK/57442-0.jpg" alt="รูป 7">
    </div>

    <audio id="mySong" loop>
        <source src="ท็อปในรุ่น - ฮันเตอร์.mp3" type="audio/mpeg">
    </audio>

    <script>
        const stack = document.getElementById('photoStack');
        const song = document.getElementById('mySong');
        const images = Array.from(stack.getElementsByTagName('img'));
        
        images.forEach((img, index) => {
            img.style.zIndex = images.length - index;
        });

        // ฟังก์ชันสร้างหัวใจ
        function createHeart(x, y) {
            for(let i=0; i<8; i++) { // สร้าง 8 ดวงต่อการคลิก 1 ครั้ง
                const heart = document.createElement('div');
                heart.innerHTML = '❤️';
                heart.className = 'heart';
                heart.style.left = x + 'px';
                heart.style.top = y + 'px';
                
                // สุ่มทิศทางที่จะลอยไป
                heart.style.setProperty('--x', (Math.random() - 0.5) * 200 + 'px');
                heart.style.setProperty('--y', (Math.random() - 1) * 200 + 'px');
                
                document.body.appendChild(heart);
                
                // ลบทิ้งเมื่ออนิเมชั่นจบ
                setTimeout(() => heart.remove(), 1000);
            }
        }

        stack.addEventListener('click', function(e) {
            if (e.target.tagName === 'IMG') {
                song.play(); // เล่นเพลงเมื่อคลิก
                createHeart(e.clientX, e.clientY); // สร้างหัวใจตรงจุดที่คลิก

                const topImg = e.target;
                topImg.classList.add('swiped');

                setTimeout(() => {
                    topImg.classList.remove('swiped');
                    const currentImages = Array.from(stack.getElementsByTagName('img'));
                    currentImages.forEach(img => {
                        img.style.zIndex = parseInt(img.style.zIndex || 0) + 1;
                    });
                    topImg.style.zIndex = 1;
                    stack.appendChild(topImg);
                }, 500);
            }
        });
    </script>
</body>
</html>
