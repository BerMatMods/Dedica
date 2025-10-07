
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no" />
  <title>Carta de Amor - Personalizador</title>

  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Playfair+Display:wght@700&family=Poppins:wght@400;500;600&family=Georgia&display=swap" rel="stylesheet">

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #f9f0ff, #e6d7ff, #f0e6ff);
      color: #2c2c2c;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 25px;
      overflow-x: hidden;
      position: relative;
    }

    /* Modal de descarga */
    #downloadModal {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.8);
      display: none;
      justify-content: center;
      align-items: center;
      z-index: 2000;
    }

    .download-content {
      background: white;
      border-radius: 28px;
      padding: 40px;
      text-align: center;
      max-width: 520px;
      width: 92%;
      box-shadow: 0 0 50px rgba(142, 36, 170, 0.7);
      position: relative;
      border: 3px solid #ba68c8;
      animation: popIn 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    }

    @keyframes popIn {
      0% { transform: scale(0.7); opacity: 0; }
      100% { transform: scale(1); opacity: 1; }
    }

    .download-content h3 {
      font-family: 'Georgia', serif;
      font-weight: bold;
      color: #7b1fa2;
      font-size: 2rem;
      margin-bottom: 20px;
      text-shadow: 0 0 10px rgba(123, 31, 162, 0.3);
    }

    .download-content p {
      margin: 12px 0;
      color: #444;
      line-height: 1.6;
      font-size: 1.05rem;
    }

    .close-download {
      position: absolute;
      top: 18px;
      right: 18px;
      font-size: 1.8rem;
      color: #e91e63;
      cursor: pointer;
      font-weight: bold;
      transition: transform 0.3s;
    }
    .close-download:hover {
      transform: rotate(90deg);
    }

    /* Contenedor principal de opciones */
    .controls-container {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(310px, 1fr));
      gap: 28px;
      width: 100%;
      max-width: 1100px;
      margin: 25px 0;
    }

    .control-box {
      background: rgba(255, 255, 255, 0.92);
      border-radius: 22px;
      padding: 24px;
      position: relative;
      overflow: hidden;
      font-weight: 600;
      box-shadow: 0 10px 30px rgba(0,0,0,0.12);
    }

    .control-box::before {
      content: '';
      position: absolute;
      top: -3px; left: -3px; right: -3px; bottom: -3px;
      background: linear-gradient(45deg, #e91e63, #9c27b0, #673ab7, #3f51b5, #e91e63);
      z-index: -1;
      border-radius: 25px;
      opacity: 0.8;
      filter: blur(12px);
      animation: neonGlow 4s infinite alternate;
    }

    @keyframes neonGlow {
      0% { opacity: 0.6; filter: blur(8px); }
      100% { opacity: 0.9; filter: blur(14px); }
    }

    .control-label {
      display: block;
      margin-bottom: 14px;
      font-weight: 700;
      color: #7b1fa2;
      font-size: 1.1rem;
      font-family: 'Georgia', serif;
      text-shadow: 0 0 6px rgba(123, 31, 162, 0.2);
    }

    textarea, input[type="text"], input[type="color"], select, input[type="range"] {
      width: 100%;
      padding: 13px;
      border: 2px solid #e0e0e0;
      border-radius: 14px;
      font-family: 'Poppins', sans-serif;
      font-size: 1rem;
      background: white;
      font-weight: 600;
      transition: all 0.3s;
    }

    textarea {
      min-height: 110px;
      resize: vertical;
    }

    input[type="range"] {
      padding: 0;
    }

    textarea:focus, input:focus, select:focus {
      outline: none;
      border-color: #9c27b0;
      box-shadow: 0 0 0 4px rgba(156, 39, 176, 0.25);
    }

    .btn-group {
      display: flex;
      gap: 18px;
      margin: 30px 0;
      width: 100%;
      max-width: 520px;
      justify-content: center;
    }

    .btn {
      flex: 1;
      padding: 16px;
      border: none;
      border-radius: 16px;
      font-weight: 700;
      cursor: pointer;
      font-family: 'Poppins', sans-serif;
      font-size: 1.1rem;
      transition: all 0.35s;
      box-shadow: 0 8px 20px rgba(0,0,0,0.18);
    }

    .btn-preview {
      background: linear-gradient(45deg, #2196f3, #03a9f4);
      color: white;
    }

    .btn-download {
      background: linear-gradient(45deg, #4caf50, #8bc34a);
      color: white;
    }

    .btn:hover {
      transform: translateY(-4px) scale(1.02);
      box-shadow: 0 12px 28px rgba(0,0,0,0.28);
    }

    /* Vista previa libre */
    #preview-container {
      width: 100%;
      max-width: 950px;
      margin: 30px 0;
      display: flex;
      justify-content: center;
    }

    iframe {
      width: 100%;
      min-height: 700px;
      border: none;
      border-radius: 26px;
      box-shadow: 0 14px 45px rgba(0,0,0,0.22);
    }

    h1 {
      text-align: center;
      margin: 30px 0 20px;
      color: #7b1fa2;
      font-family: 'Georgia', serif;
      font-size: 2.5rem;
      font-weight: bold;
      text-shadow: 0 0 12px rgba(123, 31, 162, 0.4);
    }

    .subtitle {
      text-align: center;
      max-width: 750px;
      margin-bottom: 28px;
      color: #444;
      font-size: 1.15rem;
      line-height: 1.65;
      font-weight: 600;
    }

    footer {
      margin: 35px 0;
      text-align: center;
      font-size: 1.3rem;
      color: #7b1fa2;
      font-weight: 700;
      font-family: 'Georgia', serif;
      text-shadow: 0 0 10px rgba(123, 31, 162, 0.35);
    }

    .support-section {
      display: flex;
      gap: 25px;
      margin: 30px 0;
      flex-wrap: wrap;
      justify-content: center;
    }

    .support-box {
      background: white;
      border-radius: 22px;
      padding: 24px;
      text-align: center;
      min-width: 240px;
      box-shadow: 0 10px 30px rgba(156, 39, 176, 0.35);
      position: relative;
      overflow: hidden;
    }

    .support-box::before {
      content: '';
      position: absolute;
      top: -3px; left: -3px; right: -3px; bottom: -3px;
      background: linear-gradient(45deg, #9c27b0, #673ab7, #512da8);
      z-index: -1;
      border-radius: 25px;
      opacity: 0.75;
      filter: blur(10px);
    }

    .support-box h4 {
      color: white;
      margin-bottom: 12px;
      font-family: 'Poppins', sans-serif;
      font-weight: 700;
      font-size: 1.25rem;
      text-shadow: 0 0 8px rgba(0,0,0,0.6);
    }

    .support-box p, .support-box a {
      color: #333;
      font-size: 1rem;
      margin: 6px 0;
      display: block;
      font-weight: 600;
    }

    .support-box a {
      color: #25D366;
      text-decoration: none;
      font-weight: 700;
    }

    .support-box a:hover {
      text-decoration: underline;
    }

    .fontSizeValue {
      display: block;
      text-align: center;
      margin-top: 10px;
      font-weight: 700;
      color: #7b1fa2;
      font-size: 1.1rem;
    }
  </style>
</head>
<body>

  <h1>💌 Generador de Carta de Amor Personalizada</h1>
  <p class="subtitle">
    Personaliza cada detalle desde aquí. Todo se actualiza automáticamente en tiempo real.
  </p>

  <!-- Controles de personalización -->
  <div class="controls-container">
    <div class="control-box">
      <label class="control-label">🔐 Código de acceso</label>
      <input type="text" id="inputCode" value="2050">
    </div>

    <div class="control-box">
      <label class="control-label">💌 Mensaje de la carta</label>
      <textarea id="inputMessage">Hoy quiero que sepas, con cada latido de mi corazón,
que eres la persona más hermosa, dulce y especial
que he tenido la fortuna de conocer.

Desde que llegaste a mi vida, todo tiene más color,
más sentido, más magia. Tus risas son mi melodía favorita,
tu mirada, mi refugio, y tu amor, mi mayor bendición.

Cada día a tu lado es un regalo que agradezco profundamente.
No hay palabras suficientes para describir lo que siento,
pero si pudiera dibujarlo, sería un cielo lleno de estrellas,
un jardín infinito de flores, y un océano de paz.

Gracias por ser tú, por amarme como soy,
por entenderme sin necesidad de palabras,
por abrazarme incluso cuando no lo merezco.

Te amo más de lo que las palabras pueden decir,
más de lo que el tiempo puede medir,
más de lo que el universo puede contener.

Siempre serás mi hogar, mi sueño, mi razón.

Con todo mi corazón, siempre tuyo.</textarea>
    </div>

    <div class="control-box">
      <label class="control-label">🎵 URL de música (MP3)</label>
      <input type="text" id="inputMusic" value="https://files.catbox.moe/s5tmq9.mp3">
    </div>

    <div class="control-box">
      <label class="control-label">🖼️ GIF 1 (superior)</label>
      <input type="text" id="inputGif1" value="https://media2.giphy.com/media/v1.Y2lkPTZjMDliOTUyZTAxbHV0Mm1rYmI2emc3ZmdvcGdka2szMGMzMHl4ZXlhcmEzN3A4cCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/Y62ofc4S1Vst2/giphy.gif">
    </div>

    <div class="control-box">
      <label class="control-label">🖼️ GIF 2 (medio)</label>
      <input type="text" id="inputGif2" value="https://media0.giphy.com/media/v1.Y2lkPTZjMDliOTUyMzl0NTh2ZHhmOHF1Nm45NHNqcmN1bTVrdHNtbDgwbjZpZTFqMno3diZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/11TyfGbDbBv4be/giphy.gif">
    </div>

    <div class="control-box">
      <label class="control-label">🖼️ GIF 3 (final)</label>
      <input type="text" id="inputGif3" value="https://media3.giphy.com/media/v1.Y2lkPTZjMDliOTUybnhtaWRrZDV4bDh6a25hZXpqZG5mczhyNnZld3YybXU3YTNuYXNhNSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/MDJ9IbxxvDUQM/giphy.gif">
    </div>

    <div class="control-box">
      <label class="control-label">🎨 Color de fondo</label>
      <input type="color" id="bgColor" value="#fff0f5">
    </div>

    <div class="control-box">
      <label class="control-label">✍️ Color del texto</label>
      <input type="color" id="textColor" value="#d81b60">
    </div>

    <div class="control-box">
      <label class="control-label">💖 Color de acento</label>
      <input type="color" id="accentColor" value="#e91e63">
    </div>

    <div class="control-box">
      <label class="control-label">🔤 Fuente del título</label>
      <select id="fontTitle">
        <option value="'Georgia', serif">Georgia (Clásica)</option>
        <option value="'Playfair Display', serif">Playfair Display</option>
        <option value="'Dancing Script', cursive">Dancing Script</option>
      </select>
    </div>

    <div class="control-box">
      <label class="control-label">📜 Fuente de la carta</label>
      <select id="fontLetter">
        <option value="'Dancing Script', cursive">Dancing Script</option>
        <option value="'Georgia', serif">Georgia</option>
        <option value="'Playfair Display', serif">Playfair Display</option>
        <option value="'Poppins', sans-serif">Poppins</option>
      </select>
    </div>

    <div class="control-box">
      <label class="control-label">📏 Tamaño de fuente (carta)</label>
      <input type="range" id="fontSize" min="14" max="28" value="19">
      <span class="fontSizeValue" id="fontSizeValue">19px</span>
    </div>
  </div>

  <div class="btn-group">
    <button class="btn btn-preview" onclick="previewCustom()">👁️ Vista previa</button>
    <button class="btn btn-download" onclick="downloadCustom()">💾 Descargar carta</button>
  </div>

  <!-- Vista previa libre -->
  <div id="preview-container">
    <iframe id="preview"></iframe>
  </div>

  <!-- Apoyo -->
  <div class="support-section">
    <div class="support-box">
      <h4>📱 TikTok</h4>
      <p>Sígueme para más proyectos</p>
      <a href="https://www.tiktok.com/@bermat_mods" target="_blank">@bermat_mods</a>
    </div>
    <div class="support-box">
      <h4>💛 Yape</h4>
      <p>Puedes apoyarme con tu voluntad</p>
      <p>930569195</p>
      <p style="font-size:0.9rem; margin-top:10px;">
        ¡Me ayudarías muchísimo a seguir desarrollando proyectos como este!
      </p>
    </div>
  </div>

  <footer>By AnthZz Berrocal • BerMatMods</footer>

  <!-- Modal de descarga -->
  <div id="downloadModal">
    <div class="download-content">
      <div class="close-download" onclick="document.getElementById('downloadModal').style.display='none'">×</div>
      <h3>✅ ¡Carta descargada con éxito!</h3>
      <p>Ya puedes visualizarla desde tu memoria interna.</p>
      <p>¡Compártela con tus seres queridos y hazlos sonreír! 💖</p>
      <p>No te olvides de seguirme en TikTok, dar like y compartir el video.</p>
      <p>¡Gracias por tu apoyo! 🌟</p>
    </div>
  </div>

  <script>
    // Actualización automática
    document.querySelectorAll('input, textarea, select').forEach(el => {
      el.addEventListener('input', previewCustom);
    });

    document.getElementById('fontSize').addEventListener('input', () => {
      document.getElementById('fontSizeValue').textContent = document.getElementById('fontSize').value + 'px';
    });

    // Almacenar el HTML actual para la descarga
    let currentHTML = '';

    function getCustomData() {
      return {
        code: document.getElementById('inputCode').value.trim() || '2050',
        message: document.getElementById('inputMessage').value.trim() || 'Mensaje predeterminado...',
        music: document.getElementById('inputMusic').value.trim() || 'https://files.catbox.moe/s5tmq9.mp3',
        gif1: document.getElementById('inputGif1').value.trim(),
        gif2: document.getElementById('inputGif2').value.trim(),
        gif3: document.getElementById('inputGif3').value.trim(),
        bgColor: document.getElementById('bgColor').value || '#fff0f5',
        textColor: document.getElementById('textColor').value || '#d81b60',
        accentColor: document.getElementById('accentColor').value || '#e91e63',
        fontTitle: document.getElementById('fontTitle').value,
        fontLetter: document.getElementById('fontLetter').value,
        fontSize: document.getElementById('fontSize').value + 'px'
      };
    }

    function hexToRgb(hex) {
      const r = parseInt(hex.slice(1, 3), 16);
      const g = parseInt(hex.slice(3, 5), 16);
      const b = parseInt(hex.slice(5, 7), 16);
      return [r, g, b];
    }

    function buildHTML(data) {
      const safeMessage = JSON.stringify(data.message);
      const safeMusic = JSON.stringify(data.music);
      const safeGif1 = JSON.stringify(data.gif1 || '');
      const safeGif2 = JSON.stringify(data.gif2 || '');
      const safeGif3 = JSON.stringify(data.gif3 || '');
      const safeCode = JSON.stringify(data.code);

      return `<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no" />
  <title>Carta de Amor - Código: ${data.code}</title>
  <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Playfair+Display:wght@700&family=Poppins:wght@400;500;600&family=Georgia&display=swap" rel="stylesheet">
  <style>
    * { margin:0; padding:0; box-sizing:border-box; }
    body {
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, ${data.bgColor}, #f8bbd0, #ffecf0);
      color: ${data.textColor};
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 20px;
      overflow-x: hidden;
      position: relative;
      filter: saturate(1.5);
    }
    .menu-btn {
      position: absolute;
      top: 20px;
      left: 20px;
      width: 52px;
      height: 52px;
      background: rgba(${hexToRgb(data.accentColor).join(',')}, 0.25);
      border-radius: 50%;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      cursor: pointer;
      z-index: 100;
      box-shadow: 0 6px 20px rgba(${hexToRgb(data.accentColor).join(',')}, 0.5);
    }
    .menu-btn span {
      display: block;
      width: 26px;
      height: 3px;
      background: ${data.accentColor};
      margin: 4px 0;
      border-radius: 2px;
    }
    .lock-screen, .main-container {
      text-align: center;
      max-width: 95%;
      padding: 2.2rem 1.8rem;
    }
    .lock-screen h2 {
      font-family: ${data.fontTitle};
      font-size: 2.2rem;
      color: ${data.accentColor};
      margin: 1.2rem 0;
      font-weight: bold;
    }
    .letter {
      font-family: ${data.fontLetter};
      font-size: ${data.fontSize};
      line-height: 1.85;
      color: ${data.textColor};
      text-align: left;
      white-space: pre-line;
      margin: 0;
      font-weight: 600;
    }
    .btn-iniciar {
      margin-top: 1.8rem;
      padding: 1.1rem 2.4rem;
      font-size: 1.35rem;
      font-weight: 700;
      background: linear-gradient(45deg, ${data.accentColor}, #ba68c8, #8e24aa);
      color: white;
      border: none;
      border-radius: 34px;
      cursor: pointer;
      box-shadow: 0 8px 25px rgba(${hexToRgb(data.accentColor).join(',')}, 0.6);
    }
    .final-love-note {
      margin: 2.2rem auto;
      max-width: 420px;
      font-family: ${data.fontLetter};
      font-size: 1.9rem;
      color: ${data.accentColor};
      text-align: center;
      text-shadow: 0 0 12px rgba(${hexToRgb(data.accentColor).join(',')}, 0.5);
      font-weight: 700;
    }
    img {
      max-width: 100%;
      height: auto;
      border-radius: 18px;
      margin: 1.2rem 0;
      box-shadow: 0 6px 18px rgba(0,0,0,0.15);
    }
    footer {
      margin-top: 1.8rem;
      font-style: italic;
      color: ${data.accentColor};
      font-size: 1.2rem;
      font-weight: 700;
    }
  </style>
</head>
<body>

  <!-- Menú de WhatsApp -->
  <div class="menu-btn" onclick="window.open('https://wa.me/51930569195', '_blank')">
    <span></span><span></span><span></span>
  </div>

  <div id="lockScreen" class="lock-screen">
    <h2>🔐 Tu Carta de Amor</h2>
    <p>👇INGRESA EL CÓDIGO DE ACCESO 👇</p>
    ${data.gif1 ? `<img src=${safeGif1} alt="Corazones">` : ''}
    <div id="display" style="font-family:monospace; font-size:1.9rem; color:${data.accentColor}; background:#fff0f5; padding:1.1rem; border-radius:18px; margin:1.2rem auto; width:90%; letter-spacing:4px; font-weight:700;"></div>
    <div class="keypad" style="display:grid; grid-template-columns:repeat(3,1fr); gap:12px; margin:1.2rem 0;">
      ${[1,2,3,4,5,6,7,8,9,0,'/','⌫'].map(k => 
        `<div onclick="${k === '⌫' ? "clearInput()" : `addDigit('${k}')`}" 
             style="padding:1.1rem; background:#ffe6f0; color:${data.accentColor}; border-radius:14px; cursor:pointer; font-weight:700; font-size:1.2rem;">${k}</div>`
      ).join('')}
    </div>
    <button class="btn-iniciar" onclick="submitKey()">Iniciar</button>
    ${data.gif2 ? `<img src=${safeGif2} alt="Bailarina">` : ''}
    <footer>Desarrollado por AnthZz Berrocal • BerMatMods</footer>
  </div>

  <div id="mainContainer" style="display:none;">
    <div style="background:white; border-radius:32px; padding:2.4rem; box-shadow:0 12px 35px rgba(0,0,0,0.25);">
      <h1 style="font-family:${data.fontTitle}; font-size:2.6rem; color:${data.accentColor}; margin-bottom:2rem; font-weight:bold;">Una Carta de Amor 💖</h1>
      <div id="letter" class="letter"></div>
      <footer style="margin-top:2.2rem; font-style:italic; color:${data.accentColor}; font-weight:700;">Con todo mi corazón, siempre tuyo.</footer>
    </div>
    <div class="final-love-note">Te amo muchísimo 💖</div>
    ${data.gif3 ? `<img src=${safeGif3} alt="Explosión">` : ''}
    <footer>Desarrollado por AnthZz Berrocal • BerMatMods</footer>
  </div>

  <audio id="bgMusic" src=${safeMusic} preload="auto"></audio>

  <script>
    let input = '';
    const correctKey = ${safeCode};

    function addDigit(d) { if (input.length < 8) { input += d; updateDisplay(); } }
    function clearInput() { input = ''; updateDisplay(); }
    function updateDisplay() { document.getElementById('display').textContent = input; }
    function submitKey() {
      if (input === correctKey) {
        document.getElementById('lockScreen').style.display = 'none';
        document.getElementById('mainContainer').style.display = 'block';
        typeWriter();
        document.getElementById('bgMusic').play().catch(()=>{});
      } else {
        alert('Código incorrecto. Por favor, verifica.');
        clearInput();
      }
    }

    function getMessage() { return ${safeMessage}; }
    function typeWriter() {
      const el = document.getElementById('letter');
      el.textContent = '';
      let i = 0; const msg = getMessage(); const speed = 38;
      function type() {
        if (i < msg.length) {
          el.textContent += msg.charAt(i);
          i++; setTimeout(type, speed);
        }
      }
      setTimeout(type, 350);
    }
  <\/script>
</body>
</html>`;
    }

    function previewCustom() {
      const data = getCustomData();
      const html = buildHTML(data);
      currentHTML = html; // Guardar para la descarga
      document.getElementById('preview').srcdoc = html;
    }

    function downloadCustom() {
      // Asegurarse de tener el HTML más reciente
      const data = getCustomData();
      const html = buildHTML(data);
      currentHTML = html;

      const blob = new Blob([html], { type: 'text/html;charset=utf-8' });
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = `carta_amor_${data.code}.html`;
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      URL.revokeObjectURL(url);

      // Mostrar mensaje
      document.getElementById('downloadModal').style.display = 'flex';
    }

    // Inicial
    window.onload = () => {
      previewCustom();
    };
  </script>
</body>
</html>
