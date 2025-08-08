<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FedEx Tracking Number Separator</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .container {
            max-width: 800px;
        }
    </style>
</head>
<body class="bg-gray-100 flex items-center justify-center min-h-screen">
    <div class="container bg-white p-8 rounded-xl shadow-lg border border-gray-200">
        <h1 class="text-3xl font-bold text-gray-800 mb-6 text-center">FedEx Tracking Number Separator</h1>
        <p class="text-gray-600 mb-6 text-center">
            Paste your text below and the program will extract the tracking numbers.
        </p>

        <textarea id="inputText" rows="10"
                   class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 transition-all"
                   placeholder="e.g.,
Hello, this is a message about some packages.
The tracking numbers are 784381023758 and 784381023759.
Another number is here: 123-456-789-012 but that's not a valid length.
Here is a third tracking number: 784381023760. And another: 784381023761
Please disregard all the other information on this page."></textarea>

        <button id="extractButton"
                class="w-full bg-blue-600 text-white font-semibold py-3 rounded-lg hover:bg-blue-700 transition-colors focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2 mt-4">
            Extract Tracking Numbers
        </button>

        <div class="mt-8">
            <label class="block text-sm font-medium text-gray-700 mb-2">
                Extracted Numbers (with tabs)
            </label>
            <textarea id="outputArea" rows="5" readonly
                   class="w-full px-4 py-2 border border-gray-300 rounded-lg bg-gray-50 text-gray-700 font-mono"></textarea>
            <button id="copyButton"
                    class="mt-2 w-full bg-green-500 text-white font-semibold py-2 rounded-lg hover:bg-green-600 transition-colors focus:outline-none focus:ring-2 focus:ring-green-500 focus:ring-offset-2">
                Copy to Clipboard
            </button>
        </div>
    </div>

    <script>
        const trackingNumberRegex = /[a-zA-Z0-9]{12,22}/g;
        
        function extractAndFormat(inputText) {
            const matches = inputText.match(trackingNumberRegex);
            if (!matches) {
                return "";
            }
            return matches.join("\t");
        }

        document.getElementById('extractButton').addEventListener('click', () => {
            const inputText = document.getElementById('inputText').value;
            const outputText = extractAndFormat(inputText);
            document.getElementById('outputArea').value = outputText;
        });

        document.getElementById('copyButton').addEventListener('click', () => {
            const outputArea = document.getElementById('outputArea');
            outputArea.select();
            document.execCommand('copy');
        });

        // Initialize with the example text
        document.getElementById('inputText').value = `
Hello, this is a message about some packages.
The tracking numbers are 784381023758 and 784381023759.
Another number is here: 123-456-789-012 but that's not a valid length.
Here is a third tracking number: 784381023760. And another: 784381023761
Please disregard all the other information on this page.
`;
    </script>
</body>
</html>
