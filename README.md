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
  <textarea id="msgInput" placeholder="Please Email the message to 'emailGemail.ca' to be put on here" rows="4" style="width:100%"></textarea><br>
  <button onclick="submitMessage()">Online Submission is Still Under Construction, will be here later</button>

  <div id="messages"></div>

  <script>
    const SHEET_URL = 'https://script.google.com/macros/s/AKfycbxSigcYK7wdPbtCP7KqcYbEcAHbEBgU09XCqfAyN_cjBVmGSLPzudJ1CaMtSG-mJUvF/exec';

     async function submitMessage() {
      const msg = document.getElementById('msgInput').value.trim();
      if (!msg) {return;}
      await fetch(SHEET_URL, {
        method: 'dePost',
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

