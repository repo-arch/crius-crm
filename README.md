<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Crius CRM</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=Roboto+Mono:wght@500&display=swap');

  /* ============================== TOKENS ============================== */
  :root{
    --canvas:#F4F6FA;
    --card:#FFFFFF;
    --line:#E3E8F0;
    --line-soft:#EEF1F6;

    --ink-900:#10182B;
    --ink-700:#2B3548;
    --ink-500:#5B6579;
    --ink-400:#8791A3;
    --ink-300:#AEB6C4;

    --brand-900:#0A3B33;
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
    --shadow-lg:0 16px 40px rgba(10,17,32,.16);
    --topbar-h:58px;
  }
  *{box-sizing:border-box;}
  html,body{height:100%;}
  body{margin:0;font-family:'Inter',Arial,sans-serif;background:var(--canvas);color:var(--ink-900);font-size:13.5px;-webkit-font-smoothing:antialiased;}
  code,.mono{font-family:'Roboto Mono',monospace;}
  h1,h2,h3{font-family:'Inter',Arial,sans-serif;letter-spacing:-.01em;}
  a{color:inherit;}
  ::selection{background:var(--brand-100);}
  ::-webkit-scrollbar{width:9px;height:9px;}
  ::-webkit-scrollbar-thumb{background:#D6DCE6;border-radius:20px;border:2px solid var(--canvas);}
  #app{display:flex;height:100vh;}
  svg.icon{width:16px;height:16px;stroke:currentColor;fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round;flex-shrink:0;display:block;}

  /* ============================== SIDEBAR ============================== */
  #sidebar{width:230px;background:var(--sidebar);color:var(--sidebar-text);flex-shrink:0;display:flex;flex-direction:column;transition:width .16s ease;position:relative;}
  #sidebar.collapsed{width:66px;}
  #sidebar.collapsed .brand-text,#sidebar.collapsed .nav-label,#sidebar.collapsed .nav-group-label,#sidebar.collapsed .nav-item span.lbl{display:none;}
  #sidebar.collapsed .nav-item{justify-content:center;}
  #sidebar.collapsed .brand{justify-content:center;padding:0 0 18px;}

  .brand{padding:18px 18px 16px;display:flex;align-items:center;gap:10px;border-bottom:1px solid var(--sidebar-line);margin-bottom:6px;}
  .brand-mark{width:30px;height:30px;border-radius:8px;background:linear-gradient(140deg,var(--brand-500),var(--brand-900) 85%);flex-shrink:0;display:flex;align-items:center;justify-content:center;color:#fff;font-weight:800;font-size:13px;font-family:'Inter';}
  .brand-text .brand-name{color:var(--sidebar-text-hi);font-weight:700;font-size:14.5px;letter-spacing:-.01em;line-height:1.2;}
  .brand-text .brand-sub{color:#5D6E8C;font-size:10px;letter-spacing:.6px;text-transform:uppercase;font-weight:600;}

  .nav-scroll{flex:1;overflow-y:auto;padding:4px 10px 10px;}
  .nav-group-label{font-size:10px;text-transform:uppercase;letter-spacing:1.1px;color:#4A5A7A;padding:16px 10px 6px;font-weight:700;}
  .nav-item{padding:8px 10px;cursor:pointer;font-size:13px;display:flex;align-items:center;gap:11px;border-radius:8px;font-weight:500;color:var(--sidebar-text);margin-bottom:1px;}
  .nav-item svg{opacity:.8;}
  .nav-item:hover{background:var(--sidebar-hi);color:var(--sidebar-text-hi);}
  .nav-item.active{background:linear-gradient(90deg,rgba(21,163,140,.22),rgba(21,163,140,.05));color:#fff;box-shadow:inset 2px 0 0 var(--brand-500);}
  .nav-item.active svg{opacity:1;color:var(--brand-500);}

  .sidebar-foot{padding:10px;border-top:1px solid var(--sidebar-line);}
  .collapse-btn{width:100%;display:flex;align-items:center;justify-content:center;gap:8px;padding:8px;border-radius:8px;background:transparent;border:none;color:var(--sidebar-text);cursor:pointer;font-size:12px;font-family:inherit;}
  .collapse-btn:hover{background:var(--sidebar-hi);color:#fff;}

  /* ============================== SHELL / TOPBAR ============================== */
  #shell{flex:1;display:flex;flex-direction:column;min-width:0;}
  #topbar{height:var(--topbar-h);background:var(--card);border-bottom:1px solid var(--line);display:flex;align-items:center;justify-content:space-between;padding:0 20px;flex-shrink:0;gap:16px;}
  .topbar-left{display:flex;align-items:center;gap:14px;flex:1;min-width:0;}
  .search-box{position:relative;max-width:380px;flex:1;}
  .search-box svg{position:absolute;left:11px;top:50%;transform:translateY(-50%);color:var(--ink-400);}
  .search-box input{width:100%;padding:8px 12px 8px 34px;border:1px solid var(--line);border-radius:8px;font-size:12.5px;background:var(--canvas);font-family:inherit;color:var(--ink-900);}
  .search-box input:focus{outline:none;border-color:var(--brand-500);background:#fff;box-shadow:0 0 0 3px var(--brand-100);}

  .topbar-right{display:flex;align-items:center;gap:8px;}
  .icon-btn{width:32px;height:32px;border-radius:8px;border:1px solid transparent;background:transparent;display:flex;align-items:center;justify-content:center;color:var(--ink-500);cursor:pointer;position:relative;}
  .icon-btn:hover{background:var(--canvas);border-color:var(--line);color:var(--ink-900);}
  .dot-badge{position:absolute;top:5px;right:6px;width:6px;height:6px;border-radius:50%;background:var(--red-500);border:1.5px solid #fff;}

  .quickcreate{position:relative;}
  .qc-menu{position:absolute;top:calc(100% + 8px);right:0;background:#fff;border:1px solid var(--line);border-radius:10px;box-shadow:var(--shadow-lg);width:190px;padding:6px;display:none;z-index:60;}
  .qc-menu.open{display:block;}
  .qc-item{display:flex;align-items:center;gap:9px;padding:8px 9px;border-radius:7px;font-size:12.5px;font-weight:600;color:var(--ink-700);cursor:pointer;}
  .qc-item:hover{background:var(--brand-50);color:var(--brand-700);}
  .qc-item svg{color:var(--brand-600);}

  .role-pill{font-size:10.5px;font-weight:700;text-transform:uppercase;letter-spacing:.4px;background:var(--brand-100);color:var(--brand-700);padding:3px 9px;border-radius:20px;}
  .user-chip{display:flex;align-items:center;gap:9px;padding:4px 8px 4px 4px;border-radius:9px;cursor:pointer;}
  .user-chip:hover{background:var(--canvas);}
  .avatar{width:29px;height:29px;border-radius:50%;background:linear-gradient(140deg,var(--brand-500),var(--brand-800,var(--brand-900)));color:#fff;display:flex;align-items:center;justify-content:center;font-weight:700;font-size:11.5px;flex-shrink:0;}

  #main{flex:1;overflow-y:auto;padding:22px 26px 60px;}

  .breadcrumb{display:flex;align-items:center;gap:6px;font-size:11.5px;color:var(--ink-400);font-weight:600;margin-bottom:6px;text-transform:uppercase;letter-spacing:.4px;}
  .breadcrumb .sep{color:var(--ink-300);}
  .page-header{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:20px;gap:16px;flex-wrap:wrap;}
  .page-header h1{font-size:20px;margin:0 0 3px;font-weight:800;letter-spacing:-.02em;}
  .page-sub{font-size:12.5px;color:var(--ink-500);}
  .header-actions{display:flex;gap:8px;flex-shrink:0;}

  /* ============================== BUTTONS ============================== */
  .btn{background:var(--brand-700);color:#fff;border:none;padding:9px 15px;border-radius:8px;font-size:12.5px;cursor:pointer;font-weight:700;font-family:inherit;display:inline-flex;align-items:center;gap:7px;letter-spacing:.1px;transition:background .12s;}
  .btn:hover{background:var(--brand-900);}
  .btn.secondary{background:#fff;color:var(--ink-700);border:1px solid var(--line);font-weight:600;}
  .btn.secondary:hover{background:var(--canvas);border-color:var(--ink-300);}
  .btn.ghost{background:transparent;color:var(--ink-500);padding:6px 8px;font-weight:600;}
  .btn.ghost:hover{color:var(--ink-900);}
  .btn.danger{background:var(--red-500);}
  .btn.danger:hover{background:var(--red-600);}
  .btn.small{padding:6px 11px;font-size:11.5px;}
  .btn:disabled{opacity:.5;cursor:not-allowed;}

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
  .card{background:var(--card);border:1px solid var(--line);border-radius:var(--radius-lg);padding:18px 20px;margin-bottom:16px;box-shadow:var(--shadow-sm);}
  .card-title{font-size:13px;font-weight:700;margin-bottom:14px;display:flex;justify-content:space-between;align-items:center;letter-spacing:-.01em;}
  .card-title .muted{font-size:11px;color:var(--ink-400);font-weight:600;text-transform:none;}

  /* ============================== TABLE ============================== */
  .table-wrap{background:var(--card);border:1px solid var(--line);border-radius:var(--radius-lg);overflow:hidden;box-shadow:var(--shadow-sm);}
  .table-toolbar{display:flex;justify-content:space-between;align-items:center;padding:12px 16px;border-bottom:1px solid var(--line-soft);gap:10px;flex-wrap:wrap;}
  .view-toggle{display:flex;background:var(--canvas);border:1px solid var(--line);border-radius:8px;padding:2px;gap:2px;}
  .view-toggle button{border:none;background:transparent;padding:6px 11px;border-radius:6px;font-size:11.5px;font-weight:700;color:var(--ink-500);cursor:pointer;display:flex;align-items:center;gap:6px;}
  .view-toggle button.active{background:#fff;color:var(--brand-700);box-shadow:var(--shadow-sm);}
  .filter-chip{display:inline-flex;align-items:center;gap:6px;background:var(--canvas);border:1px solid var(--line);border-radius:20px;padding:5px 10px;font-size:11.5px;font-weight:600;color:var(--ink-600);cursor:pointer;}
  .filter-chip:hover{border-color:var(--ink-300);}

  table{width:100%;border-collapse:collapse;}
  th{background:#FAFBFD;text-align:left;padding:10px 16px;font-size:10.5px;color:var(--ink-500);text-transform:uppercase;letter-spacing:.5px;font-weight:700;border-bottom:1px solid var(--line);white-space:nowrap;}
  td{padding:11px 16px;font-size:12.8px;border-bottom:1px solid var(--line-soft);color:var(--ink-700);}
  tbody tr{cursor:pointer;}
  tr:last-child td{border-bottom:none;}
  tr:hover td{background:#FAFBFD;}
  .row-primary{font-weight:700;color:var(--ink-900);}
  .row-actions{display:flex;gap:6px;justify-content:flex-end;}

  .pill{display:inline-block;padding:3px 10px;border-radius:20px;font-size:10.5px;font-weight:700;letter-spacing:.2px;}
  .pill.stage-Quotation{background:var(--amber-100);color:var(--amber-600);}
  .pill.stage-Negotiation{background:var(--blue-100);color:var(--blue-600);}
  .pill.stage-PORaised,.pill.stage-EnquiryRaised,.pill.stage-Existing{background:var(--brand-100);color:var(--brand-700);}
  .pill.stage-OrderLost,.pill.stage-NotConverted{background:var(--red-100);color:var(--red-600);}
  .pill.stage-New{background:var(--blue-100);color:var(--blue-600);}
  .pill.role-pill{background:var(--ink-100,#EEF1F6);color:var(--ink-700);}

  /* ============================== KANBAN ============================== */
  .kanban{display:flex;gap:14px;overflow-x:auto;padding-bottom:6px;}
  .kanban-col{flex:0 0 270px;background:#EEF1F7;border-radius:var(--radius-lg);padding:10px;max-height:calc(100vh - 260px);display:flex;flex-direction:column;}
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

  .tabs{display:flex;gap:2px;margin-bottom:18px;border-bottom:1px solid var(--line);}
  .tab{padding:9px 14px;cursor:pointer;font-size:12.5px;color:var(--ink-500);border-bottom:2px solid transparent;font-weight:700;}
  .tab:hover{color:var(--ink-900);}
  .tab.active{color:var(--brand-700);border-bottom:2px solid var(--brand-600);}

  /* ============================== MODALS ============================== */
  .modal-overlay{position:fixed;inset:0;background:rgba(10,16,30,0.52);display:none;align-items:flex-start;justify-content:center;padding:44px 20px;overflow-y:auto;z-index:70;backdrop-filter:blur(1px);}
  .modal-overlay.open{display:flex;}
  .modal{background:#fff;border-radius:14px;width:100%;max-width:760px;padding:24px 26px;box-shadow:var(--shadow-lg);}
  .modal.wide{max-width:920px;}
  .modal-head{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:16px;}
  .modal h2{margin:0;font-size:16px;font-weight:800;letter-spacing:-.01em;}
  .modal-close{background:none;border:none;font-size:18px;color:var(--ink-400);cursor:pointer;padding:2px 6px;border-radius:6px;}
  .modal-close:hover{background:var(--canvas);color:var(--ink-900);}
  .modal-footer{display:flex;justify-content:flex-end;gap:10px;margin-top:20px;padding-top:16px;border-top:1px solid var(--line);}

  /* Detail panel */
  .detail-summary{display:flex;gap:16px;align-items:center;padding-bottom:16px;margin-bottom:16px;border-bottom:1px solid var(--line);}
  .detail-avatar{width:46px;height:46px;border-radius:12px;background:var(--brand-100);color:var(--brand-700);display:flex;align-items:center;justify-content:center;font-weight:800;font-size:16px;flex-shrink:0;}
  .detail-title{font-size:16.5px;font-weight:800;letter-spacing:-.01em;}
  .detail-meta{font-size:12px;color:var(--ink-500);margin-top:2px;}
  .kv-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px 20px;margin-bottom:6px;}
  .kv-item .kv-label{font-size:10.5px;text-transform:uppercase;letter-spacing:.4px;color:var(--ink-400);font-weight:700;}
  .kv-item .kv-value{font-size:13px;color:var(--ink-900);font-weight:600;margin-top:2px;}

  .activity-item{display:flex;gap:10px;padding:11px 0;border-bottom:1px solid var(--line-soft);}
  .activity-item:last-child{border-bottom:none;}
  .activity-ic{width:28px;height:28px;border-radius:8px;background:var(--brand-50);color:var(--brand-700);display:flex;align-items:center;justify-content:center;flex-shrink:0;}
  .activity-body .a-title{font-size:12.5px;font-weight:700;color:var(--ink-900);}
  .activity-body .a-text{font-size:12px;color:var(--ink-600);margin-top:2px;}
  .activity-body .a-time{font-size:10.5px;color:var(--ink-400);margin-top:3px;font-weight:600;}
  .activity-composer{display:flex;gap:8px;margin-top:14px;padding-top:14px;border-top:1px solid var(--line);}
  .activity-composer textarea{flex:1;min-height:44px;}

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
        <div style="font-size:13px;color:#A9C4BE;margin-top:12px;max-width:340px;line-height:1.6;">Leads, product-wise enquiries, quotes and pipeline — one workspace across every internal company and territory.</div>
      </div>
      <div style="display:flex;gap:22px;font-size:11.5px;color:#8FB3AA;font-weight:600;">
        <div>Multi-company</div><div>Role-based access</div><div>Pipeline analytics</div>
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
      <div class="nav-group-label">Workspace</div>
      <div class="nav-item active" data-page="dashboard"></div>
      <div class="nav-item" data-page="companies"></div>
      <div class="nav-item" data-page="contacts"></div>
      <div class="nav-item" data-page="leads"></div>
      <div class="nav-item" data-page="enquiries"></div>
      <div class="nav-item" data-page="mail"></div>
      <div class="nav-item" data-page="quotes"></div>
      <div class="nav-item" data-page="projects"></div>
      <div class="nav-item" data-page="reports"></div>

      <div class="nav-group-label admin-only" id="setupLabel">Setup — Admin</div>
      <div class="nav-item admin-only" data-page="sfmaster"></div>
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
          <input id="globalSearch" placeholder="Search companies, leads, enquiries…">
        </div>
      </div>
      <div class="topbar-right">
        <div class="quickcreate">
          <button class="btn small" id="qcBtn"><svg class="icon" viewBox="0 0 24 24" style="width:14px;height:14px;"><path d="M12 5v14M5 12h14"/></svg>Create</button>
          <div class="qc-menu" id="qcMenu">
            <div class="qc-item" data-qc="companies"><svg class="icon" viewBox="0 0 24 24"><path d="M3 21h18M6 21V7l6-4 6 4v14M9 21v-6h6v6"/></svg>Company</div>
            <div class="qc-item" data-qc="contacts"><svg class="icon" viewBox="0 0 24 24"><circle cx="12" cy="8" r="3.5"/><path d="M5 20c1-4 4-6 7-6s6 2 7 6"/></svg>Contact</div>
            <div class="qc-item" data-qc="leads"><svg class="icon" viewBox="0 0 24 24"><path d="M3 5h18M3 5l7 8v6l4-2v-4l7-8"/></svg>Lead</div>
            <div class="qc-item" data-qc="enquiries"><svg class="icon" viewBox="0 0 24 24"><path d="M6 3h9l5 5v13H6z"/><path d="M14 3v5h5"/></svg>Enquiry</div>
          </div>
        </div>
        <button class="icon-btn" title="Notifications"><svg class="icon" viewBox="0 0 24 24"><path d="M6 8a6 6 0 0112 0c0 5 2 6 2 6H4s2-1 2-6z"/><path d="M10 20a2 2 0 004 0"/></svg><span class="dot-badge"></span></button>
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

const PIPELINE_STAGES = ["Quotation","Negotiation","P.O. Raised","Order Lost"];
const STAGE_COLOR = { "Quotation":"var(--amber-500)", "Negotiation":"var(--blue-500)", "P.O. Raised":"var(--brand-500)", "Order Lost":"var(--red-500)" };

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
  arrowUp:'<path d="M12 19V5M6 11l6-6 6 6"/>'
};
function icon(name, cls){ return `<svg class="icon ${cls||''}" viewBox="0 0 24 24">${ICONS[name]||''}</svg>`; }

const NAV_META = {
  dashboard:{label:'Dashboard',icon:'dashboard'}, companies:{label:'Companies',icon:'building'},
  contacts:{label:'Contacts',icon:'contacts'}, leads:{label:'Leads',icon:'leads'},
  enquiries:{label:'Enquiries',icon:'enquiries'}, mail:{label:'Mail',icon:'mail'},
  quotes:{label:'Quotes',icon:'quotes'}, projects:{label:'Projects',icon:'projects'},
  reports:{label:'Reports',icon:'reports'}, sfmaster:{label:'SF Master',icon:'flask'},
  masters:{label:'Masters',icon:'masters'}, fields:{label:'Custom Fields',icon:'fields'},
  users:{label:'Users & Roles',icon:'users'}, settings:{label:'Mail Integration',icon:'settings'}
};
document.querySelectorAll('.nav-item[data-page]').forEach(item=>{
  const m = NAV_META[item.dataset.page];
  item.innerHTML = icon(m.icon) + `<span class="lbl">${m.label}</span>`;
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

const pages = {
  dashboard: renderDashboard, companies: renderCompanies, contacts: renderContacts, leads: renderLeads,
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
document.addEventListener('click', ()=> document.getElementById('qcMenu').classList.remove('open'));
document.querySelectorAll('.qc-item').forEach(qi=>{
  qi.onclick = ()=>{
    const page = qi.dataset.qc;
    document.querySelectorAll('.nav-item').forEach(i=>i.classList.remove('active'));
    document.querySelector(`[data-page="${page}"]`)?.classList.add('active');
    pages[page]().then(()=>{
      const openers = { companies:'newCompanyBtn', contacts:'newContactBtn', leads:'newLeadBtn', enquiries:'newEnquiryBtn' };
      document.getElementById(openers[page])?.click();
    });
  };
});

// Global search — quick lookup across companies / leads / enquiries
let searchDebounce;
document.getElementById('globalSearch').addEventListener('input',(e)=>{
  clearTimeout(searchDebounce);
  const q = e.target.value.trim();
  if(!q) return;
  searchDebounce = setTimeout(()=> runGlobalSearch(q), 350);
});
async function runGlobalSearch(q){
  const { data } = await supa.from('company_master').select('id,company_name').ilike('company_name', `%${q}%`).limit(5);
  if(data && data.length) toast(`${data.length} matching compan${data.length===1?'y':'ies'} — open Companies to view`);
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
  // On redirect back, onAuthStateChange (below) picks up the session and
  // calls loadCurrentUserAndEnter() — first-time Google sign-ins still need
  // an app_users row created (handled there) with role defaulting to 'user'.
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
    // New signups default to 'user' role — an admin promotes them later
    // from Users & Roles. Internal Company / Division are intentionally
    // not collected at signup — an admin assigns those afterward.
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
    // No app_users row yet — create a starter profile automatically (role
    // always defaults to 'user') instead of blocking login. Covers manual
    // signups where the insert step failed, password-reset logins, Google.
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
  currentRole = profile.role;   // <-- role comes entirely from the DB row tied to this login
  document.getElementById('authScreen').style.display = 'none';
  document.getElementById('app').style.display = 'flex';
  document.getElementById('currentRoleBadge').textContent = currentRole.replace('_',' ');
  document.getElementById('userNameLabel').textContent = profile.full_name;
  document.getElementById('userEmailLabel').textContent = profile.email;
  document.getElementById('userAvatar').textContent = initials(profile.full_name);
  applyRoleVisibility();
  renderDashboard();
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

function pageHeader(main, title, sub, actionsHtml, crumbs){
  main.innerHTML = `
    <div class="breadcrumb">${(crumbs||['Workspace',title]).map((c,i,a)=> i<a.length-1 ? `<span>${c}</span><span class="sep">/</span>` : `<span style="color:var(--ink-600)">${c}</span>`).join('')}</div>
    <div class="page-header">
      <div><h1>${title}</h1><div class="page-sub">${sub||''}</div></div>
      <div class="header-actions">${actionsHtml||''}</div>
    </div>`;
}

// ============================================================================
// DASHBOARD — role-aware, customizable widgets + pipeline chart
// ============================================================================
const ALL_WIDGETS = [
  { key:'open_leads',   label:'Open Leads',              table:'leads',     filter:{closure_status:'open'}, icon:'leads', accent:'var(--blue-500)', accentSoft:'var(--blue-100)' },
  { key:'open_enquiry', label:'Open Enquiries',          table:'enquiries', filter:{}, icon:'enquiries', accent:'var(--brand-500)', accentSoft:'var(--brand-100)' },
  { key:'po_raised',    label:'P.O. Raised (this month)',table:'enquiries', filter:{pipeline_stage_id:'P.O. Raised'}, icon:'flag', accent:'var(--brand-700)', accentSoft:'var(--brand-100)' },
  { key:'order_lost',   label:'Orders Lost (this month)',table:'enquiries', filter:{pipeline_stage_id:'Order Lost'}, icon:'x', accent:'var(--red-500)', accentSoft:'var(--red-100)' },
  { key:'unassigned',   label:'Unassigned Mail',         table:'email_threads', filter:{is_assigned:false}, icon:'mail', accent:'var(--amber-500)', accentSoft:'var(--amber-100)' },
  { key:'team_size',    label:'Team Members',            table:'app_users', filter:{}, icon:'users', accent:'var(--ink-700)', accentSoft:'#EEF1F6' }
];
let activeWidgets = JSON.parse(localStorage.getItem('crm_widgets') || 'null') || ['open_leads','open_enquiry','po_raised','unassigned'];
let pipelineChart = null;

async function renderDashboard(){
  applyRoleVisibility();
  const main = document.getElementById('main');
  pageHeader(main, 'Dashboard', `Scope: ${ROLE_SCOPE[currentRole].label}`,
    `<button class="btn secondary small" id="customizeBtn">${icon('fields')}Customize widgets</button>`, ['Workspace','Dashboard']);
  main.insertAdjacentHTML('beforeend', `
    <div class="kpi-grid" id="kpiGrid"></div>
    <div class="grid-2">
      <div class="card">
        <div class="card-title">Pipeline by stage <span class="muted">Open enquiries, value-weighted</span></div>
        <div style="height:230px;"><canvas id="pipelineCanvas"></canvas></div>
      </div>
      <div class="card">
        <div class="card-title">Recent activity</div>
        <div id="recentActivity"></div>
      </div>
    </div>
  `);
  renderKpiGrid();
  renderPipelineChart();
  renderRecentActivity();
  document.getElementById('customizeBtn').onclick = openWidgetPicker;
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
async function renderRecentActivity(){
  const box = document.getElementById('recentActivity'); if(!box) return;
  const { data, error } = await supa.from('activities').select('*').order('created_at',{ascending:false}).limit(6);
  if(error || !data || !data.length){ box.innerHTML = `<div class="empty-state" style="padding:20px 6px;">Notes and calls logged against records will show up here.</div>`; return; }
  box.innerHTML = data.map(a=>`
    <div class="activity-item">
      <div class="activity-ic">${icon(a.activity_type==='call'?'phone':'note')}</div>
      <div class="activity-body">
        <div class="a-title">${a.title || (a.activity_type[0].toUpperCase()+a.activity_type.slice(1))}</div>
        <div class="a-text">${a.body||''}</div>
        <div class="a-time">${timeAgo(a.created_at)} · ${a.record_type}</div>
      </div>
    </div>`).join('');
}

// ============================================================================
// COMPANIES
// ============================================================================
async function renderCompanies(){
  const main = document.getElementById('main');
  pageHeader(main, 'Companies', 'Company Master — one-time entry per customer',
    `<button class="btn small" id="newCompanyBtn">${icon('plus')}New Company</button>`);
  main.insertAdjacentHTML('beforeend', `
    <div class="table-wrap">
      <div class="table-toolbar"><span class="filter-chip">${icon('building')} All companies</span><span style="font-size:11.5px;color:var(--ink-400);font-weight:600;" id="companyCount"></span></div>
      <table>
      <thead><tr><th>Code</th><th>Company Name</th><th>Country</th><th>State</th><th>Domestic/Export</th><th></th></tr></thead>
      <tbody id="companyRows"><tr><td colspan="6" class="empty-state">Loading…</td></tr></tbody>
    </table></div>
    ${modalShell('companyModal','New Company', companyFormHtml())}
  `);
  document.getElementById('newCompanyBtn').onclick = ()=> {
    openModal('companyModal');
    populateMasterDropdown('f_country', 'country_master');
    populateStateDropdown('f_state', '');
    document.getElementById('f_country').onchange = (e)=> populateStateDropdown('f_state', e.target.value);
  };
  const { data, error } = await supa.from('company_master').select('*').order('created_at',{ascending:false});
  const rows = document.getElementById('companyRows');
  if(error || !data || !data.length){
    rows.innerHTML = `<tr><td colspan="6">${emptyState('building','No companies yet','Add your first company to get started.')}</td></tr>`; return;
  }
  document.getElementById('companyCount').textContent = `${data.length} total`;
  rows.innerHTML = data.map(c=>`
    <tr onclick="openDetailPanel('company','${c.id}')">
      <td class="mono">${c.company_code}</td><td class="row-primary">${c.company_name}</td><td>${c.country_id||'–'}</td>
      <td>${c.state_id||'–'}</td><td><span class="pill stage-New">${c.domestic_export||'–'}</span></td>
      <td class="row-actions" onclick="event.stopPropagation()"><button class="btn secondary small" onclick="openDetailPanel('company','${c.id}')">View</button></td></tr>`).join('');
}
function companyFormHtml(){
  return `<div class="form-grid">
    <div class="form-group"><label class="required">Company Name</label><input id="f_company_name"></div>
    <div class="form-group"><label class="required">Country</label><select id="f_country"></select></div>
    <div class="form-group"><label class="required">State</label><select id="f_state"></select></div>
    <div class="form-group"><label class="required">Domestic / Export</label>
      <select id="f_domestic_export"><option>Domestic</option><option>Export</option></select></div>
    <div class="form-group"><label>GST No.</label><input id="f_gst"></div>
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
    company_code: 'C' + Date.now().toString().slice(-6)
  };
  const { error } = await supa.from('company_master').insert(payload);
  if(error){ toast('Error: '+error.message); return; }
  toast('Company saved'); closeModal('companyModal'); renderCompanies();
}

// ============================================================================
// CONTACTS
// ============================================================================
async function renderContacts(){
  const main = document.getElementById('main');
  pageHeader(main, 'Contacts', 'People at each company you deal with',
    `<button class="btn small" id="newContactBtn">${icon('plus')}New Contact</button>`);
  main.insertAdjacentHTML('beforeend', `
    <div class="table-wrap"><table>
      <thead><tr><th>Name</th><th>Company</th><th>Designation</th><th>Email</th><th>Phone</th><th></th></tr></thead>
      <tbody id="contactRows"><tr><td colspan="6" class="empty-state">Loading…</td></tr></tbody>
    </table></div>
    ${modalShell('contactModal','New Contact', `<div class="form-grid">
      <div class="form-group full"><label class="required">Company</label><select id="ct_company"></select></div>
      <div class="form-group"><label class="required">Contact Name</label><input id="ct_name"></div>
      <div class="form-group"><label>Designation</label><input id="ct_designation"></div>
      <div class="form-group"><label>Email</label><input type="email" id="ct_email"></div>
      <div class="form-group"><label>Phone</label><input id="ct_phone"></div>
      <div class="form-group"><label><input type="checkbox" id="ct_primary" style="width:auto;vertical-align:middle;"> Primary contact for this company</label></div>
    </div>`)}
  `);
  document.getElementById('newContactBtn').onclick = ()=>{ openModal('contactModal'); populateMasterDropdown('ct_company','company_master','company_name'); };
  const { data, error } = await supa.from('contact_master').select('*, company_master(company_name)').order('created_at',{ascending:false});
  const rows = document.getElementById('contactRows');
  if(error || !data || !data.length){ rows.innerHTML = `<tr><td colspan="6">${emptyState('contacts','No contacts yet','Add the people you correspond with at each company.')}</td></tr>`; return; }
  rows.innerHTML = data.map(c=>`
    <tr><td class="row-primary">${c.contact_name}${c.is_primary?' <span class="pill stage-PORaised">Primary</span>':''}</td>
      <td>${c.company_master?.company_name || c.company_id}</td><td>${c.designation||'–'}</td>
      <td>${c.email||'–'}</td><td>${c.phone||'–'}</td>
      <td class="row-actions"><button class="btn secondary small" onclick="toast('Open contact detail for ${c.contact_name}')">View</button></td></tr>`).join('');
}
async function saveContact(){
  const payload = {
    contact_code: 'CT' + Date.now().toString().slice(-6),
    company_id: document.getElementById('ct_company').value,
    contact_name: document.getElementById('ct_name').value,
    designation: document.getElementById('ct_designation').value,
    email: document.getElementById('ct_email').value,
    phone: document.getElementById('ct_phone').value,
    is_primary: document.getElementById('ct_primary').checked
  };
  const { error } = await supa.from('contact_master').insert(payload);
  if(error){ toast('Error: '+error.message); return; }
  toast('Contact saved'); closeModal('contactModal'); renderContacts();
}

// ============================================================================
// LEADS
// ============================================================================
async function renderLeads(){
  const main = document.getElementById('main');
  pageHeader(main, 'Leads', `Scope: ${ROLE_SCOPE[currentRole].label}`,
    `<button class="btn small" id="newLeadBtn">${icon('plus')}New Lead</button>`);
  main.insertAdjacentHTML('beforeend', `
    <div class="table-wrap"><table>
      <thead><tr><th>Lead No.</th><th>Company</th><th>Internal Co.</th><th>Source</th><th>Status</th><th></th></tr></thead>
      <tbody id="leadRows"><tr><td colspan="6" class="empty-state">Loading…</td></tr></tbody>
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
  const { data, error } = await supa.from('leads').select('*').order('created_at',{ascending:false});
  const rows = document.getElementById('leadRows');
  if(error || !data || !data.length){
    rows.innerHTML = `<tr><td colspan="6">${emptyState('leads','No leads yet','Capture an enquiry as soon as it comes in.')}</td></tr>`; return;
  }
  rows.innerHTML = data.map(l=>`
    <tr onclick="openDetailPanel('lead','${l.id}')">
      <td class="mono">${l.lead_no}</td><td class="row-primary">${l.company_id}</td><td>${l.internal_company_id}</td>
      <td>${l.source_id}</td><td><span class="pill ${pillClass(l.closure_status)}">${l.closure_status||'Open'}</span></td>
      <td class="row-actions" onclick="event.stopPropagation()"><button class="btn secondary small" onclick="openDetailPanel('lead','${l.id}')">View</button>
      ${l.closure_status==='enquiry_raised' ? `<button class="btn small" onclick="startEnquiryFromLead('${l.id}')">Add Products</button>` : ''}
      </td></tr>`).join('');
}
function leadFormHtml(){
  return `<div class="tabs"><div class="tab active">Via Lead</div><div class="tab">Direct-to-Enquiry</div></div>
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
    closure_status: 'open'
  };
  const { error } = await supa.from('leads').insert(payload);
  if(error){ toast('Error: '+error.message); return; }
  toast('Lead saved'); closeModal('leadModal'); renderLeads();
}

// ============================================================================
// ENQUIRIES (product-wise) — List + Kanban pipeline view
// ============================================================================
let productLineCount = 0;
let enquiryView = 'kanban';
async function renderEnquiries(){
  const main = document.getElementById('main');
  pageHeader(main, 'Enquiries', 'Product-wise entry — one line per SF',
    `<button class="btn small" id="newEnquiryBtn">${icon('plus')}New Enquiry</button>`);
  main.insertAdjacentHTML('beforeend', `
    <div class="table-wrap" style="margin-bottom:16px;">
      <div class="table-toolbar">
        <div class="view-toggle">
          <button data-view="kanban" class="${enquiryView==='kanban'?'active':''}">${icon('kanban')}Pipeline</button>
          <button data-view="list" class="${enquiryView==='list'?'active':''}">${icon('list')}List</button>
        </div>
        <span style="font-size:11.5px;color:var(--ink-400);font-weight:600;" id="enquiryCount"></span>
      </div>
      <div id="enquiryBody" style="padding:14px;"></div>
    </div>
    ${modalShell('enquiryModal','New Enquiry — Product-wise Entry', `<div id="productLines"></div>
      <button class="btn secondary small" id="addProductLineBtn">${icon('plus')}Add another product</button>`)}
  `);
  document.querySelectorAll('.view-toggle button').forEach(b=> b.onclick = ()=>{ enquiryView = b.dataset.view; renderEnquiries(); });
  document.getElementById('newEnquiryBtn').onclick = ()=>{
    document.getElementById('productLines').innerHTML=''; productLineCount = 0; addProductLine(); openModal('enquiryModal');
  };
  document.getElementById('addProductLineBtn').onclick = addProductLine;

  const { data, error } = await supa.from('enquiries').select('*').order('created_at',{ascending:false});
  const body = document.getElementById('enquiryBody');
  if(error || !data || !data.length){ body.innerHTML = emptyState('enquiries','No enquiries yet','Create one from a lead or directly here.'); return; }
  document.getElementById('enquiryCount').textContent = `${data.length} total`;
  enquiryView === 'kanban' ? renderEnquiryKanban(body, data) : renderEnquiryList(body, data);
}
function renderEnquiryKanban(container, data){
  container.style.padding = '0';
  const cols = PIPELINE_STAGES.map(stage=>{
    const items = data.filter(e => (e.pipeline_stage_id||'Quotation') === stage);
    const total = items.reduce((s,e)=> s + (Number(e.enquiry_amount)||0), 0);
    return `
      <div class="kanban-col">
        <div class="kanban-col-head">
          <div class="kanban-col-title"><span class="kanban-dot" style="background:${STAGE_COLOR[stage]}"></span>${stage}</div>
          <span class="kanban-count">${items.length}</span>
        </div>
        <div class="kanban-col-total">${total ? '₹'+money(total)+' total' : ''}</div>
        <div class="kanban-cards">
          ${items.length ? items.map(e=>`
            <div class="kanban-card" onclick="openDetailPanel('enquiry','${e.id}')">
              <div class="kc-title">${e.enquiry_no}</div>
              <div class="kc-sub">${e.company_id} · SF ${e.sf_id?.toString().slice(0,8)||''}</div>
              <div class="kc-foot"><span class="kc-amount">${e.enquiry_amount? '₹'+money(e.enquiry_amount) : '–'}</span>
              <button class="btn secondary small" style="padding:3px 8px;" onclick="event.stopPropagation();openQuoteBuilder('${e.id}')">Quote</button></div>
            </div>`).join('') : `<div class="kanban-empty">No enquiries at this stage</div>`}
        </div>
      </div>`;
  }).join('');
  container.innerHTML = `<div class="kanban">${cols}</div>`;
}
function renderEnquiryList(container, data){
  container.style.padding = '0';
  container.innerHTML = `<table>
    <thead><tr><th>Enquiry No.</th><th>Company</th><th>SF (Product)</th><th>Qty</th><th>Amount</th><th>Stage</th><th></th></tr></thead>
    <tbody>${data.map(e=>`
      <tr onclick="openDetailPanel('enquiry','${e.id}')">
        <td class="mono">${e.enquiry_no}</td><td class="row-primary">${e.company_id}</td><td>${e.sf_id}</td>
        <td>${e.enquiry_qty||'–'}</td><td>${e.enquiry_amount?'₹'+money(e.enquiry_amount):'–'}</td>
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
        <div class="form-group"><label>Dosage Form</label><select id="pl_dosage_${idx}"></select></div>
        <div class="form-group"><label>Enquiry Qty</label><input type="number" id="pl_qty_${idx}"></div>
        <div class="form-group"><label>Qty Unit</label><select id="pl_qtyunit_${idx}"></select></div>
        <div class="form-group"><label>Enquiry Rate</label><input type="number" step="0.01" id="pl_rate_${idx}"></div>
        <div class="form-group"><label>Target Rate</label><input type="number" step="0.01" id="pl_target_${idx}"></div>
        <div class="form-group"><label>Pipeline Stage</label>
          <select id="pl_stage_${idx}">${PIPELINE_STAGES.map(s=>`<option>${s}</option>`).join('')}</select></div>
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
  populateMasterDropdown(`pl_internal_company_${idx}`, 'internal_company_master');
  populateMasterDropdown(`pl_source_${idx}`, 'source_master');
  populateMasterDropdown(`pl_sf_${idx}`, 'sf_master', 'sf_name', true);
  populateMasterDropdown(`pl_dosage_${idx}`, 'dosage_form_master');
  populateMasterDropdown(`pl_qtyunit_${idx}`, 'qty_unit_master');
}
async function saveEnquiry(){
  const lines = document.querySelectorAll('.product-line'); const inserts = [];
  lines.forEach(line=>{
    const idx = line.dataset.idx;
    inserts.push({
      enquiry_no: 'E' + Date.now().toString().slice(-6) + '-' + idx,
      internal_company_id: document.getElementById(`pl_internal_company_${idx}`).value,
      source_id: document.getElementById(`pl_source_${idx}`).value,
      sf_id: document.getElementById(`pl_sf_${idx}`).value,
      dosage_form_id: document.getElementById(`pl_dosage_${idx}`).value || null,
      enquiry_qty: parseFloat(document.getElementById(`pl_qty_${idx}`).value) || null,
      qty_unit_id: document.getElementById(`pl_qtyunit_${idx}`).value || null,
      enquiry_rate: parseFloat(document.getElementById(`pl_rate_${idx}`).value) || null,
      target_rate: parseFloat(document.getElementById(`pl_target_${idx}`).value) || null,
      pipeline_stage_id: document.getElementById(`pl_stage_${idx}`).value,
      po_qty: parseFloat(document.getElementById(`pl_po_qty_${idx}`)?.value) || null,
      po_rate: parseFloat(document.getElementById(`pl_po_rate_${idx}`)?.value) || null,
      order_lost_reason: document.getElementById(`pl_lost_reason_${idx}`)?.value || null
    });
  });
  const { error } = await supa.from('enquiries').insert(inserts);
  if(error){ toast('Error: '+error.message); return; }
  toast(`${inserts.length} enquiry line(s) saved`); closeModal('enquiryModal'); renderEnquiries();
}

// ============================================================================
// SF MASTER — full product master with fixed + customizable fields
// ============================================================================
async function renderSFMaster(){
  const main = document.getElementById('main');
  pageHeader(main, 'SF Master', 'Product / formulation master — the source of truth for every enquiry line',
    `<button class="btn small" id="newSFBtn">${icon('plus')}New SF Product</button>`);
  main.insertAdjacentHTML('beforeend', `
    <div class="table-wrap"><table>
      <thead><tr><th>SF Code</th><th>SF Name</th><th>Composition</th><th>Category</th><th>Dosage Form</th><th>Pack Size</th><th>Status</th><th></th></tr></thead>
      <tbody id="sfRows"><tr><td colspan="8" class="empty-state">Loading…</td></tr></tbody>
    </table></div>
    ${modalShell('sfModal','New SF Product', sfFormHtml())}
  `);
  document.getElementById('newSFBtn').onclick = ()=> openModal('sfModal');
  populateMasterDropdown('sf_category', 'category_master');
  populateMasterDropdown('sf_dosage', 'dosage_form_master');
  renderSFCustomFieldInputs();

  const { data, error } = await supa.from('sf_master').select('*').order('created_at',{ascending:false});
  const rows = document.getElementById('sfRows');
  if(error || !data || !data.length){
    rows.innerHTML = `<tr><td colspan="8">${emptyState('flask','No SF products yet','New products can also be generated on the fly from Enquiry entry.')}</td></tr>`; return;
  }
  rows.innerHTML = data.map(s=>`
    <tr><td class="mono">${s.sf_code}</td><td class="row-primary">${s.sf_name}</td><td>${s.composition||'–'}</td>
      <td>${s.category_id||'–'}</td><td>${s.dosage_form_id||'–'}</td><td>${s.pack_size||'–'}</td>
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
      return `<div class="form-group"><label ${f.is_required?'class="required"':''}>${f.label}</label>
        <select id="${inputId}">${(f.dropdown_options||[]).map(o=>`<option>${o}</option>`).join('')}</select></div>`;
    }
    const type = f.field_type==='checkbox' ? 'checkbox' : f.field_type==='number' ? 'number' : f.field_type==='date' ? 'date' : 'text';
    return `<div class="form-group"><label ${f.is_required?'class="required"':''}>${f.label}</label><input type="${type}" id="${inputId}"></div>`;
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
  toast('SF product saved'); closeModal('sfModal'); renderSFMaster();
}

// ============================================================================
// MAIL
// ============================================================================
async function renderMail(){
  const main = document.getElementById('main');
  pageHeader(main, 'Mail', 'Inbound mail matched to your open leads and enquiries');
  main.insertAdjacentHTML('beforeend', `
    <div class="tabs">
      <div class="tab active" data-mailtab="unassigned">Unassigned</div>
      <div class="tab" data-mailtab="assigned">Assigned to Lead/Enquiry</div>
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
      <div><strong>${t.subject||'(no subject)'}</strong><div style="font-size:12px;color:var(--ink-500)">Thread: ${t.provider_thread_id}</div></div>
      ${tab==='unassigned' ? `<div><button class="btn small" onclick="assignMailToLead('${t.id}')">Add as Lead</button>
        <button class="btn secondary small" onclick="assignMailToEnquiry('${t.id}')">Add to Enquiry</button></div>`
        : `<span class="pill stage-EnquiryRaised">Linked</span>`}
    </div>`).join('');
}

// ============================================================================
// QUOTES
// ============================================================================
async function renderQuotes(){
  const main = document.getElementById('main');
  pageHeader(main, 'Quotes', 'Every quote sent, generated straight from an enquiry');
  main.insertAdjacentHTML('beforeend', `
    <div class="table-wrap"><table><thead><tr><th>Quote No.</th><th>Enquiry</th><th>Amount</th><th>Sent</th><th></th></tr></thead>
    <tbody id="quoteRows"><tr><td colspan="5" class="empty-state">Loading…</td></tr></tbody></table></div>`);
  const { data, error } = await supa.from('quotes').select('*').order('created_at',{ascending:false});
  const rows = document.getElementById('quoteRows');
  if(error || !data || !data.length){ rows.innerHTML = `<tr><td colspan="5">${emptyState('quotes','No quotes yet','Build one from an Enquiry row.')}</td></tr>`; return; }
  rows.innerHTML = data.map(q=>`<tr><td class="mono">${q.quote_no}</td><td>${q.enquiry_id}</td><td>${q.quoted_amount?'₹'+money(q.quoted_amount):'–'}</td>
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
  main.insertAdjacentHTML('beforeend', emptyState('projects','Project boards render here','Same pattern as Leads/Enquiries — Supabase tables: projects / project_tasks.'));
}

// ============================================================================
// REPORTS — customizable builder
// ============================================================================
const REPORT_MODULES = {
  leads:     { table:'leads', fields:['lead_no','company_id','internal_company_id','source_id','closure_status'] },
  enquiries: { table:'enquiries', fields:['enquiry_no','company_id','sf_id','enquiry_qty','enquiry_amount','pipeline_stage_id','po_value'] },
  companies: { table:'company_master', fields:['company_code','company_name','country_id','domestic_export'] }
};
let reportSelectedFields = [];
async function renderReports(){
  const main = document.getElementById('main');
  pageHeader(main, 'Reports', 'Build a custom report — pick a module, choose columns, run.');
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
  rows.innerHTML = data.map(r=>`<tr><td>${r.name}</td><td style="text-align:right"><button class="btn secondary small" onclick="deleteMasterValue('${table}','${r.id}')">Remove</button></td></tr>`).join('');
}
async function addMasterValue(table){
  const val = document.getElementById('newMasterValue').value.trim(); if(!val) return;
  const { error } = await supa.from(table).insert({ name: val });
  if(error){ toast('Error: '+error.message); return; }
  document.getElementById('newMasterValue').value=''; loadMasterRows(table);
}
async function deleteMasterValue(table,id){ await supa.from(table).delete().eq('id', id); loadMasterRows(table); }

// ============================================================================
// CUSTOM FIELDS — covers Company / Lead / Enquiry / SF Master / Project
// ============================================================================
async function renderCustomFields(){
  const main = document.getElementById('main');
  pageHeader(main, 'Custom Fields', 'Add fields to any module without a developer');
  main.insertAdjacentHTML('beforeend', `
    <div class="tabs" id="fieldModuleTabs">
      <div class="tab active" data-module="company">Company</div>
      <div class="tab" data-module="lead">Lead</div>
      <div class="tab" data-module="enquiry">Enquiry</div>
      <div class="tab" data-module="sf">SF Master</div>
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
  box.innerHTML = data.map(f=>`<span class="field-chip">${f.label} <span class="type-tag">(${f.field_type}${f.is_required?', required':''})</span>
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
  pageHeader(main, 'Users & Roles', 'Role hierarchy: User → Manager → Super Manager → Admin. A Manager sees their direct reports\\' records; a Super Manager sees every team below them.',
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
  rows.innerHTML = data.map(u=>`<tr><td class="row-primary">${u.full_name}</td><td>${u.email}</td>
    <td><span class="pill role-pill">${u.role}</span></td><td>${u.reports_to||'–'}</td>
    <td class="row-actions"><button class="btn secondary small">Edit</button></td></tr>`).join('');
}

// ============================================================================
// SETTINGS — mail integration
// ============================================================================
async function renderSettings(){
  const main = document.getElementById('main');
  pageHeader(main, 'Mail Integration', 'Connect a mailbox to route replies straight into leads and enquiries');
  main.insertAdjacentHTML('beforeend', `
    <div class="card">
      <p style="margin:0;line-height:1.6;color:var(--ink-700);">Each user connects their own inbox. Once connected, incoming mail is matched to open leads/enquiries by
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
// RECORD DETAIL PANEL — Overview + Activity timeline, shared across modules
// ============================================================================
const DETAIL_CONFIG = {
  company: { table:'company_master', titleField:'company_name', subField:'company_code',
    kv:[['company_code','Code'],['country_id','Country'],['state_id','State'],['domestic_export','Domestic/Export'],['gst_no','GST No.']] },
  lead: { table:'leads', titleField:'lead_no', subField:'company_id',
    kv:[['company_id','Company'],['internal_company_id','Internal Company'],['source_id','Source'],['closure_status','Status']] },
  enquiry: { table:'enquiries', titleField:'enquiry_no', subField:'company_id',
    kv:[['company_id','Company'],['sf_id','SF Product'],['enquiry_qty','Qty'],['enquiry_amount','Amount'],['pipeline_stage_id','Stage']] },
  sf: { table:'sf_master', titleField:'sf_name', subField:'sf_code',
    kv:[['sf_code','Code'],['composition','Composition'],['pack_size','Pack Size'],['hsn_code','HSN Code'],['status','Status']] }
};
async function openDetailPanel(type, id){
  const cfg = DETAIL_CONFIG[type];
  const { data: record, error } = await supa.from(cfg.table).select('*').eq('id', id).single();
  if(error || !record){ toast('Could not load record'); return; }
  const main = document.getElementById('main');
  main.appendChild(el(modalShell('detailModal', '', `
    <div class="detail-summary">
      <div class="detail-avatar">${initials(record[cfg.titleField])}</div>
      <div><div class="detail-title">${record[cfg.titleField]||'–'}</div><div class="detail-meta mono">${record[cfg.subField]||''}</div></div>
    </div>
    <div class="tabs" id="detailTabs">
      <div class="tab active" data-dtab="overview">Overview</div>
      <div class="tab" data-dtab="activity">Activity</div>
    </div>
    <div id="detailOverview">
      <div class="kv-grid">
        ${cfg.kv.map(([f,label])=>`<div class="kv-item"><div class="kv-label">${label}</div><div class="kv-value">${record[f]??'–'}</div></div>`).join('')}
      </div>
    </div>
    <div id="detailActivity" style="display:none;">
      <div id="activityList"></div>
      <div class="activity-composer">
        <textarea id="activityNote" placeholder="Log a note or call..."></textarea>
        <button class="btn small" id="logActivityBtn">Log</button>
      </div>
    </div>
  `, true, true)));
  document.querySelector('#detailModal .modal h2').remove?.();
  openModal('detailModal');
  document.querySelectorAll('#detailTabs .tab').forEach(t=>{
    t.onclick = ()=>{
      document.querySelectorAll('#detailTabs .tab').forEach(x=>x.classList.remove('active')); t.classList.add('active');
      document.getElementById('detailOverview').style.display = t.dataset.dtab==='overview' ? 'block':'none';
      document.getElementById('detailActivity').style.display = t.dataset.dtab==='activity' ? 'block':'none';
      if(t.dataset.dtab==='activity') loadActivities(type, id);
    };
  });
  document.getElementById('logActivityBtn').onclick = ()=> logActivity(type, id);
}
async function loadActivities(type, id){
  const { data, error } = await supa.from('activities').select('*').eq('record_type', type).eq('record_id', id).order('created_at',{ascending:false});
  const box = document.getElementById('activityList');
  if(error || !data || !data.length){ box.innerHTML = `<div class="empty-state" style="padding:24px 4px;">No activity logged yet.</div>`; return; }
  box.innerHTML = data.map(a=>`
    <div class="activity-item">
      <div class="activity-ic">${icon(a.activity_type==='call'?'phone':'note')}</div>
      <div class="activity-body"><div class="a-title">${a.activity_type[0].toUpperCase()+a.activity_type.slice(1)}</div>
      <div class="a-text">${a.body||''}</div><div class="a-time">${timeAgo(a.created_at)}</div></div>
    </div>`).join('');
}
async function logActivity(type, id){
  const body = document.getElementById('activityNote').value.trim(); if(!body) return;
  const { error } = await supa.from('activities').insert({ record_type:type, record_id:id, activity_type:'note', body, created_by: currentUser?.id });
  if(error){ toast('Error: '+error.message); return; }
  document.getElementById('activityNote').value='';
  loadActivities(type, id);
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
function closeModal(id){ const m = document.getElementById(id); m?.classList.remove('open'); if(id==='detailModal') setTimeout(()=>m?.remove(), 200); }

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
function assignMailToEnquiry(threadId){ toast('Attach thread '+threadId+' to an enquiry'); }
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
