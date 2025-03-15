<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8"> 
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Animated Coding Grid</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Bubblegum+Sans&display=swap');

        body {
            font-family: Arial, sans-serif;
            background: radial-gradient(circle, #021B79, #0575E6);
            color: white;
            margin: 0;
            padding: 80px 0 20px;
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* Fixed Bar for Title */
        .fixed-bar {
            position: fixed;
            top: 0;
            width: 100%;
            height: 60px;
            background: rgba(0, 0, 0, 0.7);
            display: flex;
            justify-content: center;
            align-items: center;
            box-shadow: 0 4px 10px rgba(0, 183, 255, 0.5);
            z-index: 100;
        }

        /* Heading Style */
        .title {
            font-family: 'Bubblegum Sans', cursive;
            font-size: 36px;
            font-weight: bold;
            text-transform: uppercase;
            color: #fff;
            text-shadow: 0 0 15px rgba(0, 183, 255, 0.8);
        }

        /* Floating Numbers */
        .floating-numbers {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            pointer-events: none;
            z-index: -1;
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
            width: 100%;
            margin-top: 20px;
            padding-bottom: 50px;
        }

        .row {
            display: flex;
            justify-content: center;
            align-items: center;
            width: 100%;
            margin: 20px 0;
        }

        .box {
            width: 200px;
            height: 200px;
            display: flex;
            justify-content: center;
            align-items: center;
            border-radius: 12px;
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 0 15px rgba(0, 183, 255, 0.5);
            transition: transform 0.8s ease-out, opacity 0.8s ease-out;
            cursor: pointer;
            opacity: 0;
        }

        /* Animation classes */
        .box.left {
            transform: translateX(-100px);
        }

        .box.right {
            transform: translateX(100px);
        }

        .box.visible {
            opacity: 1;
            transform: translateX(0);
        }

        .box.hidden-left {
            opacity: 0;
            transform: translateX(-100px);
        }

        .box.hidden-right {
            opacity: 0;
            transform: translateX(100px);
        }

        .box:hover {
            transform: scale(1.05);
            box-shadow: 0 0 20px rgba(0, 183, 255, 0.8);
            background: rgba(0, 183, 255, 0.2);
        }

        a {
            text-decoration: none;
            color: white;
            font-weight: bold;
            font-size: 18px;
        }

    </style>
</head>
<body>
    <!-- Fixed Bar with Title -->
    <div class="fixed-bar">
        <div class="title">WAY TO RISE</div>
    </div>

    <div class="floating-numbers" id="floating-numbers"></div>
    <div class="tree" id="tree-container"></div>

    <script>
        const links = [
            { url: "https://example1.com", text: "Branch 1" },
            { url: "https://example2.com", text: "Branch 2" },
            { url: "https://example3.com", text: "Branch 3" },
            { url: "https://example4.com", text: "Branch 4" },
            { url: "https://example5.com", text: "Branch 5" },
            { url: "https://example6.com", text: "Branch 6" }
        ];

        const treeContainer = document.getElementById("tree-container");

        for (let i = 0; i < links.length; i++) {
            const row = document.createElement('div');
            row.classList.add('row');

            const box = document.createElement('div');
            box.classList.add('box');

            // Alternate animation: left for even, right for odd
            if (i % 2 === 0) {
                box.classList.add('left');
            } else {
                box.classList.add('right');
            }

            const anchor = document.createElement('a');
            anchor.href = links[i].url;
            anchor.textContent = links[i].text;
            anchor.target = "_blank";

            box.appendChild(anchor);
            row.appendChild(box);
            treeContainer.appendChild(row);
        }

        let lastScrollTop = window.scrollY;

        function revealOnScroll() {
            const boxes = document.querySelectorAll('.box');
            const triggerBottom = window.innerHeight * 0.9;
            const currentScrollTop = window.scrollY;

            boxes.forEach(box => {
                const boxTop = box.getBoundingClientRect().top;

                if (boxTop < triggerBottom && currentScrollTop > lastScrollTop) {
                    // Scrolling down: reveal
                    box.classList.add('visible');
                    box.classList.remove('hidden-left', 'hidden-right');
                } else if (boxTop > triggerBottom && currentScrollTop < lastScrollTop) { 
                    // Scrolling up: hide again
                    if (box.classList.contains('left')) {
                        box.classList.add('hidden-left');
                    } else {
                        box.classList.add('hidden-right');
                    }
                    box.classList.remove('visible');
                }
            });

            lastScrollTop = currentScrollTop;
        }

        window.addEventListener('scroll', revealOnScroll);
        revealOnScroll();

        // Generate Floating Numbers
        const floatingNumbers = document.getElementById("floating-numbers");

        function createNumber() {
            const num = document.createElement("div");
            num.classList.add("number");
            num.textContent = Math.random() > 0.5 ? "0" : "1";
            num.style.left = `${Math.random() * 100}vw`;
            num.style.animationDuration = `${2 + Math.random() * 2}s`;
            floatingNumbers.appendChild(num);
            setTimeout(() => num.remove(), 9000);
        }

        setInterval(createNumber, 150);
    </script>
</body>
</html>
