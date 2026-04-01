<!DOCTYPE html>
<html lang="en">
<head>
    <style>
        body { margin: 0; background: #0a0a0a; color: #fff; font-family: sans-serif; text-align: center; }
        canvas { background: #000; border: 2px solid #0ff; display: block; margin: 20px auto; cursor: crosshair; }
        h1 { color: #0ff; text-shadow: 0 0 10px #0ff; }
    </style>
</head>
<body>
    <h1>NEON STRIKER</h1>
    <p>Score: <span id="score">0</span></p>
    <canvas id="gameCanvas" width="600" height="400"></canvas>
    <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        let score = 0;
        let target = { x: 300, y: 200, r: 20 };

        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = '#f00';
            ctx.beginPath();
            ctx.arc(target.x, target.y, target.r, 0, Math.PI * 2);
            ctx.fill();
        }

        canvas.onclick = (e) => {
            const rect = canvas.getBoundingClientRect();
            const mouseX = e.clientX - rect.left;
            const mouseY = e.clientY - rect.top;
            const dist = Math.hypot(mouseX - target.x, mouseY - target.y);
            
            if (dist < target.r) {
                score++;
                document.getElementById('score').innerText = score;
                target.x = Math.random() * (canvas.width - 40) + 20;
                target.y = Math.random() * (canvas.height - 40) + 20;
            }
            draw();
        };
        draw();
    </script>
</body>
</html>
