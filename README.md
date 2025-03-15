<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8"> 
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Animated Coding Grid</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background: radial-gradient(circle, #021B79, #0575E6);
            overflow: hidden;
            flex-direction: column;
            position: relative;
            color: white;
        }
        
        /* Floating Numbers */
        .floating-numbers {
            position: absolute;
            width: 100%;
            height: 100%;
            overflow: hidden;
            pointer-events: none;
        }
        .number {
            position: absolute;
            font-size: 20px;
            color: rgba(255, 255, 255, 0.3);
            animation: floatUp 5s linear infinite;
        }

        @keyframes floatUp {
            from {
                transform: translateY(100vh) scale(0.5);
                opacity: 0;
            }
            50% {
                opacity: 1;
            }
            to {
                transform: translateY(-10vh) scale(1);
                opacity: 1;
            }
        }
        
        .tree {
            display: flex;
            flex-direction: column;
            align-items: center;
            z-index: 2;
        }
        .row {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 40px;
            margin: 20px 0;
            position: relative;
        }
        .box {
            width: 150px;
            height: 150px;
            display: flex;
            justify-content: center;
            align-items: center;
            border-radius: 12px;
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 0 15px rgba(0, 183, 255, 0.5);
            transition: transform 0.3s, box-shadow 0.3s;
            cursor: pointer;
            opacity: 1;
        }
        .box:hover {
            transform: translateY(-5px);
            box-shadow: 0 0 20px rgba(0, 183, 255, 0.8);
            background: rgba(0, 183, 255, 0.2);
        }
        a {
            text-decoration: none;
            color: white;
            font-weight: bold;
            font-size: 18px;
        }

        /* Animation: Smooth Slide */
        @keyframes smoothSlide {
            from {
                opacity: 0;
                transform: translateX(-100px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        /* Animation: Rotate In */
        @keyframes rotateIn {
            from {
                opacity: 0;
                transform: rotate(-360deg) scale(0);
            }
            to {
                opacity: 1;
                transform: rotate(0deg) scale(1);
            }
        }

        /* Animation: Spiral In */
        @keyframes spiralIn {
            from {
                opacity: 0;
                transform: translate(50px, 50px) rotate(720deg) scale(0.5);
            }
            to {
                opacity: 1;
                transform: translate(0, 0) rotate(0deg) scale(1);
            }
        }

        /* Animation: Rotate and Move Grid 3 */
        @keyframes moveAndRotate {
            0% {
                opacity: 0;
                transform: translate(-100vw, -100vh) rotate(0deg);
            }
            50% {
                opacity: 1;
                transform: translate(50vw, 50vh) rotate(720deg);
            }
            100% {
                opacity: 1;
                transform: translate(0, 0) rotate(0deg);
            }
        }
    </style>
</head>
<body>
    <div class="floating-numbers" id="floating-numbers"></div>
    <div class="tree" id="tree-container"></div>

    <script>
        const links = [
            { url: "https://example1.com", text: "Branch 1" },
            { url: "https://example2.com", text: "Branch 2" },
            { url: "https://example3.com", text: "Branch 3" },
            { url: "https://example4.com", text: "Branch 4" }
        ];
        
        const animations = ["smoothSlide", "rotateIn", "moveAndRotate", "spiralIn"];
        const treeContainer = document.getElementById("tree-container");

        for (let i = 0; i < links.length; i += 2) {
            const row = document.createElement('div');
            row.classList.add('row');

            for (let j = 0; j < 2 && (i + j) < links.length; j++) {
                const box = document.createElement('div');
                box.classList.add('box');
                box.style.animation = `${animations[i + j]} 2s ease-out forwards`;
                box.style.animationDelay = `${(i + j) * 0.3}s`;
                
                const anchor = document.createElement('a');
                anchor.href = links[i + j].url;
                anchor.textContent = links[i + j].text;
                anchor.target = "_blank";

                box.appendChild(anchor);
                row.appendChild(box);
            }
            treeContainer.appendChild(row);
        }

        // Generate Floating Numbers
        const floatingNumbers = document.getElementById("floating-numbers");
        function createNumber() {
            const num = document.createElement("div");
            num.classList.add("number");
            num.textContent = Math.random() > 0.5 ? "0" : "1";
            num.style.left = `${Math.random() * 100}vw`;
            num.style.animationDuration = `${3 + Math.random() * 3}s`;
            floatingNumbers.appendChild(num);
            setTimeout(() => num.remove(), 6000);
        }
        setInterval(createNumber, 300);
    </script>
</body>
</html>
