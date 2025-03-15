# subbu.github.io
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tree Branch Linked Boxes</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background: black;
            background: url('https://static.vecteezy.com/system/resources/previews/032/325/417/non_2x/3d-cartoon-character-cute-student-kids-boy-dancing-isolated-on-transparent-background-file-cut-out-ai-generated-png.png') no-repeat center center/cover;
            padding: 20px;
            overflow-y: auto;
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
            margin: 10px 0;
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
            transition: transform 0.3s, box-shadow 0.3s, opacity 0.5s;
            cursor: pointer;
        }
        .box:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
            background: #e3f2fd;
        }
        .hidden {
            opacity: 0;
            transform: scale(0);
            transition: opacity 0.5s, transform 0.5s;
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
    </style>
</head>
<body>
    <div class="tree" id="tree-container"></div>
    <script>
        const links = [
            { url: "https://example1.com", text: "Branch 1" },
            { url: "https://example2.com", text: "Branch 2" },
            { url: "https://example3.com", text: "Branch 3" },
            { url: "https://example4.com", text: "Branch 4" },
            { url: "https://example5.com", text: "Branch 5" },
            { url: "https://example6.com", text: "Branch 6" },
            { url: "https://example7.com", text: "Branch 7" },
            { url: "https://example8.com", text: "Branch 8" }
        ];
        
        const treeContainer = document.getElementById("tree-container");

        for (let i = 0; i < links.length; i += 2) {
            const row = document.createElement('div');
            row.classList.add('row');

            for (let j = i; j < i + 2 && j < links.length; j++) {
                const branch = document.createElement('div');
                branch.classList.add('branch');

                const box = document.createElement('div');
                box.classList.add('box');
                box.dataset.index = j; 

                const anchor = document.createElement('a');
                anchor.href = links[j].url;
                anchor.textContent = links[j].text;
                anchor.target = "_blank";

                const imageFrame = document.createElement('div');
                imageFrame.classList.add('image-frame');

                box.appendChild(anchor);
                branch.appendChild(box);
                branch.appendChild(imageFrame);
                row.appendChild(branch);

                box.addEventListener('click', function() {
                    box.classList.add('hidden');
                    setTimeout(() => {
                        box.style.display = 'none';
                        imageFrame.classList.add('show');
                    }, 500);
                });
            }

            treeContainer.appendChild(row);
        }
    </script>
</body>
</html>
