<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#090909">
  <title>Psngamerent — Marvel's Spider-Man 2</title>
  <style>
    :root{
      --bg:#070707; --panel:#111111; --panel2:#171717; --text:#f5f5f5;
      --muted:#a5a5a5; --red:#e50914; --red2:#ff2530; --green:#25d366;
      --border:#292929; --shadow:0 20px 60px rgba(0,0,0,.45);
    }
    *{box-sizing:border-box}
    html{scroll-behavior:smooth}
    body{
      margin:0;background:
      radial-gradient(circle at 50% -10%,rgba(229,9,20,.22),transparent 38%),
      linear-gradient(180deg,#080808 0%,#050505 100%);
      color:var(--text);font-family:Inter,system-ui,-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif;
      min-height:100vh;
    }
    button,a{font:inherit}
    a{text-decoration:none;color:inherit}
    .wrap{width:min(1100px,92%);margin:auto}
    header{padding:22px 0;position:sticky;top:0;z-index:10;background:rgba(5,5,5,.82);backdrop-filter:blur(14px);border-bottom:1px solid rgba(255,255,255,.06)}
    .nav{display:flex;align-items:center;justify-content:space-between;gap:16px}
    .brand{font-weight:900;letter-spacing:.8px;font-size:22px}
    .brand span{color:var(--red)}
    .gear{
      width:42px;height:42px;border:1px solid var(--border);border-radius:50%;
      background:#111;color:#fff;cursor:pointer;font-size:20px;transition:.2s
    }
    .gear:hover{border-color:var(--red);transform:rotate(25deg)}
    .hero{padding:55px 0 35px;text-align:center}
    .cover{
      width:min(300px,72vw);aspect-ratio:2/3;object-fit:cover;display:block;margin:0 auto 30px;
      border-radius:18px;border:1px solid #333;box-shadow:0 25px 70px rgba(229,9,20,.18);
      background:#151515;
    }
    h1{font-size:clamp(34px,7vw,68px);line-height:1.02;margin:0 0 14px;font-weight:950;letter-spacing:-2px}
    .accent{color:var(--red)}
    .sub{color:var(--muted);max-width:650px;margin:auto;font-size:16px;line-height:1.65}
    .notice{
      margin:28px auto 0;max-width:850px;text-align:left;padding:18px 20px;
      background:linear-gradient(135deg,rgba(229,9,20,.13),rgba(255,255,255,.025));
      border:1px solid rgba(229,9,20,.38);border-left:4px solid var(--red);border-radius:14px;
      color:#ddd;line-height:1.6
    }
    .section-title{font-size:27px;margin:48px 0 18px;text-align:center}
    .status{
      display:flex;justify-content:center;align-items:center;gap:9px;margin:16px auto 30px;
      color:#ddd;font-weight:700
    }
    .dot{width:10px;height:10px;border-radius:50%;background:var(--green);box-shadow:0 0 14px var(--green)}
    .dot.sold{background:var(--red);box-shadow:0 0 14px var(--red)}
    .plans{display:grid;grid-template-columns:repeat(3,1fr);gap:18px}
    .card{
      position:relative;background:linear-gradient(180deg,#151515,#0f0f0f);border:1px solid var(--border);
      border-radius:18px;padding:27px 22px;box-shadow:var(--shadow);transition:.2s
    }
    .card:hover{transform:translateY(-4px);border-color:#444}
    .card.popular{border-color:var(--red);box-shadow:0 20px 70px rgba(229,9,20,.14)}
    .badge{position:absolute;right:16px;top:16px;background:var(--red);padding:6px 10px;border-radius:999px;font-size:11px;font-weight:900}
    .days{font-size:20px;font-weight:800}
    .price{font-size:38px;font-weight:950;margin:12px 0 20px}
    .price small{font-size:14px;color:var(--muted);font-weight:600}
    .rent{
      width:100%;border:0;border-radius:11px;padding:13px;background:var(--red);color:#fff;
      font-weight:900;cursor:pointer;transition:.2s
    }
    .rent:hover{background:var(--red2);transform:translateY(-1px)}
    .rent:disabled{background:#333;color:#777;cursor:not-allowed;transform:none}
    .sold-note{text-align:center;color:#aaa;font-size:13px;margin-top:11px;min-height:20px}
    .contact{text-align:center;padding:55px 0 35px}
    .wa{
      display:inline-flex;align-items:center;justify-content:center;gap:9px;background:var(--green);
      color:#061b0c;padding:13px 21px;border-radius:11px;font-weight:900;margin:10px 0
    }
    .contact p{color:#aaa;margin:8px 0}
    footer{border-top:1px solid var(--border);padding:22px 0;text-align:center;color:#666;font-size:13px}
    .overlay{
      position:fixed;inset:0;background:rgba(0,0,0,.78);backdrop-filter:blur(8px);
      display:none;align-items:center;justify-content:center;padding:18px;z-index:50
    }
    .overlay.show{display:flex}
    .modal{
      width:min(500px,100%);max-height:92vh;overflow:auto;background:#101010;border:1px solid #333;
      border-radius:20px;padding:24px;box-shadow:0 30px 100px #000
    }
    .modal-head{display:flex;align-items:center;justify-content:space-between;gap:15px}
    .modal h2{margin:0;font-size:23px}
    .close{border:0;background:#222;color:#fff;border-radius:9px;width:36px;height:36px;cursor:pointer}
    .selected{margin:18px 0;padding:15px;border-radius:12px;background:#171717;border:1px solid #2a2a2a}
    .selected strong{font-size:20px}
    .qr{
      width:min(280px,80vw);aspect-ratio:1;object-fit:contain;display:block;margin:18px auto;
      background:#fff;padding:10px;border-radius:14px
    }
    .upi{text-align:center;background:#171717;border:1px dashed #444;border-radius:10px;padding:11px;word-break:break-all}
    .steps{padding-left:20px;color:#ccc;line-height:1.7}
    .steps li{margin:5px 0}
    .wa-modal{display:block;text-align:center;background:var(--green);color:#061b0c;padding:12px;border-radius:10px;font-weight:900;margin-top:18px}
    .admin .field{margin:17px 0}
    .admin label{display:block;color:#bbb;font-size:13px;margin-bottom:8px}
    select,.admin input{
      width:100%;background:#171717;color:#fff;border:1px solid #333;border-radius:10px;padding:12px;outline:none
    }
    .admin button.save{width:100%;border:0;background:var(--red);color:#fff;border-radius:10px;padding:13px;font-weight:900;cursor:pointer}
    .admin-note{font-size:12px;color:#777;line-height:1.5;margin-top:14px}
    .timer{color:#ffb3b6;font-weight:800}
    @media(max-width:760px){
      .plans{grid-template-columns:1fr}
      .hero{padding-top:38px}
      .card{padding:23px 19px}
      header{position:static}
    }
  </style>
</head>
<body>
  <header>
    <div class="wrap nav">
      <div class="brand">PS<span>NGAMERENT</span></div>
      <button class="gear" id="gearBtn" aria-label="Open admin panel">⚙</button>
    </div>
  </header>

  <main class="wrap">
    <section class="hero">
      <!-- Put spiderman2-cover.jpg in the same folder as this HTML file -->
      <img class="cover" src="spiderman2-cover.jpg" alt="Marvel's Spider-Man 2 cover"
           onerror="this.style.display='none'">
      <h1>Marvel's <span class="accent">Spider-Man 2</span></h1>
      <p class="sub">Rent access for your preferred duration. Simple plans, clear pricing.</p>

      <div class="notice">
        <strong>Notice:</strong> This is my first time running this service, so currently only Marvel's Spider-Man 2 is available.
        More games will be added soon. Sorry for the limited options and thank you for your understanding!
      </div>
    </section>

    <section>
      <h2 class="section-title">Choose Your Plan</h2>
      <div class="status">
        <span class="dot" id="statusDot"></span>
        <span id="statusText">Available</span>
        <span id="timer" class="timer"></span>
      </div>

      <div class="plans">
        <article class="card">
          <div class="days">7 Days</div>
          <div class="price">₹200 <small>/ 7 days</small></div>
          <button class="rent" data-days="7" data-price="200">Rent Now</button>
          <div class="sold-note"></div>
        </article>

        <article class="card popular">
          <div class="badge">POPULAR</div>
          <div class="days">14 Days</div>
          <div class="price">₹335 <small>/ 14 days</small></div>
          <button class="rent" data-days="14" data-price="335">Rent Now</button>
          <div class="sold-note"></div>
        </article>

        <article class="card">
          <div class="days">30 Days</div>
          <div class="price">₹500 <small>/ 30 days</small></div>
          <button class="rent" data-days="30" data-price="500">Rent Now</button>
          <div class="sold-note"></div>
        </article>
      </div>
    </section>

    <section class="contact">
      <h2 class="section-title">Need Help?</h2>
      <p>Contact only via WhatsApp message. No calls please.</p>
      <a class="wa" href="https://wa.me/qr/2YRY23DVM5YLA1" target="_blank" rel="noopener">💬 Message on WhatsApp</a>
    </section>
  </main>

  <footer>© <span id="year"></span> Psngamerent</footer>

  <!-- Payment popup -->
  <div class="overlay" id="paymentOverlay">
    <div class="modal">
      <div class="modal-head">
        <h2>Complete Payment</h2>
        <button class="close" data-close="paymentOverlay">✕</button>
      </div>
      <div class="selected">
        <div>Selected plan</div>
        <strong id="selectedPlan">14 Days</strong>
        <span id="selectedPrice"> — ₹335</span>
      </div>

      <!-- Put phonepe-qr.png in the same folder as this HTML file -->
      <img class="qr" src="phonepe-qr.png" alt="PhonePe QR code"
           onerror="this.alt='QR image not found — add phonepe-qr.png beside this HTML file'">

      <div class="upi"><strong>UPI ID</strong><br>8319426596.wallet@phonepe</div>

      <ol class="steps">
        <li>Open PhonePe and scan the QR code, or use the UPI ID above.</li>
        <li>Pay the exact amount shown for your selected plan.</li>
        <li>Take a screenshot of the successful payment.</li>
        <li>Send the payment screenshot via WhatsApp to confirm your rental.</li>
      </ol>

      <a class="wa-modal" href="https://wa.me/qr/2YRY23DVM5YLA1" target="_blank" rel="noopener">
        Send Screenshot on WhatsApp
      </a>
    </div>
  </div>

  <!-- Admin panel -->
  <div class="overlay" id="adminOverlay">
    <div class="modal admin">
      <div class="modal-head">
        <h2>Admin Panel</h2>
        <button class="close" data-close="adminOverlay">✕</button>
      </div>

      <div class="field">
        <label for="adminStatus">Service Status</label>
        <select id="adminStatus">
          <option value="available">Available</option>
          <option value="soldout">Sold Out</option>
        </select>
      </div>

      <div class="field">
        <label for="adminDays">Sold Out Duration</label>
        <select id="adminDays">
          <option value="7">7 Days</option>
          <option value="14">14 Days</option>
          <option value="30">30 Days</option>
        </select>
      </div>

      <div class="field">
        <label for="adminStart">Sold Out Started (optional)</label>
        <input id="adminStart" type="datetime-local">
      </div>

      <button class="save" id="saveAdmin">Save Settings</button>
      <div class="admin-note">
        This is a client-side admin panel: settings are saved only in this browser using localStorage.
        It is not a secure server-side admin system. For a real public store, use server authentication/database controls.
      </div>
    </div>
  </div>

  <script>
    const KEY = "psngamerent_settings_v1";
    const defaults = {
      status: "available",
      days: 14,
      start: null
    };

    function getSettings(){
      try { return {...defaults, ...(JSON.parse(localStorage.getItem(KEY)) || {})}; }
      catch(e){ return {...defaults}; }
    }

    function saveSettings(s){
      localStorage.setItem(KEY, JSON.stringify(s));
    }

    function formatRemaining(ms){
      if(ms <= 0) return "0d 0h";
      const totalHours = Math.floor(ms / 3600000);
      const days = Math.floor(totalHours / 24);
      const hours = totalHours % 24;
      return `${days}d ${hours}h remaining`;
    }

    function renderStatus(){
      const s = getSettings();
      const dot = document.getElementById("statusDot");
      const text = document.getElementById("statusText");
      const timer = document.getElementById("timer");
      const buttons = document.querySelectorAll(".rent");
      const notes = document.querySelectorAll(".sold-note");

      if(s.status === "available"){
        dot.classList.remove("sold");
        text.textContent = "Available";
        timer.textContent = "";
        buttons.forEach(b => b.disabled = false);
        notes.forEach(n => n.textContent = "");
        return;
      }

      dot.classList.add("sold");
      text.textContent = "Sold Out";

      let remaining = s.days * 24 * 60 * 60 * 1000;
      if(s.start){
        const end = new Date(s.start).getTime() + remaining;
        const left = end - Date.now();
        if(left <= 0){
          s.status = "available";
          s.start = null;
          saveSettings(s);
          renderStatus();
          return;
        }
        remaining = left;
      }

      timer.textContent = `• ${formatRemaining(remaining)}`;
      buttons.forEach(b => b.disabled = true);
      notes.forEach(n => n.textContent = "Currently unavailable");
    }

    document.querySelectorAll(".rent").forEach(btn => {
      btn.addEventListener("click", () => {
        if(btn.disabled) return;
        document.getElementById("selectedPlan").textContent = `${btn.dataset.days} Days`;
        document.getElementById("selectedPrice").textContent = ` — ₹${btn.dataset.price}`;
        document.getElementById("paymentOverlay").classList.add("show");
      });
    });

    document.getElementById("gearBtn").addEventListener("click", () => {
      const s = getSettings();
      document.getElementById("adminStatus").value = s.status;
      document.getElementById("adminDays").value = s.days;
      document.getElementById("adminStart").value = s.start || "";
      document.getElementById("adminOverlay").classList.add("show");
    });

    document.getElementById("saveAdmin").addEventListener("click", () => {
      const status = document.getElementById("adminStatus").value;
      const days = Number(document.getElementById("adminDays").value);
      let start = document.getElementById("adminStart").value || null;

      if(status === "soldout" && !start){
        const local = new Date();
        local.setMinutes(local.getMinutes() - local.getTimezoneOffset());
        start = local.toISOString().slice(0,16);
      }
      if(status === "available") start = null;

      saveSettings({status, days, start});
      renderStatus();
      document.getElementById("adminOverlay").classList.remove("show");
    });

    document.querySelectorAll("[data-close]").forEach(btn => {
      btn.addEventListener("click", () => {
        document.getElementById(btn.dataset.close).classList.remove("show");
      });
    });

    document.querySelectorAll(".overlay").forEach(overlay => {
      overlay.addEventListener("click", e => {
        if(e.target === overlay) overlay.classList.remove("show");
      });
    });

    document.addEventListener("keydown", e => {
      if(e.key === "Escape")
        document.querySelectorAll(".overlay").forEach(o => o.classList.remove("show"));
    });

    document.getElementById("year").textContent = new Date().getFullYear();
    renderStatus();
    setInterval(renderStatus, 30000);
  </script>
</body>
</html>
