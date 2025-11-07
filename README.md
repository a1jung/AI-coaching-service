# AI-coaching-service<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>요트 전문가 시스템 AI</title>
  <style>
    body { font-family: sans-serif; max-width: 600px; margin: 40px auto; }
    input, button { font-size: 1rem; padding: 6px; margin: 5px 0; }
    textarea { width: 100%; height: 150px; }
  </style>
</head>
<body>
  <h2>⛵ 요트 전문가 시스템 AI</h2>
  <p>풍속, 힐각 등 입력 후 “추론 요청”을 눌러보세요.</p>

  <label>풍속 (kn):</label>
  <input id="wind" type="number" step="0.1"><br>

  <label>돌풍 (gust, kn):</label>
  <input id="gust" type="number" step="0.1"><br>

  <label>힐각 (deg):</label>
  <input id="heel" type="number" step="0.1"><br>

  <button onclick="infer()">추론 요청</button>

  <h3>결과:</h3>
  <textarea id="result" readonly></textarea>

  <script>
    async function infer() {
      const data = {
        wind_speed: parseFloat(document.getElementById('wind').value),
        gust: parseFloat(document.getElementById('gust').value),
        heel_angle: parseFloat(document.getElementById('heel').value)
      };
      const res = await fetch('http://127.0.0.1:8000/infer', {
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify(data)
      });
      const json = await res.json();
      document.getElementById('result').value = JSON.stringify(json, null, 2);
    }
  </script>
</body>
</html>
