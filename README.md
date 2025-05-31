<html>
<head>
  <title>Graduation Wall</title>
  <style>
    body { font-family: Arial; padding: 20px; background: #f8f9fa; }
    .message { background: white; padding: 10px; border-radius: 8px; margin-bottom: 10px; box-shadow: 0 2px 4px rgba(0,0,0,0.1); }
  </style>
</head>
<body>

  <h1>🎓 Graduation Wall</h1>
  <textarea id="msgInput" placeholder="Write your message here..." rows="4" style="width:100%"></textarea><br>
  <button onclick="submitMessage()">Submit</button>

  <div id="messages"></div>

  <script>
    const SHEET_URL = 'https://script.google.com/macros/library/d/1M2ev74MMtwxWy3hJ7RDgrTr_sqgOcudm_FLrH-8dIgk6yA3l63Zo6A9W/2';

loadMessages()

    async function submitMessage() {
      const msg = document.getElementById('msgInput').value.trim();
      if (!msg) return;
      await fetch(SHEET_URL, {
        method: 'POST',
        body: JSON.stringify({ message: msg }),
        headers: { 'Content-Type': 'application/json' }
      });
      document.getElementById('msgInput').value = '';
      loadMessages();
    }

    async function loadMessages() {
      const res = await fetch(SHEET_URL);
      const data = await res.json();
      const container = document.getElementById('messages');
      container.innerHTML = '';
      data.forEach(d => {
        const div = document.createElement('div');
        div.className = 'message';
        div.textContent = d.message;
        container.appendChild(div);
      });
    }

    loadMessages();
  </script>

</body>
</html>

