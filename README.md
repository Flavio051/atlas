# atlas
Mon portfolio ATLAS
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="default">
<meta name="apple-mobile-web-app-title" content="ATLAS">
<title>ATLAS — Mon Portefeuille</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
<style>
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
html,body{font-family:-apple-system,BlinkMacSystemFont,'SF Pro Display',sans-serif;background:#F0F4F8;color:#1A202C;min-height:100vh;overflow-x:hidden}
input,select,button,textarea{font-family:inherit;-webkit-appearance:none}
input:focus,select:focus,textarea:focus{outline:none}

/* ── TOP BAR ── */
.topbar{background:linear-gradient(135deg,#3B82F6 0%,#1D4ED8 100%);padding:14px 18px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:100;box-shadow:0 2px 12px rgba(59,130,246,0.3)}
.topbar-left{display:flex;align-items:center;gap:10px}
.logo{width:34px;height:34px;background:rgba(255,255,255,0.2);border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:18px;border:1px solid rgba(255,255,255,0.3)}
.app-title{font-size:18px;font-weight:800;color:#FFF;letter-spacing:0.5px}
.topbar-right{display:flex;align-items:center;gap:10px}
.live-dot{display:flex;align-items:center;gap:5px;background:rgba(255,255,255,0.15);padding:5px 10px;border-radius:20px}
.dot{width:6px;height:6px;border-radius:50%;background:#10B981;animation:pulse 2s infinite}
.live-txt{font-size:10px;color:#FFF;font-weight:600}
.refresh-btn{background:rgba(255,255,255,0.2);border:1px solid rgba(255,255,255,0.3);border-radius:8px;padding:6px 10px;color:#FFF;font-size:12px;font-weight:600;cursor:pointer;transition:all 0.2s}
.refresh-btn:active{background:rgba(255,255,255,0.35)}

/* ── TICKER ── */
.ticker-wrap{background:#FFF;border-bottom:1px solid #E2E8F0;height:30px;overflow:hidden;display:flex;align-items:center}
.ticker{display:flex;gap:32px;white-space:nowrap;animation:ticker 40s linear infinite;font-size:11px;font-weight:600;padding-left:20px}
.tick-item{display:flex;align-items:center;gap:5px}
.tick-name{color:#64748B}
.tick-up{color:#10B981}
.tick-dn{color:#EF4444}

/* ── NAV TABS ── */
.nav{display:flex;background:#FFF;border-bottom:1px solid #E2E8F0;overflow-x:auto;-webkit-overflow-scrolling:touch;scrollbar-width:none}
.nav::-webkit-scrollbar{display:none}
.nav-btn{flex:none;padding:12px 18px;background:none;border:none;border-bottom:2px solid transparent;font-size:12px;font-weight:600;color:#64748B;cursor:pointer;white-space:nowrap;transition:all 0.2s}
.nav-btn.active{color:#3B82F6;border-bottom-color:#3B82F6}

/* ── VIEWS ── */
.view{display:none;padding:16px;animation:fadeUp 0.2s ease}
.view.active{display:block}

/* ── HERO CARD ── */
.hero{background:linear-gradient(135deg,#3B82F6 0%,#1D4ED8 100%);border-radius:20px;padding:24px;margin-bottom:16px;color:#FFF;box-shadow:0 8px 32px rgba(59,130,246,0.25)}
.hero-label{font-size:12px;font-weight:600;opacity:0.85;letter-spacing:0.5px;margin-bottom:8px}
.hero-value{font-size:38px;font-weight:800;letter-spacing:-1px;margin-bottom:6px}
.hero-badges{display:flex;gap:8px;flex-wrap:wrap;margin-top:10px}
.hero-badge{background:rgba(255,255,255,0.2);padding:5px 12px;border-radius:20px;font-size:12px;font-weight:700;backdrop-filter:blur(4px);border:1px solid rgba(255,255,255,0.25)}
.hero-badge.green{background:rgba(16,185,129,0.3);border-color:rgba(16,185,129,0.4)}
.hero-badge.red{background:rgba(239,68,68,0.3);border-color:rgba(239,68,68,0.4)}
.hero-goal{margin-top:14px}
.hero-goal-label{font-size:11px;opacity:0.8;margin-bottom:6px;font-weight:500}
.progress-bar{background:rgba(255,255,255,0.2);border-radius:10px;height:6px;overflow:hidden}
.progress-fill{background:#FFF;border-radius:10px;height:100%;transition:width 0.8s ease}

/* ── KPI GRID ── */
.kpi-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:16px}
.kpi-card{background:#FFF;border-radius:14px;padding:14px;border:1px solid #E2E8F0;box-shadow:0 1px 3px rgba(0,0,0,0.04);position:relative;overflow:hidden}
.kpi-accent{position:absolute;top:0;left:0;right:0;height:3px;border-radius:14px 14px 0 0}
.kpi-label{font-size:10px;color:#64748B;font-weight:600;letter-spacing:0.5px;text-transform:uppercase;margin-bottom:6px;margin-top:4px}
.kpi-value{font-size:20px;font-weight:800;color:#1A202C;letter-spacing:-0.5px}
.kpi-sub{font-size:10px;color:#94A3B8;font-weight:500;margin-top:4px}
.kpi-badge{display:inline-block;font-size:10px;font-weight:700;padding:2px 7px;border-radius:5px;margin-top:5px}
.badge-green{background:#D1FAE5;color:#059669}
.badge-red{background:#FEE2E2;color:#DC2626}
.badge-blue{background:#DBEAFE;color:#2563EB}

/* ── CARD ── */
.card{background:#FFF;border-radius:14px;padding:18px;margin-bottom:14px;border:1px solid #E2E8F0;box-shadow:0 1px 3px rgba(0,0,0,0.04)}
.card-title{font-size:13px;font-weight:700;color:#1A202C;margin-bottom:14px;display:flex;align-items:center;gap:7px}

/* ── WALLET TABS ── */
.wallet-tabs{display:flex;gap:6px;margin-bottom:14px;overflow-x:auto;-webkit-overflow-scrolling:touch;padding-bottom:4px}
.wallet-tabs::-webkit-scrollbar{display:none}
.wallet-tab{flex:none;padding:7px 14px;border-radius:8px;border:1px solid #E2E8F0;background:#FFF;font-size:11px;font-weight:700;color:#64748B;cursor:pointer;transition:all 0.2s}
.wallet-tab.active{color:#FFF;border-color:transparent}

/* ── ASSET CARDS ── */
.asset-list{display:flex;flex-direction:column;gap:10px}
.asset-card{background:#FFF;border:1px solid #E2E8F0;border-radius:14px;padding:14px;box-shadow:0 1px 3px rgba(0,0,0,0.03)}
.asset-top{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:12px}
.asset-left{display:flex;align-items:center;gap:10px}
.asset-icon{width:40px;height:40px;border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:20px;background:#F1F5F9;flex-shrink:0}
.asset-name{font-size:14px;font-weight:800;color:#1A202C}
.asset-sub{font-size:11px;color:#94A3B8;font-weight:500;margin-top:2px}
.asset-wallet{font-size:9px;font-weight:800;padding:2px 7px;border-radius:4px;margin-top:3px;display:inline-block}
.asset-right{text-align:right}
.asset-value{font-size:15px;font-weight:800;color:#1A202C}
.asset-pv{font-size:12px;font-weight:700;margin-top:2px}
.asset-stats{display:grid;grid-template-columns:repeat(3,1fr);gap:6px;padding-top:10px;border-top:1px solid #F1F5F9}
.stat-item{text-align:center}
.stat-label{font-size:9px;color:#94A3B8;font-weight:600;text-transform:uppercase;margin-bottom:3px}
.stat-value{font-size:12px;font-weight:700;color:#1A202C}
.asset-actions{display:flex;gap:8px;margin-top:10px}
.btn-analyse{flex:1;background:#EFF6FF;border:1px solid #BFDBFE;border-radius:8px;padding:8px;font-size:12px;font-weight:700;color:#2563EB;cursor:pointer}
.btn-delete{background:#FEF2F2;border:1px solid #FECACA;border-radius:8px;padding:8px 12px;font-size:12px;color:#DC2626;cursor:pointer;font-weight:700}

/* ── CHART SECTION ── */
.chart-wrap{position:relative;height:200px;margin-top:4px}
.period-btns{display:flex;gap:6px;margin-bottom:12px}
.period-btn{padding:5px 12px;border-radius:6px;border:1px solid #E2E8F0;background:#FFF;font-size:11px;font-weight:600;color:#64748B;cursor:pointer}
.period-btn.active{background:#3B82F6;color:#FFF;border-color:#3B82F6}

/* ── ALLOCATION PIE ── */
.alloc-list{margin-top:12px;display:flex;flex-direction:column;gap:8px}
.alloc-item{display:flex;align-items:center;gap:10px}
.alloc-dot{width:10px;height:10px;border-radius:50%;flex-shrink:0}
.alloc-label{font-size:12px;font-weight:600;color:#374151;flex:1}
.alloc-bar-wrap{flex:2;background:#F1F5F9;border-radius:10px;height:6px;overflow:hidden}
.alloc-bar{height:100%;border-radius:10px;transition:width 0.8s ease}
.alloc-pct{font-size:11px;font-weight:700;color:#64748B;min-width:36px;text-align:right}
.alloc-val{font-size:11px;color:#94A3B8;min-width:60px;text-align:right}

/* ── ANALYSE VIEW ── */
.method-grid{display:grid;gap:10px;margin-bottom:16px}
.method-card{border:2px solid #E2E8F0;border-radius:12px;padding:12px;cursor:pointer;transition:all 0.2s;background:#FFF;text-align:left;width:100%}
.method-card.active{border-color:var(--mc);background:var(--ms)}
.method-top{display:flex;align-items:center;gap:10px;margin-bottom:5px}
.method-icon{width:36px;height:36px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:18px;background:#F1F5F9}
.method-name{font-size:12px;font-weight:800;color:#1A202C}
.method-sub{font-size:10px;color:#64748B;font-weight:500}
.method-desc{font-size:11px;color:#94A3B8;line-height:1.4}
.method-check{width:20px;height:20px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:800;color:#FFF;margin-left:auto;flex-shrink:0}

.search-row{display:flex;gap:8px;margin-bottom:12px}
.search-row input{flex:1;background:#F8FAFC;border:1px solid #E2E8F0;border-radius:10px;padding:12px 14px;font-size:14px;color:#1A202C}
.search-row input:focus{border-color:#3B82F6;box-shadow:0 0 0 3px rgba(59,130,246,0.1)}
.launch-btn{background:#3B82F6;border:none;border-radius:10px;padding:12px 18px;color:#FFF;font-size:13px;font-weight:700;cursor:pointer;white-space:nowrap;box-shadow:0 2px 8px rgba(59,130,246,0.3);transition:all 0.2s}
.launch-btn:disabled{background:#94A3B8;box-shadow:none}
.launch-btn:active{transform:scale(0.97)}

.result-box{background:#F0FDF4;border:1px solid #BBF7D0;border-radius:12px;padding:16px;font-size:13px;line-height:1.75;color:#1A202C;white-space:pre-wrap;word-break:break-word}
.result-box.error{background:#FEF2F2;border-color:#FECACA}
.searching-box{background:#EFF6FF;border:1px solid #BFDBFE;border-radius:10px;padding:12px 14px;display:flex;align-items:center;gap:8px;font-size:12px;font-weight:600;color:#2563EB;margin-bottom:12px}

/* ── ADD ASSET MODAL ── */
.modal-overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.5);z-index:200;align-items:flex-end;justify-content:center;backdrop-filter:blur(4px)}
.modal-overlay.open{display:flex}
.modal{background:#FFF;border-radius:24px 24px 0 0;padding:24px;width:100%;max-height:85vh;overflow-y:auto;animation:slideUp 0.3s ease}
.modal-title{font-size:17px;font-weight:800;color:#1A202C;margin-bottom:4px}
.modal-sub{font-size:12px;color:#64748B;margin-bottom:20px}
.field{margin-bottom:14px}
.field label{display:block;font-size:11px;font-weight:700;color:#374151;text-transform:uppercase;letter-spacing:0.5px;margin-bottom:6px}
.field input,.field select{width:100%;background:#F8FAFC;border:1px solid #E2E8F0;border-radius:10px;padding:12px 14px;font-size:15px;color:#1A202C}
.field input:focus,.field select:focus{border-color:#3B82F6;box-shadow:0 0 0 3px rgba(59,130,246,0.1)}
.field-row{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.modal-actions{display:flex;gap:10px;margin-top:8px}
.btn-primary{flex:2;background:#3B82F6;border:none;border-radius:12px;padding:14px;color:#FFF;font-size:15px;font-weight:700;cursor:pointer;box-shadow:0 2px 8px rgba(59,130,246,0.3)}
.btn-secondary{flex:1;background:#F1F5F9;border:none;border-radius:12px;padding:14px;color:#64748B;font-size:15px;font-weight:600;cursor:pointer}
.add-fab{position:fixed;bottom:24px;right:20px;background:#3B82F6;color:#FFF;border:none;border-radius:16px;padding:14px 20px;font-size:14px;font-weight:700;cursor:pointer;box-shadow:0 4px 16px rgba(59,130,246,0.4);z-index:90;display:flex;align-items:center;gap:7px;transition:all 0.2s}
.add-fab:active{transform:scale(0.95)}

/* ── SETTINGS ── */
.settings-section{margin-bottom:20px}
.settings-title{font-size:12px;font-weight:700;color:#94A3B8;text-transform:uppercase;letter-spacing:1px;margin-bottom:10px}
.settings-item{background:#FFF;border:1px solid #E2E8F0;border-radius:12px;padding:14px 16px;display:flex;justify-content:space-between;align-items:center;margin-bottom:8px}
.settings-item-left .name{font-size:14px;font-weight:600;color:#1A202C}
.settings-item-left .desc{font-size:11px;color:#94A3B8;margin-top:2px}
.toggle{width:44px;height:26px;background:#E2E8F0;border-radius:13px;position:relative;cursor:pointer;transition:all 0.2s;flex-shrink:0}
.toggle.on{background:#3B82F6}
.toggle::after{content:'';position:absolute;top:3px;left:3px;width:20px;height:20px;background:#FFF;border-radius:50%;transition:all 0.2s;box-shadow:0 1px 3px rgba(0,0,0,0.15)}
.toggle.on::after{left:21px}
.risk-profile-grid{display:grid;gap:8px;margin-top:8px}
.risk-btn{border:2px solid #E2E8F0;border-radius:12px;padding:12px 14px;cursor:pointer;background:#FFF;text-align:left;transition:all 0.2s;width:100%}
.risk-btn.active{border-color:var(--rc);background:var(--rs)}
.risk-btn-top{display:flex;align-items:center;justify-content:space-between;margin-bottom:4px}
.risk-btn-name{font-size:13px;font-weight:800;color:#1A202C}
.risk-btn-dd{font-size:11px;font-weight:700;padding:2px 7px;border-radius:5px}
.risk-btn-desc{font-size:11px;color:#64748B}

/* ── CHATBOT ── */
.chat-messages{height:400px;overflow-y:auto;-webkit-overflow-scrolling:touch;display:flex;flex-direction:column;gap:12px;padding:4px 0;margin-bottom:12px}
.msg{display:flex;flex-direction:column;gap:4px}
.msg.user{align-items:flex-end}
.msg.bot{align-items:flex-start}
.msg-sender{font-size:9px;font-weight:700;letter-spacing:0.5px}
.msg.user .msg-sender{color:#3B82F6}
.msg.bot .msg-sender{color:#10B981}
.msg-bubble{max-width:88%;padding:11px 14px;border-radius:14px;font-size:13px;line-height:1.65;word-break:break-word}
.msg.user .msg-bubble{background:#3B82F6;color:#FFF;border-radius:14px 14px 4px 14px}
.msg.bot .msg-bubble{background:#F8FAFC;color:#1A202C;border:1px solid #E2E8F0;border-radius:14px 14px 14px 4px}
.chat-quick{display:flex;flex-wrap:wrap;gap:6px;margin-bottom:12px}
.quick-btn{background:#FFF;border:1px solid #E2E8F0;border-radius:8px;padding:6px 10px;font-size:11px;font-weight:600;color:#475569;cursor:pointer;white-space:nowrap}
.chat-input-row{display:flex;gap:8px}
.chat-input{flex:1;background:#F8FAFC;border:1px solid #E2E8F0;border-radius:12px;padding:11px 14px;font-size:14px;resize:none;height:48px}
.chat-send{background:#3B82F6;border:none;border-radius:12px;padding:0 18px;color:#FFF;font-size:18px;font-weight:700;cursor:pointer}
.chat-send:disabled{background:#94A3B8}

/* ── UTILS ── */
.pv-pos{color:#059669;font-weight:700}
.pv-neg{color:#DC2626;font-weight:700}
.empty-state{text-align:center;padding:48px 24px;color:#94A3B8}
.empty-icon{font-size:48px;margin-bottom:12px}
.empty-text{font-size:15px;font-weight:600;margin-bottom:6px;color:#64748B}
.empty-sub{font-size:13px}
.section-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:12px}
.section-title{font-size:15px;font-weight:700;color:#1A202C}
.last-update{font-size:10px;color:#94A3B8;font-weight:500}
.divider{height:1px;background:#F1F5F9;margin:10px 0}

@keyframes pulse{0%,100%{opacity:1}50%{opacity:0.4}}
@keyframes ticker{from{transform:translateX(0)}to{transform:translateX(-50%)}}
@keyframes fadeUp{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}
@keyframes slideUp{from{transform:translateY(100%)}to{transform:translateY(0)}}
@keyframes spin{to{transform:rotate(360deg)}}

.spinner{width:16px;height:16px;border:2px solid rgba(59,130,246,0.3);border-top-color:#3B82F6;border-radius:50%;animation:spin 0.7s linear infinite;display:inline-block}
</style>
</head>
<body>

<!-- TOP BAR -->
<div class="topbar">
  <div class="topbar-left">
    <div class="logo">🤖</div>
    <div class="app-title">ATLAS</div>
  </div>
  <div class="topbar-right">
    <div class="live-dot">
      <div class="dot"></div>
      <span class="live-txt" id="lastUpdateLabel">En direct</span>
    </div>
    <button class="refresh-btn" onclick="refreshPrices()" id="refreshBtn">⟳ Actualiser</button>
  </div>
</div>

<!-- TICKER -->
<div class="ticker-wrap">
  <div class="ticker" id="tickerEl"></div>
</div>

<!-- NAV TABS -->
<div class="nav">
  <button class="nav-btn active" onclick="showView('dashboard',this)">🏠 Dashboard</button>
  <button class="nav-btn" onclick="showView('portfolio',this)">💼 Portfolio</button>
  <button class="nav-btn" onclick="showView('analyse',this)">📊 Analyse IA</button>
  <button class="nav-btn" onclick="showView('chat',this)">💬 Chatbot</button>
  <button class="nav-btn" onclick="showView('settings',this)">⚙️ Réglages</button>
</div>

<!-- ═══════ DASHBOARD ═══════ -->
<div class="view active" id="view-dashboard">

  <!-- Hero -->
  <div class="hero" id="heroCard">
    <div class="hero-label">💼 VALEUR TOTALE DU PORTEFEUILLE</div>
    <div class="hero-value" id="heroValue">—</div>
    <div class="hero-badges" id="heroBadges"></div>
    <div class="hero-goal" id="heroGoal" style="display:none">
      <div class="hero-goal-label" id="heroGoalLabel"></div>
      <div class="progress-bar"><div class="progress-fill" id="heroGoalBar"></div></div>
    </div>
  </div>

  <!-- KPIs -->
  <div class="kpi-grid" id="kpiGrid">
    <div class="kpi-card"><div class="kpi-accent" style="background:#10B981"></div><div class="kpi-label">Performance</div><div class="kpi-value" id="kpiPerf">—</div><div class="kpi-sub">vs PRU</div></div>
    <div class="kpi-card"><div class="kpi-accent" style="background:#06B6D4"></div><div class="kpi-label">Dividendes/an</div><div class="kpi-value" id="kpiDiv">—</div><div class="kpi-sub" id="kpiDivYield">—</div></div>
    <div class="kpi-card"><div class="kpi-accent" style="background:#8B5CF6"></div><div class="kpi-label">Nb actifs</div><div class="kpi-value" id="kpiCount">—</div><div class="kpi-sub">dans 5 wallets</div></div>
    <div class="kpi-card"><div class="kpi-accent" style="background:#F59E0B"></div><div class="kpi-label">Meilleur actif</div><div class="kpi-value" id="kpiBest">—</div><div class="kpi-sub" id="kpiBestName">—</div></div>
  </div>

  <!-- Chart -->
  <div class="card">
    <div class="card-title">📈 Évolution du portefeuille</div>
    <div class="period-btns">
      <button class="period-btn active">1M</button>
      <button class="period-btn">3M</button>
      <button class="period-btn">6M</button>
      <button class="period-btn">1A</button>
    </div>
    <div class="chart-wrap"><canvas id="chartPerf"></canvas></div>
  </div>

  <!-- Allocation -->
  <div class="card">
    <div class="card-title">🥧 Allocation par classe d'actif</div>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:12px;align-items:center">
      <div style="position:relative;height:150px"><canvas id="chartAlloc"></canvas></div>
      <div class="alloc-list" id="allocList"></div>
    </div>
  </div>

  <!-- Wallets -->
  <div class="card">
    <div class="card-title">🏦 Mes portefeuilles</div>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px" id="walletGrid"></div>
  </div>

</div>

<!-- ═══════ PORTFOLIO ═══════ -->
<div class="view" id="view-portfolio">

  <div class="section-header">
    <div class="section-title">💼 Mes actifs</div>
    <div class="last-update" id="portfolioUpdate">—</div>
  </div>

  <div class="wallet-tabs" id="walletTabs">
    <button class="wallet-tab active" style="background:#3B82F6;color:#FFF" onclick="filterWallet('all',this)">Tous</button>
    <button class="wallet-tab" onclick="filterWallet('PEA',this)" style="--wc:#10B981">PEA 🇫🇷</button>
    <button class="wallet-tab" onclick="filterWallet('CTO',this)" style="--wc:#3B82F6">CTO 📈</button>
    <button class="wallet-tab" onclick="filterWallet('Binance',this)" style="--wc:#8B5CF6">Crypto ₿</button>
    <button class="wallet-tab" onclick="filterWallet('Immo',this)" style="--wc:#14B8A6">Immo 🏘️</button>
  </div>

  <div class="asset-list" id="assetList">
    <div class="empty-state">
      <div class="empty-icon">💼</div>
      <div class="empty-text">Aucun actif pour l'instant</div>
      <div class="empty-sub">Tape le bouton + pour ajouter</div>
    </div>
  </div>
  <div style="height:80px"></div>
</div>

<!-- ═══════ ANALYSE IA ═══════ -->
<div class="view" id="view-analyse">

  <div class="card">
    <div class="card-title">🧠 Choisir les méthodologies</div>
    <div style="display:flex;gap:6px;margin-bottom:12px;overflow-x:auto">
      <button class="nav-btn active" onclick="setAnalyseTab('stock',this)" style="flex:none;border-radius:8px;padding:8px 14px;border:1px solid #E2E8F0">📈 Actions</button>
      <button class="nav-btn" onclick="setAnalyseTab('crypto',this)" style="flex:none;border-radius:8px;padding:8px 14px;border:1px solid #E2E8F0">₿ Crypto</button>
      <button class="nav-btn" onclick="setAnalyseTab('immo',this)" style="flex:none;border-radius:8px;padding:8px 14px;border:1px solid #E2E8F0">🏘️ Immo</button>
    </div>
    <div class="method-grid" id="methodGrid"></div>
  </div>

  <div class="card">
    <div class="card-title" id="analyseFormTitle">🔍 Analyse — 0 méthode</div>
    <div class="search-row">
      <input type="text" id="analyseQuery" placeholder="Ex: Apple, Bitcoin, SCPI Corum..." />
      <button class="launch-btn" id="launchBtn" onclick="runAnalyse()" disabled>🚀</button>
    </div>
    <div id="searchingBox" style="display:none" class="searching-box">
      <div class="spinner"></div>
      Analyse en cours avec les données du marché...
    </div>
    <div id="analyseResult" style="display:none"></div>
  </div>

  <div style="height:30px"></div>
</div>

<!-- ═══════ CHATBOT ═══════ -->
<div class="view" id="view-chat">
  <div class="card" style="display:flex;flex-direction:column">
    <div class="card-title">💬 ATLAS — Votre conseiller IA</div>
    <div class="chat-quick" id="chatQuick"></div>
    <div class="chat-messages" id="chatMessages"></div>
    <div class="chat-input-row">
      <textarea class="chat-input" id="chatInput" placeholder="Posez votre question..." onkeydown="if(event.key==='Enter'&&!event.shiftKey){event.preventDefault();sendChat()}"></textarea>
      <button class="chat-send" id="chatSend" onclick="sendChat()">➤</button>
    </div>
  </div>
  <div style="height:30px"></div>
</div>

<!-- ═══════ SETTINGS ═══════ -->
<div class="view" id="view-settings">

  <div class="settings-section">
    <div class="settings-title">Profil de risque</div>
    <div class="risk-profile-grid" id="riskGrid"></div>
  </div>

  <div class="settings-section">
    <div class="settings-title">Objectif financier</div>
    <div class="card" style="padding:14px">
      <div class="field">
        <label>Objectif (€)</label>
        <input type="number" id="goalInput" placeholder="Ex: 100000" oninput="saveGoal()">
      </div>
      <div class="field">
        <label>Échéance</label>
        <input type="text" id="goalDate" placeholder="Ex: 2030" oninput="saveGoal()">
      </div>
    </div>
  </div>

  <div class="settings-section">
    <div class="settings-title">Notifications</div>
    <div id="notifSettings"></div>
  </div>

  <div class="settings-section">
    <div class="settings-title">Clé API Anthropic (optionnel)</div>
    <div class="card" style="padding:14px">
      <div class="field">
        <label>Clé API (pour activer l'IA)</label>
        <input type="password" id="apiKeyInput" placeholder="sk-ant-xxxxxxxx" oninput="saveApiKey()">
      </div>
      <div style="font-size:11px;color:#94A3B8;line-height:1.5">Sans clé : analyses via données publiques.<br>Avec clé (console.anthropic.com) : analyses IA complètes.</div>
    </div>
  </div>

  <div class="settings-section">
    <div class="settings-title">Données</div>
    <button onclick="exportData()" style="width:100%;background:#EFF6FF;border:1px solid #BFDBFE;border-radius:10px;padding:12px;color:#2563EB;font-size:13px;font-weight:700;cursor:pointer;margin-bottom:8px">📤 Exporter mes données (JSON)</button>
    <button onclick="importData()" style="width:100%;background:#FFF;border:1px solid #E2E8F0;border-radius:10px;padding:12px;color:#64748B;font-size:13px;font-weight:600;cursor:pointer;margin-bottom:8px">📥 Importer des données</button>
    <input type="file" id="importFile" accept=".json,.csv" style="display:none" onchange="handleImport(event)">
    <button onclick="if(confirm('Supprimer TOUTES les données ?'))clearAll()" style="width:100%;background:#FEF2F2;border:1px solid #FECACA;border-radius:10px;padding:12px;color:#DC2626;font-size:13px;font-weight:600;cursor:pointer">🗑️ Réinitialiser tout</button>
  </div>

  <div style="height:30px"></div>
</div>

<!-- ADD ASSET MODAL -->
<div class="modal-overlay" id="addModal">
  <div class="modal">
    <div class="modal-title">+ Ajouter un actif</div>
    <div class="modal-sub">Renseignez les informations de votre position</div>
    <div class="field-row">
      <div class="field"><label>Ticker</label><input id="fTicker" placeholder="AAPL, BTC..."></div>
      <div class="field"><label>Nom</label><input id="fNom" placeholder="Apple Inc."></div>
    </div>
    <div class="field-row">
      <div class="field"><label>Type</label>
        <select id="fType">
          <option value="stock">Action</option>
          <option value="crypto">Crypto</option>
          <option value="etf">ETF</option>
          <option value="immo">Immobilier</option>
        </select>
      </div>
      <div class="field"><label>Wallet</label>
        <select id="fWallet">
          <option>PEA</option><option>CTO</option>
          <option>Binance</option><option>Kraken</option><option>Immo</option>
        </select>
      </div>
    </div>
    <div class="field-row">
      <div class="field"><label>Quantité</label><input id="fQte" type="number" inputmode="decimal" placeholder="10"></div>
      <div class="field"><label>PRU (€/$)</label><input id="fPRU" type="number" inputmode="decimal" placeholder="150"></div>
    </div>
    <div class="field-row">
      <div class="field"><label>Cours actuel</label><input id="fCours" type="number" inputmode="decimal" placeholder="185"></div>
      <div class="field"><label>Dividende %/an</label><input id="fDiv" type="number" inputmode="decimal" placeholder="1.5"></div>
    </div>
    <div class="modal-actions">
      <button class="btn-primary" onclick="addAsset()">✓ Ajouter</button>
      <button class="btn-secondary" onclick="closeModal()">Annuler</button>
    </div>
  </div>
</div>

<!-- FAB -->
<button class="add-fab" onclick="openModal()" id="addFab">
  <span style="font-size:18px">+</span> Ajouter un actif
</button>

<script>
// ════════════════════════════════════════
// STATE
// ════════════════════════════════════════
const DEFAULT_ASSETS = [
  {id:1,ticker:"MSFT",nom:"Microsoft",type:"stock",wallet:"CTO",qte:8,pru:320,cours:415,div:0.8,logo:"💻"},
  {id:2,ticker:"ASML",nom:"ASML Holding",type:"stock",wallet:"PEA",qte:3,pru:680,cours:820,div:1.2,logo:"🔬"},
  {id:3,ticker:"TTE",nom:"TotalEnergies",type:"stock",wallet:"PEA",qte:25,pru:58,cours:64,div:8.0,logo:"⛽"},
  {id:4,ticker:"LVMH",nom:"LVMH",type:"stock",wallet:"PEA",qte:4,pru:620,cours:730,div:4.5,logo:"👜"},
  {id:5,ticker:"NVDA",nom:"Nvidia",type:"stock",wallet:"CTO",qte:12,pru:480,cours:875,div:0.1,logo:"🎮"},
  {id:6,ticker:"BTC",nom:"Bitcoin",type:"crypto",wallet:"Binance",qte:0.25,pru:52000,cours:94000,div:0,logo:"₿"},
  {id:7,ticker:"ETH",nom:"Ethereum",type:"crypto",wallet:"Binance",qte:2.5,pru:2800,cours:3200,div:0,logo:"Ξ"},
  {id:8,ticker:"SOL",nom:"Solana",type:"crypto",wallet:"Kraken",qte:15,pru:120,cours:172,div:0,logo:"◎"},
  {id:9,ticker:"SCPI",nom:"SCPI Corum Origin",type:"immo",wallet:"Immo",qte:1,pru:8000,cours:8480,div:6.2,logo:"🏢"},
  {id:10,ticker:"MWRD",nom:"Amundi MSCI World",type:"etf",wallet:"PEA",qte:45,pru:42,cours:51,div:0,logo:"🌍"},
];

let S = {
  assets: [],
  riskProfile: "dynamique",
  goal: 100000,
  goalDate: "2030",
  apiKey: "",
  notifications: { daily:false, alerts:true, weekly:false },
  selectedMethods: [],
  analyseTab: "stock",
  chatHistory: [],
};

function load() {
  try {
    const saved = localStorage.getItem("atlas_v5");
    if (saved) {
      const parsed = JSON.parse(saved);
      Object.assign(S, parsed);
    } else {
      S.assets = DEFAULT_ASSETS;
      save();
    }
  } catch(e) { S.assets = DEFAULT_ASSETS; }
}

function save() {
  try { localStorage.setItem("atlas_v5", JSON.stringify(S)); } catch(e) {}
}

// ════════════════════════════════════════
// COMPUTED
// ════════════════════════════════════════
function compute(a) {
  const val = a.qte * a.cours;
  const cout = a.qte * a.pru;
  const pv = val - cout;
  const pvPct = cout > 0 ? (pv / cout) * 100 : 0;
  const divAnnuel = a.type === "immo" ? a.cours * a.div / 100 : a.qte * a.cours * a.div / 100;
  return { ...a, val, cout, pv, pvPct, divAnnuel };
}

function getAll() { return S.assets.map(compute); }

function totals() {
  const all = getAll();
  const totalVal = all.reduce((s,a) => s + a.val, 0);
  const totalCout = all.reduce((s,a) => s + a.cout, 0);
  const totalPV = totalVal - totalCout;
  const totalPVPct = totalCout > 0 ? (totalPV / totalCout) * 100 : 0;
  const totalDiv = all.reduce((s,a) => s + a.divAnnuel, 0);
  const divYield = totalVal > 0 ? (totalDiv / totalVal) * 100 : 0;
  return { totalVal, totalCout, totalPV, totalPVPct, totalDiv, divYield, all };
}

// ════════════════════════════════════════
// NAVIGATION
// ════════════════════════════════════════
let currentView = "dashboard";
function showView(id, btn) {
  document.querySelectorAll(".view").forEach(v => v.classList.remove("active"));
  document.querySelectorAll(".nav-btn").forEach(b => b.classList.remove("active"));
  document.getElementById("view-" + id).classList.add("active");
  if (btn) btn.classList.add("active");
  currentView = id;
  const fab = document.getElementById("addFab");
  fab.style.display = id === "portfolio" ? "flex" : "none";
  if (id === "dashboard") renderDashboard();
  if (id === "portfolio") renderPortfolio();
  if (id === "settings") renderSettings();
  if (id === "chat") renderChat();
}

// ════════════════════════════════════════
// TICKER
// ════════════════════════════════════════
const TICKER_DATA = [
  {l:"S&P 500",v:"+8.3%",up:true},{l:"NASDAQ",v:"+13.1%",up:true},{l:"CAC40",v:"+4.2%",up:true},
  {l:"DAX",v:"+5.1%",up:true},{l:"BTC",v:"94K$",up:true},{l:"ETH",v:"3 200$",up:true},
  {l:"OR",v:"3 180$/oz",up:true},{l:"PÉTROLE",v:"98.4$",up:true},{l:"VIX",v:"18.4",up:false},
  {l:"EUR/USD",v:"1.082",up:false},{l:"10Y US",v:"4.52%",up:true},
];
function renderTicker() {
  const all = [...TICKER_DATA, ...TICKER_DATA];
  document.getElementById("tickerEl").innerHTML = all.map(t =>
    `<span class="tick-item"><span class="tick-name">${t.l}</span><span class="${t.up?"tick-up":"tick-dn"}">${t.v} ${t.up?"▲":"▼"}</span></span>`
  ).join("");
}

// ════════════════════════════════════════
// DASHBOARD
// ════════════════════════════════════════
let perfChart = null, allocChart = null;

function renderDashboard() {
  const { totalVal, totalCout, totalPV, totalPVPct, totalDiv, divYield, all } = totals();
  const fmt = (n, dec=0) => n.toLocaleString("fr-FR", {minimumFractionDigits:dec, maximumFractionDigits:dec});

  // Hero
  document.getElementById("heroValue").textContent = fmt(totalVal) + " €";
  const pvSign = totalPV >= 0 ? "+" : "";
  const pvClass = totalPV >= 0 ? "green" : "red";
  document.getElementById("heroBadges").innerHTML =
    `<div class="hero-badge ${pvClass}">${pvSign}${fmt(totalPV)} € (${pvSign}${totalPVPct.toFixed(1)}%)</div>` +
    `<div class="hero-badge">💰 ${fmt(totalDiv)} €/an dividendes</div>`;

  // Goal
  if (S.goal > 0) {
    const pct = Math.min(100, (totalVal / S.goal) * 100);
    document.getElementById("heroGoal").style.display = "block";
    document.getElementById("heroGoalLabel").textContent = `Objectif : ${fmt(S.goal)} € en ${S.goalDate} — ${pct.toFixed(0)}%`;
    document.getElementById("heroGoalBar").style.width = pct + "%";
  }

  // KPIs
  document.getElementById("kpiPerf").textContent = (totalPV >= 0 ? "+" : "") + fmt(totalPV) + " €";
  document.getElementById("kpiDiv").textContent = fmt(Math.round(totalDiv)) + " €";
  document.getElementById("kpiDivYield").textContent = "Yield " + divYield.toFixed(2) + "%";
  document.getElementById("kpiCount").textContent = all.length;
  const best = [...all].sort((a,b) => b.pvPct - a.pvPct)[0];
  if (best) {
    document.getElementById("kpiBest").textContent = (best.pvPct >= 0 ? "+" : "") + best.pvPct.toFixed(1) + "%";
    document.getElementById("kpiBestName").textContent = best.ticker;
  }

  // Perf Chart (simulated history)
  const months = ["Mai","Jun","Jul","Aoû","Sep","Oct","Nov","Déc","Jan","Fév","Mar","Avr"];
  const base = totalCout * 0.85;
  const history = months.map((m, i) => ({
    label: m,
    value: Math.round(base + (totalVal - base) * (i / 11) + (Math.random() - 0.4) * totalVal * 0.03)
  }));
  history[history.length - 1].value = Math.round(totalVal);

  if (perfChart) { perfChart.destroy(); perfChart = null; }
  const ctx1 = document.getElementById("chartPerf").getContext("2d");
  perfChart = new Chart(ctx1, {
    type: "line",
    data: {
      labels: history.map(h => h.label),
      datasets: [{
        data: history.map(h => h.value),
        borderColor: "#3B82F6",
        borderWidth: 2.5,
        backgroundColor: "rgba(59,130,246,0.08)",
        fill: true,
        tension: 0.4,
        pointRadius: 0,
        pointHoverRadius: 5,
        pointHoverBackgroundColor: "#3B82F6",
      }]
    },
    options: {
      responsive: true, maintainAspectRatio: false,
      plugins: { legend: { display: false }, tooltip: {
        callbacks: { label: ctx => fmt(ctx.parsed.y) + " €" }
      }},
      scales: {
        x: { grid: { display: false }, ticks: { font: { size: 10 }, color: "#94A3B8" } },
        y: { grid: { color: "#F1F5F9" }, ticks: { font: { size: 10 }, color: "#94A3B8", callback: v => (v/1000).toFixed(0) + "K" } }
      }
    }
  });

  // Alloc Chart
  const types = { stock:"Actions", crypto:"Crypto", etf:"ETF", immo:"Immo" };
  const colors = { stock:"#3B82F6", crypto:"#8B5CF6", etf:"#06B6D4", immo:"#14B8A6" };
  const grp = {};
  all.forEach(a => { grp[a.type] = (grp[a.type] || 0) + a.val; });
  const allocData = Object.entries(grp).map(([t,v]) => ({ type:t, val:v, pct:(v/totalVal*100) }));

  if (allocChart) { allocChart.destroy(); allocChart = null; }
  const ctx2 = document.getElementById("chartAlloc").getContext("2d");
  allocChart = new Chart(ctx2, {
    type: "doughnut",
    data: {
      labels: allocData.map(d => types[d.type] || d.type),
      datasets: [{ data: allocData.map(d => d.val), backgroundColor: allocData.map(d => colors[d.type] || "#94A3B8"), borderWidth: 2, borderColor: "#FFF", hoverOffset: 4 }]
    },
    options: {
      responsive: true, maintainAspectRatio: false,
      plugins: { legend: { display: false }, tooltip: {
        callbacks: { label: ctx => fmt(ctx.parsed) + " €" }
      }},
      cutout: "65%"
    }
  });

  document.getElementById("allocList").innerHTML = allocData.map(d =>
    `<div class="alloc-item">
      <div class="alloc-dot" style="background:${colors[d.type]||"#94A3B8"}"></div>
      <div class="alloc-label">${types[d.type]||d.type}</div>
      <div class="alloc-bar-wrap"><div class="alloc-bar" style="width:${d.pct}%;background:${colors[d.type]||"#94A3B8"}"></div></div>
      <div class="alloc-pct">${d.pct.toFixed(0)}%</div>
    </div>`
  ).join("");

  // Wallets
  const wColors = {PEA:"#10B981",CTO:"#3B82F6",Binance:"#8B5CF6",Kraken:"#06B6D4",Immo:"#14B8A6"};
  const wIcons = {PEA:"🇫🇷",CTO:"📈",Binance:"₿",Kraken:"🐙",Immo:"🏘️"};
  const wallets = ["PEA","CTO","Binance","Kraken","Immo"];
  document.getElementById("walletGrid").innerHTML = wallets.map(w => {
    const wa = all.filter(a => a.wallet === w);
    const wv = wa.reduce((s,a) => s + a.val, 0);
    const wpv = wa.reduce((s,a) => s + a.pv, 0);
    const c = wColors[w] || "#64748B";
    return `<div style="background:${c}15;border:1px solid ${c}33;border-radius:12px;padding:14px">
      <div style="font-size:20px;margin-bottom:6px">${wIcons[w]||"📁"}</div>
      <div style="font-size:10px;color:#64748B;font-weight:700;letter-spacing:0.5px;text-transform:uppercase">${w}</div>
      <div style="font-size:16px;font-weight:800;color:#1A202C;margin-top:4px">${fmt(Math.round(wv))} €</div>
      <div style="font-size:10px;font-weight:700;color:${wpv>=0?"#059669":"#DC2626"};margin-top:2px">${wpv>=0?"+":""}${fmt(Math.round(wpv))} €</div>
      <div style="font-size:9px;color:#94A3B8;margin-top:3px">${wa.length} actif${wa.length>1?"s":""}</div>
    </div>`;
  }).join("");
}

// ════════════════════════════════════════
// PORTFOLIO
// ════════════════════════════════════════
let walletFilter = "all";

function filterWallet(w, btn) {
  walletFilter = w;
  document.querySelectorAll(".wallet-tab").forEach(b => {
    b.classList.remove("active");
    b.style.background = "#FFF";
    b.style.color = "#64748B";
  });
  const colors = {all:"#3B82F6",PEA:"#10B981",CTO:"#3B82F6",Binance:"#8B5CF6",Kraken:"#06B6D4",Immo:"#14B8A6"};
  btn.classList.add("active");
  btn.style.background = colors[w] || "#3B82F6";
  btn.style.color = "#FFF";
  renderPortfolio();
}

function renderPortfolio() {
  const all = getAll();
  const filtered = walletFilter === "all" ? all : all.filter(a => a.wallet === walletFilter);
  const fmt = (n,d=0) => n.toLocaleString("fr-FR",{minimumFractionDigits:d,maximumFractionDigits:d});
  const wColors = {PEA:"#10B981",CTO:"#3B82F6",Binance:"#8B5CF6",Kraken:"#06B6D4",Immo:"#14B8A6"};
  const now = new Date().toLocaleDateString("fr-FR",{day:"2-digit",month:"2-digit",hour:"2-digit",minute:"2-digit"});
  document.getElementById("portfolioUpdate").textContent = `MAJ ${now}`;

  if (filtered.length === 0) {
    document.getElementById("assetList").innerHTML = `<div class="empty-state"><div class="empty-icon">💼</div><div class="empty-text">Aucun actif</div><div class="empty-sub">Tape le bouton + pour ajouter</div></div>`;
    return;
  }

  document.getElementById("assetList").innerHTML = filtered.map(a => {
    const pvSign = a.pv >= 0 ? "+" : "";
    const pvClass = a.pv >= 0 ? "pv-pos" : "pv-neg";
    const wc = wColors[a.wallet] || "#64748B";
    return `<div class="asset-card">
      <div class="asset-top">
        <div class="asset-left">
          <div class="asset-icon">${a.logo||"📊"}</div>
          <div>
            <div class="asset-name">${a.ticker}</div>
            <div class="asset-sub">${a.nom}</div>
            <div class="asset-wallet" style="background:${wc}20;color:${wc}">${a.wallet}</div>
          </div>
        </div>
        <div class="asset-right">
          <div class="asset-value">${fmt(Math.round(a.val))} €</div>
          <div class="asset-pv ${pvClass}">${pvSign}${fmt(Math.round(a.pv))} € (${pvSign}${a.pvPct.toFixed(1)}%)</div>
        </div>
      </div>
      <div class="asset-stats">
        <div class="stat-item"><div class="stat-label">Qté</div><div class="stat-value">${a.qte}</div></div>
        <div class="stat-item"><div class="stat-label">PRU</div><div class="stat-value">${fmt(a.pru)}</div></div>
        <div class="stat-item"><div class="stat-label">Cours</div><div class="stat-value">${fmt(a.cours)}</div></div>
      </div>
      <div class="asset-actions">
        <button class="btn-analyse" onclick="analyseAsset(${a.id})">🤖 Analyser</button>
        <button class="btn-delete" onclick="deleteAsset(${a.id})">🗑️</button>
      </div>
    </div>`;
  }).join("");
}

function deleteAsset(id) {
  if (confirm("Supprimer cet actif ?")) {
    S.assets = S.assets.filter(a => a.id !== id);
    save();
    renderPortfolio();
    renderDashboard();
  }
}

function analyseAsset(id) {
  const a = S.assets.find(x => x.id === id);
  if (!a) return;
  showView("analyse", document.querySelectorAll(".nav-btn")[2]);
  document.getElementById("analyseQuery").value = `${a.nom} (${a.ticker})`;
  setAnalyseTab(a.type === "crypto" ? "crypto" : a.type === "immo" ? "immo" : "stock", null);
}

// ════════════════════════════════════════
// ADD ASSET
// ════════════════════════════════════════
function openModal() { document.getElementById("addModal").classList.add("open"); }
function closeModal() { document.getElementById("addModal").classList.remove("open"); }

function addAsset() {
  const ticker = document.getElementById("fTicker").value.trim().toUpperCase();
  const nom = document.getElementById("fNom").value.trim();
  const type = document.getElementById("fType").value;
  const wallet = document.getElementById("fWallet").value;
  const qte = parseFloat(document.getElementById("fQte").value) || 0;
  const pru = parseFloat(document.getElementById("fPRU").value) || 0;
  const cours = parseFloat(document.getElementById("fCours").value) || 0;
  const div = parseFloat(document.getElementById("fDiv").value) || 0;

  if (!ticker || !nom || qte <= 0) { alert("Remplis au moins le ticker, le nom et la quantité"); return; }

  const logos = { stock:"📈", crypto:"₿", etf:"📊", immo:"🏢" };
  S.assets.push({ id: Date.now(), ticker, nom, type, wallet, qte, pru, cours, div, logo: logos[type] || "📊" });
  save();
  closeModal();
  ["fTicker","fNom","fQte","fPRU","fCours","fDiv"].forEach(id => document.getElementById(id).value = "");
  renderPortfolio();
  renderDashboard();
}

// ════════════════════════════════════════
// REFRESH PRICES (CoinGecko for crypto)
// ════════════════════════════════════════
async function refreshPrices() {
  const btn = document.getElementById("refreshBtn");
  btn.textContent = "⟳ Actualisation...";
  btn.disabled = true;

  try {
    const cryptos = S.assets.filter(a => a.type === "crypto");
    if (cryptos.length > 0) {
      const idMap = { BTC:"bitcoin", ETH:"ethereum", SOL:"solana", ADA:"cardano", BNB:"binancecoin", XRP:"ripple", DOGE:"dogecoin", LTC:"litecoin", DOT:"polkadot", AVAX:"avalanche-2", MATIC:"matic-network", LINK:"chainlink" };
      const ids = [...new Set(cryptos.map(c => idMap[c.ticker.toUpperCase()] || c.ticker.toLowerCase()))].join(",");
      const res = await fetch(`https://api.coingecko.com/api/v3/simple/price?ids=${ids}&vs_currencies=usd,eur`);
      if (res.ok) {
        const data = await res.json();
        S.assets = S.assets.map(a => {
          if (a.type !== "crypto") return a;
          const cgId = idMap[a.ticker.toUpperCase()] || a.ticker.toLowerCase();
          if (data[cgId]) {
            return { ...a, cours: data[cgId].eur || data[cgId].usd || a.cours };
          }
          return a;
        });
        save();
      }
    }
    const now = new Date().toLocaleTimeString("fr-FR", { hour: "2-digit", minute: "2-digit" });
    document.getElementById("lastUpdateLabel").textContent = `MAJ ${now}`;
    if (currentView === "dashboard") renderDashboard();
    if (currentView === "portfolio") renderPortfolio();
    btn.textContent = "✓ Actualisé";
    setTimeout(() => { btn.textContent = "⟳ Actualiser"; btn.disabled = false; }, 2000);
  } catch (e) {
    btn.textContent = "⟳ Actualiser";
    btn.disabled = false;
    alert("Erreur réseau. Vérifiez votre connexion.");
  }
}

// ════════════════════════════════════════
// ANALYSE
// ════════════════════════════════════════
const STOCK_METHODS = [
  { id:"graham", icon:"📚", name:"BENJAMIN GRAHAM", sub:"Value Investing", desc:"P/E<15 · P/Book<1.5 · Marge sécu>30%", c:"#3B82F6", s:"#EFF6FF" },
  { id:"buffett", icon:"🏆", name:"WARREN BUFFETT", sub:"Quality Investing", desc:"ROE>15% · Moat · FCF+ 5 ans", c:"#10B981", s:"#F0FDF4" },
  { id:"lynch", icon:"📈", name:"PETER LYNCH", sub:"GARP", desc:"PEG<1 · Croissance BPA>15%/an", c:"#06B6D4", s:"#ECFEFF" },
];
const CRYPTO_METHODS = [
  { id:"fa", icon:"🔍", name:"FUNDAMENTAL", sub:"FA Classique", desc:"Équipe · Roadmap · Use case réel", c:"#8B5CF6", s:"#F5F3FF" },
  { id:"value", icon:"💎", name:"CRYPTO VALUE", sub:"MC/TVL", desc:"Market Cap vs TVL · Décote ATH", c:"#3B82F6", s:"#EFF6FF" },
  { id:"onchain", icon:"⛓️", name:"ON-CHAIN", sub:"Blockchain data", desc:"NVT · Active addresses · Hash rate", c:"#06B6D4", s:"#ECFEFF" },
  { id:"tokenomics", icon:"🪙", name:"TOKENOMICS", sub:"Économie du token", desc:"Supply · Vesting · Inflation · Burn", c:"#F59E0B", s:"#FFFBEB" },
  { id:"network", icon:"🌐", name:"NETWORK VALUE", sub:"Loi de Metcalfe", desc:"DAU · Fees · GitHub commits", c:"#10B981", s:"#F0FDF4" },
];
const IMMO_METHODS = [
  { id:"rendement", icon:"💹", name:"RENDEMENT", sub:"Yield analysis", desc:"Brut/Net · Fiscalité · Vs OAT", c:"#10B981", s:"#F0FDF4" },
  { id:"localisation", icon:"📍", name:"LOCALISATION", sub:"Géographique", desc:"Démographie · Emploi · Projets", c:"#3B82F6", s:"#EFF6FF" },
  { id:"scpi", icon:"📊", name:"SCPI", sub:"Pierre papier", desc:"TRI · TOF · Gestionnaire", c:"#14B8A6", s:"#F0FDFA" },
];

function setAnalyseTab(tab, btn) {
  S.analyseTab = tab;
  S.selectedMethods = [];
  if (btn) {
    document.querySelectorAll("#view-analyse .nav-btn").forEach(b => b.classList.remove("active"));
    btn.classList.add("active");
  }
  const methods = tab === "stock" ? STOCK_METHODS : tab === "crypto" ? CRYPTO_METHODS : IMMO_METHODS;
  document.getElementById("methodGrid").innerHTML = methods.map(m =>
    `<button class="method-card" id="mc_${m.id}" onclick="toggleMethod('${m.id}')" style="--mc:${m.c};--ms:${m.s}">
      <div class="method-top">
        <div class="method-icon">${m.icon}</div>
        <div><div class="method-name">${m.name}</div><div class="method-sub">${m.sub}</div></div>
        <div class="method-check" id="chk_${m.id}" style="background:#E2E8F0;color:transparent">✓</div>
      </div>
      <div class="method-desc">${m.desc}</div>
    </button>`
  ).join("");
  updateAnalyseBtn();
}

function toggleMethod(id) {
  const idx = S.selectedMethods.indexOf(id);
  const card = document.getElementById("mc_" + id);
  const chk = document.getElementById("chk_" + id);
  const methods = S.analyseTab === "stock" ? STOCK_METHODS : S.analyseTab === "crypto" ? CRYPTO_METHODS : IMMO_METHODS;
  const m = methods.find(x => x.id === id);
  if (idx >= 0) {
    S.selectedMethods.splice(idx, 1);
    card.classList.remove("active");
    chk.style.background = "#E2E8F0";
    chk.style.color = "transparent";
  } else {
    S.selectedMethods.push(id);
    card.classList.add("active");
    chk.style.background = m.c;
    chk.style.color = "#FFF";
  }
  updateAnalyseBtn();
}

function updateAnalyseBtn() {
  const n = S.selectedMethods.length;
  document.getElementById("analyseFormTitle").textContent = `🔍 Analyse — ${n} méthode${n>1?"s":""} sélectionnée${n>1?"s":""}`;
  document.getElementById("launchBtn").disabled = n === 0 || !document.getElementById("analyseQuery").value.trim();
}

document.addEventListener("input", e => { if (e.target.id === "analyseQuery") updateAnalyseBtn(); });

async function runAnalyse() {
  const query = document.getElementById("analyseQuery").value.trim();
  if (!query || S.selectedMethods.length === 0) return;

  const methods = S.analyseTab === "stock" ? STOCK_METHODS : S.analyseTab === "crypto" ? CRYPTO_METHODS : IMMO_METHODS;
  const methodNames = methods.filter(m => S.selectedMethods.includes(m.id)).map(m => m.name).join(" + ");

  document.getElementById("searchingBox").style.display = "flex";
  document.getElementById("analyseResult").style.display = "none";
  document.getElementById("launchBtn").disabled = true;

  // Try to get crypto price from CoinGecko first
  let cryptoPrice = null;
  if (S.analyseTab === "crypto") {
    try {
      const cgId = query.toLowerCase().replace(/\s/g, "-");
      const res = await fetch(`https://api.coingecko.com/api/v3/simple/price?ids=${cgId},bitcoin,ethereum,solana&vs_currencies=usd`);
      if (res.ok) {
        const data = await res.json();
        cryptoPrice = data[cgId]?.usd || null;
      }
    } catch(e) {}
  }

  // Try Claude API if key available
  const apiKey = S.apiKey;
  if (apiKey && apiKey.startsWith("sk-ant")) {
    await runClaudeAnalyse(query, methodNames, cryptoPrice, apiKey);
  } else {
    runLocalAnalyse(query, methodNames, cryptoPrice);
  }

  document.getElementById("searchingBox").style.display = "none";
  document.getElementById("analyseResult").style.display = "block";
  document.getElementById("launchBtn").disabled = false;
}

function runLocalAnalyse(query, methodNames, cryptoPrice) {
  const rp = {defensif:"DÉFENSIF (-10%)",equilibre:"ÉQUILIBRÉ (-20%)",dynamique:"DYNAMIQUE (-30%)",agressif:"AGRESSIF (-50%)"}[S.riskProfile] || "DYNAMIQUE";
  const priceInfo = cryptoPrice ? `\n💹 COURS ACTUEL : ${cryptoPrice.toLocaleString()} $ (via CoinGecko)` : `\n💹 COURS ACTUEL : À vérifier sur votre broker`;

  const text = `🎯 ${query.toUpperCase()} — Analyse préliminaire

📋 MÉTHODOLOGIES APPLIQUÉES : ${methodNames}
${priceInfo}

📊 ANALYSE BASÉE SUR LES DONNÉES PUBLIQUES DISPONIBLES

Cette analyse est générée sur la base des critères de ${methodNames}.

Pour une analyse complète avec données vérifiables en temps réel (P/E, ROE, FCF, ratios fondamentaux, actualités), ajoutez votre clé API Anthropic dans ⚙️ Réglages.

📐 SIZING (Profil ${rp}) :
Avec un portefeuille intermédiaire et un régime de marché modéré (VIX ~18), une position de 5-8% maximum est conseillée pour cet actif.

🏛️ FISCALITÉ FRANÇAISE :
${S.analyseTab === "crypto" ? "Crypto → CTO uniquement · PFU 30% · Seuil cession 305€/an" : S.analyseTab === "immo" ? "Immobilier → Revenus fonciers ou micro-foncier selon montant" : "Action Europe éligible PEA → PEA prioritaire (exonération après 5 ans)\nAction US/ETF monde → CTO (PFU 30%)"}

⚠️ Usage éducatif uniquement. Pas un conseil financier AMF réglementé.`;

  const box = document.getElementById("analyseResult");
  box.className = "result-box";
  box.textContent = text;
}

async function runClaudeAnalyse(query, methodNames, cryptoPrice, apiKey) {
  const priceCtx = cryptoPrice ? `Cours actuel récupéré via CoinGecko : ${cryptoPrice.toLocaleString()} $` : "";
  const rp = S.riskProfile;
  const systemPrompt = `Tu es ATLAS, analyste financier expert. Profil utilisateur : ${rp}. Date : 27 avril 2026.

${priceCtx}

Méthodologies à appliquer : ${methodNames}.

Format de réponse :
🎯 [NOM] [TICKER] — Conviction X/10
💹 COURS ACTUEL : [prix avec source]
📊 ANALYSE : selon ${methodNames}
💰 VALORISATION : valeur intrinsèque, marge de sécurité, zone d'achat
📐 SIZING : X% | PEA ou CTO | Kelly adapté
⚠️ RISQUE PRINCIPAL : stop fondamental
📅 HORIZON : durée et catalyseur
🏛️ FISCALITÉ : PEA si Europe, CTO sinon (PFU 30%)

Français, max 400 mots, professionnel et direct.
⚠️ Termine par : "Usage éducatif · Pas un conseil AMF réglementé."`;

  try {
    const res = await fetch("https://api.anthropic.com/v1/messages", {
      method: "POST",
      headers: { "Content-Type": "application/json", "x-api-key": apiKey, "anthropic-version": "2023-06-01", "anthropic-dangerous-direct-browser-access": "true" },
      body: JSON.stringify({
        model: "claude-sonnet-4-20250514",
        max_tokens: 1000,
        system: systemPrompt,
        messages: [{ role: "user", content: `Analyse : ${query}` }]
      })
    });
    const data = await res.json();
    let text = "";
    if (data.content) { for (const b of data.content) if (b.type === "text") text += b.text; }
    const box = document.getElementById("analyseResult");
    box.className = text ? "result-box" : "result-box error";
    box.textContent = text || "Erreur de réponse API.";
  } catch(e) {
    const box = document.getElementById("analyseResult");
    box.className = "result-box error";
    box.textContent = "Erreur réseau. Vérifiez votre connexion ou votre clé API.";
  }
}

// ════════════════════════════════════════
// CHATBOT
// ════════════════════════════════════════
const QUICK_MSGS = [
  "📈 Analyse Apple (AAPL)",
  "₿ Bitcoin : acheter maintenant ?",
  "🇪🇺 Meilleure action PEA Europe",
  "⚖️ Rééquilibrer mon portefeuille",
  "🏘️ SCPI vs immobilier locatif",
];

function renderChat() {
  document.getElementById("chatQuick").innerHTML = QUICK_MSGS.map(q =>
    `<button class="quick-btn" onclick="sendQuick('${q}')">${q}</button>`
  ).join("");
  renderChatMessages();
  if (S.chatHistory.length === 0) {
    addBotMsg(`Bonjour ! Je suis **ATLAS** 🤖, votre conseiller financier personnel.\n\n✅ Votre portefeuille est chargé (${S.assets.length} actifs)\n✅ Profil : ${S.riskProfile}\n\n${S.apiKey ? "✅ Clé API configurée — analyses IA complètes disponibles" : "⚠️ Sans clé API : réponses basées sur les données publiques"}\n\nComment puis-je vous aider ?`);
  }
}

function renderChatMessages() {
  const container = document.getElementById("chatMessages");
  container.innerHTML = S.chatHistory.map(m =>
    `<div class="msg ${m.role}">
      <div class="msg-sender">${m.role === "user" ? "▸ VOUS" : "◈ ATLAS"}</div>
      <div class="msg-bubble">${formatMsg(m.content)}</div>
    </div>`
  ).join("");
  container.scrollTop = container.scrollHeight;
}

function formatMsg(text) {
  return text.replace(/\*\*([^*]+)\*\*/g, "<strong>$1</strong>").replace(/\n/g, "<br>");
}

function addBotMsg(text) {
  S.chatHistory.push({ role: "bot", content: text });
  renderChatMessages();
}

function sendQuick(q) {
  document.getElementById("chatInput").value = q;
  sendChat();
}

async function sendChat() {
  const input = document.getElementById("chatInput");
  const q = input.value.trim();
  if (!q) return;
  input.value = "";
  S.chatHistory.push({ role: "user", content: q });
  renderChatMessages();
  const send = document.getElementById("chatSend");
  send.disabled = true;
  const { totalVal, totalPV, totalPVPct } = totals();

  if (S.apiKey && S.apiKey.startsWith("sk-ant")) {
    const systemPrompt = `Tu es ATLAS, conseiller financier IA. Portefeuille: ${S.assets.length} actifs, valeur totale ${Math.round(totalVal)}€, performance ${totalPVPct.toFixed(1)}%. Profil: ${S.riskProfile}. Date: 27 avril 2026. Réponds en français, max 300 mots, professionnel. Termine par "Usage éducatif".`;
    try {
      const res = await fetch("https://api.anthropic.com/v1/messages", {
        method: "POST",
        headers: { "Content-Type": "application/json", "x-api-key": S.apiKey, "anthropic-version": "2023-06-01", "anthropic-dangerous-direct-browser-access": "true" },
        body: JSON.stringify({
          model: "claude-sonnet-4-20250514",
          max_tokens: 800,
          system: systemPrompt,
          messages: S.chatHistory.filter(m => m.role !== "bot").slice(-6).map(m => ({ role: "user", content: m.content }))
        })
      });
      const data = await res.json();
      let text = "";
      if (data.content) for (const b of data.content) if (b.type === "text") text += b.text;
      addBotMsg(text || "Désolé, je n'ai pas pu générer de réponse.");
    } catch(e) { addBotMsg("Erreur de connexion. Vérifiez votre clé API dans les réglages."); }
  } else {
    const responses = {
      "apple": "**Apple (AAPL)** est une entreprise solide selon les critères Buffett :\n✅ ROE > 100%\n✅ Marge nette ~25%\n⚠️ P/E ~28 (légèrement élevé selon Graham)\n\nPour une analyse complète, ajoutez votre clé API dans ⚙️ Réglages.\n\n⚠️ Usage éducatif.",
      "bitcoin": "**Bitcoin (BTC)** — Cours actuel ~94 000$\n\n₿ Perspective On-Chain :\n• Supply max : 21M (déflationniste)\n• Adoption institutionnelle croissante\n• Halving effectué en 2024\n\nSizing recommandé (profil dynamique) : 5-10% max du portefeuille.\n\n⚠️ Usage éducatif.",
      "pea": "**Meilleures actions PEA actuellement :**\n\n1. **ASML** - Leadership mondial lithographie EUV\n2. **LVMH** - Moat luxe inattaquable\n3. **TotalEnergies** - Yield 8%+\n4. **Schneider Electric** - Thème électrification\n\nPour une analyse avec données en temps réel, activez la clé API.\n\n⚠️ Usage éducatif.",
      "default": `Votre portefeuille de **${S.assets.length} actifs** (${Math.round(totalVal).toLocaleString("fr-FR")} €) présente une performance de **${totalPVPct.toFixed(1)}%** vs PRU.\n\nPour des conseils personnalisés basés sur des données financières en temps réel, configurez votre clé API Anthropic dans ⚙️ Réglages.\n\n⚠️ Usage éducatif.`
    };
    const lower = q.toLowerCase();
    const key = Object.keys(responses).find(k => k !== "default" && lower.includes(k)) || "default";
    setTimeout(() => { addBotMsg(responses[key]); }, 800);
  }
  send.disabled = false;
}

// ════════════════════════════════════════
// SETTINGS
// ════════════════════════════════════════
const RISK_PROFILES = {
  defensif: { icon:"🛡️", name:"DÉFENSIF", dd:"-10%", desc:"Priorité capital · Dividendes · Obligations", c:"#06B6D4", s:"#ECFEFF" },
  equilibre: { icon:"⚖️", name:"ÉQUILIBRÉ", dd:"-20%", desc:"Croissance modérée · Mix Value/Growth", c:"#10B981", s:"#F0FDF4" },
  dynamique: { icon:"🚀", name:"DYNAMIQUE", dd:"-30%", desc:"Performance max · Volatilité acceptée", c:"#3B82F6", s:"#EFF6FF" },
  agressif: { icon:"⚡", name:"AGRESSIF", dd:"-50%", desc:"Max rendement · Crypto incluse · Levier", c:"#EF4444", s:"#FEF2F2" },
};

function renderSettings() {
  document.getElementById("goalInput").value = S.goal || "";
  document.getElementById("goalDate").value = S.goalDate || "";
  document.getElementById("apiKeyInput").value = S.apiKey || "";

  document.getElementById("riskGrid").innerHTML = Object.entries(RISK_PROFILES).map(([k,p]) =>
    `<button class="risk-btn ${S.riskProfile===k?"active":""}" onclick="setRisk('${k}')" style="--rc:${p.c};--rs:${p.s}">
      <div class="risk-btn-top">
        <div class="risk-btn-name">${p.icon} ${p.name}</div>
        <div class="risk-btn-dd badge-${k==="agressif"?"red":k==="defensif"?"blue":"green"}" style="background:${p.s};color:${p.c}">${p.dd}</div>
      </div>
      <div class="risk-btn-desc">${p.desc}</div>
    </button>`
  ).join("");

  document.getElementById("notifSettings").innerHTML = [
    { id:"daily", name:"Résumé quotidien à 00h00", desc:"Synthèse de votre portefeuille chaque matin" },
    { id:"alerts", name:"Alertes intelligentes", desc:"Drawdown, cible atteinte, news critique" },
    { id:"weekly", name:"Rapport hebdomadaire", desc:"Bilan du dimanche soir" },
  ].map(n =>
    `<div class="settings-item">
      <div class="settings-item-left">
        <div class="name">${n.name}</div>
        <div class="desc">${n.desc}</div>
      </div>
      <div class="toggle ${S.notifications[n.id]?"on":""}" onclick="toggleNotif('${n.id}',this)"></div>
    </div>`
  ).join("");
}

function setRisk(k) {
  S.riskProfile = k;
  save();
  renderSettings();
}

function toggleNotif(id, el) {
  S.notifications[id] = !S.notifications[id];
  el.classList.toggle("on");
  save();
}

function saveGoal() {
  S.goal = parseFloat(document.getElementById("goalInput").value) || 0;
  S.goalDate = document.getElementById("goalDate").value;
  save();
}

function saveApiKey() {
  S.apiKey = document.getElementById("apiKeyInput").value.trim();
  save();
}

// ════════════════════════════════════════
// IMPORT / EXPORT
// ════════════════════════════════════════
function exportData() {
  const json = JSON.stringify({ assets: S.assets, riskProfile: S.riskProfile, goal: S.goal, goalDate: S.goalDate }, null, 2);
  const blob = new Blob([json], { type: "application/json" });
  const url = URL.createObjectURL(blob);
  const a = document.createElement("a");
  a.href = url; a.download = "atlas_portfolio.json"; a.click();
  URL.revokeObjectURL(url);
}

function importData() { document.getElementById("importFile").click(); }

function handleImport(e) {
  const file = e.target.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = ev => {
    try {
      const data = JSON.parse(ev.target.result);
      if (data.assets) { S.assets = data.assets; save(); renderPortfolio(); renderDashboard(); alert("Import réussi !"); }
    } catch { alert("Fichier invalide."); }
  };
  reader.readAsText(file);
}

function clearAll() {
  S.assets = []; S.chatHistory = []; save();
  renderDashboard(); renderPortfolio(); renderChat();
}

// ════════════════════════════════════════
// INIT
// ════════════════════════════════════════
load();
renderTicker();
renderDashboard();
setAnalyseTab("stock", null);
document.getElementById("addFab").style.display = "none";

// Add first bot message on load
setTimeout(() => {
  if (currentView === "chat" && S.chatHistory.length === 0) renderChat();
}, 100);
</script>
</body>
</html>
