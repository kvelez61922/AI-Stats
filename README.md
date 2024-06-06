<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Statistics Calculator</title>
<style>
    body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        background-color: #f2f2f2;
    }
    .container {
        text-align: center;
    }
    input[type="text"] {
        padding: 10px;
        margin-bottom: 10px;
        width: 200px;
        font-size: 16px;
    }
    button {
        padding: 10px 20px;
        background-color: #4CAF50;
        color: white;
        border: none;
        cursor: pointer;
        font-size: 16px;
    }
    button:hover {
        background-color: #45a049;
    }
    #result {
        margin-top: 20px;
        font-size: 18px;
    }
</style>
</head>
<body>

<div class="container">
    <h2>Statistics Calculator</h2>
    <input type="text" id="numbers" placeholder="Enter numbers separated by commas">
    <br>
    <button onclick="calculateStatistics()">Calculate</button>
    <div id="result"></div>
</div>

<script>
    function calculateStatistics() {
        var numbersInput = document.getElementById("numbers").value.trim();
        var numbersArray = numbersInput.split(",").map(Number);
        
        var mean = calculateMean(numbersArray);
        var median = calculateMedian(numbersArray);
        var stdDev = calculateStandardDeviation(numbersArray);
        var interquartileRange = calculateInterquartileRange(numbersArray);

        var resultDiv = document.getElementById("result");
        resultDiv.innerHTML = "Mean: " + mean.toFixed(2) + "<br>" +
                              "Median: " + median.toFixed(2) + "<br>" +
                              "Standard Deviation: " + stdDev.toFixed(2) + "<br>" +
                              "Interquartile Range: " + interquartileRange.toFixed(2);
    }

    function calculateMean(numbers) {
        var sum = numbers.reduce(function (acc, val) {
            return acc + val;
        }, 0);
        return sum / numbers.length;
    }

    function calculateMedian(numbers) {
        var sorted = numbers.sort(function (a, b) {
            return a - b;
        });
        var mid = Math.floor(sorted.length / 2);
        return sorted.length % 2 !== 0 ? sorted[mid] : (sorted[mid - 1] + sorted[mid]) / 2;
    }

    function calculateStandardDeviation(numbers) {
        var mean = calculateMean(numbers);
        var squaredDiffs = numbers.map(function (value) {
            var diff = value - mean;
            return diff * diff;
        });
        var avgSquaredDiff = calculateMean(squaredDiffs);
        return Math.sqrt(avgSquaredDiff);
    }

    function calculateInterquartileRange(numbers) {
        var sorted = numbers.sort(function (a, b) {
            return a - b;
        });
        var mid = Math.floor(sorted.length / 2);
        var lowerHalf = sorted.slice(0, mid);
        var upperHalf = sorted.slice(mid + (sorted.length % 2 === 0 ? 0 : 1));
        var lowerQuartile = calculateMedian(lowerHalf);
        var upperQuartile = calculateMedian(upperHalf);
        return upperQuartile - lowerQuartile;
    }
</script>

</body>
</html>
