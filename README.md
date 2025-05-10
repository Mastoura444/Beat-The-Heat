<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Heat Risk Monitor - Abqaiq</title>
  <style>
    body {
      font-family: Arial; 
      text-align: center; 
      background: #f0f8ff; 
      padding: 20px;
    }
    .box {
      padding: 20px; 
      border-radius: 15px; 
      margin-top: 20px; 
      display: inline-block;
    }
    .low { background: #a8e6cf; }
    .moderate { background: #ffd3b6; }
    .high { background: #ffaaa5; }
    .extreme { background: #ff8b94; color: white; }

    .icon {
      width: 80px;
      margin-bottom: 10px;
    }

    .gif-person {
      max-width: 200px;
      margin: 10px auto;
      display: block;
      border-radius: 10px;
    }
  </style>
</head>
<body>

  <h1>Beat The Heat ... 🌡️</h1>
  <div id="weatherBox" class="box">Loading weather data...</div>

  <script>
    const apiKey = '049b3bb41da1e7325fd301e774c02b9f';
    const city = 'Abqaiq';
    const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${apiKey}&lang=en`;

    fetch(url)
      .then(response => response.json())
      .then(data => {
        const temp = data.main.temp;
        let risk = '';
        let advice = '';
        let cssClass = '';
        let gifUrl = '';

        if (temp < 30) {
          risk = 'Low';
          advice = 'Enjoy the pleasant weather and stay hydrated.';
          cssClass = 'low';
          gifUrl = 'https://media.giphy.com/media/h4OGaSgJGhKMEVuO6J/giphy.gif'; // شخص مبتسم
        } else if (temp < 38) {
          risk = 'Moderate';
          advice = 'Drink water regularly and take a break every hour.';
          cssClass = 'moderate';
          gifUrl = 'https://media.giphy.com/media/Ll22OhMLAlVDb8UQWe/giphy.gif'; // يشرب ماء
        } else if (temp < 44) {
          risk = 'High';
          advice = 'Take a break every 30 minutes and stay in the shade.';
          cssClass = 'high';
          gifUrl = 'https://media.giphy.com/media/f9k1tV7HyORcngKF8v/giphy.gif'; // يمسح عرقه
        } else {
          risk = 'Very High 🔥';
          advice = 'Take a break every 20 minutes and drink lots of water. Watch for heat exhaustion signs.';
          cssClass = 'extreme';
          gifUrl = 'https://media.giphy.com/media/3oKIPwoeGErMmaI43C/giphy.gif'; // شخص مرهق جداً
        }

        document.getElementById('weatherBox').className = 'box ' + cssClass;
        document.getElementById('weatherBox').innerHTML = `
          <img src="${gifUrl}" alt="Heat Animation" class="gif-person" />
          <h2>${temp}°C</h2>
          <h3>Heat Risk Level: ${risk}</h3>
          <p><strong>Tip:</strong> ${advice}</p>
        `;
      })
      .catch(() => {
        document.getElementById('weatherBox').innerText = 'Could not load weather data.';
      });
  </script>

</body>
</html>
