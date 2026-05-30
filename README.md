<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>맥서브 오산 LG화학 안전관리 시스템</title>
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@400;500;600;700;800;900&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet"/>
  <style>
  :root {
    --bg:#0d1117; --bg2:#161b22; --bg3:#1c2128;
    --surface:#21262d; --surface2:#2d333b;
    --border:#30363d;
    --text:#e6edf3; --text2:#8b949e; --text3:#484f58;
    --blue:#388bfd; --blue-dim:rgba(56,139,253,.15);
    --green:#3fb950; --green-dim:rgba(63,185,80,.12);
    --amber:#e3b341; --amber-dim:rgba(227,179,65,.12);
    --red:#f85149; --red-dim:rgba(248,81,73,.12);
    --purple:#bc8cff; --purple-dim:rgba(188,140,255,.12);
    --cyan:#39c5cf; --cyan-dim:rgba(57,197,207,.12);
    --radius:12px; --radius-lg:20px;
    --admin-accent:#f0883e; --admin-dim:rgba(240,136,62,.12);
  }
  *{margin:0;padding:0;box-sizing:border-box;}
  body{font-family:'Noto Sans KR',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;overflow-x:hidden;}
  body::before{content:'';position:fixed;inset:0;z-index:0;pointer-events:none;
    background-image:linear-gradient(rgba(56,139,253,.04) 1px,transparent 1px),linear-gradient(90deg,rgba(56,139,253,.04) 1px,transparent 1px);
    background-size:32px 32px;}
  #app{position:relative;z-index:1;max-width:1060px;margin:0 auto;padding:0 20px 80px;}

  header{padding:32px 0 24px;border-bottom:1px solid var(--border);margin-bottom:28px;display:flex;align-items:center;justify-content:space-between;gap:12px;flex-wrap:wrap;}
  .header-brand{display:flex;align-items:center;gap:14px;}
  .header-logo{width:48px;height:48px;border-radius:12px;background:linear-gradient(135deg,#388bfd,#bc8cff);display:flex;align-items:center;justify-content:center;font-size:22px;box-shadow:0 0 20px rgba(56,139,253,.3);flex-shrink:0;}
  .company{font-size:18px;font-weight:900;color:#fff;letter-spacing:-.5px;}
  .site{font-size:12px;color:var(--blue);font-weight:600;margin-top:1px;}
  .header-right{display:flex;align-items:center;gap:10px;flex-wrap:wrap;}
  .header-system{font-size:13px;font-weight:700;color:var(--text2);padding:6px 12px;border:1px solid var(--border);border-radius:8px;white-space:nowrap;}
  .admin-badge{display:none;align-items:center;gap:6px;background:var(--admin-dim);border:1px solid var(--admin-accent);color:var(--admin-accent);font-size:12px;font-weight:800;padding:5px 12px;border-radius:8px;}
  .admin-badge.show{display:flex;}
  .admin-dot{width:6px;height:6px;border-radius:50%;background:var(--admin-accent);animation:pulse 1.5s infinite;}
  @keyframes pulse{0%,100%{opacity:1}50%{opacity:.3}}
  #adminLoginBtn{display:flex;align-items:center;gap:7px;padding:7px 14px;border-radius:8px;border:1px solid var(--border);background:var(--surface);color:var(--text2);font-size:13px;font-weight:700;cursor:pointer;transition:all .2s;font-family:'Noto Sans KR',sans-serif;}
  #adminLoginBtn:hover{border-color:var(--admin-accent);color:var(--admin-accent);}
  #adminLogoutBtn{display:none;align-items:center;gap:7px;padding:7px 14px;border-radius:8px;border:1px solid var(--border);background:var(--surface);color:var(--text2);font-size:13px;font-weight:700;cursor:pointer;transition:all .2s;font-family:'Noto Sans KR',sans-serif;}
  #adminLogoutBtn.show{display:flex;}
  #adminLogoutBtn:hover{border-color:var(--red);color:var(--red);}

  .view{display:none;animation:fadeUp .3s ease;}
  .view.active{display:block;}
  @keyframes fadeUp{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}

  .notice-banner{background:var(--bg2);border:1px solid var(--border);border-left:4px solid var(--amber);border-radius:var(--radius-lg);padding:18px 20px;display:flex;align-items:center;gap:14px;cursor:pointer;transition:all .25s ease;margin-bottom:24px;color:inherit;}
  .notice-banner:hover{border-color:var(--amber);transform:translateX(4px);background:var(--bg3);}
  .nb-icon{font-size:22px;flex-shrink:0;}
  .nb-label{font-size:10px;font-weight:900;letter-spacing:1px;padding:2px 8px;border-radius:4px;display:inline-block;margin-bottom:3px;}
  .nb-title{font-size:15px;font-weight:700;color:var(--text);}
  .nb-date{font-size:11px;color:var(--text3);margin-top:2px;font-family:'JetBrains Mono',monospace;}
  .nb-arrow{margin-left:auto;font-size:18px;color:var(--text3);flex-shrink:0;}

  .menu-grid{display:grid;grid-template-columns:repeat(5,1fr);gap:12px;margin-bottom:32px;}
  @media(max-width:860px){.menu-grid{grid-template-columns:repeat(3,1fr);}}
  @media(max-width:520px){.menu-grid{grid-template-columns:repeat(2,1fr);}}
  .menu-card{background:var(--bg2);border:1px solid var(--border);border-radius:var(--radius-lg);padding:20px 14px 16px;cursor:pointer;transition:all .3s cubic-bezier(.4,0,.2,1);text-align:center;display:flex;flex-direction:column;align-items:center;gap:8px;position:relative;overflow:hidden;text-decoration:none;color:inherit;}
  .menu-card::after{content:'';position:absolute;bottom:0;left:0;right:0;height:3px;border-radius:0 0 var(--radius-lg) var(--radius-lg);opacity:0;transition:opacity .3s;}
  .menu-card:hover{transform:translateY(-5px);border-color:rgba(56,139,253,.3);}
  .menu-card:hover::after{opacity:1;}
  .mc-notice::after{background:linear-gradient(90deg,var(--amber),#f0883e);}
  .mc-safety::after{background:linear-gradient(90deg,var(--purple),#818cf8);}
  .mc-msds::after{background:linear-gradient(90deg,var(--red),#ec4899);}
  .mc-report::after{background:linear-gradient(90deg,var(--cyan),var(--blue));}
  .mc-opinion::after{background:linear-gradient(90deg,var(--green),#10b981);}
  .mc-icon{width:48px;height:48px;border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:22px;transition:transform .3s ease;}
  .menu-card:hover .mc-icon{transform:scale(1.12) rotate(-6deg);}
  .mc-notice .mc-icon{background:var(--amber-dim);border:1px solid rgba(227,179,65,.2);}
  .mc-safety .mc-icon{background:var(--purple-dim);border:1px solid rgba(188,140,255,.2);}
  .mc-msds .mc-icon{background:var(--red-dim);border:1px solid rgba(248,81,73,.2);}
  .mc-report .mc-icon{background:var(--cyan-dim);border:1px solid rgba(57,197,207,.2);}
  .mc-opinion .mc-icon{background:var(--green-dim);border:1px solid rgba(63,185,80,.2);}
  .mc-title{font-size:13px;font-weight:800;color:var(--text);letter-spacing:-.3px;}
  .mc-sub{font-size:11px;color:var(--text3);line-height:1.4;}

  .admin-section{display:none;margin-top:16px;background:var(--admin-dim);border:1px solid var(--admin-accent);border-radius:var(--radius-lg);padding:20px;}
  .admin-section.show{display:block;}
  .admin-section-title{font-size:12px;font-weight:900;color:var(--admin-accent);letter-spacing:1px;margin-bottom:14px;display:flex;align-items:center;gap:8px;}
  .admin-menu-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:10px;}
  .admin-menu-btn{background:var(--bg2);border:1px solid var(--border);border-radius:var(--radius);padding:14px 12px;cursor:pointer;transition:all .2s;text-align:center;display:flex;flex-direction:column;align-items:center;gap:6px;font-family:'Noto Sans KR',sans-serif;color:var(--text);text-decoration:none;}
  .admin-menu-btn:hover{border-color:var(--admin-accent);transform:translateY(-2px);}
  .ambi{font-size:20px;}.ambt{font-size:12px;font-weight:700;}.ambs{font-size:11px;color:var(--text3);margin-top:1px;}

  .page-header{display:flex;align-items:center;gap:12px;margin-bottom:20px;flex-wrap:wrap;}
  .back-btn{display:inline-flex;align-items:center;gap:6px;padding:8px 14px;border-radius:8px;border:1px solid var(--border);background:var(--surface);color:var(--text2);font-size:13px;font-weight:700;cursor:pointer;transition:all .2s;text-decoration:none;flex-shrink:0;font-family:'Noto Sans KR',sans-serif;}
  .back-btn:hover{border-color:var(--blue);color:var(--blue);}
  .page-ttl{font-size:22px;font-weight:900;color:#fff;letter-spacing:-.5px;}
  .page-sub{font-size:13px;color:var(--text3);margin-top:2px;}
  .panel{background:var(--bg2);border:1px solid var(--border);border-radius:var(--radius-lg);padding:24px;margin-bottom:16px;}

  .filter-row{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:16px;}
  .flt-btn{padding:6px 14px;border-radius:99px;border:1px solid var(--border);background:transparent;font-size:12px;font-weight:700;color:var(--text3);cursor:pointer;transition:all .2s;font-family:'Noto Sans KR',sans-serif;}
  .flt-btn:hover{border-color:var(--amber);color:var(--amber);}
  .flt-btn.active{background:var(--amber);border-color:var(--amber);color:#000;}
  .search-row{display:flex;gap:10px;margin-bottom:16px;}
  .search-inp{flex:1;padding:10px 14px;background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);color:var(--text);font-size:14px;outline:none;transition:border-color .2s;font-family:'Noto Sans KR',sans-serif;}
  .search-inp:focus{border-color:var(--blue);}
  .search-inp::placeholder{color:var(--text3);}

  .notice-list{display:grid;gap:10px;}
  .ni{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:14px 16px;display:flex;align-items:flex-start;gap:12px;transition:all .22s ease;}
  .ni:hover{border-color:rgba(56,139,253,.35);transform:translateX(4px);background:var(--surface2);}
  .ni.pinned{border-left:3px solid var(--amber);}
  .ni-badge{font-size:10px;font-weight:900;padding:2px 8px;border-radius:4px;flex-shrink:0;margin-top:2px;border:1px solid transparent;}
  .ni-body{flex:1;min-width:0;cursor:pointer;}
  .ni-title{font-size:14px;font-weight:700;color:var(--text);margin-bottom:3px;}
  .ni-summary{font-size:12px;color:var(--text3);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
  .ni-meta{font-size:11px;color:var(--text3);margin-top:4px;font-family:'JetBrains Mono',monospace;}
  .ni-arr{font-size:16px;color:var(--text3);flex-shrink:0;}

  .nd-badge-row{display:flex;align-items:center;gap:8px;margin-bottom:8px;}
  .nd-title{font-size:20px;font-weight:900;color:#fff;margin-bottom:6px;line-height:1.4;}
  .nd-info{font-size:12px;color:var(--text3);font-family:'JetBrains Mono',monospace;margin-bottom:18px;padding-bottom:16px;border-bottom:1px solid var(--border);}
  .nd-body{font-size:14px;color:var(--text2);line-height:1.9;white-space:pre-wrap;}
  .nd-body strong{color:var(--text);}

  .safety-cat-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;margin-top:4px;}
  @media(max-width:600px){.safety-cat-grid{grid-template-columns:repeat(2,1fr);}}
  .sc-btn{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:20px 14px;cursor:pointer;transition:all .28s ease;text-align:center;display:flex;flex-direction:column;align-items:center;gap:6px;font-family:'Noto Sans KR',sans-serif;}
  .sc-btn:hover{border-color:rgba(188,140,255,.5);transform:translateY(-3px);box-shadow:0 10px 24px rgba(0,0,0,.3);}
  .sc-icon{font-size:30px;}.sc-title{font-size:14px;font-weight:800;color:var(--text);line-height:1.3;}.sc-count{font-size:11px;color:var(--text3);font-family:'JetBrains Mono',monospace;}
  .rule-list{display:grid;gap:10px;margin-top:8px;}
  .rule-item{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:13px 15px;display:flex;gap:10px;}
  .rule-num{font-family:'JetBrains Mono',monospace;font-size:10px;font-weight:700;color:var(--purple);background:var(--purple-dim);border:1px solid rgba(188,140,255,.2);width:26px;height:20px;border-radius:5px;display:flex;align-items:center;justify-content:center;flex-shrink:0;margin-top:1px;}
  .rule-label{font-size:13px;font-weight:800;color:var(--text);margin-bottom:4px;}
  .rule-content{font-size:13px;color:var(--text2);line-height:1.6;}

  .proc-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px;}
  @media(max-width:500px){.proc-grid{grid-template-columns:1fr;}}
  .proc-btn{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:20px 16px;cursor:pointer;display:flex;align-items:center;gap:14px;transition:all .25s;font-family:'Noto Sans KR',sans-serif;}
  .proc-btn:hover{border-color:rgba(248,81,73,.4);transform:translateY(-3px);}
  .proc-icon{width:46px;height:46px;border-radius:12px;background:linear-gradient(135deg,rgba(248,81,73,.25),rgba(236,72,153,.25));border:1px solid rgba(248,81,73,.3);display:flex;align-items:center;justify-content:center;font-size:22px;flex-shrink:0;}
  .proc-title{font-size:15px;font-weight:800;color:var(--text);}
  .proc-count{font-size:12px;color:var(--text3);margin-top:2px;font-family:'JetBrains Mono',monospace;}
  .msds-list{display:grid;gap:10px;}
  .msds-item{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:13px 15px;display:flex;align-items:center;gap:12px;cursor:pointer;transition:all .22s;}
  .msds-item:hover{border-color:rgba(248,81,73,.35);transform:translateX(4px);}
  .msds-item-icon{width:40px;height:40px;border-radius:10px;background:linear-gradient(135deg,#ec4899,#ef4444);display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0;}
  .msds-item-name{font-size:13px;font-weight:700;color:var(--text);}
  .msds-item-desc{font-size:12px;color:var(--text3);margin-top:2px;}
  .msds-item-arr{margin-left:auto;font-size:16px;color:var(--text3);flex-shrink:0;}
  .msds-sec{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:18px;margin-bottom:12px;}
  .msds-sec h4{font-size:13px;font-weight:800;color:var(--blue);margin-bottom:12px;padding-bottom:8px;border-bottom:1px solid var(--border);}
  .info-grid{display:grid;gap:6px;}
  .info-row{display:grid;grid-template-columns:140px 1fr;gap:8px;padding:7px 10px;background:var(--bg2);border-radius:8px;font-size:13px;}
  @media(max-width:500px){.info-row{grid-template-columns:1fr;}}
  .info-lbl{color:var(--text3);font-weight:700;}.info-val{color:var(--text);}
  .hazard-box{background:var(--red-dim);border:1px solid rgba(248,81,73,.2);border-radius:8px;padding:10px 12px;}
  .hazard-item{font-size:13px;color:var(--red);padding:4px 0;border-bottom:1px solid rgba(248,81,73,.1);}
  .hazard-item:last-child{border-bottom:none;}
  .comp-table{width:100%;border-collapse:collapse;font-size:13px;margin-top:4px;}
  .comp-table th{background:var(--bg2);padding:8px 10px;text-align:left;color:var(--text3);font-weight:700;border-bottom:1px solid var(--border);}
  .comp-table td{padding:8px 10px;border-bottom:1px solid rgba(255,255,255,.04);color:var(--text2);}
  .mono{font-family:'JetBrains Mono',monospace;font-size:12px;color:var(--cyan);}
  .special-box{background:rgba(248,81,73,.08);border:1px solid rgba(248,81,73,.3);border-radius:8px;padding:12px;font-size:13px;color:var(--red);font-weight:700;line-height:1.6;}
  .msds-dl-btn{display:inline-flex;align-items:center;gap:8px;padding:11px 20px;border-radius:10px;background:linear-gradient(135deg,#ec4899,#ef4444);color:#fff;font-weight:800;font-size:13px;text-decoration:none;transition:all .25s ease;margin-top:14px;font-family:'Noto Sans KR',sans-serif;}
  .msds-dl-btn:hover{transform:translateY(-2px);box-shadow:0 8px 18px rgba(236,72,153,.3);}

  .form-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
  @media(max-width:580px){.form-grid{grid-template-columns:1fr;}}
  .form-full{grid-column:1/-1;}
  .inp{width:100%;padding:10px 13px;background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);color:var(--text);font-size:14px;font-family:'Noto Sans KR',sans-serif;outline:none;transition:border-color .2s;}
  .inp:focus{border-color:var(--blue);}
  .inp::placeholder{color:var(--text3);}
  textarea.inp{min-height:120px;resize:vertical;}
  select.inp{appearance:none;cursor:pointer;}
  .sub-btn{padding:11px 24px;border-radius:var(--radius);border:none;font-size:14px;font-weight:900;color:#fff;cursor:pointer;transition:all .25s;display:inline-flex;align-items:center;gap:8px;font-family:'Noto Sans KR',sans-serif;margin-top:6px;}
  .sub-btn:hover{transform:translateY(-2px);}
  .btn-report{background:linear-gradient(135deg,var(--cyan),var(--blue));}
  .btn-opinion{background:linear-gradient(135deg,var(--green),#059669);}
  .btn-admin{background:linear-gradient(135deg,var(--admin-accent),#e3891e);}
  .ok-msg{display:none;margin-top:10px;padding:12px 14px;border-radius:var(--radius);background:var(--green-dim);border:1px solid rgba(63,185,80,.3);color:var(--green);font-weight:700;font-size:13px;}
  .err-msg{display:none;margin-top:10px;padding:12px 14px;border-radius:var(--radius);background:var(--red-dim);border:1px solid rgba(248,81,73,.3);color:var(--red);font-weight:700;font-size:13px;}

  .submission-list{display:grid;gap:10px;}
  .sub-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:16px;}
  .sub-card-header{display:flex;align-items:center;gap:10px;margin-bottom:10px;flex-wrap:wrap;}
  .sub-card-title{font-size:14px;font-weight:800;color:var(--text);flex:1;}
  .sub-card-meta{font-size:11px;color:var(--text3);font-family:'JetBrains Mono',monospace;}
  .sub-card-body{font-size:13px;color:var(--text2);line-height:1.7;border-top:1px solid var(--border);padding-top:10px;margin-top:4px;white-space:pre-wrap;}
  .status-badge{font-size:10px;font-weight:900;padding:2px 8px;border-radius:4px;border:1px solid transparent;flex-shrink:0;}
  .status-new{background:var(--blue-dim);color:var(--blue);border-color:rgba(56,139,253,.3);}
  .status-done{background:var(--green-dim);color:var(--green);border-color:rgba(63,185,80,.3);}
  .del-btn{padding:4px 10px;border-radius:6px;border:1px solid var(--border);background:transparent;color:var(--text3);font-size:11px;font-weight:700;cursor:pointer;transition:all .2s;font-family:'Noto Sans KR',sans-serif;}
  .del-btn:hover{border-color:var(--red);color:var(--red);}

  .admin-form-panel{background:var(--admin-dim);border:1px solid var(--admin-accent);border-radius:var(--radius-lg);padding:20px;margin-bottom:16px;}
  .admin-form-title{font-size:13px;font-weight:900;color:var(--admin-accent);letter-spacing:.5px;margin-bottom:14px;display:flex;align-items:center;gap:8px;}

  .modal-overlay{position:fixed;inset:0;z-index:999;background:rgba(0,0,0,.75);backdrop-filter:blur(4px);display:none;align-items:center;justify-content:center;}
  .modal-overlay.show{display:flex;}
  .modal{background:var(--bg2);border:1px solid var(--border);border-radius:var(--radius-lg);padding:32px;width:100%;max-width:380px;box-shadow:0 24px 48px rgba(0,0,0,.5);}
  .modal h3{font-size:18px;font-weight:900;color:#fff;margin-bottom:6px;}
  .modal p{font-size:13px;color:var(--text3);margin-bottom:20px;}
  .modal-actions{display:flex;gap:10px;margin-top:16px;}

  .loading{text-align:center;padding:40px 20px;color:var(--text3);font-size:13px;}
  .spinner{width:28px;height:28px;border:3px solid var(--border);border-top-color:var(--blue);border-radius:50%;animation:spin .8s linear infinite;margin:0 auto 12px;}
  @keyframes spin{to{transform:rotate(360deg)}}
  .empty-msg{text-align:center;padding:40px 20px;color:var(--text3);}
  .empty-icon{font-size:40px;display:block;margin-bottom:10px;}

  .tab-row{display:flex;border-bottom:1px solid var(--border);margin-bottom:18px;gap:4px;flex-wrap:wrap;}
  .tab-btn{padding:9px 16px;font-size:13px;font-weight:700;color:var(--text3);cursor:pointer;border:none;background:none;border-bottom:2px solid transparent;transition:all .2s;font-family:'Noto Sans KR',sans-serif;margin-bottom:-1px;}
  .tab-btn:hover{color:var(--text);}
  .tab-btn.active{color:var(--blue);border-bottom-color:var(--blue);}
  .tab-content{display:none;}
  .tab-content.active{display:block;}

  .live-dot{display:inline-flex;align-items:center;gap:5px;font-size:10px;font-weight:700;color:var(--green);background:var(--green-dim);border:1px solid rgba(63,185,80,.25);padding:3px 8px;border-radius:99px;font-family:'JetBrains Mono',monospace;}
  .live-dot::before{content:'';width:5px;height:5px;border-radius:50%;background:var(--green);display:block;animation:pulse 1.5s infinite;}
  .rule-del{float:right;margin-left:8px;}

  footer{text-align:center;padding:24px 20px;border-top:1px solid var(--border);color:var(--text3);font-size:12px;position:relative;z-index:1;max-width:1060px;margin:0 auto;}
  footer strong{color:var(--text2);}
  </style>
</head>
<body>
<div id="app">
  <header>
    <div class="header-brand">
      <div class="header-logo">🏢</div>
      <div>
        <div class="company">맥서브</div>
        <div class="site">오산 LG화학 CS캠퍼스</div>
      </div>
    </div>
    <div class="header-right">
      <div class="live-dot">LIVE</div>
      <div class="header-system">안전 및 보건관리 시스템</div>
      <div class="admin-badge" id="adminBadge"><span class="admin-dot"></span>관리자 모드</div>
      <button id="adminLoginBtn" onclick="openLoginModal()">🔐 관리자 로그인</button>
      <button id="adminLogoutBtn" onclick="adminLogout()">로그아웃</button>
    </div>
  </header>

  <section id="view-home" class="view active">
    <div class="notice-banner" onclick="nav('notice')">
      <div class="nb-icon">📢</div>
      <div style="flex:1;min-width:0">
        <div class="nb-label" id="bannerLabel" style="background:rgba(227,179,65,.15);color:var(--amber);border:1px solid rgba(227,179,65,.3)">공지</div>
        <div class="nb-title" id="bannerTitle">등록된 공지사항을 확인하세요</div>
        <div class="nb-date" id="bannerDate"></div>
      </div>
      <div class="nb-arrow">→</div>
    </div>
    <div class="menu-grid">
      <a class="menu-card mc-notice" href="#" onclick="nav('notice');return false;"><div class="mc-icon">📢</div><div class="mc-title">공지사항</div><div class="mc-sub">최신 공지·교육일정</div></a>
      <a class="menu-card mc-safety" href="#" onclick="nav('safety');return false;"><div class="mc-icon">📋</div><div class="mc-title">안전규정</div><div class="mc-sub">작업별 안전수칙</div></a>
      <a class="menu-card mc-msds" href="#" onclick="nav('msds');return false;"><div class="mc-icon">🧪</div><div class="mc-title">MSDS</div><div class="mc-sub">물질안전보건자료</div></a>
      <a class="menu-card mc-report" href="#" onclick="nav('report');return false;"><div class="mc-icon">⚠️</div><div class="mc-title">아차사고 신고</div><div class="mc-sub">위험상황 즉시보고</div></a>
      <a class="menu-card mc-opinion" href="#" onclick="nav('opinion');return false;"><div class="mc-icon">💬</div><div class="mc-title">근로자 의견</div><div class="mc-sub">개선·건의사항</div></a>
    </div>
    <div class="admin-section" id="adminSection">
      <div class="admin-section-title">🔐 관리자 전용 메뉴</div>
      <div class="admin-menu-grid">
        <a class="admin-menu-btn" href="#" onclick="nav('admin-notice');return false;"><div class="ambi">📝</div><div class="ambt">공지 작성·관리</div><div class="ambs">작성/수정/삭제</div></a>
        <a class="admin-menu-btn" href="#" onclick="nav('admin-safety');return false;"><div class="ambi">📋</div><div class="ambt">안전규정 관리</div><div class="ambs">항목 추가/삭제</div></a>
        <a class="admin-menu-btn" href="#" onclick="nav('admin-msds');return false;"><div class="ambi">🧪</div><div class="ambt">MSDS 관리</div><div class="ambs">제품 추가/삭제</div></a>
        <a class="admin-menu-btn" href="#" onclick="nav('admin-reports');return false;"><div class="ambi">⚠️</div><div class="ambt">신고 목록</div><div class="ambs">아차사고 접수내역</div></a>
        <a class="admin-menu-btn" href="#" onclick="nav('admin-opinions');return false;"><div class="ambi">💬</div><div class="ambt">의견 목록</div><div class="ambs">근로자 의견 접수</div></a>
      </div>
    </div>
  </section>

  <section id="view-notice"         class="view"></section>
  <section id="view-safety"         class="view"></section>
  <section id="view-msds"           class="view"></section>
  <section id="view-report"         class="view"></section>
  <section id="view-opinion"        class="view"></section>
  <section id="view-admin-notice"   class="view"></section>
  <section id="view-admin-safety"   class="view"></section>
  <section id="view-admin-msds"     class="view"></section>
  <section id="view-admin-reports"  class="view"></section>
  <section id="view-admin-opinions" class="view"></section>
</div>

<footer>
  <strong>맥서브 안전관리팀</strong> · 안전한 작업환경 조성을 위해 최선을 다하겠습니다<br/>
  © 2026 Maxserve · Firebase Realtime Sync
</footer>

<div class="modal-overlay" id="loginModal">
  <div class="modal">
    <h3>🔐 관리자 로그인</h3>
    <p>관리자 비밀번호를 입력하세요.</p>
    <input class="inp" type="password" id="loginPwInput" placeholder="비밀번호" style="width:100%"
      onkeydown="if(event.key==='Enter')doLogin()"/>
    <div class="modal-actions">
      <button class="sub-btn btn-admin" style="flex:1" onclick="doLogin()">로그인</button>
      <button class="sub-btn" style="background:var(--surface);color:var(--text2);flex:1" onclick="closeLoginModal()">취소</button>
    </div>
    <div class="err-msg" id="loginErr" style="display:none">비밀번호가 올바르지 않습니다.</div>
  </div>
</div>

<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-firestore-compat.js"></script>

<script>
const firebaseConfig = {
  apiKey:            "AIzaSyCcji8oDXnQkOAYUbtQUxag7vd9NDq6lUY",
  authDomain:        "maxserv-3a050.firebaseapp.com",
  projectId:         "maxserv-3a050",
  storageBucket:     "maxserv-3a050.firebasestorage.app",
  messagingSenderId: "416337710696",
  appId:             "1:416337710696:web:46932c487f236d738475dd"
};
const ADMIN_PASSWORD = "0109";
firebase.initializeApp(firebaseConfig);
const db = firebase.firestore();
</script>

<script>
/* ── 유틸 ── */
function esc(s){ return (s||'').replace(/[&<>"']/g,m=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[m])); }
function md(s){ return esc(s).replace(/\*\*(.+?)\*\*/g,'<strong>$1</strong>'); }
function ts(d){
  try{
    const dt = d && d.toDate ? d.toDate() : (d ? new Date(d) : null);
    if(!dt||isNaN(dt)) return '';
    return dt.toLocaleDateString('ko-KR',{year:'numeric',month:'2-digit',day:'2-digit'});
  }catch(e){ return ''; }
}
function tsf(d){
  try{
    const dt = d && d.toDate ? d.toDate() : (d ? new Date(d) : null);
    if(!dt||isNaN(dt)) return '';
    return dt.toLocaleString('ko-KR');
  }catch(e){ return ''; }
}
function showLoading(el){ el.innerHTML=`<div class="loading"><div class="spinner"></div>잠시만 기다려 주세요…</div>`; }
function showEmpty(el,msg='등록된 항목이 없습니다.'){ el.innerHTML=`<div class="empty-msg"><span class="empty-icon">📭</span>${esc(msg)}</div>`; }
function showFbErr(el,err){
  el.innerHTML=`<div class="err-msg" style="display:block">❌ Firebase 오류: ${esc(err.message)}<br/><small style="color:var(--text3)">Firebase 콘솔 → Firestore → 규칙을 확인하세요.</small></div>`;
  console.error(err);
}

/* ── 관리자 ── */
let isAdmin = false;
function openLoginModal(){ document.getElementById('loginModal').classList.add('show'); setTimeout(()=>document.getElementById('loginPwInput').focus(),100); }
function closeLoginModal(){ document.getElementById('loginModal').classList.remove('show'); document.getElementById('loginPwInput').value=''; document.getElementById('loginErr').style.display='none'; }
function doLogin(){
  if(document.getElementById('loginPwInput').value === ADMIN_PASSWORD){
    isAdmin=true; sessionStorage.setItem('ms_admin','1');
    closeLoginModal(); applyAdminUI(); nav('home');
  } else { document.getElementById('loginErr').style.display='block'; }
}
function adminLogout(){ isAdmin=false; sessionStorage.removeItem('ms_admin'); applyAdminUI(); nav('home'); }
function applyAdminUI(){
  document.getElementById('adminBadge').classList.toggle('show',isAdmin);
  document.getElementById('adminLogoutBtn').classList.toggle('show',isAdmin);
  document.getElementById('adminLoginBtn').style.display = isAdmin?'none':'flex';
  document.getElementById('adminSection').classList.toggle('show',isAdmin);
}
if(sessionStorage.getItem('ms_admin')==='1') isAdmin=true;

/* ── 라우터 ── */
const VIEWS=['home','notice','safety','msds','report','opinion','admin-notice','admin-safety','admin-msds','admin-reports','admin-opinions'];
const mounted={}, pageInit={}, navHistory=[];
function nav(name,push=true){
  if(push){ const cur=VIEWS.find(v=>document.getElementById('view-'+v)?.classList.contains('active')); if(cur&&cur!==name) navHistory.push(cur); }
  VIEWS.forEach(v=>document.getElementById('view-'+v)?.classList.remove('active'));
  const el=document.getElementById('view-'+name); if(!el) return;
  el.classList.add('active'); window.scrollTo({top:0,behavior:'smooth'});
  if(name!=='home'&&!mounted[name]&&pageInit[name]){ pageInit[name](el); mounted[name]=true; }
}
function goBack(){ nav(navHistory.length>0?navHistory.pop():'home',false); }
window.addEventListener('DOMContentLoaded',()=>{ applyAdminUI(); nav('home',false); });
</script>

<script>
/* ════════ 공지사항 ════════ */
const NOTICE_CAT={
  '중요':{bg:'rgba(227,179,65,.15)',color:'#e3b341',bc:'rgba(227,179,65,.3)'},
  '안전':{bg:'rgba(248,81,73,.15)', color:'#f85149',bc:'rgba(248,81,73,.3)'},
  '교육':{bg:'rgba(56,139,253,.15)',color:'#388bfd',bc:'rgba(56,139,253,.3)'},
  '일반':{bg:'rgba(139,148,158,.12)',color:'#8b949e',bc:'rgba(139,148,158,.3)'},
  '기타':{bg:'rgba(63,185,80,.12)', color:'#3fb950',bc:'rgba(63,185,80,.3)'},
};
function nStyle(cat){ return NOTICE_CAT[cat]||NOTICE_CAT['기타']; }
function nBadge(cat){ const s=nStyle(cat); return `<span class="ni-badge" style="background:${s.bg};color:${s.color};border-color:${s.bc}">${esc(cat||'일반')}</span>`; }

/* 홈 배너 — orderBy 단일 필드만 사용 */
function initHomeBanner(){
  try{
    db.collection('notices').orderBy('createdAt','desc').limit(10)
      .onSnapshot(snap=>{
        if(snap.empty){ return; }
        const docs=snap.docs.map(d=>({...d.data()}));
        docs.sort((a,b)=>{ if(a.pinned!==b.pinned) return a.pinned?-1:1; return 0; });
        const d=docs[0]; const s=nStyle(d.category);
        const lbl=document.getElementById('bannerLabel');
        if(lbl){ lbl.textContent=d.category||'공지'; lbl.style.background=s.bg; lbl.style.color=s.color; lbl.style.borderColor=s.bc; }
        const t=document.getElementById('bannerTitle'); if(t) t.textContent=(d.pinned?'📌 ':'')+d.title;
        const dt=document.getElementById('bannerDate'); if(dt) dt.textContent=ts(d.createdAt)+' · '+(d.author||'안전관리팀');
      },()=>{});
  }catch(e){}
}

let noticeFilter='전체', noticeUnsub=null;

pageInit['notice']=function(container){
  container.innerHTML=`
    <div class="page-header"><button class="back-btn" onclick="goBack()">← 뒤로</button>
      <div><div class="page-ttl">📢 공지사항</div><div class="page-sub">안전관리팀 공지 · 교육 · 안전 정보</div></div></div>
    <div class="panel">
      <div class="filter-row" id="noticeFilterRow">
        ${['전체','중요','안전','교육','일반','기타'].map(c=>`<button class="flt-btn${c==='전체'?' active':''}" onclick="setNoticeFilter('${c}',this)">${c}</button>`).join('')}
      </div>
      <div id="noticeListWrap"></div>
      <div id="noticeDetailWrap" style="display:none">
        <button class="back-btn" style="margin-bottom:16px" onclick="showNoticeList()">← 목록으로</button>
        <div id="noticeDetailInner"></div>
      </div>
    </div>`;
  subscribeNoticeList();
};

function setNoticeFilter(f,btn){
  noticeFilter=f;
  document.querySelectorAll('#noticeFilterRow .flt-btn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  subscribeNoticeList();
}

function subscribeNoticeList(){
  const wrap=document.getElementById('noticeListWrap'); if(!wrap) return;
  if(noticeUnsub){ noticeUnsub(); noticeUnsub=null; }
  showLoading(wrap);
  /* orderBy 단일 필드 → 복합 인덱스 불필요 */
  noticeUnsub=db.collection('notices').orderBy('createdAt','desc')
    .onSnapshot(snap=>{
      let docs=snap.docs.map(d=>({id:d.id,...d.data(),dateStr:ts(d.data().createdAt)}));
      docs.sort((a,b)=>{ if(a.pinned!==b.pinned) return a.pinned?-1:1; return 0; });
      if(noticeFilter!=='전체') docs=docs.filter(d=>d.category===noticeFilter);
      renderNoticeList(docs);
    }, err=>showFbErr(wrap,err));
}

function renderNoticeList(docs){
  const wrap=document.getElementById('noticeListWrap'); if(!wrap) return;
  if(!docs.length){ showEmpty(wrap,'등록된 공지가 없습니다.'); return; }
  wrap.innerHTML=`<div class="notice-list">${docs.map(d=>`
    <div class="ni${d.pinned?' pinned':''}">
      ${nBadge(d.category)}
      <div class="ni-body" onclick='showNoticeDetailData(${JSON.stringify(d).replace(/'/g,"&#39;")})'>
        <div class="ni-title">${d.pinned?'📌 ':''}${esc(d.title)}</div>
        <div class="ni-summary">${esc(d.summary||'')}</div>
        <div class="ni-meta">${esc(d.dateStr||'')} · ${esc(d.author||'안전관리팀')}</div>
      </div>
      ${isAdmin?`<div style="display:flex;flex-direction:column;gap:5px;flex-shrink:0">
        <button class="del-btn" style="color:var(--amber);border-color:rgba(227,179,65,.3)" onclick="event.stopPropagation();editNotice('${d.id}')">수정</button>
        <button class="del-btn" onclick="event.stopPropagation();deleteNotice('${d.id}')">삭제</button>
      </div>`:`<div class="ni-arr">›</div>`}
    </div>`).join('')}</div>`;
}

function showNoticeDetailData(d){
  const lw=document.getElementById('noticeListWrap'),dw=document.getElementById('noticeDetailWrap');
  if(!lw||!dw) return;
  lw.style.display='none'; dw.style.display='block';
  document.getElementById('noticeDetailInner').innerHTML=`
    <div class="nd-badge-row">${nBadge(d.category)} ${d.pinned?'<span style="font-size:13px;color:var(--amber)">📌 고정</span>':''}</div>
    <div class="nd-title">${esc(d.title)}</div>
    <div class="nd-info">${esc(d.dateStr||'')} · ${esc(d.author||'안전관리팀')}</div>
    <div class="nd-body">${md(d.content||'')}</div>`;
  window.scrollTo({top:0,behavior:'smooth'});
}
function showNoticeList(){
  const lw=document.getElementById('noticeListWrap'),dw=document.getElementById('noticeDetailWrap');
  if(lw) lw.style.display=''; if(dw) dw.style.display='none';
}

/* 관리자 공지 관리 */
let adminNoticeUnsub=null, editingNoticeId=null;

pageInit['admin-notice']=function(container){
  if(!isAdmin){ container.innerHTML='<div class="panel"><p style="color:var(--red)">⛔ 관리자 권한이 필요합니다.</p></div>'; return; }
  editingNoticeId=null;
  container.innerHTML=`
    <div class="page-header"><button class="back-btn" onclick="goBack()">← 뒤로</button>
      <div><div class="page-ttl">📝 공지 작성·관리</div><div class="page-sub">관리자 전용</div></div></div>
    <div class="admin-form-panel">
      <div class="admin-form-title" id="noticeFormTitle">🔐 공지 작성</div>
      <div class="form-grid">
        <input class="inp" id="nTitle" placeholder="제목 *"/>
        <select class="inp" id="nCat">
          <option value="중요">📌 중요</option><option value="안전">⚠️ 안전</option>
          <option value="교육">📚 교육</option><option value="일반">📄 일반</option><option value="기타">💬 기타</option>
        </select>
        <input class="inp" id="nSummary" placeholder="한 줄 요약"/>
        <input class="inp" id="nAuthor" placeholder="작성자 (기본: 안전관리팀)"/>
        <textarea class="inp form-full" id="nContent" placeholder="본문 내용 (**굵게** 마크다운 지원)" style="min-height:130px"></textarea>
        <label style="display:flex;align-items:center;gap:8px;font-size:13px;color:var(--text2);cursor:pointer">
          <input type="checkbox" id="nPinned" style="width:16px;height:16px"/> 📌 상단 고정
        </label>
      </div>
      <div style="margin-top:12px;display:flex;gap:10px;flex-wrap:wrap">
        <button class="sub-btn btn-admin" id="noticeSubmitBtn" onclick="submitNotice()">✅ 공지 등록</button>
        <button class="sub-btn" style="background:var(--surface);color:var(--text2)" onclick="resetNoticeForm()">초기화</button>
      </div>
      <div class="ok-msg" id="nOk"></div><div class="err-msg" id="nErr"></div>
    </div>
    <div class="panel">
      <div style="font-size:13px;font-weight:800;color:var(--text2);margin-bottom:14px">등록된 공지 목록</div>
      <div id="adminNoticeList"></div>
    </div>`;
  subscribeAdminNoticeList();
};

function subscribeAdminNoticeList(){
  const el=document.getElementById('adminNoticeList'); if(!el) return;
  if(adminNoticeUnsub){ adminNoticeUnsub(); adminNoticeUnsub=null; }
  showLoading(el);
  adminNoticeUnsub=db.collection('notices').orderBy('createdAt','desc')
    .onSnapshot(snap=>{
      if(snap.empty){ showEmpty(el,'등록된 공지가 없습니다.'); return; }
      let items=snap.docs.map(d=>({id:d.id,...d.data(),dateStr:ts(d.data().createdAt)}));
      items.sort((a,b)=>{ if(a.pinned!==b.pinned) return a.pinned?-1:1; return 0; });
      el.innerHTML=`<div class="notice-list">${items.map(d=>`
        <div class="ni${d.pinned?' pinned':''}">
          ${nBadge(d.category)}
          <div class="ni-body"><div class="ni-title">${d.pinned?'📌 ':''}${esc(d.title)}</div>
            <div class="ni-meta">${esc(d.dateStr||'')} · ${esc(d.author||'')}</div></div>
          <div style="display:flex;gap:6px;flex-shrink:0">
            <button class="del-btn" style="color:var(--amber);border-color:rgba(227,179,65,.3)" onclick="editNotice('${d.id}')">수정</button>
            <button class="del-btn" onclick="deleteNotice('${d.id}')">삭제</button>
          </div>
        </div>`).join('')}</div>`;
    }, err=>showFbErr(el,err));
}

async function submitNotice(){
  const title=document.getElementById('nTitle').value.trim();
  const cat=document.getElementById('nCat').value;
  const summary=document.getElementById('nSummary').value.trim();
  const author=document.getElementById('nAuthor').value.trim()||'안전관리팀';
  const content=document.getElementById('nContent').value.trim();
  const pinned=document.getElementById('nPinned').checked;
  const ok=document.getElementById('nOk'), err=document.getElementById('nErr');
  ok.style.display=err.style.display='none';
  if(!title||!content){ err.textContent='제목과 본문은 필수입니다.'; err.style.display='block'; return; }
  const btn=document.getElementById('noticeSubmitBtn');
  btn.disabled=true; btn.textContent='처리 중…';
  try{
    if(editingNoticeId){
      await db.collection('notices').doc(editingNoticeId).update({title,category:cat,summary,author,content,pinned});
      ok.textContent='✅ 공지가 수정되었습니다.';
    } else {
      await db.collection('notices').add({title,category:cat,summary,author,content,pinned,createdAt:firebase.firestore.FieldValue.serverTimestamp()});
      ok.textContent='✅ 공지가 등록되었습니다.';
    }
    ok.style.display='block'; resetNoticeForm();
  }catch(e){ err.textContent='❌ Firebase 오류: '+e.message; err.style.display='block'; console.error(e); }
  finally{ btn.disabled=false; btn.textContent=editingNoticeId?'✅ 수정 완료':'✅ 공지 등록'; }
}

function resetNoticeForm(){
  editingNoticeId=null;
  ['nTitle','nSummary','nAuthor','nContent'].forEach(id=>{ const el=document.getElementById(id); if(el) el.value=''; });
  const c=document.getElementById('nCat'); if(c) c.value='중요';
  const p=document.getElementById('nPinned'); if(p) p.checked=false;
  const ft=document.getElementById('noticeFormTitle'); if(ft) ft.textContent='🔐 공지 작성';
  const btn=document.getElementById('noticeSubmitBtn'); if(btn) btn.textContent='✅ 공지 등록';
}

async function editNotice(id){
  const snap=await db.collection('notices').doc(id).get();
  if(!snap.exists) return;
  const d=snap.data(); editingNoticeId=id;
  document.getElementById('nTitle').value=d.title||'';
  document.getElementById('nCat').value=d.category||'중요';
  document.getElementById('nSummary').value=d.summary||'';
  document.getElementById('nAuthor').value=d.author||'';
  document.getElementById('nContent').value=d.content||'';
  document.getElementById('nPinned').checked=!!d.pinned;
  const ft=document.getElementById('noticeFormTitle'); if(ft) ft.textContent='🔐 공지 수정';
  const btn=document.getElementById('noticeSubmitBtn'); if(btn) btn.textContent='✅ 수정 완료';
  window.scrollTo({top:0,behavior:'smooth'});
}

async function deleteNotice(id){
  if(!confirm('이 공지를 삭제하시겠습니까?')) return;
  try{ await db.collection('notices').doc(id).delete(); }
  catch(e){ alert('삭제 오류: '+e.message); }
}
</script>

<script>
/* ════════ 안전규정 ════════ */
const SAFETY_CATS=[
  {key:'fire',            icon:'🔥',label:'화기작업'},
  {key:'confined-before', icon:'🚪',label:'밀폐공간 (개방 전)'},
  {key:'confined-during', icon:'⚠️',label:'밀폐공간 (작업 시)'},
  {key:'general',         icon:'🛠️',label:'일반위험작업'},
  {key:'electric',        icon:'⚡',label:'전기작업'},
  {key:'height',          icon:'🪜',label:'고소작업'},
];

pageInit['safety']=function(container){
  container.innerHTML=`
    <div class="page-header"><button class="back-btn" onclick="goBack()">← 뒤로</button>
      <div><div class="page-ttl">📋 안전규정</div><div class="page-sub">카테고리 선택 또는 검색</div></div></div>
    <div class="panel">
      <div class="search-row">
        <input class="search-inp" id="safetyQ" placeholder="🔍 안전규정 검색"/>
        <button class="sub-btn btn-admin" style="margin-top:0;padding:10px 16px;font-size:13px" onclick="searchSafety()">검색</button>
        <button id="safetyResetBtn" class="sub-btn" style="display:none;margin-top:0;padding:10px 16px;font-size:13px;background:var(--surface);color:var(--text2)" onclick="resetSafetySearch()">전체보기</button>
      </div>
      <div id="safetySearchInfo" style="display:none;padding:8px 12px;background:var(--amber-dim);border:1px solid rgba(227,179,65,.3);border-radius:8px;font-size:13px;font-weight:700;color:var(--amber);margin-bottom:12px"></div>
      <div id="safetyCatGrid" class="safety-cat-grid"></div>
      <div id="safetyDetail" style="display:none">
        <button class="back-btn" style="margin-bottom:14px" onclick="showSafetyCatGrid()">← 카테고리로</button>
        <div style="font-size:16px;font-weight:900;color:#fff;margin-bottom:14px" id="safetyDetailTitle"></div>
        <div class="rule-list" id="safetyRuleList"></div>
      </div>
    </div>`;
  document.getElementById('safetyQ').addEventListener('keydown',e=>{ if(e.key==='Enter') searchSafety(); });
  renderSafetyCatGrid();
};

function renderSafetyCatGrid(){
  const el=document.getElementById('safetyCatGrid'); if(!el) return;
  el.innerHTML=SAFETY_CATS.map(c=>`
    <button class="sc-btn" onclick="showSafetyCategory('${c.key}','${esc(c.label)}')">
      <div class="sc-icon">${c.icon}</div><div class="sc-title">${esc(c.label)}</div>
      <div class="sc-count" id="safetyCount_${c.key}">로딩 중…</div>
    </button>`).join('');
  /* 카운트: where만 사용 → 인덱스 불필요 */
  SAFETY_CATS.forEach(c=>{
    db.collection('safety').where('category','==',c.key).get()
      .then(snap=>{ const el2=document.getElementById('safetyCount_'+c.key); if(el2) el2.textContent=snap.size+'개 항목'; })
      .catch(()=>{});
  });
}
function showSafetyCatGrid(){ document.getElementById('safetyCatGrid').style.display='grid'; document.getElementById('safetyDetail').style.display='none'; }
function showSafetyCategory(key,label){
  document.getElementById('safetyCatGrid').style.display='none';
  document.getElementById('safetyDetail').style.display='block';
  const cat=SAFETY_CATS.find(c=>c.key===key);
  document.getElementById('safetyDetailTitle').textContent=(cat?cat.icon+' ':'')+label;
  loadSafetyRules(key,document.getElementById('safetyRuleList'),isAdmin);
}

function loadSafetyRules(catKey,el,showDelete){
  showLoading(el);
  /*
   * ★ 핵심 수정 ★
   * where + orderBy 조합 제거 → where만 사용 후 클라이언트 정렬
   * → 복합 인덱스 완전 불필요
   */
  db.collection('safety').where('category','==',catKey)
    .onSnapshot(snap=>{
      if(snap.empty){ showEmpty(el,'등록된 규정이 없습니다.'); return; }
      const docs=snap.docs.slice().sort((a,b)=>{
        const oa=a.data().order??99, ob=b.data().order??99;
        if(oa!==ob) return oa-ob;
        const ca=a.data().createdAt?.toMillis?.()||0;
        const cb=b.data().createdAt?.toMillis?.()||0;
        return ca-cb;
      });
      el.innerHTML=docs.map((doc,i)=>{
        const d=doc.data();
        return `<div class="rule-item">
          <div class="rule-num">${String(i+1).padStart(2,'0')}</div>
          <div style="flex:1">
            <div class="rule-label">${esc(d.label)}</div>
            <div class="rule-content">${esc(d.content)}</div>
          </div>
          ${showDelete&&isAdmin?`<button class="del-btn rule-del" onclick="deleteSafetyItem('${doc.id}')">삭제</button>`:''}
        </div>`;
      }).join('');
    }, err=>showFbErr(el,err));
}

function searchSafety(){
  const q=(document.getElementById('safetyQ').value||'').trim().toLowerCase();
  if(!q) return;
  const si=document.getElementById('safetySearchInfo'),cg=document.getElementById('safetyCatGrid'),det=document.getElementById('safetyDetail'),rl=document.getElementById('safetyRuleList');
  showLoading(rl); document.getElementById('safetyResetBtn').style.display='inline-flex';
  /* 전체 컬렉션 get → where 없이 → 인덱스 불필요 */
  db.collection('safety').get().then(snap=>{
    const results=snap.docs.filter(d=>{ const v=d.data(); return (v.label||'').toLowerCase().includes(q)||(v.content||'').toLowerCase().includes(q); });
    si.style.display='block'; si.innerHTML=`🔍 총 <strong>${results.length}개</strong> 항목을 찾았습니다.`;
    cg.style.display='none'; det.style.display='block';
    document.getElementById('safetyDetailTitle').textContent=`검색 결과: "${q}"`;
    if(!results.length){ showEmpty(rl,'검색 결과가 없습니다.'); return; }
    rl.innerHTML=results.map((doc,i)=>{
      const d=doc.data(); const cat=SAFETY_CATS.find(c=>c.key===d.category);
      return `<div class="rule-item">
        <div class="rule-num">${String(i+1).padStart(2,'0')}</div>
        <div><div style="font-size:11px;color:var(--purple);margin-bottom:3px">${cat?cat.icon+' '+cat.label:''}</div>
          <div class="rule-label">${esc(d.label)}</div><div class="rule-content">${esc(d.content)}</div></div>
      </div>`;
    }).join('');
  }).catch(err=>showFbErr(rl,err));
}

function resetSafetySearch(){
  document.getElementById('safetyQ').value='';
  document.getElementById('safetySearchInfo').style.display='none';
  document.getElementById('safetyResetBtn').style.display='none';
  showSafetyCatGrid();
}

pageInit['admin-safety']=function(container){
  if(!isAdmin){ container.innerHTML='<div class="panel"><p style="color:var(--red)">⛔ 관리자 권한이 필요합니다.</p></div>'; return; }
  container.innerHTML=`
    <div class="page-header"><button class="back-btn" onclick="goBack()">← 뒤로</button>
      <div><div class="page-ttl">📋 안전규정 관리</div><div class="page-sub">관리자 전용</div></div></div>
    <div class="admin-form-panel">
      <div class="admin-form-title">🔐 새 항목 추가</div>
      <div class="form-grid">
        <select class="inp" id="sCat">${SAFETY_CATS.map(c=>`<option value="${c.key}">${c.icon} ${c.label}</option>`).join('')}</select>
        <input class="inp" id="sLabel" placeholder="항목명 *"/>
        <textarea class="inp form-full" id="sContent" placeholder="규정 내용 *" style="min-height:100px"></textarea>
        <input class="inp" id="sOrder" placeholder="순서 번호 (낮을수록 앞)" type="number" value="99"/>
      </div>
      <button class="sub-btn btn-admin" style="margin-top:10px" onclick="addSafetyItem()">✅ 항목 추가</button>
      <div class="ok-msg" id="sOk"></div><div class="err-msg" id="sErr"></div>
    </div>
    <div class="panel">
      <div style="font-size:13px;font-weight:800;color:var(--text2);margin-bottom:14px">카테고리별 규정 목록</div>
      <div class="tab-row" id="safetyAdminTabs">
        ${SAFETY_CATS.map((c,i)=>`<button class="tab-btn${i===0?' active':''}" onclick="showSafetyAdminTab('${c.key}',this)">${c.icon} ${c.label}</button>`).join('')}
      </div>
      ${SAFETY_CATS.map((c,i)=>`<div class="tab-content${i===0?' active':''}" id="safetyAdminTab_${c.key}">
        <div class="rule-list" id="adminRuleList_${c.key}"></div></div>`).join('')}
    </div>`;
  SAFETY_CATS.forEach(c=>loadSafetyRules(c.key,document.getElementById('adminRuleList_'+c.key),true));
};

function showSafetyAdminTab(key,btn){
  document.querySelectorAll('#safetyAdminTabs .tab-btn').forEach(b=>b.classList.remove('active'));
  document.querySelectorAll('[id^="safetyAdminTab_"]').forEach(el=>el.classList.remove('active'));
  btn.classList.add('active'); document.getElementById('safetyAdminTab_'+key).classList.add('active');
}

async function addSafetyItem(){
  const cat=document.getElementById('sCat').value,label=document.getElementById('sLabel').value.trim(),content=document.getElementById('sContent').value.trim(),order=parseInt(document.getElementById('sOrder').value)||99;
  const ok=document.getElementById('sOk'),err=document.getElementById('sErr');
  ok.style.display=err.style.display='none';
  if(!label||!content){ err.textContent='항목명과 내용은 필수입니다.'; err.style.display='block'; return; }
  try{
    await db.collection('safety').add({category:cat,label,content,order,createdAt:firebase.firestore.FieldValue.serverTimestamp()});
    ok.textContent='✅ 항목이 추가되었습니다.'; ok.style.display='block';
    document.getElementById('sLabel').value=''; document.getElementById('sContent').value='';
  }catch(e){ err.textContent='❌ Firebase 오류: '+e.message; err.style.display='block'; }
}

async function deleteSafetyItem(id){
  if(!confirm('이 항목을 삭제하시겠습니까?')) return;
  try{ await db.collection('safety').doc(id).delete(); }
  catch(e){ alert('삭제 오류: '+e.message); }
}
</script>

<script>
/* ════════ MSDS ════════ */
const MSDS_PROCESSES=[
  {key:'cleaning',   icon:'🧹',label:'미화(청소)'},
  {key:'production', icon:'⚙️',label:'소분작업'},
];

pageInit['msds']=function(container){
  container.innerHTML=`
    <div class="page-header"><button class="back-btn" onclick="goBack()">← 뒤로</button>
      <div><div class="page-ttl">🧪 MSDS 검색</div><div class="page-sub">공정별 분류 또는 검색으로 MSDS 찾기</div></div></div>
    <div class="panel">
      <div class="search-row" style="margin-bottom:16px">
        <input class="search-inp" id="msdsQ" placeholder="🔍 제품명 또는 CAS No. 검색"/>
        <button class="sub-btn" style="margin-top:0;padding:10px 16px;font-size:13px;background:linear-gradient(135deg,#ec4899,#ef4444)" onclick="searchMsds()">검색</button>
        <button id="msdsResetBtn" class="sub-btn" style="display:none;margin-top:0;padding:10px 16px;font-size:13px;background:var(--surface);color:var(--text2)" onclick="resetMsdsSearch()">전체보기</button>
      </div>
      <div id="msdsSearchInfo" style="display:none;padding:8px 12px;background:var(--red-dim);border:1px solid rgba(248,81,73,.3);border-radius:8px;font-size:13px;font-weight:700;color:var(--red);margin-bottom:12px"></div>
      <div id="msdsProcGrid" class="proc-grid"></div>
      <div id="msdsListWrap" style="display:none">
        <button class="back-btn" style="margin-bottom:14px" onclick="showMsdsProcGrid()">← 공정 선택으로</button>
        <div style="font-size:16px;font-weight:900;color:#fff;margin-bottom:14px" id="msdsListTitle"></div>
        <div class="msds-list" id="msdsProductList"></div>
      </div>
      <div id="msdsDetailWrap" style="display:none">
        <button class="back-btn" style="margin-bottom:14px" onclick="showMsdsProductList()">← 목록으로</button>
        <div id="msdsDetailInner"></div>
      </div>
    </div>
    <p style="font-size:12px;color:var(--text3);text-align:right">※ MSDS는 정기적으로 업데이트되므로 최신 정보는 원본 문서를 확인하세요.</p>`;
  document.getElementById('msdsQ').addEventListener('keydown',e=>{ if(e.key==='Enter') searchMsds(); });
  renderMsdsProcGrid();
};

function renderMsdsProcGrid(){
  const el=document.getElementById('msdsProcGrid'); if(!el) return;
  el.innerHTML=MSDS_PROCESSES.map(p=>`
    <div class="proc-btn" onclick="showMsdsProcess('${p.key}')">
      <div class="proc-icon">${p.icon}</div>
      <div><div class="proc-title">${esc(p.label)}</div><div class="proc-count" id="msdsCount_${p.key}">로딩 중…</div></div>
    </div>`).join('');
  MSDS_PROCESSES.forEach(p=>{
    /* where만 사용 → 인덱스 불필요 */
    db.collection('msds').where('process','==',p.key).get()
      .then(snap=>{ const el2=document.getElementById('msdsCount_'+p.key); if(el2) el2.textContent=snap.size+'개 제품'; })
      .catch(()=>{});
  });
}

function showMsdsProcGrid(){
  document.getElementById('msdsProcGrid').style.display='grid';
  document.getElementById('msdsListWrap').style.display='none';
  document.getElementById('msdsDetailWrap').style.display='none';
}
function showMsdsProductList(){
  document.getElementById('msdsListWrap').style.display='block';
  document.getElementById('msdsDetailWrap').style.display='none';
}

let msdsCurrentProcess='';
function showMsdsProcess(procKey){
  msdsCurrentProcess=procKey;
  const proc=MSDS_PROCESSES.find(p=>p.key===procKey);
  document.getElementById('msdsProcGrid').style.display='none';
  document.getElementById('msdsListWrap').style.display='block';
  document.getElementById('msdsListTitle').textContent=proc?proc.icon+' '+proc.label:'';
  loadMsdsProductList(procKey,document.getElementById('msdsProductList'),isAdmin);
}

function loadMsdsProductList(procKey,el,showAdmin){
  showLoading(el);
  /*
   * ★ 핵심 수정 ★
   * where + orderBy 제거 → where만 사용 후 클라이언트 정렬
   * → 복합 인덱스 완전 불필요
   */
  db.collection('msds').where('process','==',procKey)
    .onSnapshot(snap=>{
      if(snap.empty){ showEmpty(el,'등록된 제품이 없습니다.'); return; }
      const docs=snap.docs.slice().sort((a,b)=>{
        const ca=a.data().createdAt?.toMillis?.()||0;
        const cb=b.data().createdAt?.toMillis?.()||0;
        return ca-cb;
      });
      el.innerHTML=docs.map(doc=>{
        const d=doc.data();
        return `<div class="msds-item" onclick="showMsdsDetail('${doc.id}')">
          <div class="msds-item-icon">🧪</div>
          <div><div class="msds-item-name">${esc(d.name)}</div>
            <div class="msds-item-desc">${esc(d.company||'')} | ${esc(d.use||'')}</div></div>
          <div class="msds-item-arr">→</div>
          ${showAdmin&&isAdmin?`<button class="del-btn" onclick="event.stopPropagation();deleteMsdsItem('${doc.id}')">삭제</button>`:''}
        </div>`;
      }).join('');
    }, err=>showFbErr(el,err));
}

async function showMsdsDetail(id){
  document.getElementById('msdsListWrap').style.display='none';
  document.getElementById('msdsDetailWrap').style.display='block';
  const inner=document.getElementById('msdsDetailInner');
  showLoading(inner);
  const snap=await db.collection('msds').doc(id).get();
  if(!snap.exists){ inner.innerHTML='<p style="color:var(--red)">제품을 찾을 수 없습니다.</p>'; return; }
  const d=snap.data();
  const hazards=(d.hazards||[]).map(h=>`<div class="hazard-item">⚠ ${esc(h)}</div>`).join('');
  const comps=(d.components||[]).map(c=>`<tr><td>${esc(c.name)}</td><td><span class="mono">${esc(c.cas)}</span></td><td>${esc(c.content)}</td></tr>`).join('');
  inner.innerHTML=`
    <div style="font-size:18px;font-weight:900;color:#fff;margin-bottom:16px">${esc(d.name)}</div>
    <div class="msds-sec"><h4>📌 제품 기본 정보</h4><div class="info-grid">
      <div class="info-row"><div class="info-lbl">제품명</div><div class="info-val">${esc(d.name)}</div></div>
      <div class="info-row"><div class="info-lbl">제조/공급사</div><div class="info-val">${esc(d.company||'-')}</div></div>
      <div class="info-row"><div class="info-lbl">용도</div><div class="info-val">${esc(d.use||'-')}</div></div>
      <div class="info-row"><div class="info-lbl">신호어</div><div class="info-val"><strong style="color:${d.signalWord==='위험'?'var(--red)':'var(--amber)'}">${esc(d.signalWord||'-')}</strong></div></div>
    </div></div>
    <div class="msds-sec"><h4>⚠️ 유해·위험성</h4>
      <div class="hazard-box">${hazards||'<div class="hazard-item" style="color:var(--text3)">정보 없음</div>'}</div>
    </div>
    <div class="msds-sec"><h4>🧬 구성성분</h4>
      <table class="comp-table"><thead><tr><th>물질명</th><th>CAS No.</th><th>함유량</th></tr></thead>
      <tbody>${comps||'<tr><td colspan="3" style="color:var(--text3)">정보 없음</td></tr>'}</tbody></table>
    </div>
    <div class="msds-sec"><h4>🚑 응급조치 요령</h4><div class="info-grid">
      <div class="info-row"><div class="info-lbl">눈에 들어갔을 때</div><div class="info-val">${esc(d.faEye||'-')}</div></div>
      <div class="info-row"><div class="info-lbl">피부에 접촉했을 때</div><div class="info-val">${esc(d.faSkin||'-')}</div></div>
      <div class="info-row"><div class="info-lbl">흡입했을 때</div><div class="info-val">${esc(d.faInhal||'-')}</div></div>
      <div class="info-row"><div class="info-lbl">먹었을 때</div><div class="info-val">${esc(d.faIng||'-')}</div></div>
    </div></div>
    <div class="msds-sec"><h4>📦 취급 및 저장방법</h4><div class="info-grid">
      <div class="info-row"><div class="info-lbl">안전취급요령</div><div class="info-val">${esc(d.handling||'-')}</div></div>
      <div class="info-row"><div class="info-lbl">안전한 저장방법</div><div class="info-val">${esc(d.storage||'-')}</div></div>
    </div></div>
    ${d.specialNote?`<div class="msds-sec" style="background:rgba(248,81,73,.06);border-color:rgba(248,81,73,.25)">
      <h4 style="color:var(--red)">🔥 특별 주의사항</h4><div class="special-box">${esc(d.specialNote)}</div></div>`:''}
    ${d.driveLink?`<a href="${esc(d.driveLink)}" target="_blank" rel="noopener" class="msds-dl-btn">📄 원본 MSDS 보기 (구글 드라이브)</a>`:''}`;
  window.scrollTo({top:0,behavior:'smooth'});
}

function searchMsds(){
  const q=(document.getElementById('msdsQ').value||'').trim().toLowerCase(); if(!q) return;
  document.getElementById('msdsResetBtn').style.display='inline-flex';
  document.getElementById('msdsProcGrid').style.display='none';
  document.getElementById('msdsDetailWrap').style.display='none';
  document.getElementById('msdsListWrap').style.display='block';
  document.getElementById('msdsListTitle').textContent=`검색 결과: "${q}"`;
  const pl=document.getElementById('msdsProductList'); showLoading(pl);
  db.collection('msds').get().then(snap=>{
    const results=snap.docs.filter(d=>{
      const v=d.data();
      return (v.name||'').toLowerCase().includes(q)||(v.company||'').toLowerCase().includes(q)||
             (v.use||'').toLowerCase().includes(q)||
             (v.components||[]).some(c=>(c.name||'').toLowerCase().includes(q)||(c.cas||'').includes(q));
    });
    const si=document.getElementById('msdsSearchInfo');
    si.style.display='block'; si.innerHTML=`🔍 총 <strong>${results.length}개</strong> 제품을 찾았습니다.`;
    if(!results.length){ showEmpty(pl,'검색 결과가 없습니다.'); return; }
    pl.innerHTML=results.map(doc=>{
      const d=doc.data(); const proc=MSDS_PROCESSES.find(p=>p.key===d.process);
      return `<div class="msds-item" onclick="showMsdsDetail('${doc.id}')">
        <div class="msds-item-icon">🧪</div>
        <div><div class="msds-item-name">${esc(d.name)}</div>
          <div class="msds-item-desc">${proc?proc.icon+' '+proc.label:''} | ${esc(d.company||'')}</div></div>
        <div class="msds-item-arr">→</div>
      </div>`;
    }).join('');
  }).catch(err=>showFbErr(pl,err));
}

function resetMsdsSearch(){
  document.getElementById('msdsQ').value='';
  document.getElementById('msdsSearchInfo').style.display='none';
  document.getElementById('msdsResetBtn').style.display='none';
  showMsdsProcGrid();
}

pageInit['admin-msds']=function(container){
  if(!isAdmin){ container.innerHTML='<div class="panel"><p style="color:var(--red)">⛔ 관리자 권한이 필요합니다.</p></div>'; return; }
  container.innerHTML=`
    <div class="page-header"><button class="back-btn" onclick="goBack()">← 뒤로</button>
      <div><div class="page-ttl">🧪 MSDS 관리</div><div class="page-sub">관리자 전용</div></div></div>
    <div class="admin-form-panel">
      <div class="admin-form-title">🔐 MSDS 제품 추가</div>
      <div class="form-grid">
        <select class="inp" id="mProc">${MSDS_PROCESSES.map(p=>`<option value="${p.key}">${p.icon} ${p.label}</option>`).join('')}</select>
        <input class="inp" id="mName" placeholder="제품명 *"/>
        <input class="inp" id="mCo" placeholder="제조/공급사"/>
        <input class="inp" id="mUse" placeholder="용도"/>
        <select class="inp" id="mSig"><option value="경고">경고</option><option value="위험">위험</option></select>
        <input class="inp" id="mHazards" placeholder="유해·위험성 (쉼표로 구분)"/>
        <textarea class="inp form-full" id="mComps" placeholder="구성성분 (줄바꿈, 형식: 물질명|CAS번호|함유량)" style="min-height:80px"></textarea>
        <textarea class="inp form-full" id="mFaEye"   placeholder="눈 응급조치"></textarea>
        <textarea class="inp form-full" id="mFaSkin"  placeholder="피부 응급조치"></textarea>
        <textarea class="inp form-full" id="mFaInhal" placeholder="흡입 응급조치"></textarea>
        <textarea class="inp form-full" id="mFaIng"   placeholder="섭취 응급조치"></textarea>
        <textarea class="inp form-full" id="mHandling" placeholder="안전취급요령"></textarea>
        <textarea class="inp form-full" id="mStorage"  placeholder="저장방법"></textarea>
        <input class="inp form-full" id="mSpecial" placeholder="특별 주의사항 (없으면 빈칸)"/>
        <input class="inp form-full" id="mDrive"   placeholder="구글 드라이브 URL (원본 MSDS)"/>
      </div>
      <button class="sub-btn btn-admin" style="margin-top:12px" onclick="addMsdsProduct()">✅ 제품 추가</button>
      <div class="ok-msg" id="mOk"></div><div class="err-msg" id="mErr"></div>
    </div>
    <div class="panel">
      <div style="font-size:13px;font-weight:800;color:var(--text2);margin-bottom:14px">등록된 MSDS 제품 목록</div>
      <div class="tab-row" id="msdsAdminTabs">
        ${MSDS_PROCESSES.map((p,i)=>`<button class="tab-btn${i===0?' active':''}" onclick="showMsdsAdminTab('${p.key}',this)">${p.icon} ${p.label}</button>`).join('')}
      </div>
      ${MSDS_PROCESSES.map((p,i)=>`<div class="tab-content${i===0?' active':''}" id="msdsAdminTab_${p.key}">
        <div class="msds-list" id="adminMsdsList_${p.key}"></div></div>`).join('')}
    </div>`;
  MSDS_PROCESSES.forEach(p=>loadMsdsProductList(p.key,document.getElementById('adminMsdsList_'+p.key),true));
};

function showMsdsAdminTab(key,btn){
  document.querySelectorAll('#msdsAdminTabs .tab-btn').forEach(b=>b.classList.remove('active'));
  document.querySelectorAll('[id^="msdsAdminTab_"]').forEach(el=>el.classList.remove('active'));
  btn.classList.add('active'); document.getElementById('msdsAdminTab_'+key).classList.add('active');
}

async function addMsdsProduct(){
  const ok=document.getElementById('mOk'),err=document.getElementById('mErr');
  ok.style.display=err.style.display='none';
  const name=document.getElementById('mName').value.trim();
  if(!name){ err.textContent='제품명은 필수입니다.'; err.style.display='block'; return; }
  const compsRaw=document.getElementById('mComps').value.trim();
  const components=compsRaw?compsRaw.split('\n').map(line=>{ const p=line.split('|'); return {name:(p[0]||'').trim(),cas:(p[1]||'-').trim(),content:(p[2]||'').trim()}; }).filter(c=>c.name):[];
  const hazardsRaw=document.getElementById('mHazards').value.trim();
  const hazards=hazardsRaw?hazardsRaw.split(',').map(s=>s.trim()).filter(Boolean):[];
  const data={
    process:document.getElementById('mProc').value, name,
    company:document.getElementById('mCo').value.trim(), use:document.getElementById('mUse').value.trim(),
    signalWord:document.getElementById('mSig').value, hazards, components,
    faEye:document.getElementById('mFaEye').value.trim(), faSkin:document.getElementById('mFaSkin').value.trim(),
    faInhal:document.getElementById('mFaInhal').value.trim(), faIng:document.getElementById('mFaIng').value.trim(),
    handling:document.getElementById('mHandling').value.trim(), storage:document.getElementById('mStorage').value.trim(),
    specialNote:document.getElementById('mSpecial').value.trim(), driveLink:document.getElementById('mDrive').value.trim(),
    createdAt:firebase.firestore.FieldValue.serverTimestamp(),
  };
  try{
    await db.collection('msds').add(data);
    ok.textContent='✅ 제품이 추가되었습니다.'; ok.style.display='block';
    ['mName','mCo','mUse','mHazards','mComps','mFaEye','mFaSkin','mFaInhal','mFaIng','mHandling','mStorage','mSpecial','mDrive'].forEach(id=>{ document.getElementById(id).value=''; });
  }catch(e){ err.textContent='❌ Firebase 오류: '+e.message; err.style.display='block'; }
}

async function deleteMsdsItem(id){
  if(!confirm('이 제품을 삭제하시겠습니까?')) return;
  try{ await db.collection('msds').doc(id).delete(); }
  catch(e){ alert('삭제 오류: '+e.message); }
}
</script>

<script>
/* ════════ 아차사고 신고 ════════ */
pageInit['report']=function(container){
  container.innerHTML=`
    <div class="page-header"><button class="back-btn" onclick="goBack()">← 뒤로</button>
      <div><div class="page-ttl">⚠️ 아차사고 신고</div><div class="page-sub">위험 상황 발견 시 즉시 신고하세요</div></div></div>
    <div class="panel">
      <p style="font-size:13px;color:var(--text2);margin-bottom:16px">
        아래 내용을 작성 후 제출하면 <strong style="color:var(--cyan)">관리자에게 즉시 전달</strong>됩니다.
      </p>
      <div class="form-grid">
        <input class="inp" id="rPlace"  placeholder="📍 발생 위치 * (예: 1층 창고, 전기실 앞)"/>
        <input class="inp" id="rType"   placeholder="🚨 위험 유형 * (예: 전도, 감전, 낙하, 화재)"/>
        <textarea class="inp form-full" id="rDetail" placeholder="📝 상세 내용 *"></textarea>
        <input class="inp" id="rName"  placeholder="👤 작성자 (선택 — 익명 가능)"/>
        <input class="inp" id="rPhone" placeholder="📞 연락처 (선택)"/>
      </div>
      <button class="sub-btn btn-report" id="reportSubmitBtn" onclick="submitReport()">신고 제출 ✅</button>
      <div class="ok-msg" id="rOk"></div><div class="err-msg" id="rErr"></div>
      <div style="margin-top:20px;padding:14px 16px;background:var(--cyan-dim);border:1px solid rgba(57,197,207,.25);border-radius:var(--radius);font-size:13px;color:var(--text2);line-height:1.8">
        <strong style="color:var(--cyan)">📋 신고 안내</strong><br/>
        • 발생 위치, 위험 유형, 상세 내용은 <strong>필수 항목</strong>입니다.<br/>
        • 작성자와 연락처는 입력하지 않아도 익명으로 제출됩니다.
      </div>
    </div>`;
};

async function submitReport(){
  const place=document.getElementById('rPlace').value.trim(),type=document.getElementById('rType').value.trim(),detail=document.getElementById('rDetail').value.trim();
  const name=document.getElementById('rName').value.trim(),phone=document.getElementById('rPhone').value.trim();
  const ok=document.getElementById('rOk'),err=document.getElementById('rErr');
  ok.style.display=err.style.display='none';
  if(!place||!type||!detail){ err.textContent='⚠️ 필수 항목(위치/위험유형/상세내용)을 입력해 주세요.'; err.style.display='block'; return; }
  const btn=document.getElementById('reportSubmitBtn'); btn.disabled=true; btn.textContent='제출 중…';
  try{
    await db.collection('reports').add({place,type,detail,name:name||'익명',phone:phone||'-',status:'신규',createdAt:firebase.firestore.FieldValue.serverTimestamp()});
    ok.textContent='✅ 신고가 접수되었습니다. 안전관리팀이 신속히 조치하겠습니다.'; ok.style.display='block';
    ['rPlace','rType','rDetail','rName','rPhone'].forEach(id=>{ document.getElementById(id).value=''; });
  }catch(e){ err.textContent='❌ Firebase 오류: '+e.message; err.style.display='block'; console.error(e); }
  finally{ btn.disabled=false; btn.textContent='신고 제출 ✅'; }
}

let reportUnsub=null, reportStatusFilter='전체';

pageInit['admin-reports']=function(container){
  if(!isAdmin){ container.innerHTML='<div class="panel"><p style="color:var(--red)">⛔ 관리자 권한이 필요합니다.</p></div>'; return; }
  container.innerHTML=`
    <div class="page-header"><button class="back-btn" onclick="goBack()">← 뒤로</button>
      <div><div class="page-ttl">⚠️ 아차사고 신고 목록</div><div class="page-sub">관리자 전용 · 실시간</div></div></div>
    <div class="panel">
      <div class="filter-row" id="reportFilterRow">
        ${['전체','신규','처리중','완료'].map(s=>`<button class="flt-btn${s==='전체'?' active':''}" onclick="setReportFilter('${s}',this)">${s}</button>`).join('')}
      </div>
      <div id="reportListWrap"></div>
    </div>`;
  setTimeout(()=>subscribeReportList(),0);
};

function setReportFilter(f,btn){
  reportStatusFilter=f;
  document.querySelectorAll('#reportFilterRow .flt-btn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active'); subscribeReportList();
}

function subscribeReportList(){
  const el=document.getElementById('reportListWrap'); if(!el) return;
  if(reportUnsub){ reportUnsub(); reportUnsub=null; }
  showLoading(el);
  /* reports는 단일 orderBy → 인덱스 불필요 */
  reportUnsub=db.collection('reports').orderBy('createdAt','desc')
    .onSnapshot(snap=>{
      let docs=snap.docs.map(d=>({id:d.id,...d.data()}));
      if(reportStatusFilter!=='전체') docs=docs.filter(d=>d.status===reportStatusFilter);
      if(!docs.length){ showEmpty(el,'접수된 신고가 없습니다.'); return; }
      el.innerHTML=`<div class="submission-list">${docs.map(d=>renderReportCard(d)).join('')}</div>`;
    }, err=>showFbErr(el,err));
}

function renderReportCard(d){
  const sc=d.status==='완료'?'status-done':'status-new';
  return `<div class="sub-card">
    <div class="sub-card-header">
      <span class="status-badge ${sc}">${esc(d.status||'신규')}</span>
      <div class="sub-card-title">📍 ${esc(d.place)} — ${esc(d.type)}</div>
      <div class="sub-card-meta">${tsf(d.createdAt)}</div>
    </div>
    <div class="sub-card-body">${esc(d.detail)}\n<span style="color:var(--text3);font-size:12px">👤 ${esc(d.name||'익명')} ${d.phone&&d.phone!=='-'?'| 📞 '+esc(d.phone):''}</span></div>
    <div style="margin-top:10px;display:flex;gap:8px;flex-wrap:wrap">
      <select class="inp" style="width:auto;flex:0 0 auto;font-size:12px;padding:5px 10px" onchange="updateReportStatus('${d.id}',this.value)">
        ${['신규','처리중','완료'].map(s=>`<option value="${s}"${d.status===s?' selected':''}>${s}</option>`).join('')}
      </select>
      <button class="del-btn" onclick="deleteReport('${d.id}')">삭제</button>
    </div>
  </div>`;
}

async function updateReportStatus(id,status){ try{ await db.collection('reports').doc(id).update({status}); }catch(e){ alert('오류: '+e.message); } }
async function deleteReport(id){ if(!confirm('삭제하시겠습니까?')) return; try{ await db.collection('reports').doc(id).delete(); }catch(e){ alert('삭제 오류: '+e.message); } }
</script>

<script>
/* ════════ 근로자 의견 ════════ */
pageInit['opinion']=function(container){
  container.innerHTML=`
    <div class="page-header"><button class="back-btn" onclick="goBack()">← 뒤로</button>
      <div><div class="page-ttl">💬 근로자 의견 청취</div><div class="page-sub">개선사항·건의사항을 자유롭게 제안하세요</div></div></div>
    <div class="panel">
      <p style="font-size:13px;color:var(--text2);margin-bottom:16px">
        현장의 안전 개선사항, 불편사항 등을 제안해 주세요. <strong style="color:var(--green)">관리자에게 즉시 전달</strong>됩니다.
      </p>
      <div class="form-grid">
        <select class="inp" id="opCat">
          <option value="">의견 유형 선택 *</option>
          <option value="안전개선">⛑️ 안전 개선 제안</option>
          <option value="설비개선">🔧 설비/장비 개선</option>
          <option value="작업환경">🏭 작업 환경 개선</option>
          <option value="교육훈련">📚 교육/훈련 관련</option>
          <option value="복지">☕ 복지/편의시설</option>
          <option value="기타">💬 기타 건의사항</option>
        </select>
        <input class="inp" id="opTitle" placeholder="📋 제목 *"/>
        <textarea class="inp form-full" id="opContent" placeholder="✍️ 의견 내용을 자세히 작성해 주세요. *" style="min-height:140px"></textarea>
        <input class="inp" id="opName"  placeholder="👤 작성자 (선택 — 익명 가능)"/>
        <input class="inp" id="opPhone" placeholder="📞 연락처 (회신 필요 시 입력)"/>
      </div>
      <button class="sub-btn btn-opinion" id="opinionSubmitBtn" onclick="submitOpinion()">의견 제출 📝</button>
      <div class="ok-msg" id="opOk"></div><div class="err-msg" id="opErr"></div>
      <div style="margin-top:20px;padding:14px 16px;background:var(--green-dim);border:1px solid rgba(63,185,80,.2);border-radius:var(--radius);font-size:13px;color:var(--text2);line-height:1.8">
        <strong style="color:var(--green)">💡 좋은 의견 작성 팁</strong><br/>
        • 어떤 상황에서 어떻게 위험한지 <strong>구체적으로</strong> 작성해 주세요.<br/>
        • 문제점과 함께 <strong>개선 방안</strong>도 제시하면 더 좋습니다.<br/>
        • 이름·연락처 없이 <strong>익명</strong>으로도 제출 가능합니다.
      </div>
    </div>`;
};

async function submitOpinion(){
  const cat=document.getElementById('opCat').value,title=document.getElementById('opTitle').value.trim(),content=document.getElementById('opContent').value.trim();
  const name=document.getElementById('opName').value.trim(),phone=document.getElementById('opPhone').value.trim();
  const ok=document.getElementById('opOk'),err=document.getElementById('opErr');
  ok.style.display=err.style.display='none';
  if(!cat||!title||!content){ err.textContent='⚠️ 필수 항목(의견 유형/제목/내용)을 입력해 주세요.'; err.style.display='block'; return; }
  const btn=document.getElementById('opinionSubmitBtn'); btn.disabled=true; btn.textContent='제출 중…';
  try{
    await db.collection('opinions').add({category:cat,title,content,name:name||'익명',phone:phone||'-',status:'신규',createdAt:firebase.firestore.FieldValue.serverTimestamp()});
    ok.textContent='✅ 의견이 접수되었습니다. 검토 후 개선에 반영하겠습니다. 감사합니다!'; ok.style.display='block';
    ['opCat','opTitle','opContent','opName','opPhone'].forEach(id=>{ const el=document.getElementById(id); if(el) el.value=''; });
  }catch(e){ err.textContent='❌ Firebase 오류: '+e.message; err.style.display='block'; console.error(e); }
  finally{ btn.disabled=false; btn.textContent='의견 제출 📝'; }
}

const OPINION_CAT_LABELS={'안전개선':'⛑️ 안전개선','설비개선':'🔧 설비개선','작업환경':'🏭 작업환경','교육훈련':'📚 교육훈련','복지':'☕ 복지','기타':'💬 기타'};
let opinionUnsub=null, opinionStatusFilter='전체';

pageInit['admin-opinions']=function(container){
  if(!isAdmin){ container.innerHTML='<div class="panel"><p style="color:var(--red)">⛔ 관리자 권한이 필요합니다.</p></div>'; return; }
  container.innerHTML=`
    <div class="page-header"><button class="back-btn" onclick="goBack()">← 뒤로</button>
      <div><div class="page-ttl">💬 근로자 의견 목록</div><div class="page-sub">관리자 전용 · 실시간</div></div></div>
    <div class="panel">
      <div class="filter-row" id="opinionFilterRow">
        ${['전체','신규','검토중','완료'].map(s=>`<button class="flt-btn${s==='전체'?' active':''}" onclick="setOpinionFilter('${s}',this)">${s}</button>`).join('')}
      </div>
      <div id="opinionListWrap"></div>
    </div>`;
  setTimeout(()=>subscribeOpinionList(),0);
};

function setOpinionFilter(f,btn){
  opinionStatusFilter=f;
  document.querySelectorAll('#opinionFilterRow .flt-btn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active'); subscribeOpinionList();
}

function subscribeOpinionList(){
  const el=document.getElementById('opinionListWrap'); if(!el) return;
  if(opinionUnsub){ opinionUnsub(); opinionUnsub=null; }
  showLoading(el);
  opinionUnsub=db.collection('opinions').orderBy('createdAt','desc')
    .onSnapshot(snap=>{
      let docs=snap.docs.map(d=>({id:d.id,...d.data()}));
      if(opinionStatusFilter!=='전체') docs=docs.filter(d=>d.status===opinionStatusFilter);
      if(!docs.length){ showEmpty(el,'접수된 의견이 없습니다.'); return; }
      el.innerHTML=`<div class="submission-list">${docs.map(d=>renderOpinionCard(d)).join('')}</div>`;
    }, err=>showFbErr(el,err));
}

function renderOpinionCard(d){
  const sc=d.status==='완료'?'status-done':'status-new';
  const catLabel=OPINION_CAT_LABELS[d.category]||d.category||'기타';
  return `<div class="sub-card">
    <div class="sub-card-header">
      <span class="status-badge ${sc}">${esc(d.status||'신규')}</span>
      <span style="font-size:11px;font-weight:800;color:var(--green);background:var(--green-dim);border:1px solid rgba(63,185,80,.2);padding:2px 8px;border-radius:4px">${esc(catLabel)}</span>
      <div class="sub-card-title">${esc(d.title)}</div>
      <div class="sub-card-meta">${tsf(d.createdAt)}</div>
    </div>
    <div class="sub-card-body">${esc(d.content)}\n<span style="color:var(--text3);font-size:12px">👤 ${esc(d.name||'익명')} ${d.phone&&d.phone!=='-'?'| 📞 '+esc(d.phone):''}</span></div>
    <div style="margin-top:10px;display:flex;gap:8px;flex-wrap:wrap">
      <select class="inp" style="width:auto;flex:0 0 auto;font-size:12px;padding:5px 10px" onchange="updateOpinionStatus('${d.id}',this.value)">
        ${['신규','검토중','완료'].map(s=>`<option value="${s}"${d.status===s?' selected':''}>${s}</option>`).join('')}
      </select>
      <button class="del-btn" onclick="deleteOpinion('${d.id}')">삭제</button>
    </div>
  </div>`;
}

async function updateOpinionStatus(id,status){ try{ await db.collection('opinions').doc(id).update({status}); }catch(e){ alert('오류: '+e.message); } }
async function deleteOpinion(id){ if(!confirm('삭제하시겠습니까?')) return; try{ await db.collection('opinions').doc(id).delete(); }catch(e){ alert('삭제 오류: '+e.message); } }

window.addEventListener('DOMContentLoaded', initHomeBanner);
</script>
</body>
</html>
