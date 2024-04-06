<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>100x100 Grid of Random Colours</title>
<style>
    body {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 0;
        background-color: black; /* Set background color to black */
    }

    .pixel {
        width: 7px; /* Each pixel is 7x7 pixels (5px for the pixel + 1px border on each side) */
        height: 7px; /* Each pixel is 7x7 pixels (5px for the pixel + 1px border on each side) */
        display: inline-block;
        margin: 0;
        font-size: 12px;
    }

    .refresh-button {
        position: relative; /* Position relative for absolute positioning of borders */
        font-size: 20px;
        font-weight: bold;
        padding: 15px 30px; /* Increased padding for larger button */
        background-color: #4CAF50; /* Green color */
        color: white;
        border: 2px solid black; /* Set border */
        cursor: pointer;
        text-decoration: none;
        border-radius: 15px; /* Rounded corners */
        transition: background-color 0.3s, box-shadow 0.3s, border-color 0.3s; /* Smooth transition on hover */
        box-shadow: 0px 8px 16px rgba(0, 0, 0, 0.1); /* Add shadow */
    }

    .refresh-button::before,
    .refresh-button::after {
        content: "";
        position: absolute;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        border: 1px solid black; /* Set border */
        border-radius: 15px; /* Match button's border radius */
        z-index: -1; /* Behind the button content */
    }

    .refresh-button::after {
        content: "";
        width: calc(100% + 2px);
        height: calc(100% + 2px);
        top: -1px;
        left: -1px;
        border: 1px solid black; /* Set border */
        border-radius: 15px; /* Match button's border radius */
        z-index: -2; /* Behind the white border */
    }

    .refresh-button:hover {
        background-color: #45a049; /* Darker green color on hover */
        box-shadow: 0px 12px 24px rgba(0, 0, 0, 0.2); /* Increase shadow on hover */
        border-color: #45a049; /* Darker green color on hover */
    }
</style>
</head>
<body>
    <script>
        // Create a 100x100 grid of pixels with random colors
        let canvas = document.createElement('canvas');
        canvas.width = 700; // 100 * 7 (pixel size)
        canvas.height = 700; // 100 * 7 (pixel size)
        let ctx = canvas.getContext('2d');

        // Set canvas background color to black
        ctx.fillStyle = "black";
        ctx.fillRect(0, 0, canvas.width, canvas.height);

        for (let i = 0; i < 100; i++) {
            for (let j = 0; j < 100; j++) {
                // Generate a random color
                let randomColor = '#' + Math.floor(Math.random() * 16777215).toString(16);
                // Set the pixel color
                ctx.fillStyle = randomColor;
                // Draw the pixel
                ctx.fillRect(j * 7 + 1, i * 7 + 1, 5, 5);
            }
        }

        // Convert canvas to base64-encoded PNG
        let imageDataURL = canvas.toDataURL('image/png');

        // Set the generated PNG as the body background
        document.body.style.backgroundImage = `url(${imageDataURL})`;
    </script>
    <button class="refresh-button" onclick="window.location.reload();">Refresh</button>
</body>
</html>
