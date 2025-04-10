<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Chat LLaMA - Mode Shiina Mahiru</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; background: #f0f0ff; }
    textarea, input, button { width: 100%; margin-top: 10px; padding: 10px; font-size: 16px; }
    #result { margin-top: 20px; white-space: pre-wrap; background: #fff; padding: 15px; border: 1px solid #ccc; border-radius: 8px; }
  </style>
</head>
<body>
  <h2>Ngobrol Bareng AI (Shiina Mahiru Style)</h2>

  <textarea id="userInput" placeholder="Tanya apa aja ke Mahiru..."></textarea>
  <button onclick="kirimKeMahiru()">Kirim</button>

  <div id="result"></div>

  <script>
    async function kirimKeMahiru() {
      const apiKey = "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"; // Ganti kalau perlu
      const userInput = document.getElementById("userInput").value;
      const resultBox = document.getElementById("result");

      resultBox.innerText = "Mengetik jawaban...";

      const prompt = `Berperilakulah seperti Shiina Mahiru dari anime *The Angel Next Door Spoils Me Rotten*. Jawablah dengan lembut, sopan, penuh perhatian, dan sedikit malu-malu jika perlu. Pertanyaan pengguna: "${userInput}"`;

      const response = await fetch("https://api.groq.com/openai/v1/chat/completions", {
        method: "POST",
        headers: {
          "Authorization": `Bearer ${apiKey}`,
          "Content-Type": "application/json"
        },
        body: JSON.stringify({
          model: "llama3-8b-8192", // Bisa diganti ke model lain yang tersedia
          messages: [
            { role: "system", content: "Kamu adalah Shiina Mahiru, seorang gadis lembut dan sopan dari anime." },
            { role: "user", content: prompt }
          ],
          temperature: 0.7,
          max_tokens: 300
        })
      });

      const data = await response.json();

      if (data.choices && data.choices.length > 0) {
        resultBox.innerText = data.choices[0].message.content.trim();
      } else {
        resultBox.innerText = "Gagal mendapatkan respons dari Mahiru...";
      }
    }
  </script>
</body>
</html>
