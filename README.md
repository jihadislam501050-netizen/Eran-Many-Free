<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Earn Many Free</title>
  <script src="https://telegram.org/js/telegram-web-app.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@600;700&display=swap" rel="stylesheet">
  <style>
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #0f0c29, #302b63);
      color: #fff;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 0 10px 100px;
      box-sizing: border-box;
      overflow: hidden;
      position: relative;
    }
    /* স্ক্রিনের চারপাশে লাল-নীল মিশ্রণ লাইন */
    body::before {
      content: "";
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      border: 4px solid transparent;
      border-image: linear-gradient(45deg, #ff416c, #4a90e2, #ff4b2b, #00d4ff) 1;
      pointer-events: none;
      z-index: 9999;
    }

    /* Profile Bar */
    .profile-bar {
      width: 100%;
      background: linear-gradient(90deg, #ff416c, #ff4b2b);
      padding: 15px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      border-radius: 0 0 20px 20px;
      box-shadow: 0 6px 20px rgba(0,0,0,0.5);
      margin-bottom: 15px;
    }
    .profile-left { display: flex; align-items: center; }
    .profile-avatar {
      width: 50px;
      height: 50px;
      background: #fff;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.8em;
      margin-right: 12px;
      box-shadow: 0 0 15px rgba(255,255,255,0.6);
      border: 3px solid #fff;
      cursor: pointer;
      transition: all 0.3s;
    }
    .profile-avatar:hover { transform: scale(1.1); }
    .profile-info h2 {
      margin: 0;
      font-size: 1.4em;
      font-weight: 700;
    }
    .profile-info p {
      margin: 4px 0 0;
      font-size: 1em;
      font-weight: 600;
    }
    .support-btn {
      width: 45px;
      height: 45px;
      background: #fff;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.6em;
      box-shadow: 0 0 15px rgba(255,255,255,0.6);
      cursor: pointer;
      transition: all 0.3s;
    }
    .support-btn:hover { transform: scale(1.1); }

    #coinCount {
      font-size: 2.6em;
      font-weight: 800;
      margin: 10px 0 20px;
      text-align: center;
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 10px;
      width: 100%;
      max-width: 320px;
      position: relative;
    }
    .small-card {
      background: linear-gradient(135deg, #ff416c, #ff4b2b);
      border-radius: 10px;
      padding: 10px 6px;
      text-align: center;
      box-shadow: 0 5px 15px rgba(0,0,0,0.4);
      cursor: pointer;
      transition: all 0.3s ease;
      border: 1px solid rgba(255,255,255,0.3);
      position: relative;
    }
    .small-card:hover {
      transform: translateY(-4px);
      box-shadow: 0 10px 25px rgba(0,0,0,0.6);
    }
    .card-icon { font-size: 2em; margin-bottom: 4px; }
    .card-title { font-size: 1em; font-weight: 700; margin-bottom: 3px; }
    .card-desc { font-size: 0.75em; opacity: 0.9; }

    /* Countdown Circle - বক্সের পাশে */
    .countdown-circle {
      position: absolute;
      width: 60px;
      height: 60px;
      border-radius: 50%;
      border: 6px solid #ff416c;
      border-top: 6px solid transparent;
      animation: spin 15s linear forwards;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 1.5em;
      font-weight: bold;
      color: #ff416c;
      background: rgba(0,0,0,0.5);
      box-shadow: 0 0 15px #ff416c;
      pointer-events: none;
      opacity: 0;
      transition: opacity 0.3s;
    }
    @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

    /* Bottom Navigation */
    .bottom-nav {
      width: 100%;
      max-width: 320px;
      display: flex;
      justify-content: space-around;
      margin-top: auto;
      padding: 10px 0;
      background: linear-gradient(90deg, #ff416c, #ff4b2b);
      border-radius: 20px;
      position: fixed;
      bottom: 10px;
      left: 50%;
      transform: translateX(-50%);
      box-shadow: 0 -6px 20px rgba(0,0,0,0.5);
    }
    .nav-btn {
      background: #fff;
      border: none;
      border-radius: 35px;
      padding: 10px 18px;
      color: #ff416c;
      font-size: 0.95em;
      font-weight: 700;
      cursor: pointer;
      transition: all 0.3s;
      box-shadow: 0 4px 12px rgba(0,0,0,0.4);
    }
    .nav-btn:hover { transform: scale(1.1); background: #ff416c; color: #fff; }

    /* Withdraw Modal */
    .modal {
      display: none;
      position: fixed;
      top: 0; left: 0; width: 100%; height: 100%;
      background: rgba(0,0,0,0.8);
      justify-content: center;
      align-items: center;
      z-index: 100;
    }
    .modal-content {
      background: linear-gradient(135deg, #ff416c, #ff4b2b);
      border-radius: 25px;
      padding: 30px 25px;
      width: 90%;
      max-width: 360px;
      text-align: center;
      color: #fff;
      box-shadow: 0 20px 60px rgba(255,75,43,0.7);
      position: relative;
    }
    .close { position: absolute; top: 12px; right: 18px; font-size: 2.2em; cursor: pointer; color: #fff; }
    .payment-box {
      background: rgba(255,255,255,0.2);
      border-radius: 16px;
      padding: 16px;
      margin: 12px 0;
      cursor: pointer;
      font-size: 1.2em;
      font-weight: bold;
      transition: all 0.4s;
      border: 2px solid #fff;
    }
    .payment-box:hover { background: rgba(255,255,255,0.3); transform: scale(1.06); }
    .payment-box.selected {
      background: #fff;
      color: #ff416c;
      border: 3px solid #ffd700;
      box-shadow: 0 0 30px rgba(255,215,0,0.8);
      transform: scale(1.1);
    }
    input {
      width: 100%;
      padding: 12px;
      margin: 10px 0;
      border-radius: 12px;
      border: 1px solid #fff;
      font-size: 1em;
      box-sizing: border-box;
      background: rgba(255,255,255,0.2);
      color: #fff;
    }
    .submit-btn {
      background: linear-gradient(45deg, #ffd700, #ff416c);
      padding: 14px;
      border: none;
      border-radius: 40px;
      font-size: 1.3em;
      font-weight: bold;
      color: #000;
      cursor: pointer;
      width: 100%;
      margin-top: 20px;
      box-shadow: 0 8px 30px rgba(255,215,0,0.6);
      transition: all 0.4s;
    }
    .submit-btn:hover { transform: scale(1.08); box-shadow: 0 12px 40px rgba(255,215,0,0.9); }
  </style>
</head>
<body>
  <!-- Profile Bar with Support Button -->
  <div class="profile-bar">
    <div class="profile-left">
      <div class="profile-avatar" id="profileAvatar">👤</div>
      <div class="profile-info">
        <h2 id="username">Player</h2>
        <p id="balance">0 Coins (০ টাকা)</p>
      </div>
    </div>
    <div class="support-btn" onclick="openSupport()">💬</div>
  </div>

  <div id="coinCount">0 Coins</div>

  <div class="grid">
    <div class="small-card" onclick="openAdLink(this)">
      <div class="card-icon">👆</div>
      <div class="card-title">Tap</div>
      <div class="card-desc">Earn</div>
    </div>

    <div class="small-card" onclick="openAdLink(this)">
      <div class="card-icon">🎡</div>
      <div class="card-title">Spin</div>
      <div class="card-desc">Rewards</div>
    </div>

    <div class="small-card" onclick="openAdLink(this)">
      <div class="card-icon">✅</div>
      <div class="card-title">Tasks</div>
      <div class="card-desc">Daily</div>
    </div>

    <div class="small-card" id="dailyCard" onclick="dailyCheckIn(this)">
      <div class="card-icon">📅</div>
      <div class="card-title">Check-in</div>
      <div class="card-desc">Bonus</div>
    </div>

    <div class="small-card" onclick="openAdLink(this)">
      <div class="card-icon">👥</div>
      <div class="card-title">Refer</div>
      <div class="card-desc">+5000</div>
    </div>

    <div class="small-card" onclick="openAdLink(this)">
      <div class="card-icon">📺</div>
      <div class="card-title">Ads</div>
      <div class="card-desc">+5000</div>
    </div>
  </div>

  <!-- Bottom Navigation -->
  <div class="bottom-nav">
    <button class="nav-btn" onclick="alert('Profile')">Profile</button>
    <button class="nav-btn" onclick="copyReferral()">Refer</button>
    <button class="nav-btn" onclick="openWithdraw()">Withdraw</button>
  </div>

  <!-- Withdraw Modal -->
  <div id="withdrawModal" class="modal">
    <div class="modal-content">
      <span class="close" onclick="closeModal()">&times;</span>
      <h2>Withdraw Earnings</h2>
      <p style="color:#fff; margin-bottom:20px;">১০০০ Coins = ১ টাকা<br>Minimum Withdraw: ৫০,০০০ Coins (৫০ টাকা)</p>

      <div id="paymentOptions">
        <div class="payment-box" onclick="selectPayment(this)">বিকাশ</div>
        <div class="payment-box" onclick="selectPayment(this)">নগদ</div>
        <div class="payment-box" onclick="selectPayment(this)">রকেট</div>
        <div class="payment-box" onclick="openSupport()">সাপোর্ট</div>
      </div>

      <input type="number" id="withdrawAmount" placeholder="Coins (e.g. 50000)" min="50000">
      <input type="text" id="accountNumber" placeholder="Account Number">

      <button class="submit-btn" onclick="submitWithdraw()">Submit Withdraw</button>
    </div>
  </div>

  <script>
    const tg = window.Telegram.WebApp;
    tg.ready();
    tg.expand();

    const user = tg.initDataUnsafe.user;
    if (user) document.getElementById('username').textContent = user.first_name || 'Player';

    let coins = localStorage.getItem('coins') ? parseInt(localStorage.getItem('coins')) : 0;
    let lastCheckIn = localStorage.getItem('lastCheckIn') ? parseInt(localStorage.getItem('lastCheckIn')) : 0;

    function updateBalance() {
      const taka = (coins / 1000).toFixed(2);
      document.getElementById('balance').textContent = coins.toLocaleString() + ' Coins (' + taka + ' টাকা)';
      document.getElementById('coinCount').textContent = coins.toLocaleString() + ' Coins';
      localStorage.setItem('coins', coins);
    }
    updateBalance();

    // Open Ad Link with Countdown Circle beside the card
    function openAdLink(card) {
      const adUrl = "https://www.effectivegatecpm.com/p97vd6w2hg?key=ef991fb8cb704dd56803de4793fb7ff6";
      const win = window.open(adUrl, '_blank');

      if (win) {
        // Create countdown circle beside the clicked card
        const circle = document.createElement('div');
        circle.className = 'countdown-circle';
        circle.style.position = 'absolute';
        circle.style.right = '-80px';
        circle.style.top = '50%';
        circle.style.transform = 'translateY(-50%)';
        circle.textContent = '15';
        card.appendChild(circle);

        let timeLeft = 15;

        const timer = setInterval(() => {
          timeLeft--;
          circle.textContent = timeLeft;
          if (timeLeft <= 0) {
            clearInterval(timer);
            circle.remove();
            coins += 500;
            updateBalance();
            alert("+৫০০ কয়েন অ্যাড হয়েছে! অ্যাড দেখার জন্য ধন্যবাদ! 🎉");
          }
        }, 1000);
      } else {
        alert("পপ-আপ ব্লক করা হয়েছে! ব্রাউজারে পপ-আপ অনুমতি দিন।");
      }
    }

    // Daily Check-in
    function dailyCheckIn(card) {
      const now = Date.now();
      if (now - lastCheckIn < 24 * 60 * 60 * 1000) {
        alert("আজকের চেক-ইন ইতিমধ্যে করা হয়েছে! আগামীকাল আবার চেষ্টা করুন।");
      } else {
        openAdLink(card);
        lastCheckIn = now;
        localStorage.setItem('lastCheckIn', lastCheckIn);
      }
    }

    // Support Chat
    function openSupport() {
      window.open("https://t.me/ZIHAD_BRAND_VIP", "_blank");
      alert("সাপোর্ট চ্যাট ওপেন হচ্ছে... @ZIHAD_BRAND_VIP এ মেসেজ করুন! 💬");
    }

    // Referral Copy
    function copyReferral() {
      const refLink = "https://t.me/EarnManyFreeBot?start=994068";
      navigator.clipboard.writeText(refLink);
      alert("Referral Link Copied!\n" + refLink + "\nপ্রতি রেফারেলে +5000 কয়েন পাবেন! 👥");
    }

    // Withdraw
    function openWithdraw() { document.getElementById('withdrawModal').style.display = 'flex'; }
    function closeModal() { document.getElementById('withdrawModal').style.display = 'none'; }
    function selectPayment(el) {
      document.querySelectorAll('.payment-box').forEach(opt => opt.classList.remove('selected'));
      el.classList.add('selected');
    }
    function submitWithdraw() {
      const amount = parseInt(document.getElementById('withdrawAmount').value);
      const account = document.getElementById('accountNumber').value;
      const selected = document.querySelector('.payment-box.selected');

      if (!amount || amount < 50000) return alert("Minimum 50,000 Coins (৫০ টাকা)!");
      if (!selected) return alert("পেমেন্ট মেথড সিলেক্ট করুন!");
      if (!account) return alert("অ্যাকাউন্ট নম্বর দিন!");

      const taka = (amount / 1000).toFixed(2);
      alert(`Withdraw Requested!\nCoins: ${amount}\nTaka: ${taka} টাকা\nMethod: ${selected.textContent}\nAccount: ${account}`);
      closeModal();
    }
  </script>
</body>
</html>
