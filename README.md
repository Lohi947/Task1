# Task1
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Language Translation Tool</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 30px; background-color: #f7f7f7; }
    textarea, select, button { width: 100%; margin-top: 10px; padding: 10px; font-size: 16px; }
    #translatedText { margin-top: 20px; background-color: #e0f7fa; padding: 10px; }
    .copy-btn { margin-top: 10px; }
  </style>
</head>
<body>
  <h2>🌍 Language Translation Tool</h2>

  <textarea id="inputText" rows="4" placeholder="Enter text to translate..."></textarea>

  <label for="sourceLang">Source Language:</label>
  <select id="sourceLang">
    <option value="en">English</option>
    <option value="es">Spanish</option>
    <option value="fr">French</option>
    <option value="hi">Hindi</option>
  </select>

  <label for="targetLang">Target Language:</label>
  <select id="targetLang">
    <option value="es">Spanish</option>
    <option value="en">English</option>
    <option value="fr">French</option>
    <option value="hi">Hindi</option>
  </select>

  <button onclick="translateText()">Translate</button>

  <div id="translatedText"></div>
  <button class="copy-btn" onclick="copyToClipboard()">📋 Copy Translated Text</button>

  <script>
    async function translateText() {
      const inputText = document.getElementById('inputText').value;
      const sourceLang = document.getElementById('sourceLang').value;
      const targetLang = document.getElementById('targetLang').value;

      if (!inputText) {
        alert("Please enter some text.");
        return;
      }

      const response = await fetch("https://libretranslate.de/translate", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          q: inputText,
          source: sourceLang,
          target: targetLang,
          format: "text"
        })
      });

      const data = await response.json();
      document.getElementById('translatedText').innerText = data.translatedText || "Translation failed.";
    }

    function copyToClipboard() {
      const translated = document.getElementById('translatedText').innerText;
      navigator.clipboard.writeText(translated).then(() => {
        alert("Translated text copied!");
      });
    }
  </script>
</body>
</html>
