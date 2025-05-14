<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Letter or Word Highlighter</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }
    #output {
      margin-top: 20px;
      white-space: pre-wrap;
      background-color: #f0f0f0;
      padding: 10px;
      border-radius: 5px;
    }
    strong {
      background-color: yellow;
    }
  </style>
</head>
<body>
  <h2>Highlight Letter or Word in Uploaded File</h2>
  <input type="file" id="fileInput"><br><br>
  <label for="wordInput">Letter or word to highlight:</label>
  <input type="text" id="wordInput">
  <button onclick="processFile()">Highlight</button>

  <div id="output"></div>

  <script>
    function escapeRegExp(string) {
      return string.replace(/[.*+?^${}()|[\]\\]/g, '\\$&');
    }

    function processFile() {
      const fileInput = document.getElementById('fileInput');
      const word = document.getElementById('wordInput').value;
      const output = document.getElementById('output');

      if (!fileInput.files[0]) {
        alert("Please upload a file first.");
        return;
      }

      if (!word) {
        alert("Please enter a letter or word to highlight.");
        return;
      }

      const reader = new FileReader();
      reader.onload = function(e) {
        let text = e.target.result;
        const escapedWord = escapeRegExp(word);
        const regex = new RegExp(escapedWord, 'gi'); // Match any instance, case-insensitive
        const highlighted = text.replace(regex, '<strong>$&</strong>');
        output.innerHTML = highlighted;
      };
      reader.readAsText(fileInput.files[0]);
    }
  </script>
</body>
</html>
