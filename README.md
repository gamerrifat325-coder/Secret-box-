<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#b5121b">
<title>RTI VOICE - News & Media</title>

<style>
:root {
  --red:#b5121b;
  --dark:#20232b;
  --bg:#f4f5f7;
  --white:#fff;
  --gray:#78818e;
  --border:#e7e9ee;
}
* {box-sizing:border-box;margin:0;padding:0}
body {
  font-family:Arial,sans-serif;
  background:var(--bg);
  color:var(--dark);
}
button,input,textarea,select {font:inherit}
button {cursor:pointer}
header {
  background:white;
  height:65px;
  display:flex;
  align-items:center;
  justify-content:space-between;
  padding:0 5%;
  position:sticky;
  top:0;
  z-index:20;
  border-bottom:1px solid var(--border);
}
.logo {
  font-size:24px;
  font-weight:900;
  color:var(--red);
}
.logo span {color:var(--dark)}
.header-actions {display:flex;gap:10px;align-items:center}
.btn {
  background:var(--red);
  color:white;
  border:0;
  padding:11px 17px;
  border-radius:9px;
  font-weight:bold;
}
.btn-outline {
  background:white;
  border:1px solid var(--red);
  color:var(--red);
}
.container {
  max-width:1150px;
  margin:22px auto;
  padding:0 14px;
}
.layout {
  display:grid;
  grid-template-columns:220px minmax(0,1fr) 230px;
  gap:18px;
}
.card {
  background:white;
  border:1px solid var(--border);
  border-radius:15px;
  padding:17px;
  margin-bottom:15px;
}
.sidebar {
  position:sticky;
  top:80px;
  height:max-content;
}
.menu-item {
  width:100%;
  border:0;
  background:white;
  text-align:left;
  padding:13px 10px;
  border-radius:9px;
  color:var(--dark);
  font-weight:600;
  display:flex;
  gap:10px;
  align-items:center;
}
.menu-item:hover,.menu-item.active {
  background:#fff0f0;
  color:var(--red);
}
.hero {
  background:linear-gradient(120deg,#8f0710,#e43a42);
  color:white;
  padding:27px;
  border-radius:15px;
  margin-bottom:16px;
}
.hero h1 {font-size:27px;margin-bottom:10px}
.hero p {line-height:1.6}
.quick-grid {
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:10px;
}
.quick {
  text-align:center;
  border:1px solid var(--border);
  padding:14px 5px;
  border-radius:12px;
  cursor:pointer;
  background:white;
}
.quick:hover {background:#fff0f0}
.quick div {font-size:25px;margin-bottom:6px}
.quick b {font-size:12px}
.search {
  width:100%;
  padding:13px;
  border:1px solid var(--border);
  border-radius:10px;
  outline:none;
  margin-bottom:15px;
}
.post-head {
  display:flex;
  align-items:center;
  gap:10px;
  margin-bottom:14px;
}
.avatar {
  width:42px;
  height:42px;
  border-radius:50%;
  display:grid;
  place-items:center;
  background:#ffeded;
  color:var(--red);
  font-weight:bold;
}
.muted {color:var(--gray);font-size:12px}
.post-image {
  width:100%;
  max-height:350px;
  object-fit:cover;
  border-radius:10px;
  margin:12px 0;
}
.post-actions {
  display:flex;
  justify-content:space-around;
  border-top:1px solid var(--border);
  padding-top:13px;
  margin-top:12px;
  gap:5px;
}
.post-actions button {
  border:0;
  background:white;
  color:#667080;
  font-size:13px;
}
.post-actions button:hover {color:var(--red)}
.section-title {
  font-size:22px;
  margin-bottom:16px;
}
.field {margin:13px 0}
.field label {
  display:block;
  font-weight:bold;
  font-size:14px;
  margin-bottom:7px;
}
.field input,.field textarea,.field select {
  width:100%;
  border:1px solid #dce0e6;
  border-radius:9px;
  padding:13px;
  outline:none;
  background:white;
}
.field textarea {min-height:120px;resize:vertical}
.field input:focus,.field textarea:focus {
  border-color:var(--red);
}
.stats {
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:10px;
  margin-bottom:15px;
}
.stat {
  background:white;
  padding:15px;
  border:1px solid var(--border);
  border-radius:12px;
  text-align:center;
}
.stat h2 {color:var(--red);font-size:22px}
.stat p {font-size:12px;color:var(--gray)}
.list-item {
  padding:15px;
  border-bottom:1px solid var(--border);
  cursor:pointer;
}
.list-item:last-child {border:0}
.list-item:hover {background:#fff7f7}
.badge {
  display:inline-block;
  background:#fff0f0;
  color:var(--red);
  padding:5px 9px;
  border-radius:20px;
  font-size:11px;
  font-weight:bold;
}
.plan {
  border:1px solid var(--border);
  padding:20px;
  border-radius:14px;
  margin-bottom:13px;
}
.plan h3 {color:var(--red);margin-bottom:10px}
.plan h2 {font-size:27px;margin:10px 0}
.plan p {color:var(--gray);line-height:1.8}
.hidden {display:none!important}
.empty {
  text-align:center;
  padding:35px;
  color:var(--gray);
}
footer {
  text-align:center;
  padding:25px;
  color:var(--gray);
  font-size:12px;
}
.bottom-nav {
  display:none;
}
#toast {
  position:fixed;
  bottom:80px;
  left:50%;
  transform:translateX(-50%);
  background:#222;
  color:white;
  padding:12px 20px;
  border-radius:9px;
  z-index:100;
  display:none;
  max-width:90%;
}
@media(max-width:850px) {
  .layout {grid-template-columns:1fr}
  .left-sidebar,.right-sidebar {display:none}
  .container {margin:12px auto;padding:0 10px}
  header {padding:0 14px}
  .bottom-nav {
    display:flex;
    position:fixed;
    bottom:0;
    left:0;
    right:0;
    height:65px;
    background:white;
    border-top:1px solid var(--border);
    justify-content:space-around;
    align-items:center;
    z-index:30;
  }
  .bottom-nav button {
    border:0;
    background:white;
    color:var(--gray);
    font-size:10px;
    display:flex;
    flex-direction:column;
    align-items:center;
    gap:4px;
  }
  .bottom-nav button span {font-size:21px}
  body {padding-bottom:65px}
  .hero h1 {font-size:24px}
}
</style>
</head>

<body>

<header>
  <div class="logo">RTI <span>VOICE</span></div>
  <div class="header-actions">
    <button class="btn btn-outline" onclick="showPage('notifications')">🔔</button>
    <button class="btn" onclick="showPage('login')" id="accountBtn">Login</button>
  </div>
</header>

<div class="container">
<div class="layout">

<!-- LEFT MENU -->
<aside class="sidebar left-sidebar">
  <div class="card">
    <div class="post-head">
      <div class="avatar">RV</div>
      <div><b>RTI VOICE</b><p class="muted">News Network</p></div>
    </div>
    <div id="leftMenu"></div>
  </div>
</aside>

<!-- MAIN CONTENT -->
<main>

<!-- HOME -->
<section id="home" class="page">
  <div class="hero">
    <h1>Welcome to RTI VOICE</h1>
    <p>Your Voice, Your News, Your Network.</p>
    <br>
    <button class="btn" style="background:white;color:#a00"
      onclick="showPage('post')">+ Publish News</button>
  </div>

  <div class="card">
    <h3 style="margin-bottom:15px">Quick Access</h3>
    <div class="quick-grid">
      <div class="quick" onclick="showPage('post')"><div>📰</div><b>Post News</b></div>
      <div class="quick" onclick="showPage('live')"><div>🔴</div><b>Live</b></div>
      <div class="quick" onclick="showPage('epaper')"><div>📖</div><b>E-Paper</b></div>
      <div class="quick" onclick="showPage('ecommerce')"><div>🛍️</div><b>E-Commerce</b></div>
      <div class="quick" onclick="showPage('network')"><div>👥</div><b>Network</b></div>
      <div class="quick" onclick="showPage('wallet')"><div>💰</div><b>Wallet</b></div>
      <div class="quick" onclick="showPage('plans')"><div>⭐</div><b>Plans</b></div>
      <div class="quick" onclick="showPage('ads')"><div>📢</div><b>Advertisement</b></div>
    </div>
  </div>

  <input class="search" id="searchBox"
    placeholder="🔍 Search news..."
    oninput="renderPosts()">

  <div id="feed"></div>
</section>

<!-- FEED -->
<section id="feedPage" class="page hidden">
  <h2 class="section-title">News Feed</h2>
  <div id="feed2"></div>
</section>

<!-- POST NEWS -->
<section id="post" class="page hidden">
  <div class="card">
    <h2 class="section-title">📰 Publish Your News</h2>
    <form id="newsForm">
      <div class="field">
        <label>News Title *</label>
        <input id="newsTitle" required placeholder="Enter news title">
      </div>
      <div class="field">
        <label>News Description *</label>
        <textarea id="newsDescription" required
          placeholder="Write your news here..."></textarea>
      </div>
      <div class="field">
        <label>Report Category</label>
        <select id="newsCategory">
          <option>Breaking News</option>
          <option>Local News</option>
          <option>National News</option>
          <option>Politics</option>
          <option>Public Issues</option>
          <option>Education</option>
          <option>Sports</option>
          <option>Other</option>
        </select>
      </div>
      <div class="field">
        <label>Upload Image</label>
        <input type="file" id="newsImage" accept="image/*">
        <img id="imagePreview" class="post-image hidden">
      </div>
      <button class="btn" type="submit">Publish News</button>
    </form>
  </div>
</section>

<!-- PROFILE -->
<section id="profile" class="page hidden">
  <div class="card" style="text-align:center">
    <div class="avatar" style="margin:auto;width:75px;height:75px;font-size:25px">RV</div>
    <h2 id="profileName" style="margin-top:12px">Guest User</h2>
    <p class="muted">RTI VOICE Member</p>
    <br>
    <button class="btn" onclick="showPage('login')">Login / Register</button>
  </div>
  <div class="stats">
    <div class="stat"><h2 id="postCount">0</h2><p>Posts</p></div>
    <div class="stat"><h2>0</h2><p>Followers</p></div>
    <div class="stat"><h2>0</h2><p>Following</p></div>
  </div>
  <div class="card">
    <h3>My Profile</h3>
    <p class="list-item">👤 Account Information</p>
    <p class="list-item">📰 My News</p>
    <p class="list-item">⭐ My Subscription</p>
    <p class="list-item">💰 My Wallet</p>
  </div>
</section>

<!-- LOGIN -->
<section id="login" class="page hidden">
  <div class="card">
    <h2 class="section-title">Login / Register</h2>
    <form id="loginForm">
      <div class="field">
        <label>Full Name</label>
        <input id="userName" required placeholder="Enter your name">
      </div>
      <div class="field">
        <label>Email</label>
        <input id="userEmail" type="email" required placeholder="Enter email">
      </div>
      <div class="field">
        <label>Password</label>
        <input id="userPassword" type="password" required minlength="6"
          placeholder="Enter password">
      </div>
      <button class="btn" type="submit">Continue</button>
    </form>
    <p class="muted" style="margin-top:15px">
      Demo account only. Secure authentication needs a backend.
    </p>
  </div>
</section>

<!-- NETWORK -->
<section id="network" class="page hidden">
  <div class="card">
    <h2 class="section-title">👥 My Network</h2>
    <div class="stats">
      <div class="stat"><h2>0</h2><p>Followers</p></div>
      <div class="stat"><h2>0</h2><p>Following</p></div>
      <div class="stat"><h2>0</h2><p>Members</p></div>
    </div>
    <p class="empty">Your network will appear here.</p>
  </div>
</section>

<!-- WALLET -->
<section id="wallet" class="page hidden">
  <div class="card">
    <h2 class="section-title">💰 My Wallet</h2>
    <div class="hero">
      <p>Available Balance</p>
      <h1>₹0.00</h1>
      <p>Demo wallet balance</p>
    </div>
    <button class="btn" onclick="toast('Payment gateway connection required')">Add Money</button>
    <button class="btn btn-outline" onclick="toast('Withdrawal service requires verification')">Withdraw</button>
    <br><br>
    <h3>Transaction History</h3>
    <p class="empty">No transactions available.</p>
  </div>
</section>

<!-- PLANS -->
<section id="plans" class="page hidden">
  <h2 class="section-title">⭐ Subscription Plans</h2>
  <div class="plan">
    <h3>FREE PLAN</h3>
    <h2>₹0</h2>
    <p>Basic news feed<br>Basic profile<br>Community access</p>
    <button class="btn" onclick="toast('Free plan selected')">Select Plan</button>
  </div>
  <div class="plan">
    <h3>PRO PLAN</h3>
    <h2>₹499 <small style="font-size:13px">/ month</small></h2>
    <p>Premium profile<br>News publishing<br>Additional features</p>
    <button class="btn" onclick="toast('Payment gateway required')">Choose Pro</button>
  </div>
  <div class="plan">
    <h3>PREMIUM PLAN</h3>
    <h2>₹999 <small style="font-size:13px">/ month</small></h2>
    <p>Premium features<br>Advanced dashboard<br>Priority support</p>
    <button class="btn" onclick="toast('Payment gateway required')">Choose Premium</button>
  </div>
</section>

<!-- ECOMMERCE -->
<section id="ecommerce" class="page hidden">
  <div class="card">
    <h2 class="section-title">🛍️ E-Commerce</h2>
    <button class="btn" onclick="showPage('sell')">+ Sell Product</button>
    <br><br>
    <div class="list-item" onclick="showPage('products')">🛒 Buy Products →</div>
    <div class="list-item" onclick="showPage('sell')">📦 Sell Products →</div>
    <div class="list-item" onclick="showPage('products')">📋 My Products →</div>
    <div class="list-item" onclick="toast('No enquiries yet')">✉️ Enquiries →</div>
  </div>
</section>

<!-- SELL PRODUCT -->
<section id="sell" class="page hidden">
  <div class="card">
    <h2 class="section-title">Sell Product</h2>
    <form id="productForm">
      <div class="field"><label>Product Name</label>
        <input id="productName" required></div>
      <div class="field"><label>Price ₹</label>
        <input id="productPrice" type="number" min="1" required></div>
      <div class="field"><label>Description</label>
        <textarea id="productDesc" required></textarea></div>
      <button class="btn">Submit Product</button>
    </form>
  </div>
</section>

<section id="products" class="page hidden">
  <h2 class="section-title">Products</h2>
  <div id="productList" class="card"></div>
</section>

<!-- ADS -->
<section id="ads" class="page hidden">
  <div class="card">
    <h2 class="section-title">📢 Advertisement</h2>
    <p>Promote your business with RTI VOICE.</p>
    <button class="btn" onclick="showPage('adpost')">Create Advertisement</button>
    <br><br>
    <div class="list-item" onclick="toast('No advertisements yet')">My Advertisements</div>
    <div class="list-item" onclick="toast('No enquiries yet')">Ad Enquiries</div>
  </div>
</section>

<section id="adpost" class="page hidden">
  <div class="card">
    <h2 class="section-title">Create Advertisement</h2>
    <div class="field"><label>Business Name</label><input id="adName"></div>
    <div class="field"><label>Advertisement Details</label><textarea id="adDetails"></textarea></div>
    <button class="btn" onclick="toast('Demo: Backend required to publish ads')">Submit Advertisement</button>
  </div>
</section>

<!-- OTHER PAGES -->
<section id="live" class="page hidden">
  <div class="card"><h2>🔴 Live Streaming</h2><p class="empty">Live streaming service needs video infrastructure.</p></div>
</section>

<section id="epaper" class="page hidden">
  <div class="card"><h2>📖 E-Paper</h2><p class="empty">Newspaper editions will appear here.</p></div>
</section>

<section id="notifications" class="page hidden">
  <div class="card"><h2>🔔 Notifications</h2><p class="empty">No new notifications.</p></div>
</section>

<!-- ADMIN -->
<section id="admin" class="page hidden">
  <div class="hero">
    <h1>Admin Dashboard</h1>
    <p>RTI VOICE Management Demo</p>
  </div>
  <div class="stats">
    <div class="stat"><h2 id="adminPosts">0</h2><p>News Posts</p></div>
    <div class="stat"><h2 id="adminProducts">0</h2><p>Products</p></div>
    <div class="stat"><h2>0</h2><p>Users</p></div>
  </div>
  <div class="card">
    <h3>Manage News</h3>
    <div id="adminFeed"></div>
  </div>
  <div class="card">
    <h3>Admin Tools</h3>
    <div class="list-item" onclick="toast('User management backend required')">👥 Manage Users</div>
    <div class="list-item" onclick="toast('Payment backend required')">💳 Manage Payments</div>
    <div class="list-item" onclick="toast('Settings backend required')">⚙️ Settings</div>
  </div>
</section>

</main>

<!-- RIGHT MENU -->
<aside class="sidebar right-sidebar">
  <div class="card">
    <h3 style="margin-bottom:12px">Quick Menu</h3>
    <div id="rightMenu"></div>
  </div>
  <div class="card">
    <h3>About Us</h3>
    <p class="muted" style="line-height:1.7">
      RTI VOICE is a community news and media platform.
    </p>
  </div>
</aside>

</div>
</div>

<!-- MOBILE NAVIGATION -->
<nav class="bottom-nav">
  <button onclick="showPage('home')"><span>🏠</span>Home</button>
  <button onclick="showPage('feedPage')"><span>📰</span>Feed</button>
  <button onclick="showPage('post')"><span>➕</span>Post</button>
  <button onclick="showPage('wallet')"><span>💰</span>Wallet</button>
  <button onclick="showPage('profile')"><span>👤</span>Profile</button>
</nav>

<div id="toast"></div>

<script>
const menus = [
  ['🏠','Home','home'],
  ['📰','News Feed','feedPage'],
  ['➕','Post News','post'],
  ['👤','My Profile','profile'],
  ['👥','My Network','network'],
  ['💰','Wallet','wallet'],
  ['⭐','Subscription','plans'],
  ['🛍️','E-Commerce','ecommerce'],
  ['📢','Advertisements','ads'],
  ['📖','E-Paper','epaper'],
  ['🔴','Live Streaming','live'],
  ['🔔','Notifications','notifications'],
  ['⚙️','Admin Panel','admin']
];

function createMenu(id) {
  document.getElementById(id).innerHTML = menus.map(m =>
    `<button class="menu-item" onclick="showPage('${m[2]}')">
      ${m[0]} ${m[1]}
    </button>`
  ).join('');
}
createMenu('leftMenu');
createMenu('rightMenu');

function showPage(id) {
  document.querySelectorAll('.page').forEach(p => p.classList.add('hidden'));
  const page = document.getElementById(id);
  if(page) page.classList.remove('hidden');
  window.scrollTo(0,0);
  renderPosts();
  renderProducts();
  renderAdmin();
}

function toast(message) {
  const el = document.getElementById('toast');
  el.textContent = message;
  el.style.display='block';
  setTimeout(()=>el.style.display='none',2500);
}

function getData(key) {
  try {return JSON.parse(localStorage.getItem(key)) || []}
  catch(e) {return []}
}
function saveData(key,value) {
  localStorage.setItem(key,JSON.stringify(value));
}

let posts = getData('rti_posts');
let products = getData('rti_products');

function safe(text) {
  return String(text).replace(/[&<>"']/g,c=>({
    '&':'&amp;','<':'&lt;','>':'&gt;',
    '"':'&quot;',"'":'&#39;'
  })[c]);
}

function renderPosts() {
  const search = (document.getElementById('searchBox')?.value || '').toLowerCase();
  const filtered = posts.filter(p =>
    (p.title+' '+p.description+' '+p.category).toLowerCase().includes(search)
  );

  const html = filtered.length ? filtered.slice().reverse().map((p)=>{
    return `
    <div class="card">
      <div class="post-head">
        <div class="avatar">RV</div>
        <div><b>${safe(p.author)}</b>
        <p class="muted">${safe(p.category)} • ${safe(p.date)}</p></div>
      </div>
      <h3>${safe(p.title)}</h3>
      <p style="line-height:1.6;margin-top:8px">${safe(p.description)}</p>
      ${p.image ? `<img class="post-image" src="${p.image}" alt="News image">` : ''}
      <div class="post-actions">
        <button onclick="likePost('${p.id}')">❤️ ${p.likes} Like</button>
        <button onclick="commentPost('${p.id}')">💬 Comment</button>
        <button onclick="sharePost('${p.id}')">↗ Share</button>
      </div>
      <p class="muted" style="margin-top:10px">${p.comments.length} comments</p>
    </div>`;
  }).join('') : '<div class="card empty">No news found. Publish your first news!</div>';

  document.getElementById('feed').innerHTML = html;
  document.getElementById('feed2').innerHTML = html;
  document.getElementById('postCount').textContent = posts.length;
}

document.getElementById('newsImage').addEventListener('change',function() {
  const file = this.files[0];
  if(!file) return;
  if(file.size > 2*1024*1024) {
    toast('Please select an image smaller than 2 MB');
    this.value='';
    return;
  }
  const reader = new FileReader();
  reader.onload = e => {
    const img = document.getElementById('imag
