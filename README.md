<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>1000 Images</title>
<style>
    body, html {
        margin: 0;
        padding: 0;
    }

    .container {
        box-sizing: border-box;
        float: left;
        padding: 20px;
        border-radius: 10px;
        background-color: rgba(0, 0, 0, 0.5);
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
        margin: 10px;
    }

    .left-container, .middle-container {
        width: calc(37.5% - 40px); /* 75% of the screen width minus margins */
    }

    .right-container {
        width: calc(27% - 40px); /* 25% of the screen width minus margins */
    }

    .container img {
        width: calc(100% / 20); /* 20 images per row */
        height: auto;
        border: 1px solid #ddd;
        box-sizing: border-box;
    }

    .pair-info {
        background-color: rgba(255, 255, 255, 0.8); /* semi-transparent white background */
        padding: 20px;
        border-radius: 10px;
    }

    .pair-info p {
        margin: 5px 0;
    }
</style>
</head>
<body>
<div class="container left-container" id="imageContainer1">
    <!-- Images for container 1 will be generated here -->
</div>

<div class="container middle-container" id="imageContainer2">
    <!-- Images for container 2 will be generated here -->
</div>

<div class="container right-container" id="newContainer">
    <!-- Token pair information will be displayed here -->
    <div class="pair-info" id="newPairInfo">
        <!-- New token pair information will be displayed here -->
    </div>
</div>

<script>
    // Base URL for the images
    var imageBaseUrl1 = "https://assets.pinit.io/6h3c4mJmuAFB4Zve9TzzDjNhRfLbBCdCBmJLACvrFEGc/a9218ec4-3336-4afc-a309-bc4825d4bc7e/";
    var imageBaseUrl2 = "https://img-cdn.magiceden.dev/rs:fit:640:0:0/plain/https://assets.pinit.io/6h3c4mJmuAFB4Zve9TzzDjNhRfLbBCdCBmJLACvrFEGc/ec05b7c9-fbe2-46e8-8b89-054792b5b075/";

    // Number of images
    var numImages = 1000;

    // Reference to the containers
    var container1 = document.getElementById("imageContainer1");
    var container2 = document.getElementById("imageContainer2");
    var newContainer = document.getElementById("newContainer");

    // Loop through and generate image tags for container 1
    for (var i = 0; i < numImages; i++) {
        var img = document.createElement("img");
        img.src = imageBaseUrl1 + i;
        img.alt = "Image " + i;
        container1.appendChild(img);
    }

    // Loop through and generate image tags for container 2 (0 to 499)
    for (var i = 0; i < 500; i++) {
        var img = document.createElement("img");
        img.src = imageBaseUrl2 + i;
        img.alt = "Image " + i;
        container2.appendChild(img);
    }

    // Function to fetch token pair information
    function fetchPairInfo(containerId) {
        // Make an API request to fetch token pair information
        fetch('https://api.dexscreener.com/latest/dex/pairs/solana/DuJjKhV11KkgPYJaCH4SxC5e9sKbxcDug2rMxnJdy2V3')
            .then(response => response.json())
            .then(data => {
                // Update the pair information in the UI
                document.getElementById(containerId).querySelector('.pair-info').innerHTML = `
                    <h1>Name: ${data.pairs[0].baseToken.name}</h1>
                    <p>Symbol: $${data.pairs[0].baseToken.symbol}</p>
                    <p>Address: ${data.pairs[0].baseToken.address}</p>
                    <h1>Token Pair Information</h1>
                    <p>Chain ID: ${data.pairs[0].chainId}</p>
                    <p>DEX ID: ${data.pairs[0].dexId}</p>
                    <p>Pair Address: ${data.pairs[0].pairAddress}</p>
                    <p>Quote Token:</p>
                    <ul>
                        <li>Name: ${data.pairs[0].quoteToken.name}</li>
                        <li>Symbol: ${data.pairs[0].quoteToken.symbol}</li>
                        <li>Address: ${data.pairs[0].quoteToken.address}</li>
                    </ul>
                    <p>Price (Native): ${data.pairs[0].priceNative}</p>
                    <p>Price (USD): ${data.pairs[0].priceUsd}</p>
                    <p>Transaction Count:</p>
                    <ul>
                        <li>5 Minutes: Buys - ${data.pairs[0].txns.m5.buys}, Sells - ${data.pairs[0].txns.m5.sells}</li>
                        <li>1 Hour: Buys - ${data.pairs[0].txns.h1.buys}, Sells - ${data.pairs[0].txns.h1.sells}</li>
                        <li>6 Hours: Buys - ${data.pairs[0].txns.h6.buys}, Sells - ${data.pairs[0].txns.h6.sells}</li>
                        <li>24 Hours: Buys - ${data.pairs[0].txns.h24.buys}, Sells - ${data.pairs[0].txns.h24.sells}</li>
                    </ul>
                    <p>Volume:</p>
                    <ul>
                        <li>24 Hours: ${data.pairs[0].volume.h24}</li>
                        <li>6 Hours: ${data.pairs[0].volume.h6}</li>
                        <li>1 Hour: ${data.pairs[0].volume.h1}</li>
                        <li>5 Minutes: ${data.pairs[0].volume.m5}</li>
                    </ul>
                    <p>Price Change:</p>
                    <ul>
                        <li>5 Minutes: ${data.pairs[0].priceChange.m5}</li>
                        <li>1 Hour: ${data.pairs[0].priceChange.h1}</li>
                        <li>6 Hours: ${data.pairs[0].priceChange.h6}</li>
                        <li>24 Hours: ${data.pairs[0].priceChange.h24}</li>
                    </ul>
                    <p>Liquidity:</p>
                    <ul>
                        <li>USD: ${data.pairs[0].liquidity.usd}</li>
                        <li>Base: ${data.pairs[0].liquidity.base}</li>
                        <li>Quote: ${data.pairs[0].liquidity.quote}</li>
                    </ul>
                    <p>FDV: ${data.pairs[0].fdv}</p>
                    <p>Pair Created At: ${data.pairs[0].pairCreatedAt}</p>
                `;
            })
            .catch(error => console.error('Error fetching pair information:', error));
    }

    // Initial fetch when the page loads for new container
    fetchPairInfo('newContainer');
</script>
</body>
</html>
