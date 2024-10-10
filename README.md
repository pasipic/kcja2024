<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>확률과 통계 - 독립시행 계산기</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100">
    <div id="root" class="container mx-auto p-4">
        <h1 class="text-3xl font-bold mb-6 text-center text-blue-600">확률과 통계 - 독립시행 계산기</h1>
        
        <div class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
            <h2 class="text-xl font-semibold mb-4">독립시행 확률 계산</h2>
            <div class="mb-4">
                <label class="block text-gray-700 text-sm font-bold mb-2" for="trials">
                    시행 횟수:
                </label>
                <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="trials" type="number" min="1" placeholder="10">
            </div>
            <div class="mb-4">
                <label class="block text-gray-700 text-sm font-bold mb-2" for="probability">
                    한 번의 시행에서 성공할 확률 (분자/분모):
                </label>
                <div class="flex">
                    <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline mr-2" id="numerator" type="number" min="0" placeholder="1">
                    <span class="text-2xl mr-2">/</span>
                    <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="denominator" type="number" min="1" placeholder="2">
                </div>
            </div>
            <div class="mb-4">
                <label class="block text-gray-700 text-sm font-bold mb-2" for="successes">
                    원하는 성공 횟수:
                </label>
                <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="successes" type="number" min="0" placeholder="5">
            </div>
            <div class="flex items-center justify-between">
                <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="button" onclick="calculateProbability()">
                    계산하기
                </button>
            </div>
        </div>
        
        <div id="result" class="mt-4 p-4 bg-green-100 rounded hidden">
            <h3 class="font-bold text-lg mb-2">계산 결과:</h3>
            <p id="resultText"></p>
        </div>
    </div>
    <script>
        function calculateProbability() {
            const numerator = parseInt(document.getElementById('numerator').value);
            const denominator = parseInt(document.getElementById('denominator').value);
            const n = parseInt(document.getElementById('trials').value);
            const k = parseInt(document.getElementById('successes').value);
            
            if (isNaN(numerator) || isNaN(denominator) || isNaN(n) || isNaN(k) || denominator === 0 || numerator < 0 || denominator < 1 || n < 1 || k < 0 || k > n) {
                alert('올바른 값을 입력해주세요.');
                return;
            }
            const p = numerator / denominator;
            const probability = binomialProbability(n, k, p);
            
            const resultElement = document.getElementById('result');
            const resultTextElement = document.getElementById('resultText');
            
            resultTextElement.textContent = `확률: ${probability.toFixed(4)} (${(probability * 100).toFixed(4)}%)`;
            resultElement.classList.remove('hidden');
        }
        function binomialProbability(n, k, p) {
            return combination(n, k) * Math.pow(p, k) * Math.pow(1 - p, n - k);
        }
        function combination(n, k) {
            return factorial(n) / (factorial(k) * factorial(n - k));
        }
        function factorial(num) {
            if (num === 0 || num === 1) return 1;
            let result = 1;
            for (let i = 2; i <= num; i++) {
                result *= i;
            }
            return result;
        }
    </script>
</body>
</html>
