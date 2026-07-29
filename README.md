<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Crius CRM</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=Roboto+Mono:wght@500&display=swap');

  /* ============================== TOKENS ============================== */
  :root{
    --canvas:#F3F5F9;
    --card:#FFFFFF;
    --line:#E3E8F0;
    --line-soft:#EEF1F6;

    --ink-900:#0E1526;
    --ink-700:#2B3548;
    --ink-600:#3D485D;
    --ink-500:#5B6579;
    --ink-400:#8791A3;
    --ink-300:#AEB6C4;
    --ink-100:#EEF1F6;

    --brand-900:#0A3B33;
    --brand-800:#0C4E44;
    --brand-700:#0F6154;
    --brand-600:#128C77;
    --brand-500:#15A38C;
    --brand-100:#E4F5F1;
    --brand-50:#F1FAF8;

    --amber-600:#9A6112;
    --amber-500:#B5791E;
    --amber-100:#FBF1DF;

    --blue-600:#264C87;
    --blue-500:#2E5EA8;
    --blue-100:#E7EEF9;

    --violet-600:#5B3E97;
    --violet-500:#7A57BE;
    --violet-100:#EFE9FA;

    --red-600:#93291F;
    --red-500:#C1392B;
    --red-100:#FBEAE8;

    --sidebar:#0A1120;
    --sidebar-card:#121B30;
    --sidebar-hi:#17233D;
    --sidebar-line:#1E2A44;
    --sidebar-text:#8393B0;
    --sidebar-text-hi:#EDF1F8;

    --radius-sm:6px;
    --radius:10px;
    --radius-lg:14px;
    --shadow-sm:0 1px 2px rgba(16,24,43,.05);
    --shadow:0 2px 8px rgba(16,24,43,.06), 0 1px 2px rgba(16,24,43,.05);
    --shadow-lg:0 20px 48px rgba(10,17,32,.18);
    --topbar-h:58px;
    --subnav-h:44px;
  }
  *{box-sizing:border-box;}
  html{margin:0;padding:0;}
  html,body{height:100%;width:100%;}
  body{margin:0;padding:0;font-family:'Inter',Arial,sans-serif;background:var(--canvas);color:var(--ink-900);font-size:13.5px;-webkit-font-smoothing:antialiased;overflow-x:hidden;}
  code,.mono{font-family:'Roboto Mono',monospace;}
  h1,h2,h3{font-family:'Inter',Arial,sans-serif;letter-spacing:-.01em;}
  a{color:inherit;}
  ::selection{background:var(--brand-100);}
  ::-webkit-scrollbar{width:9px;height:9px;}
  ::-webkit-scrollbar-thumb{background:#D6DCE6;border-radius:20px;border:2px solid var(--canvas);}
  #app{display:flex;width:100%;height:100vh;height:100dvh;}
  svg.icon{width:16px;height:16px;stroke:currentColor;fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round;flex-shrink:0;display:block;}

  /* ============================== SIDEBAR ============================== */
  #sidebar{width:232px;background:var(--sidebar);color:var(--sidebar-text);flex-shrink:0;display:flex;flex-direction:column;transition:width .16s ease;position:relative;}
  #sidebar.collapsed{width:66px;}
  #sidebar.collapsed .brand-text,#sidebar.collapsed .nav-label,#sidebar.collapsed .nav-group-label,#sidebar.collapsed .nav-item span.lbl,#sidebar.collapsed .nav-count{display:none;}
  #sidebar.collapsed .nav-item{justify-content:center;}
  #sidebar.collapsed .brand{justify-content:center;padding:0 0 18px;}

  .brand{padding:18px 18px 16px;display:flex;align-items:center;gap:10px;border-bottom:1px solid var(--sidebar-line);margin-bottom:6px;}
  .brand-mark{width:30px;height:30px;border-radius:8px;background:linear-gradient(140deg,var(--brand-500),var(--brand-900) 85%);flex-shrink:0;display:flex;align-items:center;justify-content:center;color:#fff;font-weight:800;font-size:13px;font-family:'Inter';}
  .brand-text .brand-name{color:var(--sidebar-text-hi);font-weight:700;font-size:14.5px;letter-spacing:-.01em;line-height:1.2;}
  .brand-text .brand-sub{color:#5D6E8C;font-size:10px;letter-spacing:.6px;text-transform:uppercase;font-weight:600;}

  .nav-scroll{flex:1;overflow-y:auto;padding:4px 10px 10px;}
  .nav-group-label{font-size:10px;text-transform:uppercase;letter-spacing:1.1px;color:#4A5A7A;padding:16px 10px 6px;font-weight:700;}
  .nav-item{padding:8px 10px;cursor:pointer;font-size:13px;display:flex;align-items:center;gap:11px;border-radius:8px;font-weight:500;color:var(--sidebar-text);margin-bottom:1px;justify-content:space-between;}
  .nav-item-l{display:flex;align-items:center;gap:11px;}
  .nav-item svg{opacity:.8;}
  .nav-item:hover{background:var(--sidebar-hi);color:var(--sidebar-text-hi);}
  .nav-item.active{background:linear-gradient(90deg,rgba(21,163,140,.22),rgba(21,163,140,.05));color:#fff;box-shadow:inset 2px 0 0 var(--brand-500);}
  .nav-item.active svg{opacity:1;color:var(--brand-500);}
  .nav-count{font-size:10px;font-weight:700;color:var(--sidebar-text);background:var(--sidebar-hi);padding:1px 7px;border-radius:20px;}

  .sidebar-foot{padding:10px;border-top:1px solid var(--sidebar-line);}
  .collapse-btn{width:100%;display:flex;align-items:center;justify-content:center;gap:8px;padding:8px;border-radius:8px;background:transparent;border:none;color:var(--sidebar-text);cursor:pointer;font-size:12px;font-family:inherit;}
  .collapse-btn:hover{background:var(--sidebar-hi);color:#fff;}

  /* ============================== SHELL / TOPBAR ============================== */
  #shell{flex:1 1 auto;width:100%;display:flex;flex-direction:column;min-width:0;}
  #topbar{height:var(--topbar-h);background:var(--card);border-bottom:1px solid var(--line);display:flex;align-items:center;justify-content:space-between;padding:0 20px;flex-shrink:0;gap:16px;}
  .topbar-left{display:flex;align-items:center;gap:14px;flex:1;min-width:0;}
  .search-box{position:relative;max-width:420px;flex:1;}
  .search-box svg{position:absolute;left:11px;top:50%;transform:translateY(-50%);color:var(--ink-400);}
  .search-box input{width:100%;padding:8px 12px 8px 34px;border:1px solid var(--line);border-radius:8px;font-size:12.5px;background:var(--canvas);font-family:inherit;color:var(--ink-900);}
  .search-box input:focus{outline:none;border-color:var(--brand-500);background:#fff;box-shadow:0 0 0 3px var(--brand-100);}
  .search-results{position:absolute;top:calc(100% + 6px);left:0;right:0;background:#fff;border:1px solid var(--line);border-radius:10px;box-shadow:var(--shadow-lg);z-index:80;display:none;max-height:340px;overflow-y:auto;}
  .search-results.open{display:block;}
  .search-results .sr-group-label{font-size:10px;text-transform:uppercase;letter-spacing:.6px;color:var(--ink-400);font-weight:700;padding:9px 14px 4px;}
  .search-results .sr-item{padding:8px 14px;font-size:12.5px;font-weight:600;color:var(--ink-700);cursor:pointer;display:flex;justify-content:space-between;}
  .search-results .sr-item:hover{background:var(--brand-50);color:var(--brand-700);}
  .search-results .sr-empty{padding:16px;font-size:12px;color:var(--ink-400);text-align:center;}

  .topbar-right{display:flex;align-items:center;gap:8px;}
  .icon-btn{width:32px;height:32px;border-radius:8px;border:1px solid transparent;background:transparent;display:flex;align-items:center;justify-content:center;color:var(--ink-500);cursor:pointer;position:relative;}
  .icon-btn:hover{background:var(--canvas);border-color:var(--line);color:var(--ink-900);}
  .dot-badge{position:absolute;top:5px;right:6px;width:6px;height:6px;border-radius:50%;background:var(--red-500);border:1.5px solid #fff;}

  .quickcreate{position:relative;}
  .qc-menu{position:absolute;top:calc(100% + 8px);right:0;background:#fff;border:1px solid var(--line);border-radius:10px;box-shadow:var(--shadow-lg);width:200px;padding:6px;display:none;z-index:60;}
  .qc-menu.open{display:block;}
  .qc-item{display:flex;align-items:center;gap:9px;padding:8px 9px;border-radius:7px;font-size:12.5px;font-weight:600;color:var(--ink-700);cursor:pointer;}
  .qc-item:hover{background:var(--brand-50);color:var(--brand-700);}
  .qc-item svg{color:var(--brand-600);}

  .role-pill{font-size:10.5px;font-weight:700;text-transform:uppercase;letter-spacing:.4px;background:var(--brand-100);color:var(--brand-700);padding:3px 9px;border-radius:20px;}
  .user-chip{display:flex;align-items:center;gap:9px;padding:4px 8px 4px 4px;border-radius:9px;cursor:pointer;}
  .user-chip:hover{background:var(--canvas);}
  .avatar{width:29px;height:29px;border-radius:50%;background:linear-gradient(140deg,var(--brand-500),var(--brand-900));color:#fff;display:flex;align-items:center;justify-content:center;font-weight:700;font-size:11.5px;flex-shrink:0;}
  .avatar.sm{width:22px;height:22px;font-size:9.5px;}

  #main{flex:1;overflow-y:auto;padding:22px 26px 60px;}

  .breadcrumb{display:flex;align-items:center;gap:6px;font-size:11.5px;color:var(--ink-400);font-weight:600;margin-bottom:6px;text-transform:uppercase;letter-spacing:.4px;}
  .breadcrumb .sep{color:var(--ink-300);}
  .page-header{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:16px;gap:16px;flex-wrap:wrap;}
  .page-header h1{font-size:20px;margin:0 0 3px;font-weight:800;letter-spacing:-.02em;}
  .page-sub{font-size:12.5px;color:var(--ink-500);}
  .header-actions{display:flex;gap:8px;flex-shrink:0;align-items:center;}

  /* ============================== BUTTONS ============================== */
  .btn{background:var(--brand-700);color:#fff;border:none;padding:9px 15px;border-radius:8px;font-size:12.5px;cursor:pointer;font-weight:700;font-family:inherit;display:inline-flex;align-items:center;gap:7px;letter-spacing:.1px;transition:background .12s;white-space:nowrap;}
  .btn:hover{background:var(--brand-900);}
  .btn.secondary{background:#fff;color:var(--ink-700);border:1px solid var(--line);font-weight:600;}
  .btn.secondary:hover{background:var(--canvas);border-color:var(--ink-300);}
  .btn.ghost{background:transparent;color:var(--ink-500);padding:6px 8px;font-weight:600;}
  .btn.ghost:hover{color:var(--ink-900);}
  .btn.danger{background:var(--red-500);}
  .btn.danger:hover{background:var(--red-600);}
  .btn.small{padding:6px 11px;font-size:11.5px;}
  .btn:disabled{opacity:.5;cursor:not-allowed;}

  /* ============================== SAVED VIEW TABS / SUBNAV ============================== */
  .view-tabs{display:flex;align-items:center;gap:2px;border-bottom:1px solid var(--line);margin-bottom:14px;flex-wrap:wrap;}
  .view-tab{padding:9px 14px;font-size:12.5px;font-weight:700;color:var(--ink-500);cursor:pointer;border-bottom:2px solid transparent;display:flex;align-items:center;gap:6px;}
  .view-tab:hover{color:var(--ink-900);}
  .view-tab.active{color:var(--brand-700);border-bottom-color:var(--brand-600);}

  /* ============================== KPI / CARDS ============================== */
  .kpi-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:14px;margin-bottom:16px;}
  .kpi-card{background:var(--card);border:1px solid var(--line);border-radius:var(--radius-lg);padding:16px 18px;box-shadow:var(--shadow-sm);position:relative;overflow:hidden;}
  .kpi-card::before{content:"";position:absolute;top:0;left:0;right:0;height:3px;background:var(--kpi-accent,var(--brand-500));}
  .kpi-top{display:flex;justify-content:space-between;align-items:flex-start;}
  .kpi-icon{width:32px;height:32px;border-radius:8px;background:var(--kpi-accent-soft,var(--brand-100));color:var(--kpi-accent,var(--brand-700));display:flex;align-items:center;justify-content:center;}
  .kpi-card .kpi-label{font-size:11px;text-transform:uppercase;letter-spacing:.5px;color:var(--ink-500);font-weight:700;margin-top:12px;}
  .kpi-card .kpi-value{font-size:27px;font-weight:800;margin-top:4px;letter-spacing:-.02em;}
  .kpi-card .kpi-delta{font-size:11px;margin-top:5px;color:var(--brand-600);font-weight:700;display:flex;align-items:center;gap:4px;}
  .kpi-card .kpi-remove{position:absolute;top:10px;right:10px;background:none;border:none;color:var(--ink-300);cursor:pointer;font-size:14px;line-height:1;}
  .kpi-card .kpi-remove:hover{color:var(--red-500);}
  .add-widget-card{border:1.5px dashed var(--line);border-radius:var(--radius-lg);display:flex;align-items:center;justify-content:center;gap:6px;color:var(--ink-500);cursor:pointer;font-size:12.5px;font-weight:700;min-height:110px;}
  .add-widget-card:hover{border-color:var(--brand-500);color:var(--brand-700);background:var(--brand-50);}

  .grid-2{display:grid;grid-template-columns:1.4fr 1fr;gap:16px;align-items:start;}
  .grid-3{display:grid;grid-template-columns:repeat(3,1fr);gap:14px;}
  .card{background:var(--card);border:1px solid var(--line);border-radius:var(--radius-lg);padding:18px 20px;margin-bottom:16px;box-shadow:var(--shadow-sm);}
  .card-title{font-size:13px;font-weight:700;margin-bottom:14px;display:flex;justify-content:space-between;align-items:center;letter-spacing:-.01em;}
  .card-title .muted{font-size:11px;color:var(--ink-400);font-weight:600;text-transform:none;}

  .insight-strip{display:flex;gap:12px;overflow-x:auto;margin-bottom:16px;padding-bottom:2px;}
  .insight-card{flex:0 0 260px;background:linear-gradient(160deg,var(--brand-800),var(--brand-900));color:#fff;border-radius:var(--radius-lg);padding:15px 17px;position:relative;overflow:hidden;}
  .insight-card .ic-eyebrow{font-size:10px;text-transform:uppercase;letter-spacing:.7px;color:#9FD8CB;font-weight:700;display:flex;align-items:center;gap:6px;margin-bottom:8px;}
  .insight-card .ic-text{font-size:12.6px;line-height:1.5;font-weight:500;color:#EAF6F3;}
  .insight-card .ic-text b{color:#fff;}

  /* ============================== TABLE / LIST VIEW ============================== */
  .table-wrap{background:var(--card);border:1px solid var(--line);border-radius:var(--radius-lg);overflow:hidden;box-shadow:var(--shadow-sm);}
  .table-toolbar{display:flex;justify-content:space-between;align-items:center;padding:12px 16px;border-bottom:1px solid var(--line-soft);gap:10px;flex-wrap:wrap;}
  .toolbar-left{display:flex;align-items:center;gap:8px;flex-wrap:wrap;}
  .view-toggle{display:flex;background:var(--canvas);border:1px solid var(--line);border-radius:8px;padding:2px;gap:2px;}
  .view-toggle button{border:none;background:transparent;padding:6px 11px;border-radius:6px;font-size:11.5px;font-weight:700;color:var(--ink-500);cursor:pointer;display:flex;align-items:center;gap:6px;}
  .view-toggle button.active{background:#fff;color:var(--brand-700);box-shadow:var(--shadow-sm);}
  .filter-chip{display:inline-flex;align-items:center;gap:6px;background:var(--canvas);border:1px solid var(--line);border-radius:20px;padding:5px 10px;font-size:11.5px;font-weight:600;color:var(--ink-600);cursor:pointer;}
  .filter-chip:hover{border-color:var(--ink-300);}
  .list-search{position:relative;}
  .list-search svg{position:absolute;left:9px;top:50%;transform:translateY(-50%);color:var(--ink-400);width:14px;height:14px;}
  .list-search input{padding:6px 10px 6px 28px;border:1px solid var(--line);border-radius:20px;font-size:11.8px;font-family:inherit;width:190px;background:var(--canvas);}
  .list-search input:focus{outline:none;border-color:var(--brand-500);background:#fff;}

  .mass-bar{display:none;align-items:center;gap:10px;background:var(--brand-900);color:#fff;padding:9px 16px;font-size:12px;font-weight:700;}
  .mass-bar.open{display:flex;}
  .mass-bar .mb-btn{background:rgba(255,255,255,.12);border:none;color:#fff;padding:5px 11px;border-radius:6px;cursor:pointer;font-size:11.5px;font-weight:700;font-family:inherit;}
  .mass-bar .mb-btn:hover{background:rgba(255,255,255,.22);}

  table{width:100%;border-collapse:collapse;}
  th{background:#FAFBFD;text-align:left;padding:10px 16px;font-size:10.5px;color:var(--ink-500);text-transform:uppercase;letter-spacing:.5px;font-weight:700;border-bottom:1px solid var(--line);white-space:nowrap;cursor:pointer;user-select:none;}
  th:hover{color:var(--ink-900);}
  th.sort-active{color:var(--brand-700);}
  td{padding:11px 16px;font-size:12.8px;border-bottom:1px solid var(--line-soft);color:var(--ink-700);}
  tbody tr{cursor:pointer;}
  tr:last-child td{border-bottom:none;}
  tr:hover td{background:#FAFBFD;}
  .row-primary{font-weight:700;color:var(--ink-900);}
  .row-actions{display:flex;gap:6px;justify-content:flex-end;}
  input.row-check, th input[type=checkbox]{width:14px;height:14px;accent-color:var(--brand-600);}

  .pill{display:inline-block;padding:3px 10px;border-radius:20px;font-size:10.5px;font-weight:700;letter-spacing:.2px;}
  .pill.stage-Quotation{background:var(--amber-100);color:var(--amber-600);}
  .pill.stage-Negotiation{background:var(--blue-100);color:var(--blue-600);}
  .pill.stage-PORaised,.pill.stage-EnquiryRaised,.pill.stage-Existing,.pill.stage-Completed,.pill.stage-Won{background:var(--brand-100);color:var(--brand-700);}
  .pill.stage-OrderLost,.pill.stage-NotConverted,.pill.stage-Lost{background:var(--red-100);color:var(--red-600);}
  .pill.stage-New,.pill.stage-Open{background:var(--blue-100);color:var(--blue-600);}
  .pill.role-pill{background:var(--ink-100);color:var(--ink-700);}
  .pill.high{background:var(--red-100);color:var(--red-600);}
  .pill.normal{background:var(--blue-100);color:var(--blue-600);}
  .pill.low{background:var(--ink-100);color:var(--ink-500);}
  .tag{display:inline-flex;align-items:center;background:var(--violet-100);color:var(--violet-600);font-size:10px;font-weight:700;padding:2px 8px;border-radius:20px;margin:0 4px 4px 0;}

  .prob-bar{width:64px;height:6px;background:var(--ink-100);border-radius:20px;overflow:hidden;display:inline-block;vertical-align:middle;margin-right:6px;}
  .prob-bar-fill{height:100%;background:var(--brand-500);}

  /* ============================== KANBAN ============================== */
  .kanban{display:flex;gap:14px;overflow-x:auto;padding-bottom:6px;}
  .kanban-col{flex:0 0 272px;background:#EEF1F7;border-radius:var(--radius-lg);padding:10px;max-height:calc(100vh - 300px);display:flex;flex-direction:column;}
  .kanban-col-head{display:flex;align-items:center;justify-content:space-between;padding:6px 6px 10px;}
  .kanban-col-title{display:flex;align-items:center;gap:8px;font-size:12px;font-weight:800;color:var(--ink-700);}
  .kanban-dot{width:8px;height:8px;border-radius:50%;}
  .kanban-count{font-size:10.5px;font-weight:700;background:#fff;color:var(--ink-500);padding:2px 7px;border-radius:20px;}
  .kanban-col-total{font-size:11px;color:var(--ink-500);font-weight:700;padding:0 6px 8px;}
  .kanban-cards{overflow-y:auto;display:flex;flex-direction:column;gap:8px;flex:1;}
  .kanban-card{background:#fff;border:1px solid var(--line);border-radius:10px;padding:11px 12px;box-shadow:var(--shadow-sm);cursor:pointer;}
  .kanban-card:hover{border-color:var(--brand-500);box-shadow:var(--shadow);}
  .kanban-card .kc-title{font-weight:700;font-size:12.5px;color:var(--ink-900);margin-bottom:3px;}
  .kanban-card .kc-sub{font-size:11px;color:var(--ink-500);margin-bottom:8px;}
  .kanban-card .kc-foot{display:flex;justify-content:space-between;align-items:center;font-size:11px;}
  .kanban-card .kc-amount{font-weight:800;color:var(--brand-700);font-family:'Roboto Mono',monospace;font-size:11.5px;}
  .kanban-empty{font-size:11px;color:var(--ink-400);text-align:center;padding:18px 6px;}

  /* ============================== FORMS ============================== */
  .form-grid{display:grid;grid-template-columns:1fr 1fr;gap:14px;}
  .form-grid.cols-3{grid-template-columns:1fr 1fr 1fr;}
  .form-group{display:flex;flex-direction:column;gap:5px;}
  .form-group.full{grid-column:1/-1;}
  label{font-size:11.5px;color:var(--ink-600);font-weight:700;letter-spacing:.1px;}
  label.required::after{content:" *";color:var(--red-500);}
  input,select,textarea{padding:8px 11px;border:1px solid var(--line);border-radius:8px;font-size:12.8px;font-family:inherit;background:#fff;color:var(--ink-900);}
  input:focus,select:focus,textarea:focus{outline:none;border-color:var(--brand-500);box-shadow:0 0 0 3px var(--brand-100);}
  input:disabled{background:var(--canvas);color:var(--ink-400);}
  textarea{resize:vertical;min-height:60px;}

  .product-line{border:1px solid var(--line);border-radius:var(--radius);padding:16px;margin-bottom:12px;position:relative;background:#FBFCFE;}
  .product-line .remove-line{position:absolute;top:12px;right:12px;background:none;border:none;color:var(--red-500);cursor:pointer;font-size:16px;font-weight:700;}
  .line-index{font-size:10.5px;font-weight:800;color:var(--brand-700);text-transform:uppercase;letter-spacing:.6px;margin-bottom:10px;}

  .tabs{display:flex;gap:2px;margin-bottom:18px;border-bottom:1px solid var(--line);flex-wrap:wrap;}
  .tab{padding:9px 14px;cursor:pointer;font-size:12.5px;color:var(--ink-500);border-bottom:2px solid transparent;font-weight:700;display:flex;align-items:center;gap:6px;}
  .tab:hover{color:var(--ink-900);}
  .tab.active{color:var(--brand-700);border-bottom:2px solid var(--brand-600);}
  .tab .tab-count{font-size:10px;background:var(--ink-100);color:var(--ink-500);padding:1px 6px;border-radius:20px;font-weight:700;}
  .tab.active .tab-count{background:var(--brand-100);color:var(--brand-700);}

  /* ============================== MODALS ============================== */
  .modal-overlay{position:fixed;inset:0;background:rgba(10,16,30,0.52);display:none;align-items:flex-start;justify-content:center;padding:44px 20px;overflow-y:auto;z-index:70;backdrop-filter:blur(1px);}
  .modal-overlay.open{display:flex;}
  .modal{background:#fff;border-radius:14px;width:100%;max-width:760px;padding:24px 26px;box-shadow:var(--shadow-lg);}
  .modal.wide{max-width:960px;}
  .modal.xwide{max-width:1120px;}
  .modal-head{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:16px;}
  .modal h2{margin:0;font-size:16px;font-weight:800;letter-spacing:-.01em;}
  .modal-close{background:none;border:none;font-size:18px;color:var(--ink-400);cursor:pointer;padding:2px 6px;border-radius:6px;}
  .modal-close:hover{background:var(--canvas);color:var(--ink-900);}
  .modal-footer{display:flex;justify-content:flex-end;gap:10px;margin-top:20px;padding-top:16px;border-top:1px solid var(--line);}

  /* ============================== RECORD WORKSPACE ============================== */
  .record-shell{display:grid;grid-template-columns:300px 1fr;gap:16px;align-items:start;}
  .record-side .card{padding:18px;}
  .record-avatar{width:52px;height:52px;border-radius:12px;background:var(--brand-100);color:var(--brand-700);display:flex;align-items:center;justify-content:center;font-weight:800;font-size:17px;flex-shrink:0;margin-bottom:10px;}
  .record-title{font-size:16.5px;font-weight:800;letter-spacing:-.01em;}
  .record-sub{font-size:12px;color:var(--ink-500);margin-top:2px;margin-bottom:14px;}
  .kv-list{display:flex;flex-direction:column;gap:11px;}
  .kv-list .kv-item .kv-label{font-size:10.5px;text-transform:uppercase;letter-spacing:.4px;color:var(--ink-400);font-weight:700;}
  .kv-list .kv-item .kv-value{font-size:13px;color:var(--ink-900);font-weight:600;margin-top:2px;}
  .kv-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px 20px;margin-bottom:6px;}
  .kv-item .kv-label{font-size:10.5px;text-transform:uppercase;letter-spacing:.4px;color:var(--ink-400);font-weight:700;}
  .kv-item .kv-value{font-size:13px;color:var(--ink-900);font-weight:600;margin-top:2px;}
  .related-list-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:2px;}

  .timeline-item{display:flex;gap:10px;padding:11px 0;border-bottom:1px solid var(--line-soft);}
  .timeline-item:last-child{border-bottom:none;}
  .timeline-ic{width:28px;height:28px;border-radius:8px;background:var(--brand-50);color:var(--brand-700);display:flex;align-items:center;justify-content:center;flex-shrink:0;}
  .timeline-ic.call{background:var(--blue-100);color:var(--blue-600);}
  .timeline-ic.meeting{background:var(--violet-100);color:var(--violet-600);}
  .timeline-ic.stage_change{background:var(--amber-100);color:var(--amber-600);}
  .timeline-body .tl-title{font-size:12.5px;font-weight:700;color:var(--ink-900);}
  .timeline-body .tl-text{font-size:12px;color:var(--ink-600);margin-top:2px;}
  .timeline-body .tl-time{font-size:10.5px;color:var(--ink-400);margin-top:3px;font-weight:600;}
  .composer{display:flex;gap:8px;margin-top:14px;padding-top:14px;border-top:1px solid var(--line);}
  .composer textarea{flex:1;min-height:44px;}

  .empty-state{text-align:center;padding:52px 20px;color:var(--ink-500);font-size:12.5px;}
  .empty-state .es-icon{width:40px;height:40px;margin:0 auto 12px;color:var(--ink-300);}
  .empty-state .es-title{font-weight:700;color:var(--ink-700);font-size:13px;margin-bottom:3px;}

  .toast{position:fixed;bottom:24px;right:24px;background:var(--ink-900);color:#fff;padding:12px 18px;border-radius:9px;font-size:12.5px;font-weight:600;display:none;z-index:100;box-shadow:0 12px 30px rgba(0,0,0,.3);}

  .field-chip{display:inline-flex;align-items:center;gap:6px;background:var(--canvas);border:1px solid var(--line);border-radius:20px;padding:5px 12px;font-size:11.5px;font-weight:700;margin:0 6px 6px 0;color:var(--ink-700);}
  .field-chip .type-tag{color:var(--ink-400);font-weight:500;}
  .field-chip button{background:none;border:none;color:var(--red-500);cursor:pointer;font-size:13px;padding:0;}

  .report-builder-grid{display:grid;grid-template-columns:280px 1fr;gap:16px;}
  .field-picker-list{display:flex;flex-direction:column;gap:2px;max-height:360px;overflow-y:auto;}
  .field-picker-item{display:flex;align-items:center;gap:8px;padding:7px 8px;border-radius:7px;font-size:12.3px;cursor:pointer;font-weight:600;}
  .field-picker-item:hover{background:var(--canvas);}

  .scope-note{font-size:11.5px;color:var(--brand-700);background:var(--brand-50);border:1px solid var(--brand-100);border-radius:8px;padding:9px 12px;margin-bottom:16px;display:flex;align-items:center;gap:8px;font-weight:600;}

  .checklist-row{display:flex;align-items:center;gap:10px;padding:9px 0;border-bottom:1px solid var(--line-soft);}
  .checklist-row:last-child{border-bottom:none;}
  .checklist-row input[type=checkbox]{width:16px;height:16px;accent-color:var(--brand-600);}
  .checklist-row.done .cl-title{text-decoration:line-through;color:var(--ink-400);}
  .cl-title{font-size:12.5px;font-weight:700;flex:1;}
  .cl-meta{font-size:11px;color:var(--ink-500);}
</style>
</head>
<body>

<!-- ============================== AUTH SCREEN ============================== -->
<div id="authScreen" style="min-height:100vh;display:flex;align-items:center;justify-content:center;background:radial-gradient(circle at 15% 10%, #123c34 0%, #0A1120 55%);font-family:'Inter',Arial,sans-serif;">
  <div style="width:100%;max-width:960px;display:flex;border-radius:18px;overflow:hidden;box-shadow:0 30px 80px rgba(0,0,0,.4);">
    <div style="flex:1;background:linear-gradient(160deg,#0F6154,#0A1120 120%);padding:46px 42px;color:#fff;display:flex;flex-direction:column;justify-content:space-between;min-height:520px;">
      <div style="display:flex;align-items:center;gap:10px;">
        <div style="width:32px;height:32px;border-radius:9px;background:linear-gradient(140deg,#15A38C,#0A3B33);display:flex;align-items:center;justify-content:center;font-weight:800;font-size:14px;">C</div>
        <div style="font-weight:700;font-size:17px;letter-spacing:-.01em;">Crius CRM</div>
      </div>
      <div>
        <div style="font-size:26px;font-weight:800;line-height:1.25;letter-spacing:-.02em;max-width:340px;">Run global sales &amp; sourcing from one desk.</div>
        <div style="font-size:13px;color:#A9C4BE;margin-top:12px;max-width:340px;line-height:1.6;">Leads, deals, quotes, tasks, and pipeline analytics — one workspace across every internal company and territory.</div>
      </div>
      <div style="display:flex;gap:22px;font-size:11.5px;color:#8FB3AA;font-weight:600;flex-wrap:wrap;">
        <div>Multi-company</div><div>Role-based access</div><div>Blueprint-style pipeline</div><div>Pipeline analytics</div>
      </div>
    </div>
    <div style="flex:1;background:#fff;padding:42px 40px;min-width:380px;">
      <div class="tabs" style="margin-bottom:20px;">
        <div class="tab active" id="loginTab" onclick="switchAuthTab('login')">Log In</div>
        <div class="tab" id="signupTab" onclick="switchAuthTab('signup')">Sign Up</div>
      </div>

      <button class="btn secondary" style="width:100%;justify-content:center;gap:10px;margin-bottom:10px;" onclick="authWithGoogle()">
        <svg width="16" height="16" viewBox="0 0 48 48"><path fill="#FFC107" d="M43.6 20.5H42V20H24v8h11.3C33.8 32.7 29.3 36 24 36c-6.6 0-12-5.4-12-12s5.4-12 12-12c3.1 0 5.9 1.2 8 3.1l5.7-5.7C34.5 6.1 29.5 4 24 4 12.9 4 4 12.9 4 24s8.9 20 20 20 20-8.9 20-20c0-1.3-.1-2.7-.4-3.5z"/><path fill="#FF3D00" d="M6.3 14.7l6.6 4.8C14.6 15.4 18.9 12 24 12c3.1 0 5.9 1.2 8 3.1l5.7-5.7C34.5 6.1 29.5 4 24 4 16.3 4 9.6 8.3 6.3 14.7z"/><path fill="#4CAF50" d="M24 44c5.3 0 10.1-2 13.7-5.4l-6.3-5.3C29.4 34.9 26.8 36 24 36c-5.3 0-9.7-3.4-11.3-8.1l-6.6 5.1C9.5 39.6 16.2 44 24 44z"/><path fill="#1976D2" d="M43.6 20.5H42V20H24v8h11.3c-.8 2.2-2.2 4.1-4 5.4l6.3 5.3C41.4 35.4 44 30.1 44 24c0-1.3-.1-2.7-.4-3.5z"/></svg>
        Continue with Google
      </button>
      <div style="display:flex;align-items:center;gap:10px;margin:16px 0;color:var(--ink-300);font-size:11px;font-weight:700;">
        <div style="flex:1;height:1px;background:var(--line);"></div> OR <div style="flex:1;height:1px;background:var(--line);"></div>
      </div>

      <div id="signupFieldsGroup" style="display:none;">
        <div class="form-grid" style="margin-bottom:12px;">
          <div class="form-group"><label class="required">Full Name</label><input id="auth_name"></div>
          <div class="form-group"><label>Phone</label><input id="auth_phone"></div>
          <div class="form-group full"><label>Designation</label><input id="auth_designation" placeholder="e.g. Sales Executive"></div>
        </div>
      </div>
      <div style="margin-bottom:12px;"><label>Email</label><input id="auth_email" type="email" style="width:100%;margin-top:5px;"></div>
      <div style="margin-bottom:18px;"><label>Password</label><input id="auth_password" type="password" style="width:100%;margin-top:5px;"></div>
      <button class="btn" style="width:100%;justify-content:center;" id="authSubmitBtn" onclick="submitAuth()">Log In</button>
      <div id="authError" style="color:var(--red-500);font-size:12px;margin-top:10px;font-weight:600;"></div>
      <p style="font-size:11px;color:var(--ink-500);margin-top:16px;text-align:center;line-height:1.5;">
        New accounts start as <strong>User</strong> role — an Admin upgrades access afterward in Users &amp; Roles.
      </p>
    </div>
  </div>
</div>

<!-- ============================== APP SHELL ============================== -->
<div id="app" style="display:none;">

  <div id="sidebar">
    <div class="brand">
      <div class="brand-mark">C</div>
      <div class="brand-text"><div class="brand-name">Crius CRM</div><div class="brand-sub">Sales Platform</div></div>
    </div>

    <div class="nav-scroll">
      <div class="nav-group-label">Overview</div>
      <div class="nav-item active" data-page="dashboard"></div>
      <div class="nav-item" data-page="activities"></div>

      <div class="nav-group-label">Sales</div>
      <div class="nav-item" data-page="leads"></div>
      <div class="nav-item" data-page="contacts"></div>
      <div class="nav-item" data-page="companies"></div>
      <div class="nav-item" data-page="enquiries"></div>
      <div class="nav-item" data-page="quotes"></div>

      <div class="nav-group-label">Operations</div>
      <div class="nav-item" data-page="mail"></div>
      <div class="nav-item" data-page="sfmaster"></div>
      <div class="nav-item" data-page="projects"></div>
      <div class="nav-item" data-page="reports"></div>

      <div class="nav-group-label admin-only" id="setupLabel">Setup — Admin</div>
      <div class="nav-item admin-only" data-page="masters"></div>
      <div class="nav-item admin-only" data-page="fields"></div>
      <div class="nav-item admin-only" data-page="users"></div>
      <div class="nav-item admin-only" data-page="settings"></div>
    </div>

    <div class="sidebar-foot">
      <button class="collapse-btn" id="collapseBtn"><svg class="icon" viewBox="0 0 24 24"><path d="M9 4v16M4 4h16v16H4z"/></svg><span>Collapse</span></button>
    </div>
  </div>

  <div id="shell">
    <div id="topbar">
      <div class="topbar-left">
        <div class="search-box">
          <svg class="icon" viewBox="0 0 24 24"><circle cx="11" cy="11" r="7"/><path d="M21 21l-4.3-4.3"/></svg>
          <input id="globalSearch" placeholder="Search leads, deals, companies, contacts…" autocomplete="off">
          <div class="search-results" id="searchResultsBox"></div>
        </div>
      </div>
      <div class="topbar-right">
        <div class="quickcreate">
          <button class="btn small" id="qcBtn"><svg class="icon" viewBox="0 0 24 24" style="width:14px;height:14px;"><path d="M12 5v14M5 12h14"/></svg>Create</button>
          <div class="qc-menu" id="qcMenu">
            <div class="qc-item" data-qc="companies"><svg class="icon" viewBox="0 0 24 24"><path d="M3 21h18M6 21V7l6-4 6 4v14M9 21v-6h6v6"/></svg>Account</div>
            <div class="qc-item" data-qc="contacts"><svg class="icon" viewBox="0 0 24 24"><circle cx="12" cy="8" r="3.5"/><path d="M5 20c1-4 4-6 7-6s6 2 7 6"/></svg>Contact</div>
            <div class="qc-item" data-qc="leads"><svg class="icon" viewBox="0 0 24 24"><path d="M3 5h18M3 5l7 8v6l4-2v-4l7-8"/></svg>Lead</div>
            <div class="qc-item" data-qc="enquiries"><svg class="icon" viewBox="0 0 24 24"><path d="M6 3h9l5 5v13H6z"/><path d="M14 3v5h5"/></svg>Deal</div>
            <div class="qc-item" data-qc="tasks"><svg class="icon" viewBox="0 0 24 24"><path d="M9 11l3 3L22 4M21 12v7a2 2 0 01-2 2H5a2 2 0 01-2-2V5a2 2 0 012-2h11"/></svg>Task</div>
          </div>
        </div>
        <button class="icon-btn" title="Notifications" id="notifBtn"><svg class="icon" viewBox="0 0 24 24"><path d="M6 8a6 6 0 0112 0c0 5 2 6 2 6H4s2-1 2-6z"/><path d="M10 20a2 2 0 004 0"/></svg><span class="dot-badge" id="notifDot" style="display:none;"></span></button>
        <span class="role-pill" id="currentRoleBadge">–</span>
        <div class="user-chip" onclick="signOut()" title="Sign out">
          <div class="avatar" id="userAvatar">–</div>
          <div>
            <div style="font-weight:700;font-size:12.5px;" id="userNameLabel">–</div>
            <div style="font-size:10.5px;color:var(--ink-500)" id="userEmailLabel">–</div>
          </div>
        </div>
      </div>
    </div>
    <div id="main"></div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2/dist/umd/supabase.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chart.js@4/dist/chart.umd.min.js"></script>
<script>
// ============================================================================
// 1. CONNECT TO YOUR SUPABASE PROJECT
// ============================================================================
const SUPABASE_URL = "https://ozhyjniulqxtcinrlqym.supabase.co";
const SUPABASE_ANON_KEY = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im96aHlqbml1bHF4dGNpbnJscXltIiwicm9sZSI6ImFub24iLCJpYXQiOjE3ODUyMzUxMzcsImV4cCI6MjEwMDgxMTEzN30.sMW_H-nleTVKQdTev2XYD2F8jQwmVMpmEAYB4g4Wols";
const supa = window.supabase.createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
// ============================================================================
// NOTE ON NEW TABLES: this rebuild adds richer functionality (Tasks/Calls/
// Meetings, Notes, per-record tags, deal probability, saved views). Run
// migration_v3_zoho_style.sql against the same Supabase project so the
// `tasks`, `notes` and `saved_views` tables and the new columns exist —
// every call below degrades to an empty state/toast if a table is missing,
// it won't crash the app.
// ============================================================================

const PIPELINE_STAGES = ["Quotation","Negotiation","P.O. Raised","Order Lost"];
const STAGE_COLOR = { "Quotation":"var(--amber-500)", "Negotiation":"var(--blue-500)", "P.O. Raised":"var(--brand-500)", "Order Lost":"var(--red-500)" };
const STAGE_PROBABILITY = { "Quotation":20, "Negotiation":50, "P.O. Raised":90, "Order Lost":0 };

// Role scope definitions — mirrors the RLS policies in the SQL schema.
const ROLE_SCOPE = {
  user:          { label:'My records only',                     canSeeSetup:false },
  manager:       { label:"My team's records (direct reports)",   canSeeSetup:false },
  super_manager: { label:"All teams under me (multi-level)",     canSeeSetup:false },
  admin:         { label:'Everything, plus Masters & Setup',     canSeeSetup:true  }
};
// currentRole is never chosen by the user — it is read from their app_users
// row after login. Visibility ultimately comes from Supabase RLS
// (fn_visible_user_ids), not this client-side value — it only drives nav.
let currentRole = null;
let currentUser = null;

// ---------------------------------------------------------------- ICON SET
const ICONS = {
  dashboard:'<rect x="3" y="3" width="7" height="9" rx="1.5"/><rect x="14" y="3" width="7" height="5" rx="1.5"/><rect x="14" y="12" width="7" height="9" rx="1.5"/><rect x="3" y="16" width="7" height="5" rx="1.5"/>',
  building:'<path d="M3 21h18M6 21V7l6-4 6 4v14M9 21v-6h6v6"/>',
  contacts:'<circle cx="12" cy="8" r="3.5"/><path d="M5 20c1-4 4-6 7-6s6 2 7 6"/>',
  leads:'<path d="M3 5h18M3 5l7 8v6l4-2v-4l7-8"/>',
  enquiries:'<path d="M6 3h9l5 5v13H6z"/><path d="M14 3v5h5"/><path d="M9 13h6M9 17h6"/>',
  mail:'<rect x="3" y="5" width="18" height="14" rx="2"/><path d="M3 7l9 6 9-6"/>',
  quotes:'<path d="M6 3h9l5 5v13H6z"/><path d="M14 3v5h5"/><path d="M9 12h6M9 16h4"/>',
  projects:'<rect x="3" y="4" width="18" height="16" rx="2"/><path d="M3 9h18M8 4v5"/>',
  reports:'<path d="M4 20V10M11 20V4M18 20v-7"/>',
  flask:'<path d="M9 3h6M10 3v6l-5.5 9a1.5 1.5 0 001.3 2.3h12.4a1.5 1.5 0 001.3-2.3L14 9V3"/><path d="M7.5 15h9"/>',
  masters:'<circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.7 1.7 0 00.3 1.9l.1.1a2 2 0 11-2.8 2.8l-.1-.1a1.7 1.7 0 00-1.9-.3 1.7 1.7 0 00-1 1.6V21a2 2 0 11-4 0v-.2a1.7 1.7 0 00-1-1.6 1.7 1.7 0 00-1.9.3l-.1.1a2 2 0 11-2.8-2.8l.1-.1a1.7 1.7 0 00.3-1.9 1.7 1.7 0 00-1.6-1H3a2 2 0 110-4h.2a1.7 1.7 0 001.6-1 1.7 1.7 0 00-.3-1.9l-.1-.1a2 2 0 112.8-2.8l.1.1a1.7 1.7 0 001.9.3H9a1.7 1.7 0 001-1.6V3a2 2 0 114 0v.2a1.7 1.7 0 001 1.6 1.7 1.7 0 001.9-.3l.1-.1a2 2 0 112.8 2.8l-.1.1a1.7 1.7 0 00-.3 1.9V9a1.7 1.7 0 001.6 1H21a2 2 0 110 4h-.2a1.7 1.7 0 00-1.6 1z"/>',
  fields:'<rect x="3" y="3" width="7" height="7" rx="1.5"/><rect x="14" y="3" width="7" height="7" rx="1.5"/><rect x="3" y="14" width="7" height="7" rx="1.5"/><rect x="14" y="14" width="7" height="7" rx="1.5"/>',
  users:'<circle cx="9" cy="8" r="3.5"/><path d="M2.5 20c.8-3.6 3.2-5.6 6.5-5.6s5.7 2 6.5 5.6"/><circle cx="17.5" cy="9" r="2.8"/><path d="M15.5 14.6c2.6.2 4.4 2 5 5.4"/>',
  settings:'<circle cx="12" cy="12" r="3.2"/><path d="M4 12h2M18 12h2M12 4v2M12 18v2M6.3 6.3l1.4 1.4M16.3 16.3l1.4 1.4M6.3 17.7l1.4-1.4M16.3 7.7l1.4-1.4"/>',
  plus:'<path d="M12 5v14M5 12h14"/>',
  search:'<circle cx="11" cy="11" r="7"/><path d="M21 21l-4.3-4.3"/>',
  bell:'<path d="M6 8a6 6 0 0112 0c0 5 2 6 2 6H4s2-1 2-6z"/><path d="M10 20a2 2 0 004 0"/>',
  list:'<path d="M8 6h13M8 12h13M8 18h13M3 6h.01M3 12h.01M3 18h.01"/>',
  kanban:'<rect x="3" y="4" width="6" height="16" rx="1.5"/><rect x="10.5" y="4" width="6" height="10" rx="1.5"/><rect x="18" y="4" width="3" height="7" rx="1.5"/>',
  phone:'<path d="M4 4h4l2 5-2.5 1.5a11 11 0 006 6L15 14l5 2v4a2 2 0 01-2.2 2A17 17 0 013 6.2 2 2 0 015 4z"/>',
  note:'<path d="M4 4h16v13H8l-4 4z"/>',
  x:'<path d="M18 6L6 18M6 6l12 12"/>',
  chevronDown:'<path d="M6 9l6 6 6-6"/>',
  file:'<path d="M6 3h9l5 5v13H6z"/><path d="M14 3v5h5"/>',
  flag:'<path d="M5 3v18M5 4h13l-3 4 3 4H5"/>',
  arrowUp:'<path d="M12 19V5M6 11l6-6 6 6"/>',
  tasks:'<path d="M9 11l3 3L22 4M21 12v7a2 2 0 01-2 2H5a2 2 0 01-2-2V5a2 2 0 012-2h11"/>',
  meeting:'<rect x="3" y="4" width="18" height="17" rx="2"/><path d="M3 9h18M8 2v4M16 2v4"/>',
  spark:'<path d="M12 3v4M12 17v4M3 12h4M17 12h4M6 6l2.5 2.5M15.5 15.5L18 18M18 6l-2.5 2.5M8.5 15.5L6 18"/>',
  zap:'<path d="M13 2L3 14h8l-1 8 10-12h-8l1-8z"/>'
};
function icon(name, cls){ return `<svg class="icon ${cls||''}" viewBox="0 0 24 24">${ICONS[name]||''}</svg>`; }

const NAV_META = {
  dashboard:{label:'Home',icon:'dashboard'}, activities:{label:'Activities',icon:'tasks'},
  leads:{label:'Leads',icon:'leads'}, contacts:{label:'Contacts',icon:'contacts'},
  companies:{label:'Accounts',icon:'building'}, enquiries:{label:'Deals',icon:'enquiries'},
  quotes:{label:'Quotes',icon:'quotes'}, mail:{label:'Mail',icon:'mail'},
  sfmaster:{label:'Products',icon:'flask'}, projects:{label:'Projects',icon:'projects'},
  reports:{label:'Analytics',icon:'reports'},
  masters:{label:'Masters',icon:'masters'}, fields:{label:'Custom Fields',icon:'fields'},
  users:{label:'Users & Roles',icon:'users'}, settings:{label:'Mail Integration',icon:'settings'}
};
document.querySelectorAll('.nav-item[data-page]').forEach(item=>{
  const m = NAV_META[item.dataset.page];
  item.innerHTML = `<div class="nav-item-l">${icon(m.icon)}<span class="lbl">${m.label}</span></div><span class="nav-count" data-count="${item.dataset.page}"></span>`;
});

function toast(msg){
  const t = document.getElementById('toast');
  t.textContent = msg; t.style.display='block';
  setTimeout(()=> t.style.display='none', 2600);
}
function pillClass(stage){ return 'stage-' + (stage||'').replace(/[.\s]/g,''); }
function el(html){ const d=document.createElement('div'); d.innerHTML=html.trim(); return d.firstChild; }
function initials(name){ return (name||'?').split(' ').filter(Boolean).map(n=>n[0]).join('').slice(0,2).toUpperCase(); }
function timeAgo(iso){
  if(!iso) return '';
  const s = Math.floor((Date.now()-new Date(iso).getTime())/1000);
  if(s<60) return 'just now';
  if(s<3600) return Math.floor(s/60)+'m ago';
  if(s<86400) return Math.floor(s/3600)+'h ago';
  return Math.floor(s/86400)+'d ago';
}
function money(n){ return n==null ? '–' : Number(n).toLocaleString(undefined,{maximumFractionDigits:2}); }
function esc(s){ return (s==null?'':String(s)).replace(/[&<>"']/g, m=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[m])); }
function tagsHtml(tags){ return (tags||[]).map(t=>`<span class="tag">${esc(t)}</span>`).join(''); }

const pages = {
  dashboard: renderDashboard, activities: renderActivitiesModule, companies: renderCompanies, contacts: renderContacts, leads: renderLeads,
  enquiries: renderEnquiries, mail: renderMail, quotes: renderQuotes,
  projects: renderProjects, reports: renderReports, sfmaster: renderSFMaster,
  masters: renderMasters, fields: renderCustomFields, users: renderUsers, settings: renderSettings
};

document.querySelectorAll('.nav-item[data-page]').forEach(item=>{
  item.addEventListener('click', ()=>{
    document.querySelectorAll('.nav-item').forEach(i=>i.classList.remove('active'));
    item.classList.add('active');
    pages[item.dataset.page]();
  });
});
document.getElementById('collapseBtn').onclick = ()=>{
  const sb = document.getElementById('sidebar');
  sb.classList.toggle('collapsed');
  document.getElementById('collapseBtn').querySelector('span').textContent = sb.classList.contains('collapsed') ? '' : 'Collapse';
};

// Quick create menu
document.getElementById('qcBtn').onclick = (e)=>{ e.stopPropagation(); document.getElementById('qcMenu').classList.toggle('open'); };
document.addEventListener('click', ()=>{ document.getElementById('qcMenu').classList.remove('open'); document.getElementById('searchResultsBox').classList.remove('open'); });
document.querySelectorAll('.qc-item').forEach(qi=>{
  qi.onclick = (e)=>{
    e.stopPropagation();
    const page = qi.dataset.qc;
    if(page === 'tasks'){ openTaskComposer(); return; }
    document.querySelectorAll('.nav-item').forEach(i=>i.classList.remove('active'));
    document.querySelector(`[data-page="${page}"]`)?.classList.add('active');
    pages[page]().then(()=>{
      const openers = { companies:'newCompanyBtn', contacts:'newContactBtn', leads:'newLeadBtn', enquiries:'newEnquiryBtn' };
      document.getElementById(openers[page])?.click();
    });
  };
});

// Global search — quick lookup across companies / leads / enquiries / contacts
let searchDebounce;
document.getElementById('globalSearch').addEventListener('input',(e)=>{
  clearTimeout(searchDebounce);
  const q = e.target.value.trim();
  const box = document.getElementById('searchResultsBox');
  if(!q){ box.classList.remove('open'); return; }
  searchDebounce = setTimeout(()=> runGlobalSearch(q), 300);
});
document.getElementById('globalSearch').addEventListener('click', e=> e.stopPropagation());
async function runGlobalSearch(q){
  const box = document.getElementById('searchResultsBox');
  const [companies, leadsRes, enquiriesRes, contactsRes] = await Promise.all([
    supa.from('company_master').select('id,company_name').ilike('company_name', `%${q}%`).limit(4),
    supa.from('leads').select('id,lead_no,company_id').ilike('lead_no', `%${q}%`).limit(4),
    supa.from('enquiries').select('id,enquiry_no,company_id').ilike('enquiry_no', `%${q}%`).limit(4),
    supa.from('contact_master').select('id,contact_name,company_id').ilike('contact_name', `%${q}%`).limit(4)
  ]);
  const groups = [
    { label:'Accounts', rows:companies.data||[], render:r=>r.company_name, open:r=>openDetailPanel('company', r.id) },
    { label:'Leads', rows:leadsRes.data||[], render:r=>r.lead_no+' · '+r.company_id, open:r=>openDetailPanel('lead', r.id) },
    { label:'Deals', rows:enquiriesRes.data||[], render:r=>r.enquiry_no+' · '+r.company_id, open:r=>openDetailPanel('enquiry', r.id) },
    { label:'Contacts', rows:contactsRes.data||[], render:r=>r.contact_name, open:r=>toast('Open contact '+r.contact_name) }
  ];
  const nonEmpty = groups.filter(g=>g.rows.length);
  if(!nonEmpty.length){ box.innerHTML = `<div class="sr-empty">No matches for "${esc(q)}"</div>`; box.classList.add('open'); return; }
  box.innerHTML = nonEmpty.map(g=>`
    <div class="sr-group-label">${g.label}</div>
    ${g.rows.map((r,i)=>`<div class="sr-item" data-g="${nonEmpty.indexOf(g)}" data-i="${i}">${esc(g.render(r))}</div>`).join('')}
  `).join('');
  box.classList.add('open');
  box.querySelectorAll('.sr-item').forEach(item=>{
    item.onclick = ()=>{
      const g = nonEmpty[+item.dataset.g]; const r = g.rows[+item.dataset.i];
      box.classList.remove('open'); g.open(r);
    };
  });
}

// --------------------------------------------------------------
// AUTH — login/signup gate. Role is looked up from app_users by the
// authenticated user's id/email — never set manually in the UI.
// --------------------------------------------------------------
let authMode = 'login';
function switchAuthTab(mode){
  authMode = mode;
  document.getElementById('loginTab').classList.toggle('active', mode==='login');
  document.getElementById('signupTab').classList.toggle('active', mode==='signup');
  document.getElementById('signupFieldsGroup').style.display = mode==='signup' ? 'block' : 'none';
  document.getElementById('authSubmitBtn').textContent = mode==='signup' ? 'Create Account' : 'Log In';
  document.getElementById('authError').textContent = '';
}

async function authWithGoogle(){
  const { error } = await supa.auth.signInWithOAuth({
    provider: 'google',
    options: { redirectTo: window.location.href }
  });
  if(error){ document.getElementById('authError').textContent = error.message; }
}

async function submitAuth(){
  const email = document.getElementById('auth_email').value.trim();
  const password = document.getElementById('auth_password').value;
  const errBox = document.getElementById('authError');
  errBox.textContent = '';
  if(!email || !password){ errBox.textContent = 'Email and password are required.'; return; }

  if(authMode === 'signup'){
    const fullName = document.getElementById('auth_name').value.trim();
    if(!fullName){ errBox.textContent = 'Full name is required.'; return; }
    const { data, error } = await supa.auth.signUp({ email, password });
    if(error){ errBox.textContent = error.message; return; }
    if(data.user){
      await supa.from('app_users').insert({
        id: data.user.id,
        full_name: fullName,
        email,
        role: 'user',
        phone: document.getElementById('auth_phone').value || null,
        designation: document.getElementById('auth_designation').value || null
      });
    }
    toast('Account created — check your email to confirm, then log in.');
    switchAuthTab('login');
    return;
  }

  const { data, error } = await supa.auth.signInWithPassword({ email, password });
  if(error){ errBox.textContent = error.message; return; }
  await loadCurrentUserAndEnter();
}

async function loadCurrentUserAndEnter(){
  const { data: sessionData } = await supa.auth.getUser();
  if(!sessionData?.user){ return; }
  let { data: profile, error } = await supa.from('app_users').select('*').eq('id', sessionData.user.id).single();

  if(error || !profile){
    const meta = sessionData.user.user_metadata || {};
    const insertPayload = {
      id: sessionData.user.id,
      full_name: meta.full_name || meta.name || sessionData.user.email.split('@')[0],
      email: sessionData.user.email,
      role: 'user'
    };
    const { data: created, error: createErr } = await supa.from('app_users').insert(insertPayload).select().single();
    if(!createErr) profile = created;
  }

  if(!profile){
    document.getElementById('authError').textContent = 'Signed in, but no app_users profile found for this account — ask an admin to add one.';
    return;
  }
  currentUser = profile;
  currentRole = profile.role;
  document.getElementById('authScreen').style.display = 'none';
  document.getElementById('app').style.display = 'flex';
  document.getElementById('currentRoleBadge').textContent = currentRole.replace('_',' ');
  document.getElementById('userNameLabel').textContent = profile.full_name;
  document.getElementById('userEmailLabel').textContent = profile.email;
  document.getElementById('userAvatar').textContent = initials(profile.full_name);
  applyRoleVisibility();
  renderDashboard();
  refreshNavCounts();
  refreshNotifDot();
}

supa.auth.onAuthStateChange((event, session)=>{
  if(session && (event === 'SIGNED_IN' || event === 'INITIAL_SESSION')){
    loadCurrentUserAndEnter();
  }
});

async function signOut(){
  if(!confirm('Sign out of Crius CRM?')) return;
  await supa.auth.signOut();
  currentUser = null; currentRole = null;
  document.getElementById('app').style.display = 'none';
  document.getElementById('authScreen').style.display = 'flex';
  document.getElementById('auth_password').value = '';
}

function applyRoleVisibility(){
  const canSeeSetup = ROLE_SCOPE[currentRole]?.canSeeSetup;
  document.querySelectorAll('.admin-only').forEach(n=> n.style.display = canSeeSetup ? '' : 'none');
}

// Small nav-count badges (e.g. open deals, my open tasks) — best-effort,
// silently skipped if a table/column isn't there yet.
async function refreshNavCounts(){
  try{
    const { count: leadCount } = await supa.from('leads').select('*',{count:'exact',head:true}).eq('closure_status','open');
    document.querySelector('[data-count="leads"]').textContent = leadCount ?? '';
  }catch(e){}
  try{
    const { count: dealCount } = await supa.from('enquiries').select('*',{count:'exact',head:true}).neq('pipeline_stage_id','Order Lost');
    document.querySelector('[data-count="enquiries"]').textContent = dealCount ?? '';
  }catch(e){}
  try{
    const { count: taskCount } = await supa.from('tasks').select('*',{count:'exact',head:true}).eq('status','open').eq('owner_id', currentUser?.id);
    document.querySelector('[data-count="activities"]').textContent = taskCount ?? '';
  }catch(e){}
}
async function refreshNotifDot(){
  try{
    const { count } = await supa.from('tasks').select('*',{count:'exact',head:true}).eq('status','open').eq('owner_id', currentUser?.id).lte('due_date', new Date().toISOString().slice(0,10));
    document.getElementById('notifDot').style.display = (count||0) > 0 ? 'block' : 'none';
  }catch(e){}
}

function pageHeader(main, title, sub, actionsHtml, crumbs){
  main.innerHTML = `
    <div class="breadcrumb">${(crumbs||['Workspace',title]).map((c,i,a)=> i<a.length-1 ? `<span>${c}</span><span class="sep">/</span>` : `<span style="color:var(--ink-600)">${c}</span>`).join('')}</div>
    <div class="page-header">
      <div><h1>${title}</h1><div class="page-sub">${sub||''}</div></div>
      <div class="header-actions">${actionsHtml||''}</div>
    </div>`;
}

// Shared saved-view tabs (Zoho's "All / My / Recent" pattern). onChange
// receives the selected view's filter function.
function savedViewTabs(containerId, views, onChange){
  const box = document.getElementById(containerId);
  box.innerHTML = views.map((v,i)=>`<div class="view-tab ${i===0?'active':''}" data-i="${i}">${v.label}</div>`).join('');
  box.querySelectorAll('.view-tab').forEach(t=>{
    t.onclick = ()=>{ box.querySelectorAll('.view-tab').forEach(x=>x.classList.remove('active')); t.classList.add('active'); onChange(views[+t.dataset.i]); };
  });
}

// Generic client-side row filter/sort/search helper used by list pages.
function applyListControls(rows, {search, searchFields, sortField, sortDir}){
  let out = rows;
  if(search){
    const q = search.toLowerCase();
    out = out.filter(r => searchFields.some(f => (r[f]||'').toString().toLowerCase().includes(q)));
  }
  if(sortField){
    out = [...out].sort((a,b)=>{
      const av = a[sortField], bv = b[sortField];
      if(av==null) return 1; if(bv==null) return -1;
      if(av<bv) return sortDir==='asc' ? -1 : 1;
      if(av>bv) return sortDir==='asc' ? 1 : -1;
      return 0;
    });
  }
  return out;
}

// ============================================================================
// DASHBOARD — role-aware, customizable widgets + pipeline chart + insights
// ============================================================================
const ALL_WIDGETS = [
  { key:'open_leads',   label:'Open Leads',              table:'leads',     filter:{closure_status:'open'}, icon:'leads', accent:'var(--blue-500)', accentSoft:'var(--blue-100)' },
  { key:'open_enquiry', label:'Open Deals',              table:'enquiries', filter:{}, icon:'enquiries', accent:'var(--brand-500)', accentSoft:'var(--brand-100)' },
  { key:'po_raised',    label:'P.O. Raised (this month)',table:'enquiries', filter:{pipeline_stage_id:'P.O. Raised'}, icon:'flag', accent:'var(--brand-700)', accentSoft:'var(--brand-100)' },
  { key:'order_lost',   label:'Orders Lost (this month)',table:'enquiries', filter:{pipeline_stage_id:'Order Lost'}, icon:'x', accent:'var(--red-500)', accentSoft:'var(--red-100)' },
  { key:'unassigned',   label:'Unassigned Mail',         table:'email_threads', filter:{is_assigned:false}, icon:'mail', accent:'var(--amber-500)', accentSoft:'var(--amber-100)' },
  { key:'my_tasks',     label:'My Open Tasks',           table:'tasks', filter:{status:'open'}, icon:'tasks', accent:'var(--violet-500)', accentSoft:'var(--violet-100)' },
  { key:'team_size',    label:'Team Members',            table:'app_users', filter:{}, icon:'users', accent:'var(--ink-700)', accentSoft:'#EEF1F6' }
];
let activeWidgets = JSON.parse(localStorage.getItem('crm_widgets') || 'null') || ['open_leads','open_enquiry','po_raised','my_tasks'];
let pipelineChart = null;
let sourceChart = null;

async function renderDashboard(){
  applyRoleVisibility();
  const main = document.getElementById('main');
  pageHeader(main, `Good to see you, ${currentUser?.full_name?.split(' ')[0] || ''}`, `Scope: ${ROLE_SCOPE[currentRole].label}`,
    `<button class="btn secondary small" id="customizeBtn">${icon('fields')}Customize widgets</button>`, ['Workspace','Home']);
  main.insertAdjacentHTML('beforeend', `
    <div class="insight-strip" id="insightStrip"></div>
    <div class="kpi-grid" id="kpiGrid"></div>
    <div class="grid-2">
      <div class="card">
        <div class="card-title">Pipeline by stage <span class="muted">Open deals, value-weighted</span></div>
        <div style="height:230px;"><canvas id="pipelineCanvas"></canvas></div>
      </div>
      <div class="card">
        <div class="card-title">Today &amp; overdue <span class="muted">My open tasks</span></div>
        <div id="myTasksToday"></div>
      </div>
    </div>
    <div class="grid-2">
      <div class="card">
        <div class="card-title">Leads by source</div>
        <div style="height:210px;"><canvas id="sourceCanvas"></canvas></div>
      </div>
      <div class="card">
        <div class="card-title">Recent activity</div>
        <div id="recentActivity"></div>
      </div>
    </div>
  `);
  renderKpiGrid();
  renderPipelineChart();
  renderSourceChart();
  renderRecentActivity();
  renderMyTasksToday();
  renderInsights();
  document.getElementById('customizeBtn').onclick = openWidgetPicker;
}

async function renderInsights(){
  const box = document.getElementById('insightStrip'); if(!box) return;
  const insights = [];
  try{
    const { data } = await supa.from('enquiries').select('pipeline_stage_id, enquiry_amount, created_at');
    const rows = data || [];
    const open = rows.filter(r=> r.pipeline_stage_id !== 'Order Lost');
    const weighted = open.reduce((s,r)=> s + (Number(r.enquiry_amount)||0) * ((STAGE_PROBABILITY[r.pipeline_stage_id]||20)/100), 0);
    insights.push({ icon:'zap', label:'Pipeline health', text:`<b>${open.length}</b> open deals, weighted at roughly <b>₹${money(weighted)}</b> based on stage probability.` });
    const lost = rows.filter(r=>r.pipeline_stage_id==='Order Lost').length;
    if(rows.length) insights.push({ icon:'flag', label:'Loss rate', text:`<b>${rows.length ? Math.round(lost/rows.length*100) : 0}%</b> of recorded deals were marked Order Lost — worth reviewing lost reasons in Deals.` });
  }catch(e){}
  try{
    const { count } = await supa.from('tasks').select('*',{count:'exact',head:true}).eq('status','open').eq('owner_id', currentUser?.id).lte('due_date', new Date().toISOString().slice(0,10));
    if(count) insights.push({ icon:'spark', label:'Follow-ups due', text:`You have <b>${count}</b> task(s) due today or overdue — clear these first.` });
  }catch(e){}
  if(!insights.length){ box.innerHTML=''; return; }
  box.innerHTML = insights.map(i=>`
    <div class="insight-card"><div class="ic-eyebrow">${icon(i.icon)} ${i.label}</div><div class="ic-text">${i.text}</div></div>
  `).join('');
}

async function renderKpiGrid(){
  const grid = document.getElementById('kpiGrid');
  grid.innerHTML = '';
  for(const key of activeWidgets){
    const w = ALL_WIDGETS.find(x=>x.key===key);
    if(!w) continue;
    const card = el(`
      <div class="kpi-card" style="--kpi-accent:${w.accent};--kpi-accent-soft:${w.accentSoft};">
        <button class="kpi-remove" onclick="removeWidget('${key}')">${icon('x')}</button>
        <div class="kpi-top"><div class="kpi-icon">${icon(w.icon)}</div></div>
        <div class="kpi-label">${w.label}</div>
        <div class="kpi-value" id="kpi_${key}">–</div>
      </div>`);
    grid.appendChild(card);
    try{
      let q = supa.from(w.table).select('*',{count:'exact',head:true});
      Object.entries(w.filter).forEach(([col,val])=> q = q.eq(col,val));
      if(key==='my_tasks') q = q.eq('owner_id', currentUser?.id);
      const { count } = await q;
      document.getElementById(`kpi_${key}`).textContent = count ?? 0;
    }catch(e){ document.getElementById(`kpi_${key}`).textContent = '–'; }
  }
  grid.appendChild(el(`<div class="add-widget-card" onclick="openWidgetPicker()">${icon('plus')}Add widget</div>`));
}
function removeWidget(key){
  activeWidgets = activeWidgets.filter(k=>k!==key);
  localStorage.setItem('crm_widgets', JSON.stringify(activeWidgets));
  renderKpiGrid();
}
function openWidgetPicker(){
  const available = ALL_WIDGETS.filter(w=>!activeWidgets.includes(w.key));
  const main = document.getElementById('main');
  main.appendChild(el(modalShell('widgetModal','Add a widget', `
    <div class="field-picker-list">
      ${available.length ? available.map(w=>`
        <div class="field-picker-item" onclick="addWidget('${w.key}')">${icon('plus')} ${w.label}</div>
      `).join('') : '<div class="empty-state">All available widgets are already on your dashboard.</div>'}
    </div>
  `, true)));
  openModal('widgetModal');
}
function addWidget(key){
  activeWidgets.push(key);
  localStorage.setItem('crm_widgets', JSON.stringify(activeWidgets));
  closeModal('widgetModal');
  renderKpiGrid();
}
async function renderPipelineChart(){
  const canvas = document.getElementById('pipelineCanvas'); if(!canvas) return;
  let counts = [0,0,0,0];
  try{
    const { data } = await supa.from('enquiries').select('pipeline_stage_id, enquiry_amount');
    (data||[]).forEach(r=>{
      const i = PIPELINE_STAGES.indexOf(r.pipeline_stage_id);
      if(i>-1) counts[i] += Number(r.enquiry_amount)||1;
    });
  }catch(e){}
  if(pipelineChart) pipelineChart.destroy();
  pipelineChart = new Chart(canvas, {
    type:'bar',
    data:{ labels:PIPELINE_STAGES, datasets:[{ data:counts, backgroundColor:['#B5791E','#2E5EA8','#15A38C','#C1392B'], borderRadius:6, maxBarThickness:46 }]},
    options:{ plugins:{legend:{display:false}}, scales:{ y:{ grid:{color:'#EEF1F6'}, ticks:{font:{family:'Inter',size:11}} }, x:{ grid:{display:false}, ticks:{font:{family:'Inter',size:11,weight:'600'}} } }, responsive:true, maintainAspectRatio:false }
  });
}
async function renderSourceChart(){
  const canvas = document.getElementById('sourceCanvas'); if(!canvas) return;
  let byLabel = {};
  try{
    const { data } = await supa.from('leads').select('source_id');
    (data||[]).forEach(r=>{ const k = r.source_id||'Unspecified'; byLabel[k]=(byLabel[k]||0)+1; });
  }catch(e){}
  const labels = Object.keys(byLabel); const vals = Object.values(byLabel);
  if(sourceChart) sourceChart.destroy();
  sourceChart = new Chart(canvas, {
    type:'doughnut',
    data:{ labels: labels.length?labels:['No leads yet'], datasets:[{ data: vals.length?vals:[1], backgroundColor:['#15A38C','#2E5EA8','#B5791E','#7A57BE','#C1392B','#5B6579'], borderWidth:0 }]},
    options:{ plugins:{legend:{position:'right', labels:{font:{family:'Inter',size:11}, boxWidth:10}}}, responsive:true, maintainAspectRatio:false, cutout:'62%' }
  });
}
async function renderRecentActivity(){
  const box = document.getElementById('recentActivity'); if(!box) return;
  const { data, error } = await supa.from('activities').select('*').order('created_at',{ascending:false}).limit(6);
  if(error || !data || !data.length){ box.innerHTML = `<div class="empty-state" style="padding:20px 6px;">Notes and calls logged against records will show up here.</div>`; return; }
  box.innerHTML = data.map(a=>`
    <div class="timeline-item">
      <div class="timeline-ic ${a.activity_type}">${icon(a.activity_type==='call'?'phone':(a.activity_type==='meeting'?'meeting':'note'))}</div>
      <div class="timeline-body">
        <div class="tl-title">${esc(a.title) || (a.activity_type[0].toUpperCase()+a.activity_type.slice(1))}</div>
        <div class="tl-text">${esc(a.body)||''}</div>
        <div class="tl-time">${timeAgo(a.created_at)} · ${a.record_type}</div>
      </div>
    </div>`).join('');
}
async function renderMyTasksToday(){
  const box = document.getElementById('myTasksToday'); if(!box) return;
  try{
    const { data, error } = await supa.from('tasks').select('*').eq('owner_id', currentUser?.id).eq('status','open').order('due_date',{ascending:true}).limit(6);
    if(error || !data || !data.length){ box.innerHTML = `<div class="empty-state" style="padding:20px 6px;">Nothing due — create a task from any record to see it here.</div>`; return; }
    box.innerHTML = data.map(t=>`
      <div class="checklist-row">
        <input type="checkbox" onchange="completeTask('${t.id}', this)">
        <div><div class="cl-title">${esc(t.title)}</div><div class="cl-meta">${t.due_date ? new Date(t.due_date).toLocaleDateString() : 'No due date'} · ${t.activity_kind}</div></div>
        <span class="pill ${t.priority}">${t.priority}</span>
      </div>`).join('');
  }catch(e){ box.innerHTML = `<div class="empty-state" style="padding:20px 6px;">Run migration_v3_zoho_style.sql to enable Tasks.</div>`; }
}
async function completeTask(id, checkboxEl){
  const { error } = await supa.from('tasks').update({status:'completed'}).eq('id', id);
  if(error){ toast('Error: '+error.message); checkboxEl.checked=false; return; }
  toast('Task completed');
  renderMyTasksToday(); refreshNavCounts(); refreshNotifDot();
}

// ============================================================================
// ACTIVITIES MODULE — Tasks / Calls / Meetings, Zoho-style
// ============================================================================
let activitiesKindFilter = 'all';
async function renderActivitiesModule(){
  const main = document.getElementById('main');
  pageHeader(main, 'Activities', 'Tasks, calls, and meetings across every record',
    `<button class="btn small" id="newTaskBtn">${icon('plus')}New Task</button>`);
  main.insertAdjacentHTML('beforeend', `
    <div class="view-tabs" id="activityViewTabs"></div>
    <div class="table-wrap">
      <div class="table-toolbar">
        <div class="toolbar-left">
          <span class="filter-chip" data-kind="all">All</span>
          <span class="filter-chip" data-kind="task">${icon('tasks')} Tasks</span>
          <span class="filter-chip" data-kind="call">${icon('phone')} Calls</span>
          <span class="filter-chip" data-kind="meeting">${icon('meeting')} Meetings</span>
        </div>
        <div class="list-search">${icon('search')}<input id="activitySearch" placeholder="Search activities..."></div>
      </div>
      <table>
        <thead><tr><th></th><th>Title</th><th>Type</th><th>Due</th><th>Priority</th><th>Status</th><th></th></tr></thead>
        <tbody id="activityRows"><tr><td colspan="7" class="empty-state">Loading…</td></tr></tbody>
      </table>
    </div>
    ${modalShell('taskModal','New Task', `
      <div class="form-grid">
        <div class="form-group full"><label class="required">Title</label><input id="tk_title"></div>
        <div class="form-group"><label>Type</label><select id="tk_kind"><option value="task">Task</option><option value="call">Call</option><option value="meeting">Meeting</option></select></div>
        <div class="form-group"><label>Priority</label><select id="tk_priority"><option value="normal">Normal</option><option value="high">High</option><option value="low">Low</option></select></div>
        <div class="form-group"><label>Due Date</label><input type="date" id="tk_due"></div>
        <div class="form-group"><label>Link to Record (optional)</label>
          <select id="tk_record_type"><option value="">— None —</option><option value="lead">Lead</option><option value="enquiry">Deal</option><option value="company">Account</option></select></div>
      </div>`)}
  `);
  document.getElementById('newTaskBtn').onclick = openTaskComposer;
  document.querySelectorAll('.filter-chip[data-kind]').forEach(c=>{
    c.onclick = ()=>{ activitiesKindFilter = c.dataset.kind; document.querySelectorAll('.filter-chip[data-kind]').forEach(x=>x.style.background=''); c.style.background='var(--brand-100)'; loadActivityRows(); };
  });
  document.getElementById('activitySearch').addEventListener('input', ()=> loadActivityRows());
  savedViewTabs('activityViewTabs', [
    { label:'My Open', filter:r=> r.owner_id===currentUser?.id && r.status==='open' },
    { label:'All Open', filter:r=> r.status==='open' },
    { label:'Completed', filter:r=> r.status==='completed' },
    { label:'All', filter:()=>true }
  ], (v)=>{ window.__activeActivityView = v; loadActivityRows(); });
  window.__activeActivityView = { filter:r=> r.owner_id===currentUser?.id && r.status==='open' };
  loadActivityRows();
}
function openTaskComposer(){
  const m = document.getElementById('taskModal');
  if(m){ openModal('taskModal'); return; }
  renderActivitiesModule().then(()=> openModal('taskModal'));
}
async function loadActivityRows(){
  const rows = document.getElementById('activityRows'); if(!rows) return;
  try{
    const { data, error } = await supa.from('tasks').select('*').order('due_date',{ascending:true});
    if(error) throw error;
    let filtered = (data||[]).filter(window.__activeActivityView ? window.__activeActivityView.filter : ()=>true);
    if(activitiesKindFilter !== 'all') filtered = filtered.filter(t=>t.activity_kind===activitiesKindFilter);
    const search = document.getElementById('activitySearch')?.value.trim();
    filtered = applyListControls(filtered, {search, searchFields:['title']});
    if(!filtered.length){ rows.innerHTML = `<tr><td colspan="7">${emptyState('tasks','No activities here','Create a task, call, or meeting to see it in this view.')}</td></tr>`; return; }
    rows.innerHTML = filtered.map(t=>`
      <tr>
        <td onclick="event.stopPropagation()"><input type="checkbox" class="row-check" ${t.status==='completed'?'checked':''} onchange="toggleTaskStatus('${t.id}', this.checked)"></td>
        <td class="row-primary">${esc(t.title)}</td>
        <td><span class="pill stage-New">${t.activity_kind}</span></td>
        <td>${t.due_date ? new Date(t.due_date).toLocaleDateString() : '–'}</td>
        <td><span class="pill ${t.priority}">${t.priority}</span></td>
        <td><span class="pill ${t.status==='open'?'stage-Open':'stage-Completed'}">${t.status}</span></td>
        <td class="row-actions"></td>
      </tr>`).join('');
  }catch(e){
    rows.innerHTML = `<tr><td colspan="7">${emptyState('tasks','Activities need one migration step','Run migration_v3_zoho_style.sql against your Supabase project to create the tasks table, then refresh.')}</td></tr>`;
  }
}
async function toggleTaskStatus(id, checked){
  const { error } = await supa.from('tasks').update({status: checked?'completed':'open'}).eq('id', id);
  if(error){ toast('Error: '+error.message); return; }
  loadActivityRows(); refreshNavCounts(); refreshNotifDot();
}
async function saveTask(){
  const payload = {
    title: document.getElementById('tk_title').value,
    activity_kind: document.getElementById('tk_kind').value,
    priority: document.getElementById('tk_priority').value,
    due_date: document.getElementById('tk_due').value || null,
    record_type: document.getElementById('tk_record_type').value || null,
    owner_id: currentUser.id,
    created_by: currentUser.id,
    status: 'open'
  };
  if(!payload.title){ toast('Title is required'); return; }
  const { error } = await supa.from('tasks').insert(payload);
  if(error){ toast('Error: '+error.message); return; }
  toast('Task created'); closeModal('taskModal');
  if(document.getElementById('activityRows')) loadActivityRows();
  refreshNavCounts(); refreshNotifDot();
}

// ============================================================================
// COMPANIES (Accounts)
// ============================================================================
let companyViewFilter = ()=>true;
async function renderCompanies(){
  const main = document.getElementById('main');
  pageHeader(main, 'Accounts', 'Company Master — one-time entry per customer',
    `<button class="btn small" id="newCompanyBtn">${icon('plus')}New Account</button>`);
  main.insertAdjacentHTML('beforeend', `
    <div class="view-tabs" id="companyViewTabs"></div>
    <div class="table-wrap">
      <div class="table-toolbar">
        <div class="toolbar-left"><span class="filter-chip">${icon('building')} All accounts</span></div>
        <div style="display:flex;align-items:center;gap:10px;">
          <div class="list-search">${icon('search')}<input id="companySearch" placeholder="Search accounts..."></div>
          <span style="font-size:11.5px;color:var(--ink-400);font-weight:600;" id="companyCount"></span>
        </div>
      </div>
      <div class="mass-bar" id="companyMassBar"><span id="companyMassCount">0 selected</span><button class="mb-btn" onclick="toast('Bulk export coming from Reports')">Export</button><button class="mb-btn" onclick="toast('Bulk tag editor not wired to a table yet')">Add tag</button></div>
      <table>
      <thead><tr><th style="width:32px;"><input type="checkbox" id="companySelectAll"></th><th data-sort="company_code">Code</th><th data-sort="company_name">Account Name</th><th>Country</th><th>State</th><th>Domestic/Export</th><th>Tags</th><th></th></tr></thead>
      <tbody id="companyRows"><tr><td colspan="8" class="empty-state">Loading…</td></tr></tbody>
    </table></div>
    ${modalShell('companyModal','New Account', companyFormHtml())}
  `);
  document.getElementById('newCompanyBtn').onclick = ()=> {
    openModal('companyModal');
    populateMasterDropdown('f_country', 'country_master');
    populateStateDropdown('f_state', '');
    document.getElementById('f_country').onchange = (e)=> populateStateDropdown('f_state', e.target.value);
  };
  savedViewTabs('companyViewTabs', [
    { label:'All Accounts', filter:()=>true },
    { label:'Domestic', filter:r=>r.domestic_export==='Domestic' },
    { label:'Export', filter:r=>r.domestic_export==='Export' },
    { label:'Recently Added', filter:()=>true, sortField:'created_at', sortDir:'desc' }
  ], (v)=>{ companyViewFilter = v.filter; loadCompanyRows(); });
  document.getElementById('companySearch').addEventListener('input', loadCompanyRows);
  document.querySelectorAll('#companyRows').length; // noop
  loadCompanyRows();
}
let __companyCache = [];
async function loadCompanyRows(){
  const rows = document.getElementById('companyRows'); if(!rows) return;
  const { data, error } = await supa.from('company_master').select('*').order('created_at',{ascending:false});
  __companyCache = data || [];
  if(error || !__companyCache.length){
    rows.innerHTML = `<tr><td colspan="8">${emptyState('building','No accounts yet','Add your first account to get started.')}</td></tr>`; return;
  }
  const search = document.getElementById('companySearch')?.value.trim();
  let filtered = __companyCache.filter(companyViewFilter);
  filtered = applyListControls(filtered, {search, searchFields:['company_name','company_code']});
  document.getElementById('companyCount').textContent = `${filtered.length} of ${__companyCache.length}`;
  if(!filtered.length){ rows.innerHTML = `<tr><td colspan="8">${emptyState('building','No matching accounts','Try a different search or view.')}</td></tr>`; return; }
  rows.innerHTML = filtered.map(c=>`
    <tr onclick="openDetailPanel('company','${c.id}')">
      <td onclick="event.stopPropagation()"><input type="checkbox" class="row-check company-check" value="${c.id}" onchange="updateMassBar('company')"></td>
      <td class="mono">${esc(c.company_code)}</td><td class="row-primary">${esc(c.company_name)}</td><td>${esc(c.country_id)||'–'}</td>
      <td>${esc(c.state_id)||'–'}</td><td><span class="pill stage-New">${esc(c.domestic_export)||'–'}</span></td>
      <td>${tagsHtml(c.tags) || '<span style="color:var(--ink-300)">–</span>'}</td>
      <td class="row-actions" onclick="event.stopPropagation()"><button class="btn secondary small" onclick="openDetailPanel('company','${c.id}')">View</button></td></tr>`).join('');
}
function updateMassBar(kind){
  const checked = document.querySelectorAll(`.${kind}-check:checked`);
  const bar = document.getElementById(kind+'MassBar');
  if(!bar) return;
  bar.classList.toggle('open', checked.length>0);
  const countEl = document.getElementById(kind+'MassCount');
  if(countEl) countEl.textContent = `${checked.length} selected`;
}
function companyFormHtml(){
  return `<div class="form-grid">
    <div class="form-group"><label class="required">Company Name</label><input id="f_company_name"></div>
    <div class="form-group"><label class="required">Country</label><select id="f_country"></select></div>
    <div class="form-group"><label class="required">State</label><select id="f_state"></select></div>
    <div class="form-group"><label class="required">Domestic / Export</label>
      <select id="f_domestic_export"><option>Domestic</option><option>Export</option></select></div>
    <div class="form-group"><label>GST No.</label><input id="f_gst"></div>
    <div class="form-group"><label>Tags (comma-separated)</label><input id="f_tags" placeholder="key-account, distributor"></div>
    <div class="form-group full"><label>Address</label><textarea id="f_address"></textarea></div>
  </div>`;
}
async function saveCompany(){
  const payload = {
    company_name: document.getElementById('f_company_name').value,
    country_id: document.getElementById('f_country').value || null,
    state_id: document.getElementById('f_state').value || null,
    domestic_export: document.getElementById('f_domestic_export').value,
    gst_no: document.getElementById('f_gst').value,
    address: document.getElementById('f_address').value,
    company_code: 'C' + Date.now().toString().slice(-6),
    created_by: currentUser.id
  };
  const tagsRaw = document.getElementById('f_tags').value.trim();
  if(tagsRaw) payload.tags = tagsRaw.split(',').map(s=>s.trim()).filter(Boolean);
  const { error } = await supa.from('company_master').insert(payload);
  if(error){ toast('Error: '+error.message); return; }
  toast('Account saved'); closeModal('companyModal'); loadCompanyRows();
}

// ============================================================================
// CONTACTS
// ============================================================================
async function renderContacts(){
  const main = document.getElementById('main');
  pageHeader(main, 'Contacts', 'People at each account you deal with',
    `<button class="btn small" id="newContactBtn">${icon('plus')}New Contact</button>`);
  main.insertAdjacentHTML('beforeend', `
    <div class="table-wrap">
      <div class="table-toolbar"><div class="toolbar-left"><span class="filter-chip">${icon('contacts')} All contacts</span></div>
      <div class="list-search">${icon('search')}<input id="contactSearch" placeholder="Search contacts..."></div></div>
      <table>
      <thead><tr><th>Name</th><th>Account</th><th>Designation</th><th>Email</th><th>Phone</th><th></th></tr></thead>
      <tbody id="contactRows"><tr><td colspan="6" class="empty-state">Loading…</td></tr></tbody>
    </table></div>
    ${modalShell('contactModal','New Contact', `<div class="form-grid">
      <div class="form-group full"><label class="required">Account</label><select id="ct_company"></select></div>
      <div class="form-group"><label class="required">Contact Name</label><input id="ct_name"></div>
      <div class="form-group"><label>Designation</label><input id="ct_designation"></div>
      <div class="form-group"><label>Email</label><input type="email" id="ct_email"></div>
      <div class="form-group"><label>Phone</label><input id="ct_phone"></div>
      <div class="form-group"><label><input type="checkbox" id="ct_primary" style="width:auto;vertical-align:middle;"> Primary contact for this account</label></div>
    </div>`)}
  `);
  document.getElementById('newContactBtn').onclick = ()=>{ openModal('contactModal'); populateMasterDropdown('ct_company','company_master','company_name'); };
  document.getElementById('contactSearch').addEventListener('input', loadContactRows);
  loadContactRows();
}
let __contactCache = [];
async function loadContactRows(){
  const rows = document.getElementById('contactRows'); if(!rows) return;
  const { data, error } = await supa.from('contact_master').select('*, company_master(company_name)').order('created_at',{ascending:false});
  __contactCache = data || [];
  if(error || !__contactCache.length){ rows.innerHTML = `<tr><td colspan="6">${emptyState('contacts','No contacts yet','Add the people you correspond with at each account.')}</td></tr>`; return; }
  const search = document.getElementById('contactSearch')?.value.trim();
  const filtered = applyListControls(__contactCache, {search, searchFields:['contact_name','email']});
  if(!filtered.length){ rows.innerHTML = `<tr><td colspan="6">${emptyState('contacts','No matching contacts','Try a different search.')}</td></tr>`; return; }
  rows.innerHTML = filtered.map(c=>`
    <tr><td class="row-primary">${esc(c.contact_name)}${c.is_primary?' <span class="pill stage-PORaised">Primary</span>':''}</td>
      <td>${esc(c.company_master?.company_name) || esc(c.company_id)}</td><td>${esc(c.designation)||'–'}</td>
      <td>${esc(c.email)||'–'}</td><td>${esc(c.phone)||'–'}</td>
      <td class="row-actions"><button class="btn secondary small" onclick="toast('Open contact detail for ${esc(c.contact_name)}')">View</button></td></tr>`).join('');
}
async function saveContact(){
  const payload = {
    contact_code: 'CT' + Date.now().toString().slice(-6),
    company_id: document.getElementById('ct_company').value,
    contact_name: document.getElementById('ct_name').value,
    designation: document.getElementById('ct_designation').value,
    email: document.getElementById('ct_email').value,
    phone: document.getElementById('ct_phone').value,
    is_primary: document.getElementById('ct_primary').checked,
    created_by: currentUser.id
  };
  const { error } = await supa.from('contact_master').insert(payload);
  if(error){ toast('Error: '+error.message); return; }
  toast('Contact saved'); closeModal('contactModal'); loadContactRows();
}

// ============================================================================
// LEADS
// ============================================================================
let leadViewFilter = ()=>true;
async function renderLeads(){
  const main = document.getElementById('main');
  pageHeader(main, 'Leads', `Scope: ${ROLE_SCOPE[currentRole].label}`,
    `<button class="btn small" id="newLeadBtn">${icon('plus')}New Lead</button>`);
  main.insertAdjacentHTML('beforeend', `
    <div class="view-tabs" id="leadViewTabs"></div>
    <div class="table-wrap">
      <div class="table-toolbar">
        <div class="toolbar-left"><span class="filter-chip">${icon('leads')} All leads</span></div>
        <div class="list-search">${icon('search')}<input id="leadSearch" placeholder="Search leads..."></div>
      </div>
      <table>
      <thead><tr><th>Lead No.</th><th>Company</th><th>Internal Co.</th><th>Source</th><th>Status</th><th>Tags</th><th></th></tr></thead>
      <tbody id="leadRows"><tr><td colspan="7" class="empty-state">Loading…</td></tr></tbody>
    </table></div>
    ${modalShell('leadModal','New Lead', leadFormHtml())}
  `);
  document.getElementById('newLeadBtn').onclick = ()=> {
    openModal('leadModal');
    populateMasterDropdown('f_lead_company', 'company_master', 'company_name');
    populateMasterDropdown('f_lead_internal_company', 'internal_company_master');
    populateMasterDropdown('f_lead_division', 'division_master');
    populateMasterDropdown('f_lead_source', 'source_master');
  };
  savedViewTabs('leadViewTabs', [
    { label:'All Leads', filter:()=>true },
    { label:'Open', filter:r=>r.closure_status==='open' },
    { label:'Ready to Convert', filter:r=>r.closure_status==='enquiry_raised' },
    { label:'Not Converted', filter:r=>r.closure_status==='not_converted' }
  ], (v)=>{ leadViewFilter = v.filter; loadLeadRows(); });
  document.getElementById('leadSearch').addEventListener('input', loadLeadRows);
  loadLeadRows();
}
let __leadCache = [];
async function loadLeadRows(){
  const rows = document.getElementById('leadRows'); if(!rows) return;
  const { data, error } = await supa.from('leads').select('*').order('created_at',{ascending:false});
  __leadCache = data || [];
  if(error || !__leadCache.length){
    rows.innerHTML = `<tr><td colspan="7">${emptyState('leads','No leads yet','Capture an enquiry as soon as it comes in.')}</td></tr>`; return;
  }
  const search = document.getElementById('leadSearch')?.value.trim();
  let filtered = __leadCache.filter(leadViewFilter);
  filtered = applyListControls(filtered, {search, searchFields:['lead_no','company_id']});
  if(!filtered.length){ rows.innerHTML = `<tr><td colspan="7">${emptyState('leads','No matching leads','Try a different view or search.')}</td></tr>`; return; }
  rows.innerHTML = filtered.map(l=>`
    <tr onclick="openDetailPanel('lead','${l.id}')">
      <td class="mono">${esc(l.lead_no)}</td><td class="row-primary">${esc(l.company_id)}</td><td>${esc(l.internal_company_id)}</td>
      <td>${esc(l.source_id)}</td><td><span class="pill ${pillClass(l.closure_status)}">${l.closure_status||'Open'}</span></td>
      <td>${tagsHtml(l.tags) || '<span style="color:var(--ink-300)">–</span>'}</td>
      <td class="row-actions" onclick="event.stopPropagation()"><button class="btn secondary small" onclick="openDetailPanel('lead','${l.id}')">View</button>
      ${l.closure_status==='enquiry_raised' ? `<button class="btn small" onclick="startEnquiryFromLead('${l.id}')">Add Products</button>` : ''}
      </td></tr>`).join('');
}
function leadFormHtml(){
  return `<div class="tabs"><div class="tab active">Via Lead</div><div class="tab">Direct-to-Deal</div></div>
    <div class="form-grid">
      <div class="form-group"><label class="required">Company</label><select id="f_lead_company"></select></div>
      <div class="form-group"><label>Contact Person</label><select id="f_lead_contact"></select></div>
      <div class="form-group"><label class="required">Internal Company</label><select id="f_lead_internal_company"></select></div>
      <div class="form-group"><label>Division</label><select id="f_lead_division"></select></div>
      <div class="form-group"><label class="required">Source</label><select id="f_lead_source"></select></div>
      <div class="form-group full"><label>Query</label><textarea id="f_lead_query" placeholder="Customer's requirement as received..."></textarea></div>
    </div>`;
}
async function saveLead(){
  const payload = {
    lead_no: 'L' + Date.now().toString().slice(-6),
    company_id: document.getElementById('f_lead_company').value,
    internal_company_id: document.getElementById('f_lead_internal_company').value,
    division_id: document.getElementById('f_lead_division').value || null,
    source_id: document.getElementById('f_lead_source').value,
    query: document.getElementById('f_lead_query').value,
    closure_status: 'open',
    created_by: currentUser.id
  };
  const { error } = await supa.from('leads').insert(payload);
  if(error){ toast('Error: '+error.message); return; }
  toast('Lead saved'); closeModal('leadModal'); loadLeadRows();
}

// ============================================================================
// ENQUIRIES → DEALS — List + Kanban pipeline view, probability-weighted
// ============================================================================
let productLineCount = 0;
let enquiryView = 'kanban';
let dealViewFilter = ()=>true;
async function renderEnquiries(){
  const main = document.getElementById('main');
  pageHeader(main, 'Deals', 'Product-wise entry — one line per SF, weighted by stage probability',
    `<button class="btn small" id="newEnquiryBtn">${icon('plus')}New Deal</button>`);
  main.insertAdjacentHTML('beforeend', `
    <div class="view-tabs" id="dealViewTabs"></div>
    <div class="table-wrap" style="margin-bottom:16px;">
      <div class="table-toolbar">
        <div class="toolbar-left">
          <div class="view-toggle">
            <button data-view="kanban" class="${enquiryView==='kanban'?'active':''}">${icon('kanban')}Pipeline</button>
            <button data-view="list" class="${enquiryView==='list'?'active':''}">${icon('list')}List</button>
          </div>
        </div>
        <div style="display:flex;align-items:center;gap:10px;">
          <div class="list-search">${icon('search')}<input id="dealSearch" placeholder="Search deals..."></div>
          <span style="font-size:11.5px;color:var(--ink-400);font-weight:600;" id="enquiryCount"></span>
        </div>
      </div>
      <div id="enquiryBody" style="padding:14px;"></div>
    </div>
    ${modalShell('enquiryModal','New Deal — Product-wise Entry', `<div id="productLines"></div>
      <button class="btn secondary small" id="addProductLineBtn">${icon('plus')}Add another product</button>`)}
  `);
  document.querySelectorAll('.view-toggle button').forEach(b=> b.onclick = ()=>{ enquiryView = b.dataset.view; renderEnquiries(); });
  document.getElementById('newEnquiryBtn').onclick = ()=>{
    document.getElementById('productLines').innerHTML=''; productLineCount = 0; addProductLine(); openModal('enquiryModal');
  };
  document.getElementById('addProductLineBtn').onclick = addProductLine;
  savedViewTabs('dealViewTabs', [
    { label:'All Deals', filter:()=>true },
    { label:'Open', filter:r=>r.pipeline_stage_id!=='Order Lost' },
    { label:'Closing Soon (P.O. Raised)', filter:r=>r.pipeline_stage_id==='P.O. Raised' },
    { label:'Lost', filter:r=>r.pipeline_stage_id==='Order Lost' }
  ], (v)=>{ dealViewFilter = v.filter; loadEnquiryData(); });
  document.getElementById('dealSearch').addEventListener('input', loadEnquiryData);
  loadEnquiryData();
}
let __enquiryCache = [];
async function loadEnquiryData(){
  const body = document.getElementById('enquiryBody'); if(!body) return;
  const { data, error } = await supa.from('enquiries').select('*').order('created_at',{ascending:false});
  __enquiryCache = data || [];
  if(error || !__enquiryCache.length){ body.innerHTML = emptyState('enquiries','No deals yet','Create one from a lead or directly here.'); return; }
  const search = document.getElementById('dealSearch')?.value.trim();
  let filtered = __enquiryCache.filter(dealViewFilter);
  filtered = applyListControls(filtered, {search, searchFields:['enquiry_no','company_id']});
  document.getElementById('enquiryCount').textContent = `${filtered.length} of ${__enquiryCache.length}`;
  enquiryView === 'kanban' ? renderEnquiryKanban(body, filtered) : renderEnquiryList(body, filtered);
}
function renderEnquiryKanban(container, data){
  container.style.padding = '0';
  const cols = PIPELINE_STAGES.map(stage=>{
    const items = data.filter(e => (e.pipeline_stage_id||'Quotation') === stage);
    const total = items.reduce((s,e)=> s + (Number(e.enquiry_amount)||0), 0);
    const weighted = total * ((STAGE_PROBABILITY[stage]||20)/100);
    return `
      <div class="kanban-col">
        <div class="kanban-col-head">
          <div class="kanban-col-title"><span class="kanban-dot" style="background:${STAGE_COLOR[stage]}"></span>${stage}</div>
          <span class="kanban-count">${items.length}</span>
        </div>
        <div class="kanban-col-total">${total ? '₹'+money(total)+' · ₹'+money(weighted)+' weighted' : ''}</div>
        <div class="kanban-cards">
          ${items.length ? items.map(e=>`
            <div class="kanban-card" onclick="openDetailPanel('enquiry','${e.id}')">
              <div class="kc-title">${esc(e.enquiry_no)}</div>
              <div class="kc-sub">${esc(e.company_id)} · SF ${e.sf_id?.toString().slice(0,8)||''}</div>
              <div style="margin-bottom:6px;"><span class="prob-bar"><span class="prob-bar-fill" style="width:${STAGE_PROBABILITY[stage]||20}%"></span></span><span style="font-size:10.5px;color:var(--ink-500);font-weight:700;">${STAGE_PROBABILITY[stage]||20}%</span></div>
              <div class="kc-foot"><span class="kc-amount">${e.enquiry_amount? '₹'+money(e.enquiry_amount) : '–'}</span>
              <button class="btn secondary small" style="padding:3px 8px;" onclick="event.stopPropagation();openQuoteBuilder('${e.id}')">Quote</button></div>
            </div>`).join('') : `<div class="kanban-empty">No deals at this stage</div>`}
        </div>
      </div>`;
  }).join('');
  container.innerHTML = `<div class="kanban">${cols}</div>`;
}
function renderEnquiryList(container, data){
  container.style.padding = '0';
  container.innerHTML = `<table>
    <thead><tr><th>Deal No.</th><th>Company</th><th>SF (Product)</th><th>Qty</th><th>Amount</th><th>Probability</th><th>Stage</th><th></th></tr></thead>
    <tbody>${data.map(e=>`
      <tr onclick="openDetailPanel('enquiry','${e.id}')">
        <td class="mono">${esc(e.enquiry_no)}</td><td class="row-primary">${esc(e.company_id)}</td><td>${esc(e.sf_id)}</td>
        <td>${e.enquiry_qty||'–'}</td><td>${e.enquiry_amount?'₹'+money(e.enquiry_amount):'–'}</td>
        <td><span class="prob-bar"><span class="prob-bar-fill" style="width:${STAGE_PROBABILITY[e.pipeline_stage_id]||20}%"></span></span>${STAGE_PROBABILITY[e.pipeline_stage_id]||20}%</td>
        <td><span class="pill ${pillClass(e.pipeline_stage_id)}">${e.pipeline_stage_id||'Quotation'}</span></td>
        <td class="row-actions" onclick="event.stopPropagation()"><button class="btn secondary small" onclick="openDetailPanel('enquiry','${e.id}')">View</button>
        <button class="btn small" onclick="openQuoteBuilder('${e.id}')">Quote</button></td></tr>`).join('')}</tbody></table>`;
}
function addProductLine(){
  productLineCount++; const idx = productLineCount;
  const line = el(`
    <div class="product-line" data-idx="${idx}">
      <div class="line-index">Product line ${idx}</div>
      <button class="remove-line" onclick="this.parentElement.remove()">×</button>
      <div class="form-grid cols-3">
        <div class="form-group"><label class="required">Internal Company</label><select id="pl_internal_company_${idx}"></select></div>
        <div class="form-group"><label class="required">Source</label><select id="pl_source_${idx}"></select></div>
        <div class="form-group"><label class="required">SF (Product)</label>
          <select id="pl_sf_${idx}"><option value="__new__">+ New SF (generate code)</option></select></div>
        <div class="form-group" id="pl_newsf_wrap_${idx}"><label class="required">New SF Name</label><input id="pl_newsf_name_${idx}" placeholder="e.g. Vitamin C 500mg Tablets"></div>
        <div class="form-group"><label>Dosage Form</label><select id="pl_dosage_${idx}"></select></div>
        <div class="form-group"><label>Enquiry Qty</label><input type="number" id="pl_qty_${idx}"></div>
        <div class="form-group"><label>Qty Unit</label><select id="pl_qtyunit_${idx}"></select></div>
        <div class="form-group"><label>Enquiry Rate</label><input type="number" step="0.01" id="pl_rate_${idx}"></div>
        <div class="form-group"><label>Target Rate</label><input type="number" step="0.01" id="pl_target_${idx}"></div>
        <div class="form-group"><label>Pipeline Stage</label>
          <select id="pl_stage_${idx}">${PIPELINE_STAGES.map(s=>`<option>${s}</option>`).join('')}</select></div>
        <div class="form-group"><label>Tags (comma-separated)</label><input id="pl_tags_${idx}" placeholder="urgent, repeat-order"></div>
      </div>
      <div id="pl_po_block_${idx}" style="display:none;margin-top:12px;padding-top:12px;border-top:1px dashed var(--line);">
        <div class="form-grid"><div class="form-group"><label>P.O. Qty</label><input type="number" id="pl_po_qty_${idx}"></div>
        <div class="form-group"><label>P.O. Rate</label><input type="number" step="0.01" id="pl_po_rate_${idx}"></div></div>
      </div>
      <div id="pl_lost_block_${idx}" style="display:none;margin-top:12px;">
        <div class="form-group"><label class="required">Order Lost Reason</label><textarea id="pl_lost_reason_${idx}"></textarea></div>
      </div>
    </div>`);
  document.getElementById('productLines').appendChild(line);
  document.getElementById(`pl_stage_${idx}`).addEventListener('change',(e)=>{
    document.getElementById(`pl_po_block_${idx}`).style.display = e.target.value==='P.O. Raised' ? 'block':'none';
    document.getElementById(`pl_lost_block_${idx}`).style.display = e.target.value==='Order Lost' ? 'block':'none';
  });
  document.getElementById(`pl_sf_${idx}`).addEventListener('change',(e)=>{
    document.getElementById(`pl_newsf_wrap_${idx}`).style.display = e.target.value==='__new__' ? 'flex':'none';
  });
  populateMasterDropdown(`pl_internal_company_${idx}`, 'internal_company_master');
  populateMasterDropdown(`pl_source_${idx}`, 'source_master');
  populateMasterDropdown(`pl_sf_${idx}`, 'sf_master', 'sf_name', true);
  populateMasterDropdown(`pl_dosage_${idx}`, 'dosage_form_master');
  populateMasterDropdown(`pl_qtyunit_${idx}`, 'qty_unit_master');
}
async function saveEnquiry(){
  const lines = document.querySelectorAll('.product-line'); const inserts = [];
  for(const line of lines){
    const idx = line.dataset.idx;
    const stage = document.getElementById(`pl_stage_${idx}`).value;
    const tagsRaw = document.getElementById(`pl_tags_${idx}`).value.trim();
    let sfId = document.getElementById(`pl_sf_${idx}`).value;
    if(sfId === '__new__'){
      const newName = document.getElementById(`pl_newsf_name_${idx}`).value.trim();
      if(!newName){ toast('Enter a name for the new SF product on line '+idx); return; }
      const { data: sfRow, error: sfErr } = await supa.from('sf_master').insert({
        sf_code: 'SF' + Date.now().toString().slice(-6) + idx,
        sf_name: newName,
        status: 'new',
        created_by: currentUser?.id
      }).select().single();
      if(sfErr){ toast('Error creating SF product: '+sfErr.message); return; }
      sfId = sfRow.id;
    }
    inserts.push({
      enquiry_no: 'E' + Date.now().toString().slice(-6) + '-' + idx,
      internal_company_id: document.getElementById(`pl_internal_company_${idx}`).value,
      source_id: document.getElementById(`pl_source_${idx}`).value,
      sf_id: sfId,
      dosage_form_id: document.getElementById(`pl_dosage_${idx}`).value || null,
      enquiry_qty: parseFloat(document.getElementById(`pl_qty_${idx}`).value) || null,
      qty_unit_id: document.getElementById(`pl_qtyunit_${idx}`).value || null,
      enquiry_rate: parseFloat(document.getElementById(`pl_rate_${idx}`).value) || null,
      target_rate: parseFloat(document.getElementById(`pl_target_${idx}`).value) || null,
      pipeline_stage_id: stage,
      probability: STAGE_PROBABILITY[stage] || 20,
      tags: tagsRaw ? tagsRaw.split(',').map(s=>s.trim()).filter(Boolean) : null,
      po_qty: parseFloat(document.getElementById(`pl_po_qty_${idx}`)?.value) || null,
      po_rate: parseFloat(document.getElementById(`pl_po_rate_${idx}`)?.value) || null,
      order_lost_reason: document.getElementById(`pl_lost_reason_${idx}`)?.value || null,
      created_by: currentUser?.id
    });
  }
  const { error } = await supa.from('enquiries').insert(inserts);
  if(error){ toast('Error: '+error.message); return; }
  toast(`${inserts.length} deal line(s) saved`); closeModal('enquiryModal'); loadEnquiryData();
}

// ============================================================================
// SF MASTER (Products) — full product master with fixed + customizable fields
// ============================================================================
async function renderSFMaster(){
  const main = document.getElementById('main');
  pageHeader(main, 'Products', 'SF Master — the source of truth for every deal line',
    `<button class="btn small" id="newSFBtn">${icon('plus')}New Product</button>`);
  main.insertAdjacentHTML('beforeend', `
    <div class="table-wrap"><table>
      <thead><tr><th>SF Code</th><th>SF Name</th><th>Composition</th><th>Category</th><th>Dosage Form</th><th>Pack Size</th><th>Status</th><th></th></tr></thead>
      <tbody id="sfRows"><tr><td colspan="8" class="empty-state">Loading…</td></tr></tbody>
    </table></div>
    ${modalShell('sfModal','New Product', sfFormHtml())}
  `);
  document.getElementById('newSFBtn').onclick = ()=> openModal('sfModal');
  populateMasterDropdown('sf_category', 'category_master');
  populateMasterDropdown('sf_dosage', 'dosage_form_master');
  renderSFCustomFieldInputs();

  const { data, error } = await supa.from('sf_master').select('*').order('created_at',{ascending:false});
  const rows = document.getElementById('sfRows');
  if(error || !data || !data.length){
    rows.innerHTML = `<tr><td colspan="8">${emptyState('flask','No products yet','New products can also be generated on the fly from Deal entry.')}</td></tr>`; return;
  }
  rows.innerHTML = data.map(s=>`
    <tr><td class="mono">${esc(s.sf_code)}</td><td class="row-primary">${esc(s.sf_name)}</td><td>${esc(s.composition)||'–'}</td>
      <td>${esc(s.category_id)||'–'}</td><td>${esc(s.dosage_form_id)||'–'}</td><td>${esc(s.pack_size)||'–'}</td>
      <td><span class="pill stage-${s.status==='new'?'New':'Existing'}">${s.status||'existing'}</span></td>
      <td class="row-actions"><button class="btn secondary small" onclick="openDetailPanel('sf','${s.id}')">View</button></td></tr>`).join('');
}
function sfFormHtml(){
  return `
    <div class="form-grid">
      <div class="form-group"><label>SF Code</label><input id="sf_code" placeholder="Auto-generated on save" disabled></div>
      <div class="form-group"><label class="required">SF Name</label><input id="sf_name"></div>
      <div class="form-group full"><label>Composition</label><textarea id="sf_composition" placeholder="e.g. Vitamin C 500mg + Zinc 5mg"></textarea></div>
      <div class="form-group"><label>Category</label><select id="sf_category"></select></div>
      <div class="form-group"><label>Dosage Form</label><select id="sf_dosage"></select></div>
      <div class="form-group"><label>Pack Size</label><input id="sf_pack" placeholder="e.g. 10x10 Alu-Alu"></div>
      <div class="form-group"><label>HSN Code</label><input id="sf_hsn"></div>
      <div class="form-group"><label>Shelf Life (months)</label><input type="number" id="sf_shelf"></div>
      <div class="form-group"><label>MOQ</label><input type="number" id="sf_moq"></div>
      <div class="form-group"><label>Standard Rate (reference)</label><input type="number" step="0.01" id="sf_rate"></div>
    </div>
    <div id="sfCustomFieldInputs" style="margin-top:16px;"></div>
    <div style="margin-top:10px;"><a href="#" onclick="event.preventDefault(); window.__navTo('fields')" style="font-size:12px;color:var(--brand-700);font-weight:700;">+ Add another field to this form (Custom Fields)</a></div>
  `;
}
async function renderSFCustomFieldInputs(){
  const { data } = await supa.from('custom_field_definitions').select('*').eq('module','sf').eq('is_active',true);
  const box = document.getElementById('sfCustomFieldInputs');
  if(!box) return;
  if(!data || !data.length){ box.innerHTML=''; return; }
  box.innerHTML = `<div class="form-grid">` + data.map(f=>{
    const inputId = `cf_${f.field_key}`;
    if(f.field_type==='dropdown'){
      return `<div class="form-group"><label ${f.is_required?'class="required"':''}>${esc(f.label)}</label>
        <select id="${inputId}">${(f.dropdown_options||[]).map(o=>`<option>${esc(o)}</option>`).join('')}</select></div>`;
    }
    const type = f.field_type==='checkbox' ? 'checkbox' : f.field_type==='number' ? 'number' : f.field_type==='date' ? 'date' : 'text';
    return `<div class="form-group"><label ${f.is_required?'class="required"':''}>${esc(f.label)}</label><input type="${type}" id="${inputId}"></div>`;
  }).join('') + `</div>`;
}
async function saveSF(){
  const payload = {
    sf_code: 'SF' + Date.now().toString().slice(-6),
    sf_name: document.getElementById('sf_name').value,
    composition: document.getElementById('sf_composition').value,
    category_id: document.getElementById('sf_category').value || null,
    dosage_form_id: document.getElementById('sf_dosage').value || null,
    pack_size: document.getElementById('sf_pack').value,
    hsn_code: document.getElementById('sf_hsn').value,
    shelf_life_months: parseInt(document.getElementById('sf_shelf').value) || null,
    moq: parseFloat(document.getElementById('sf_moq').value) || null,
    standard_rate: parseFloat(document.getElementById('sf_rate').value) || null,
    status: 'existing'
  };
  const { error } = await supa.from('sf_master').insert(payload);
  if(error){ toast('Error: '+error.message); return; }
  toast('Product saved'); closeModal('sfModal'); renderSFMaster();
}

// ============================================================================
// MAIL
// ============================================================================
async function renderMail(){
  const main = document.getElementById('main');
  pageHeader(main, 'Mail', 'Inbound mail matched to your open leads and deals');
  main.insertAdjacentHTML('beforeend', `
    <div class="tabs">
      <div class="tab active" data-mailtab="unassigned">Unassigned</div>
      <div class="tab" data-mailtab="assigned">Assigned to Lead/Deal</div>
    </div>
    <div id="mailList"><div class="empty-state">Connect a mailbox in Setup → Mail Integration to see messages here.</div></div>`);
  document.querySelectorAll('[data-mailtab]').forEach(t=>{
    t.onclick = ()=>{ document.querySelectorAll('[data-mailtab]').forEach(x=>x.classList.remove('active')); t.classList.add('active'); loadMail(t.dataset.mailtab); };
  });
  loadMail('unassigned');
}
async function loadMail(tab){
  const { data, error } = await supa.from('email_threads').select('*').eq('is_assigned', tab==='assigned');
  const list = document.getElementById('mailList');
  if(error || !data || !data.length){ list.innerHTML = emptyState('mail', `No ${tab} mail`, 'Nothing here right now.'); return; }
  list.innerHTML = data.map(t=>`
    <div class="card" style="display:flex;justify-content:space-between;align-items:center;">
      <div><strong>${esc(t.subject)||'(no subject)'}</strong><div style="font-size:12px;color:var(--ink-500)">Thread: ${esc(t.provider_thread_id)}</div></div>
      ${tab==='unassigned' ? `<div><button class="btn small" onclick="assignMailToLead('${t.id}')">Add as Lead</button>
        <button class="btn secondary small" onclick="assignMailToEnquiry('${t.id}')">Add to Deal</button></div>`
        : `<span class="pill stage-EnquiryRaised">Linked</span>`}
    </div>`).join('');
}

// ============================================================================
// QUOTES
// ============================================================================
async function renderQuotes(){
  const main = document.getElementById('main');
  pageHeader(main, 'Quotes', 'Every quote sent, generated straight from a deal');
  main.insertAdjacentHTML('beforeend', `
    <div class="table-wrap"><table><thead><tr><th>Quote No.</th><th>Deal</th><th>Amount</th><th>Sent</th><th></th></tr></thead>
    <tbody id="quoteRows"><tr><td colspan="5" class="empty-state">Loading…</td></tr></tbody></table></div>`);
  const { data, error } = await supa.from('quotes').select('*').order('created_at',{ascending:false});
  const rows = document.getElementById('quoteRows');
  if(error || !data || !data.length){ rows.innerHTML = `<tr><td colspan="5">${emptyState('quotes','No quotes yet','Build one from a Deal row.')}</td></tr>`; return; }
  rows.innerHTML = data.map(q=>`<tr><td class="mono">${esc(q.quote_no)}</td><td>${esc(q.enquiry_id)}</td><td>${q.quoted_amount?'₹'+money(q.quoted_amount):'–'}</td>
    <td>${q.sent_at?new Date(q.sent_at).toLocaleDateString():'Not sent'}</td><td class="row-actions"><button class="btn secondary small">Send</button></td></tr>`).join('');
}
function openQuoteBuilder(enquiryId){
  document.getElementById('main').appendChild(el(modalShell('quoteModal','Build Quote', `
    <div class="form-grid">
      <div class="form-group"><label>Template</label><select id="q_template"><option value="quotation">Quotation Mail</option><option value="introduction">Introduction Mail</option></select></div>
      <div class="form-group"><label>Base on previous quote</label><select id="q_prev"><option value="">None — start fresh</option></select></div>
      <div class="form-group"><label>Quoted Rate</label><input type="number" step="0.01" id="q_rate"></div>
      <div class="form-group"><label>Quoted Qty</label><input type="number" id="q_qty"></div>
      <div class="form-group full"><label>Preview</label><textarea id="q_preview" rows="6"></textarea></div>
    </div>`, true)));
  openModal('quoteModal');
}

// ============================================================================
// PROJECTS
// ============================================================================
async function renderProjects(){
  const main = document.getElementById('main');
  pageHeader(main, 'Projects', 'Delivery tracking once an order is won', `<button class="btn small">${icon('plus')}New Project</button>`);
  main.insertAdjacentHTML('beforeend', emptyState('projects','Project boards render here','Same pattern as Leads/Deals — Supabase tables: projects / project_tasks.'));
}

// ============================================================================
// REPORTS / ANALYTICS — customizable builder
// ============================================================================
const REPORT_MODULES = {
  leads:     { table:'leads', fields:['lead_no','company_id','internal_company_id','source_id','closure_status'] },
  enquiries: { table:'enquiries', fields:['enquiry_no','company_id','sf_id','enquiry_qty','enquiry_amount','pipeline_stage_id','probability'] },
  companies: { table:'company_master', fields:['company_code','company_name','country_id','domestic_export'] },
  tasks:     { table:'tasks', fields:['title','activity_kind','due_date','priority','status'] }
};
let reportSelectedFields = [];
async function renderReports(){
  const main = document.getElementById('main');
  pageHeader(main, 'Analytics', 'Build a custom report — pick a module, choose columns, run.');
  main.insertAdjacentHTML('beforeend', `
    <div class="report-builder-grid">
      <div class="card">
        <div class="card-title">1. Module</div>
        <select id="reportModule" style="width:100%;margin-bottom:16px;">
          ${Object.keys(REPORT_MODULES).map(m=>`<option value="${m}">${m[0].toUpperCase()+m.slice(1)}</option>`).join('')}
        </select>
        <div class="card-title">2. Columns</div>
        <div class="field-picker-list" id="reportFieldPicker"></div>
        <button class="btn small" style="margin-top:14px;width:100%;justify-content:center;" id="runReportBtn">Run report</button>
      </div>
      <div class="card">
        <div class="card-title">Result</div>
        <div id="reportResult" class="empty-state">Choose columns and click "Run report".</div>
      </div>
    </div>`);
  document.getElementById('reportModule').addEventListener('change', renderReportFieldPicker);
  document.getElementById('runReportBtn').onclick = runReport;
  renderReportFieldPicker();
}
function renderReportFieldPicker(){
  const mod = document.getElementById('reportModule').value;
  reportSelectedFields = [...REPORT_MODULES[mod].fields];
  const box = document.getElementById('reportFieldPicker');
  box.innerHTML = REPORT_MODULES[mod].fields.map(f=>`
    <label class="field-picker-item"><input type="checkbox" checked data-field="${f}" onchange="toggleReportField('${f}',this.checked)"> ${f}</label>
  `).join('');
}
function toggleReportField(field, checked){
  if(checked && !reportSelectedFields.includes(field)) reportSelectedFields.push(field);
  if(!checked) reportSelectedFields = reportSelectedFields.filter(f=>f!==field);
}
async function runReport(){
  const mod = document.getElementById('reportModule').value;
  const { table } = REPORT_MODULES[mod];
  const cols = reportSelectedFields.length ? reportSelectedFields.join(',') : '*';
  const { data, error } = await supa.from(table).select(cols).limit(100);
  const result = document.getElementById('reportResult');
  if(error || !data || !data.length){ result.innerHTML = emptyState('reports','No rows returned','Try a different module or check your filters.'); return; }
  result.innerHTML = `<div class="table-wrap"><table><thead><tr>${reportSelectedFields.map(f=>`<th>${f}</th>`).join('')}</tr></thead>
    <tbody>${data.map(r=>`<tr>${reportSelectedFields.map(f=>`<td>${r[f]??'–'}</td>`).join('')}</tr>`).join('')}</tbody></table></div>`;
}

// ============================================================================
// MASTERS
// ============================================================================
const MASTER_TABLES = [
  { key:'internal_company_master', label:'Internal Company' },
  { key:'category_master', label:'Category' },
  { key:'dosage_form_master', label:'Dosage Form' },
  { key:'division_master', label:'Division' },
  { key:'source_master', label:'Source' },
  { key:'pipeline_master', label:'Pipeline Stage' },
  { key:'qty_unit_master', label:'Qty Unit' },
  { key:'country_master', label:'Country' },
  { key:'state_master', label:'State' }
];
async function renderMasters(){
  const main = document.getElementById('main');
  pageHeader(main, 'Masters', 'Admin-editable lookup lists used across every form');
  main.insertAdjacentHTML('beforeend', `
    <div class="tabs" id="masterTabs">${MASTER_TABLES.map((m,i)=>`<div class="tab ${i===0?'active':''}" data-master="${m.key}">${m.label}</div>`).join('')}</div>
    <div class="card">
      <div style="display:flex;gap:8px;margin-bottom:14px;">
        <input id="newMasterValue" placeholder="Add new value...">
        <button class="btn small" id="addMasterBtn">Add</button>
      </div>
      <table><tbody id="masterRows"></tbody></table>
    </div>`);
  document.querySelectorAll('[data-master]').forEach(t=>{
    t.onclick = ()=>{ document.querySelectorAll('[data-master]').forEach(x=>x.classList.remove('active')); t.classList.add('active'); loadMasterRows(t.dataset.master); };
  });
  document.getElementById('addMasterBtn').onclick = ()=> addMasterValue(document.querySelector('[data-master].active').dataset.master);
  loadMasterRows(MASTER_TABLES[0].key);
}
async function loadMasterRows(table){
  const { data, error } = await supa.from(table).select('*').order('name',{ascending:true});
  const rows = document.getElementById('masterRows');
  if(error || !data || !data.length){ rows.innerHTML = `<tr><td class="empty-state">No entries yet — add the first one above.</td></tr>`; return; }
  rows.innerHTML = data.map(r=>`<tr><td>${esc(r.name)}</td><td style="text-align:right"><button class="btn secondary small" onclick="deleteMasterValue('${table}','${r.id}')">Remove</button></td></tr>`).join('');
}
async function addMasterValue(table){
  const val = document.getElementById('newMasterValue').value.trim(); if(!val) return;
  const { error } = await supa.from(table).insert({ name: val });
  if(error){ toast('Error: '+error.message); return; }
  document.getElementById('newMasterValue').value=''; loadMasterRows(table);
}
async function deleteMasterValue(table,id){ await supa.from(table).delete().eq('id', id); loadMasterRows(table); }

// ============================================================================
// CUSTOM FIELDS — covers Account / Lead / Deal / Product / Project
// ============================================================================
async function renderCustomFields(){
  const main = document.getElementById('main');
  pageHeader(main, 'Custom Fields', 'Add fields to any module without a developer');
  main.insertAdjacentHTML('beforeend', `
    <div class="tabs" id="fieldModuleTabs">
      <div class="tab active" data-module="company">Account</div>
      <div class="tab" data-module="lead">Lead</div>
      <div class="tab" data-module="enquiry">Deal</div>
      <div class="tab" data-module="sf">Product</div>
      <div class="tab" data-module="project">Project</div>
    </div>
    <div class="card">
      <div class="form-grid" style="align-items:end;">
        <div class="form-group"><label>Field Label</label><input id="nf_label"></div>
        <div class="form-group"><label>Field Type</label>
          <select id="nf_type"><option value="text">Text</option><option value="number">Number</option>
            <option value="date">Date</option><option value="dropdown">Dropdown</option><option value="checkbox">Checkbox</option></select></div>
        <div class="form-group"><label>Dropdown options (comma-separated)</label><input id="nf_options" placeholder="Only if type = Dropdown"></div>
        <div class="form-group"><label><input type="checkbox" id="nf_required" style="width:auto"> Required</label></div>
        <button class="btn" id="addFieldBtn">${icon('plus')}Add Field</button>
      </div>
    </div>
    <div id="fieldChips" style="margin-bottom:14px;"></div>
  `);
  document.querySelectorAll('[data-module]').forEach(t=>{
    t.onclick = ()=>{ document.querySelectorAll('[data-module]').forEach(x=>x.classList.remove('active')); t.classList.add('active'); loadCustomFields(t.dataset.module); };
  });
  document.getElementById('addFieldBtn').onclick = ()=> addCustomField(document.querySelector('[data-module].active').dataset.module);
  loadCustomFields('company');
}
async function loadCustomFields(module){
  const { data, error } = await supa.from('custom_field_definitions').select('*').eq('module', module).order('display_order');
  const box = document.getElementById('fieldChips');
  if(error || !data || !data.length){ box.innerHTML = `<div class="empty-state">No custom fields on ${module} yet.</div>`; return; }
  box.innerHTML = data.map(f=>`<span class="field-chip">${esc(f.label)} <span class="type-tag">(${f.field_type}${f.is_required?', required':''})</span>
    <button onclick="deleteCustomField('${f.id}')">×</button></span>`).join('');
}
async function addCustomField(module){
  const label = document.getElementById('nf_label').value.trim(); if(!label) return;
  const payload = {
    module, label, field_key: label.toLowerCase().replace(/[^a-z0-9]+/g,'_'),
    field_type: document.getElementById('nf_type').value,
    dropdown_options: document.getElementById('nf_options').value ? document.getElementById('nf_options').value.split(',').map(s=>s.trim()) : null,
    is_required: document.getElementById('nf_required').checked
  };
  const { error } = await supa.from('custom_field_definitions').insert(payload);
  if(error){ toast('Error: '+error.message); return; }
  document.getElementById('nf_label').value=''; loadCustomFields(module);
}
async function deleteCustomField(id){
  await supa.from('custom_field_definitions').delete().eq('id', id);
  loadCustomFields(document.querySelector('[data-module].active').dataset.module);
}

// ============================================================================
// USERS & ROLES
// ============================================================================
async function renderUsers(){
  const main = document.getElementById('main');
  pageHeader(main, 'Users & Roles', `Role hierarchy: User → Manager → Super Manager → Admin. A Manager sees their direct reports' records; a Super Manager sees every team below them.`,
    `<button class="btn small" id="inviteUserBtn">${icon('plus')}Invite User</button>`);
  main.insertAdjacentHTML('beforeend', `
    <div class="table-wrap"><table>
      <thead><tr><th>Name</th><th>Email</th><th>Role</th><th>Reports To</th><th></th></tr></thead>
      <tbody id="userRows"><tr><td colspan="5" class="empty-state">Loading…</td></tr></tbody>
    </table></div>
    ${modalShell('userModal','Invite User', `
      <div class="form-grid">
        <div class="form-group"><label class="required">Full Name</label><input id="u_name"></div>
        <div class="form-group"><label class="required">Email</label><input id="u_email"></div>
        <div class="form-group"><label class="required">Role</label>
          <select id="u_role"><option value="user">User</option><option value="manager">Manager</option>
            <option value="super_manager">Super Manager</option><option value="admin">Admin</option></select></div>
        <div class="form-group"><label>Reports To</label><select id="u_reports_to"><option value="">— None —</option></select></div>
      </div>`, true)}
  `);
  document.getElementById('inviteUserBtn').onclick = ()=> openModal('userModal');
  const { data, error } = await supa.from('app_users').select('*').order('created_at',{ascending:false});
  const rows = document.getElementById('userRows');
  if(error || !data || !data.length){ rows.innerHTML = `<tr><td colspan="5">${emptyState('users','No users yet','')}</td></tr>`; return; }
  rows.innerHTML = data.map(u=>`<tr><td class="row-primary">${esc(u.full_name)}</td><td>${esc(u.email)}</td>
    <td><span class="pill role-pill">${u.role}</span></td><td>${esc(u.reports_to)||'–'}</td>
    <td class="row-actions"><button class="btn secondary small">Edit</button></td></tr>`).join('');
}

// ============================================================================
// SETTINGS — mail integration
// ============================================================================
async function renderSettings(){
  const main = document.getElementById('main');
  pageHeader(main, 'Mail Integration', 'Connect a mailbox to route replies straight into leads and deals');
  main.insertAdjacentHTML('beforeend', `
    <div class="card">
      <p style="margin:0;line-height:1.6;color:var(--ink-700);">Each user connects their own inbox. Once connected, incoming mail is matched to open leads/deals by
      sender + thread; anything unmatched appears under <strong>Mail → Unassigned</strong>.</p>
      <div style="margin-top:14px;display:flex;gap:10px;">
        <button class="btn" onclick="connectMailbox('gmail')">Connect Gmail</button>
        <button class="btn secondary" onclick="connectMailbox('outlook')">Connect Outlook</button>
      </div>
      <p style="font-size:12px;color:var(--ink-500);margin-top:14px;line-height:1.6;">
        Implementation note: wire this button to a Supabase Edge Function that runs the Google/Microsoft OAuth flow
        and stores only a token reference (via Supabase Vault) in <code>connected_mailboxes</code> — never the raw token here.
      </p>
    </div>`);
}
function connectMailbox(provider){ toast(`Wire this button to your OAuth edge function for ${provider}.`); }

// ============================================================================
// RECORD WORKSPACE — full detail view: Overview + Timeline + Notes + Open/
// Closed activities, shared across modules (Zoho's record-page pattern).
// ============================================================================
const DETAIL_CONFIG = {
  company: { table:'company_master', titleField:'company_name', subField:'company_code',
    kv:[['company_code','Code'],['country_id','Country'],['state_id','State'],['domestic_export','Domestic/Export'],['gst_no','GST No.']] },
  lead: { table:'leads', titleField:'lead_no', subField:'company_id',
    kv:[['company_id','Company'],['internal_company_id','Internal Company'],['source_id','Source'],['closure_status','Status']] },
  enquiry: { table:'enquiries', titleField:'enquiry_no', subField:'company_id',
    kv:[['company_id','Company'],['sf_id','SF Product'],['enquiry_qty','Qty'],['enquiry_amount','Amount'],['pipeline_stage_id','Stage'],['probability','Win Probability (%)']] },
  sf: { table:'sf_master', titleField:'sf_name', subField:'sf_code',
    kv:[['sf_code','Code'],['composition','Composition'],['pack_size','Pack Size'],['hsn_code','HSN Code'],['status','Status']] }
};
async function openDetailPanel(type, id){
  const cfg = DETAIL_CONFIG[type];
  const { data: record, error } = await supa.from(cfg.table).select('*').eq('id', id).single();
  if(error || !record){ toast('Could not load record'); return; }
  const main = document.getElementById('main');
  main.appendChild(el(modalShell('detailModal', '', `
    <div class="record-shell">
      <div class="record-side">
        <div class="card">
          <div class="record-avatar">${initials(record[cfg.titleField])}</div>
          <div class="record-title">${esc(record[cfg.titleField])||'–'}</div>
          <div class="record-sub mono">${esc(record[cfg.subField])||''}</div>
          ${record.tags ? `<div style="margin-bottom:10px;">${tagsHtml(record.tags)}</div>` : ''}
          <div class="kv-list">
            ${cfg.kv.map(([f,label])=>`<div class="kv-item"><div class="kv-label">${label}</div><div class="kv-value">${record[f]??'–'}</div></div>`).join('')}
          </div>
        </div>
        <div class="card">
          <div class="card-title" style="margin-bottom:8px;">Quick actions</div>
          <div style="display:flex;flex-direction:column;gap:8px;">
            <button class="btn secondary small" style="justify-content:flex-start;" onclick="quickCreateTaskFor('${type}','${id}','task')">${icon('tasks')} Add task</button>
            <button class="btn secondary small" style="justify-content:flex-start;" onclick="quickCreateTaskFor('${type}','${id}','call')">${icon('phone')} Log a call</button>
            <button class="btn secondary small" style="justify-content:flex-start;" onclick="quickCreateTaskFor('${type}','${id}','meeting')">${icon('meeting')} Schedule meeting</button>
          </div>
        </div>
      </div>
      <div>
        <div class="tabs" id="detailTabs">
          <div class="tab active" data-dtab="overview">Overview</div>
          <div class="tab" data-dtab="timeline">Timeline</div>
          <div class="tab" data-dtab="opentasks">Open Activities</div>
          <div class="tab" data-dtab="notes">Notes</div>
        </div>
        <div id="detailOverview">
          <div class="card">
            <div class="card-title">Field details</div>
            <div class="kv-grid">
              ${cfg.kv.map(([f,label])=>`<div class="kv-item"><div class="kv-label">${label}</div><div class="kv-value">${record[f]??'–'}</div></div>`).join('')}
            </div>
          </div>
        </div>
        <div id="detailTimeline" style="display:none;">
          <div class="card">
            <div id="timelineList"></div>
            <div class="composer">
              <textarea id="activityNote" placeholder="Log a note or call..."></textarea>
              <button class="btn small" id="logActivityBtn">Log</button>
            </div>
          </div>
        </div>
        <div id="detailOpenTasks" style="display:none;">
          <div class="card"><div id="openTaskList"></div></div>
        </div>
        <div id="detailNotes" style="display:none;">
          <div class="card">
            <div id="notesList"></div>
            <div class="composer">
              <textarea id="noteBody" placeholder="Write a note..."></textarea>
              <button class="btn small" id="addNoteBtn">Add</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  `, true, true)));
  openModal('detailModal');
  document.getElementById('detailModal').querySelector('.modal').classList.add('xwide');
  document.querySelectorAll('#detailTabs .tab').forEach(t=>{
    t.onclick = ()=>{
      document.querySelectorAll('#detailTabs .tab').forEach(x=>x.classList.remove('active')); t.classList.add('active');
      ['overview','timeline','opentasks','notes'].forEach(k=>{
        document.getElementById('detail'+k[0].toUpperCase()+k.slice(1)).style.display = (k===t.dataset.dtab.replace('opentasks','opentasks')) ? 'block':'none';
      });
      document.getElementById('detailOverview').style.display = t.dataset.dtab==='overview' ? 'block':'none';
      document.getElementById('detailTimeline').style.display = t.dataset.dtab==='timeline' ? 'block':'none';
      document.getElementById('detailOpenTasks').style.display = t.dataset.dtab==='opentasks' ? 'block':'none';
      document.getElementById('detailNotes').style.display = t.dataset.dtab==='notes' ? 'block':'none';
      if(t.dataset.dtab==='timeline') loadTimeline(type, id);
      if(t.dataset.dtab==='opentasks') loadOpenTasksFor(type, id);
      if(t.dataset.dtab==='notes') loadNotesFor(type, id);
    };
  });
  document.getElementById('logActivityBtn').onclick = ()=> logActivity(type, id);
  document.getElementById('addNoteBtn').onclick = ()=> addNote(type, id);
}
async function loadTimeline(type, id){
  const { data, error } = await supa.from('activities').select('*').eq('record_type', type).eq('record_id', id).order('created_at',{ascending:false});
  const box = document.getElementById('timelineList');
  if(error || !data || !data.length){ box.innerHTML = `<div class="empty-state" style="padding:24px 4px;">No activity logged yet.</div>`; return; }
  box.innerHTML = data.map(a=>`
    <div class="timeline-item">
      <div class="timeline-ic ${a.activity_type}">${icon(a.activity_type==='call'?'phone':(a.activity_type==='meeting'?'meeting':'note'))}</div>
      <div class="timeline-body"><div class="tl-title">${a.activity_type[0].toUpperCase()+a.activity_type.slice(1)}</div>
      <div class="tl-text">${esc(a.body)||''}</div><div class="tl-time">${timeAgo(a.created_at)}</div></div>
    </div>`).join('');
}
async function logActivity(type, id){
  const body = document.getElementById('activityNote').value.trim(); if(!body) return;
  const { error } = await supa.from('activities').insert({ record_type:type, record_id:id, activity_type:'note', body, created_by: currentUser?.id });
  if(error){ toast('Error: '+error.message); return; }
  document.getElementById('activityNote').value='';
  loadTimeline(type, id);
}
async function loadOpenTasksFor(type, id){
  const box = document.getElementById('openTaskList');
  try{
    const { data, error } = await supa.from('tasks').select('*').eq('record_type', type).eq('record_id', id).order('due_date',{ascending:true});
    if(error) throw error;
    if(!data || !data.length){ box.innerHTML = `<div class="empty-state" style="padding:24px 4px;">No tasks linked to this record yet.</div>`; return; }
    box.innerHTML = data.map(t=>`
      <div class="checklist-row ${t.status==='completed'?'done':''}">
        <input type="checkbox" ${t.status==='completed'?'checked':''} onchange="toggleTaskStatus('${t.id}', this.checked); this.closest('.checklist-row').classList.toggle('done', this.checked)">
        <div class="cl-title">${esc(t.title)}</div>
        <span class="cl-meta">${t.due_date?new Date(t.due_date).toLocaleDateString():'No date'}</span>
        <span class="pill ${t.priority}">${t.priority}</span>
      </div>`).join('');
  }catch(e){ box.innerHTML = `<div class="empty-state" style="padding:24px 4px;">Run migration_v3_zoho_style.sql to enable linked tasks.</div>`; }
}
async function loadNotesFor(type, id){
  const box = document.getElementById('notesList');
  try{
    const { data, error } = await supa.from('notes').select('*').eq('record_type', type).eq('record_id', id).order('created_at',{ascending:false});
    if(error) throw error;
    if(!data || !data.length){ box.innerHTML = `<div class="empty-state" style="padding:24px 4px;">No notes yet.</div>`; return; }
    box.innerHTML = data.map(n=>`
      <div class="timeline-item"><div class="timeline-ic">${icon('note')}</div>
      <div class="timeline-body"><div class="tl-text">${esc(n.body)}</div><div class="tl-time">${timeAgo(n.created_at)}</div></div></div>`).join('');
  }catch(e){ box.innerHTML = `<div class="empty-state" style="padding:24px 4px;">Run migration_v3_zoho_style.sql to enable Notes.</div>`; }
}
async function addNote(type, id){
  const body = document.getElementById('noteBody').value.trim(); if(!body) return;
  const { error } = await supa.from('notes').insert({ record_type:type, record_id:id, body, created_by: currentUser?.id });
  if(error){ toast('Error: '+error.message); return; }
  document.getElementById('noteBody').value='';
  loadNotesFor(type, id);
}
function quickCreateTaskFor(type, id, kind){
  document.getElementById('main').appendChild(el(modalShell('quickTaskModal', `New ${kind}`, `
    <div class="form-grid">
      <div class="form-group full"><label class="required">Title</label><input id="qt_title"></div>
      <div class="form-group"><label>Due Date</label><input type="date" id="qt_due"></div>
      <div class="form-group"><label>Priority</label><select id="qt_priority"><option value="normal">Normal</option><option value="high">High</option><option value="low">Low</option></select></div>
    </div>`, true)));
  openModal('quickTaskModal');
  document.getElementById('quickTaskModal').querySelector('.modal-footer')?.remove();
  const footer = el(`<div class="modal-footer"><button class="btn secondary" onclick="closeModal('quickTaskModal')">Cancel</button><button class="btn" id="qtSaveBtn">Save</button></div>`);
  document.getElementById('quickTaskModal').querySelector('.modal').appendChild(footer);
  document.getElementById('qtSaveBtn').onclick = async ()=>{
    const title = document.getElementById('qt_title').value.trim(); if(!title) return;
    const { error } = await supa.from('tasks').insert({
      title, activity_kind:kind, priority: document.getElementById('qt_priority').value,
      due_date: document.getElementById('qt_due').value || null,
      record_type:type, record_id:id, owner_id: currentUser.id, created_by: currentUser.id, status:'open'
    });
    if(error){ toast('Error: '+error.message); return; }
    toast(`${kind[0].toUpperCase()+kind.slice(1)} added`); closeModal('quickTaskModal');
    if(document.getElementById('openTaskList')) loadOpenTasksFor(type, id);
    refreshNavCounts(); refreshNotifDot();
  };
}

// ============================================================================
// SHARED HELPERS
// ============================================================================
function emptyState(iconName, title, sub){
  return `<div class="empty-state">${icon(iconName,'es-icon')}<div class="es-title">${title}</div><div>${sub||''}</div></div>`;
}
function modalShell(id, title, bodyHtml, skipSave, hideHeader){
  let saveFn = "toast('Not wired yet')";
  if(id==='companyModal') saveFn = 'saveCompany()';
  if(id==='contactModal') saveFn = 'saveContact()';
  if(id==='leadModal') saveFn = 'saveLead()';
  if(id==='enquiryModal') saveFn = 'saveEnquiry()';
  if(id==='sfModal') saveFn = 'saveSF()';
  if(id==='taskModal') saveFn = 'saveTask()';
  return `
    <div class="modal-overlay" id="${id}">
      <div class="modal ${id==='enquiryModal'?'wide':''}">
        ${hideHeader ? `<div class="modal-close" style="float:right;cursor:pointer;" onclick="closeModal('${id}');this.closest('.modal-overlay').remove()">${icon('x')}</div>` :
          `<div class="modal-head"><h2>${title}</h2><button class="modal-close" onclick="closeModal('${id}')">${icon('x')}</button></div>`}
        ${bodyHtml}
        ${skipSave && id!=='detailModal' ? '' : (id==='detailModal' ? '' : `<div class="modal-footer">
          <button class="btn secondary" onclick="closeModal('${id}')">Cancel</button>
          <button class="btn" onclick="${saveFn}">Save</button>
        </div>`)}
      </div>
    </div>`;
}
function openModal(id){ document.getElementById(id).classList.add('open'); }
function closeModal(id){ const m = document.getElementById(id); m?.classList.remove('open'); if(id==='detailModal'||id==='quickTaskModal') setTimeout(()=>m?.remove(), 200); }

async function populateMasterDropdown(selectId, table, labelField='name'){
  const select = document.getElementById(selectId); if(!select) return;
  const { data, error } = await supa.from(table).select('*'); if(error || !data) return;
  data.forEach(row=>{ const opt = document.createElement('option'); opt.value = row.id; opt.textContent = row[labelField] || row.name; select.appendChild(opt); });
}

// State depends on Country (state_master.country_id) — repopulate whenever
// the Country dropdown changes, instead of showing every state up front.
async function populateStateDropdown(selectId, countryId){
  const select = document.getElementById(selectId); if(!select) return;
  select.innerHTML = '<option value="">— Select country first —</option>';
  if(!countryId) return;
  const { data, error } = await supa.from('state_master').select('*').eq('country_id', countryId);
  if(error || !data) return;
  select.innerHTML = '';
  data.forEach(row=>{ const opt = document.createElement('option'); opt.value = row.id; opt.textContent = row.name; select.appendChild(opt); });
}

function startEnquiryFromLead(id){ document.querySelector('[data-page="enquiries"]').click(); }
function assignMailToLead(threadId){ toast('Create lead from thread '+threadId); }
function assignMailToEnquiry(threadId){ toast('Attach thread '+threadId+' to a deal'); }
window.__navTo = function(page){
  document.querySelectorAll('.nav-item').forEach(i=>i.classList.remove('active'));
  document.querySelector(`[data-page="${page}"]`)?.classList.add('active');
  pages[page]();
};

// ============================================================================
// INIT — nothing to do here now; app only renders after loadCurrentUserAndEnter()
// runs (either via the login form or the resumed-session check above).
// ============================================================================
</script>
</body>
</html>
