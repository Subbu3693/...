
<html lang="en">
<head>
    <meta charset="UTF-8"> 
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Animated Grid Rows</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background: url('https://static.vecteezy.com/system/resources/previews/032/325/417/non_2x/3d-cartoon-character-cute-student-kids-boy-dancing-isolated-on-transparent-background-file-cut-out-ai-generated-png.png') ;
            overflow-y: auto;
            flex-direction: column;
        }
        .tree {
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .row {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 40px;
            margin: 20px 0;
            position: relative;
        }
        .branch {
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
        }
        .box {
            width: 150px;
            height: 150px;
            display: flex;
            justify-content: center;
            align-items: center;
            border-radius: 12px;
            background: white;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s, box-shadow 0.3s;
            cursor: pointer;
            opacity: 0;
        }
        .box:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
            background: #e3f2fd;
        }
        .image-frame {
            width: 150px;
            height: 150px;
            background: url('https://via.placeholder.com/150') no-repeat center center/cover;
            border-radius: 12px;
            display: none;
            opacity: 0;
            transition: opacity 0.5s;
        }
        .image-frame.show {
            display: block;
            opacity: 1;
        }
        a {
            text-decoration: none;
            color: #007bff;
            font-weight: bold;
            font-size: 18px;
        }

        /* 1. Smooth Slide In from Top Left */
        @keyframes smoothSlide {
            from {
                opacity: 0;
                transform: translate(-200px, -200px);
            }
            to {
                opacity: 1;
                transform: translate(0, 0);
            }
        }

        /* 2. Rotate In */
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

        /* 3. UPDATED: Move and Rotate Throughout the Page */
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
                opacity:1;
                transform: translate(0, 0) rotate(0deg);
            }
        }

        /* 4. Spiral In */
        @keyframes spiralIn {
            from {
                opacity: 0;
                transform: translateX(300px) rotate(720deg) scale(0);
            }
            to {
                opacity: 1;
                transform: translateX(0) rotate(0deg) scale(1);
            }
        }
    </style>
</head>
<body>
    <div class="tree" id="tree-container"></div>
    <script>
        const links = [
            { url: "https://example1.com", text: "Branch 1" },
            { url: "https://example2.com", text: "Branch 2" },
            { url: "https://example3.com", text: "Branch 3" }, // This one moves across the page
            { url: "https://example4.com", text: "Branch 4" }
        ];
        
        const animations = ["smoothSlide", "rotateIn", "moveAndRotate", "spiralIn"];
        const treeContainer = document.getElementById("tree-container");

        for (let i = 0; i < links.length; i += 2) {
            const row = document.createElement('div');
            row.classList.add('row');

            for (let j = 0; j < 2 && (i + j) < links.length; j++) {
                const branch = document.createElement('div');
                branch.classList.add('branch');

                const box = document.createElement('div');
                box.classList.add('box');

                // Assign unique animations
                box.style.animation = `${animations[i + j]} 2s ease-out forwards`;
                box.style.animationDelay = `${(i + j) * 0.3}s`; // Staggered effect

                const anchor = document.createElement('a');
                anchor.href = links[i + j].url;
                anchor.textContent = links[i + j].text;
                anchor.target = "_blank";

                const imageFrame = document.createElement('div');
                imageFrame.classList.add('image-frame');

                box.appendChild(anchor);
                branch.appendChild(box);
                branch.appendChild(imageFrame);
                row.appendChild(branch);

                box.addEventListener('click', function() {
                    imageFrame.classList.add('show'); // Show image on click
                });
            }

            treeContainer.appendChild(row);
        }
    </script>
</body>
</html>
