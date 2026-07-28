<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CRM Platform</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Roboto+Mono:wght@500&display=swap');

  :root{
    --ink-900:#10192B; --ink-700:#26334D; --ink-500:#5B6B85; --ink-300:#98A5B8; --ink-100:#E7ECF2;
    --surface:#F6F8FB; --card:#FFFFFF; --border:#DFE5EC;
    --brand-900:#0D3B36; --brand-700:#146356; --brand-500:#1D8A76; --brand-100:#E3F3EE;
    --amber-500:#B5791E; --amber-100:#FBF1DF;
    --blue-500:#2E5EA8; --blue-100:#E7EEF9;
    --red-500:#B23B32; --red-100:#FBEAE8;
    --sidebar:#0F1B2E; --sidebar-hi:#16263F; --sidebar-text:#8FA0BA;
    --radius:10px; --shadow:0 1px 2px rgba(16,25,43,.04), 0 4px 14px rgba(16,25,43,.06);
  }
  *{box-sizing:border-box;}
  body{margin:0;font-family:'Inter',Arial,sans-serif;background:var(--surface);color:var(--ink-900);font-size:14px;}
  code, .mono{font-family:'Roboto Mono',monospace;}
  #app{display:flex;height:100vh;}

  /* ---------- Sidebar ---------- */
  #sidebar{width:236px;background:var(--sidebar);color:var(--sidebar-text);flex-shrink:0;display:flex;flex-direction:column;padding:18px 0;}
  .brand{padding:2px 22px 20px;display:flex;align-items:center;gap:10px;}
  .brand-mark{width:28px;height:28px;border-radius:7px;background:linear-gradient(135deg,var(--brand-500),var(--brand-900));flex-shrink:0;}
  .brand-name{color:#fff;font-weight:700;font-size:15px;letter-spacing:.2px;}
  .brand-sub{color:var(--sidebar-text);font-size:10.5px;letter-spacing:.5px;text-transform:uppercase;}

  .nav-group-label{font-size:10px;text-transform:uppercase;letter-spacing:1.2px;color:#4C5B75;padding:18px 22px 6px;font-weight:600;}
  .nav-item{padding:9px 22px;cursor:pointer;font-size:13px;display:flex;align-items:center;gap:11px;border-left:3px solid transparent;font-weight:500;}
  .nav-item svg{width:16px;height:16px;opacity:.85;flex-shrink:0;}
  .nav-item:hover{background:rgba(255,255,255,0.04);color:#DCE4F0;}
  .nav-item.active{background:var(--sidebar-hi);color:#fff;border-left:3px solid var(--brand-500);}

  /* ---------- Topbar ---------- */
  #shell{flex:1;display:flex;flex-direction:column;min-width:0;}
  #topbar{height:60px;background:var(--card);border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;padding:0 26px;flex-shrink:0;}
  .role-switch{display:flex;align-items:center;gap:8px;font-size:12.5px;color:var(--ink-500);}
  .role-switch select{border:1px solid var(--border);border-radius:7px;padding:6px 10px;font-size:12.5px;font-family:inherit;background:#fff;font-weight:600;color:var(--ink-700);}
  .user-chip{display:flex;align-items:center;gap:9px;}
  .avatar{width:30px;height:30px;border-radius:50%;background:var(--brand-100);color:var(--brand-700);display:flex;align-items:center;justify-content:center;font-weight:700;font-size:12.5px;}

  #main{flex:1;overflow-y:auto;padding:26px 30px 60px;}
  .page-header{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:22px;}
  .page-header h1{font-size:19px;margin:0 0 3px;font-weight:700;}
  .page-sub{font-size:12.5px;color:var(--ink-500);}
  .header-actions{display:flex;gap:8px;}

  /* ---------- Buttons ---------- */
  .btn{background:var(--brand-700);color:#fff;border:none;padding:9px 15px;border-radius:7px;font-size:12.5px;cursor:pointer;font-weight:600;font-family:inherit;display:inline-flex;align-items:center;gap:6px;}
  .btn:hover{background:var(--brand-900);}
  .btn.secondary{background:#fff;color:var(--ink-700);border:1px solid var(--border);}
  .btn.secondary:hover{background:var(--surface);}
  .btn.ghost{background:transparent;color:var(--ink-500);padding:6px 8px;}
  .btn.danger{background:var(--red-500);}
  .btn.small{padding:5px 10px;font-size:11.5px;}

  /* ---------- Cards / KPIs ---------- */
  .kpi-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:14px;margin-bottom:22px;}
  .kpi-card{background:var(--card);border:1px solid var(--border);border-radius:var(--radius);padding:16px 18px;box-shadow:var(--shadow);position:relative;}
  .kpi-card .kpi-label{font-size:11px;text-transform:uppercase;letter-spacing:.5px;color:var(--ink-500);font-weight:600;}
  .kpi-card .kpi-value{font-size:26px;font-weight:700;margin-top:6px;}
  .kpi-card .kpi-delta{font-size:11.5px;margin-top:4px;color:var(--brand-500);font-weight:600;}
  .kpi-card .kpi-remove{position:absolute;top:10px;right:10px;background:none;border:none;color:var(--ink-300);cursor:pointer;font-size:13px;}
  .add-widget-card{border:1.5px dashed var(--border);border-radius:var(--radius);display:flex;align-items:center;justify-content:center;color:var(--ink-500);cursor:pointer;font-size:12.5px;font-weight:600;min-height:88px;}
  .add-widget-card:hover{border-color:var(--brand-500);color:var(--brand-700);}

  .card{background:var(--card);border:1px solid var(--border);border-radius:var(--radius);padding:20px;margin-bottom:18px;box-shadow:var(--shadow);}
  .card-title{font-size:13.5px;font-weight:700;margin-bottom:14px;display:flex;justify-content:space-between;align-items:center;}

  /* ---------- Table ---------- */
  .table-wrap{background:var(--card);border:1px solid var(--border);border-radius:var(--radius);overflow:hidden;box-shadow:var(--shadow);}
  table{width:100%;border-collapse:collapse;}
  th{background:#FAFBFD;text-align:left;padding:11px 14px;font-size:11px;color:var(--ink-500);text-transform:uppercase;letter-spacing:.5px;font-weight:700;border-bottom:1px solid var(--border);}
  td{padding:11px 14px;font-size:13px;border-bottom:1px solid var(--border);color:var(--ink-700);}
  tr:last-child td{border-bottom:none;}
  tr:hover td{background:#FAFBFD;}

  .pill{display:inline-block;padding:3px 10px;border-radius:20px;font-size:11px;font-weight:700;}
  .pill.stage-Quotation{background:var(--amber-100);color:var(--amber-500);}
  .pill.stage-Negotiation{background:var(--blue-100);color:var(--blue-500);}
  .pill.stage-PORaised,.pill.stage-EnquiryRaised,.pill.stage-Existing{background:var(--brand-100);color:var(--brand-700);}
  .pill.stage-OrderLost,.pill.stage-NotConverted{background:var(--red-100);color:var(--red-500);}
  .pill.stage-New{background:var(--blue-100);color:var(--blue-500);}
  .role-pill{background:var(--ink-100);color:var(--ink-700);}

  /* ---------- Forms ---------- */
  .form-grid{display:grid;grid-template-columns:1fr 1fr;gap:14px;}
  .form-grid.cols-3{grid-template-columns:1fr 1fr 1fr;}
  .form-group{display:flex;flex-direction:column;gap:5px;}
  .form-group.full{grid-column:1/-1;}
  label{font-size:11.5px;color:var(--ink-500);font-weight:700;letter-spacing:.2px;}
  label.required::after{content:" *";color:var(--red-500);}
  input,select,textarea{padding:8px 11px;border:1px solid var(--border);border-radius:7px;font-size:13px;font-family:inherit;background:#fff;color:var(--ink-900);}
  input:focus,select:focus,textarea:focus{outline:none;border-color:var(--brand-500);box-shadow:0 0 0 3px var(--brand-100);}
  textarea{resize:vertical;min-height:60px;}

  .product-line{border:1px solid var(--border);border-radius:var(--radius);padding:16px;margin-bottom:12px;position:relative;background:#FCFDFE;}
  .product-line .remove-line{position:absolute;top:12px;right:12px;background:none;border:none;color:var(--red-500);cursor:pointer;font-size:16px;font-weight:700;}
  .line-index{font-size:11px;font-weight:700;color:var(--brand-700);text-transform:uppercase;letter-spacing:.5px;margin-bottom:10px;}

  .tabs{display:flex;gap:4px;margin-bottom:20px;border-bottom:1px solid var(--border);}
  .tab{padding:9px 16px;cursor:pointer;font-size:13px;color:var(--ink-500);border-bottom:2px solid transparent;font-weight:600;}
  .tab.active{color:var(--brand-700);border-bottom:2px solid var(--brand-700);}

  .modal-overlay{position:fixed;inset:0;background:rgba(15,25,45,0.5);display:none;align-items:flex-start;justify-content:center;padding:44px 20px;overflow-y:auto;z-index:50;}
  .modal-overlay.open{display:flex;}
  .modal{background:#fff;border-radius:12px;width:100%;max-width:760px;padding:26px;box-shadow:0 20px 60px rgba(0,0,0,.25);}
  .modal h2{margin-top:0;font-size:16.5px;font-weight:700;}
  .modal-footer{display:flex;justify-content:flex-end;gap:10px;margin-top:20px;padding-top:16px;border-top:1px solid var(--border);}

  .empty-state{text-align:center;padding:56px 20px;color:var(--ink-500);font-size:13px;}
  .toast{position:fixed;bottom:24px;right:24px;background:var(--ink-900);color:#fff;padding:12px 18px;border-radius:8px;font-size:13px;display:none;z-index:100;box-shadow:0 8px 24px rgba(0,0,0,.25);}

  .field-chip{display:inline-flex;align-items:center;gap:6px;background:var(--surface);border:1px solid var(--border);border-radius:20px;padding:5px 12px 5px 12px;font-size:12px;font-weight:600;margin:0 6px 6px 0;}
  .field-chip .type-tag{color:var(--ink-300);font-weight:500;}
  .field-chip button{background:none;border:none;color:var(--red-500);cursor:pointer;font-size:13px;padding:0;}

  .report-builder-grid{display:grid;grid-template-columns:280px 1fr;gap:20px;}
  .field-picker-list{display:flex;flex-direction:column;gap:4px;max-height:360px;overflow-y:auto;}
  .field-picker-item{display:flex;align-items:center;gap:8px;padding:7px 8px;border-radius:6px;font-size:12.5px;cursor:pointer;}
  .field-picker-item:hover{background:var(--surface);}

  .scope-note{font-size:11.5px;color:var(--ink-500);background:var(--brand-100);border-radius:7px;padding:9px 12px;margin-bottom:16px;display:flex;align-items:center;gap:8px;}
</style>
</head>
<body>

<div id="authScreen" style="min-height:100vh;display:flex;align-items:center;justify-content:center;background:var(--surface);font-family:'Inter',Arial,sans-serif;">
  <div style="width:420px;background:#fff;border:1px solid var(--border);border-radius:14px;padding:32px;box-shadow:0 20px 50px rgba(16,25,43,.08);">
    <div style="display:flex;align-items:center;gap:10px;margin-bottom:22px;">
      <div style="width:30px;height:30px;border-radius:8px;background:linear-gradient(135deg,#1D8A76,#0D3B36);"></div>
      <div style="font-weight:700;font-size:16px;color:#10192B;">Crius CRM</div>
    </div>
    <div class="tabs" style="margin-bottom:18px;">
      <div class="tab active" id="loginTab" onclick="switchAuthTab('login')">Log In</div>
      <div class="tab" id="signupTab" onclick="switchAuthTab('signup')">Sign Up</div>
    </div>

    <button class="btn secondary" style="width:100%;justify-content:center;gap:10px;margin-bottom:10px;" onclick="authWithGoogle()">
      <svg width="16" height="16" viewBox="0 0 48 48"><path fill="#FFC107" d="M43.6 20.5H42V20H24v8h11.3C33.8 32.7 29.3 36 24 36c-6.6 0-12-5.4-12-12s5.4-12 12-12c3.1 0 5.9 1.2 8 3.1l5.7-5.7C34.5 6.1 29.5 4 24 4 12.9 4 4 12.9 4 24s8.9 20 20 20 20-8.9 20-20c0-1.3-.1-2.7-.4-3.5z"/><path fill="#FF3D00" d="M6.3 14.7l6.6 4.8C14.6 15.4 18.9 12 24 12c3.1 0 5.9 1.2 8 3.1l5.7-5.7C34.5 6.1 29.5 4 24 4 16.3 4 9.6 8.3 6.3 14.7z"/><path fill="#4CAF50" d="M24 44c5.3 0 10.1-2 13.7-5.4l-6.3-5.3C29.4 34.9 26.8 36 24 36c-5.3 0-9.7-3.4-11.3-8.1l-6.6 5.1C9.5 39.6 16.2 44 24 44z"/><path fill="#1976D2" d="M43.6 20.5H42V20H24v8h11.3c-.8 2.2-2.2 4.1-4 5.4l6.3 5.3C41.4 35.4 44 30.1 44 24c0-1.3-.1-2.7-.4-3.5z"/></svg>
      Continue with Google
    </button>
    <div style="display:flex;align-items:center;gap:10px;margin:16px 0;color:var(--ink-300);font-size:11.5px;">
      <div style="flex:1;height:1px;background:var(--border);"></div> OR <div style="flex:1;height:1px;background:var(--border);"></div>
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
    <div id="authError" style="color:var(--red-500);font-size:12px;margin-top:10px;"></div>
    <p style="font-size:11px;color:var(--ink-500);margin-top:14px;text-align:center;">
      New accounts start as <strong>User</strong> role — an Admin upgrades access afterward in Users &amp; Roles.
    </p>
  </div>
</div>

<div id="app" style="display:none;">

  <div id="sidebar">
    <div class="brand">
      <div class="brand-mark"></div>
      <div><div class="brand-name">Crius CRM</div><div class="brand-sub">Sales Platform</div></div>
    </div>

    <div class="nav-group-label">Workspace</div>
    <div class="nav-item active" data-page="dashboard">📊 Dashboard</div>
    <div class="nav-item" data-page="companies">🏢 Companies</div>
    <div class="nav-item" data-page="leads">📥 Leads</div>
    <div class="nav-item" data-page="enquiries">📄 Enquiries</div>
    <div class="nav-item" data-page="mail">✉️ Mail</div>
    <div class="nav-item" data-page="quotes">🧾 Quotes</div>
    <div class="nav-item" data-page="projects">🗂️ Projects</div>
    <div class="nav-item" data-page="reports">📈 Reports</div>

    <div class="nav-group-label" id="setupLabel">Setup — Admin</div>
    <div class="nav-item admin-only" data-page="sfmaster">🧪 SF Master</div>
    <div class="nav-item admin-only" data-page="masters">⚙️ Masters</div>
    <div class="nav-item admin-only" data-page="fields">🧩 Custom Fields</div>
    <div class="nav-item admin-only" data-page="users">👥 User & Roles</div>
    <div class="nav-item admin-only" data-page="settings">🔌 Mail Integration</div>
  </div>

  <div id="shell">
    <div id="topbar">
      <div class="role-switch">
        Signed in as
        <span class="pill role-pill" id="currentRoleBadge">–</span>
      </div>
      <div class="user-chip">
        <div class="avatar" id="userAvatar">–</div>
        <div>
          <div style="font-weight:600;font-size:13px;" id="userNameLabel">–</div>
          <div style="font-size:11px;color:var(--ink-500)" id="userEmailLabel">–</div>
        </div>
        <button class="btn ghost small" onclick="signOut()" title="Sign out">⏻</button>
      </div>
    </div>
    <div id="main"></div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2/dist/umd/supabase.js"></script>
<script>
// ============================================================================
// 1. CONNECT TO YOUR SUPABASE PROJECT
// ============================================================================
const SUPABASE_URL = "https://ozhyjniulqxtcinrlqym.supabase.co";
const SUPABASE_ANON_KEY = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im96aHlqbml1bHF4dGNpbnJscXltIiwicm9sZSI6ImFub24iLCJpYXQiOjE3ODUyMzUxMzcsImV4cCI6MjEwMDgxMTEzN30.sMW_H-nleTVKQdTev2XYD2F8jQwmVMpmEAYB4g4Wols";
const supa = window.supabase.createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
// ============================================================================

const PIPELINE_STAGES = ["Quotation","Negotiation","P.O. Raised","Order Lost"];

// Role scope definitions — mirrors the RLS policies in the SQL schema.
// 'user' sees own records; 'manager'/'super_manager' see their team via
// fn_visible_user_ids(); 'admin' sees everything + setup pages.
const ROLE_SCOPE = {
  user:          { label:'My records only',                     canSeeSetup:false },
  manager:       { label:"My team's records (direct reports)",   canSeeSetup:false },
  super_manager: { label:"All teams under me (multi-level)",     canSeeSetup:false },
  admin:         { label:'Everything, plus Masters & Setup',     canSeeSetup:true  }
};
// currentRole is never chosen by the user — it is read from their
// app_users row after login and is treated as read-only in the UI.
// Permissions/visibility ultimately come from Supabase RLS policies
// (fn_visible_user_ids in the schema), not from this client-side value;
// this just drives which nav items/labels render.
let currentRole = null;
let currentUser = null;

function toast(msg){
  const t = document.getElementById('toast');
  t.textContent = msg; t.style.display='block';
  setTimeout(()=> t.style.display='none', 2600);
}
function pillClass(stage){ return 'stage-' + (stage||'').replace(/[.\s]/g,''); }
function el(html){ const d=document.createElement('div'); d.innerHTML=html.trim(); return d.firstChild; }

const pages = {
  dashboard: renderDashboard, companies: renderCompanies, leads: renderLeads,
  enquiries: renderEnquiries, mail: renderMail, quotes: renderQuotes,
  projects: renderProjects, reports: renderReports, sfmaster: renderSFMaster,
  masters: renderMasters, fields: renderCustomFields, users: renderUsers, settings: renderSettings
};

document.querySelectorAll('.nav-item').forEach(item=>{
  item.addEventListener('click', ()=>{
    document.querySelectorAll('.nav-item').forEach(i=>i.classList.remove('active'));
    item.classList.add('active');
    pages[item.dataset.page]();
  });
});

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
    // from Users & Roles. Nobody can grant themselves a higher role here.
    // Internal Company / Division are intentionally not collected at
    // signup — an admin assigns those afterward from Users & Roles.
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
    // No app_users row yet for this authenticated account — create a starter
    // profile automatically (role always defaults to 'user') instead of
    // blocking login. This covers manual signups where the insert step
    // failed partway, password-reset logins, and Google sign-ins alike.
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
  document.getElementById('currentRoleBadge').textContent = currentRole;
  document.getElementById('userNameLabel').textContent = profile.full_name;
  document.getElementById('userEmailLabel').textContent = profile.email;
  document.getElementById('userAvatar').textContent = profile.full_name.split(' ').map(n=>n[0]).join('').slice(0,2).toUpperCase();
  applyRoleVisibility();
  renderDashboard();
}

// Fires on page load with an existing session, and again right after the
// Google OAuth redirect lands back on this page.
supa.auth.onAuthStateChange((event, session)=>{
  if(session && (event === 'SIGNED_IN' || event === 'INITIAL_SESSION')){
    loadCurrentUserAndEnter();
  }
});

async function signOut(){
  await supa.auth.signOut();
  currentUser = null; currentRole = null;
  document.getElementById('app').style.display = 'none';
  document.getElementById('authScreen').style.display = 'flex';
  document.getElementById('auth_password').value = '';
}

// Session resume and Google OAuth redirect handling are both covered by
// the onAuthStateChange listener above (INITIAL_SESSION fires once on load
// if a session already exists).

function applyRoleVisibility(){
  const canSeeSetup = ROLE_SCOPE[currentRole]?.canSeeSetup;
  document.querySelectorAll('.admin-only').forEach(n=> n.style.display = canSeeSetup ? 'flex' : 'none');
  document.getElementById('setupLabel').style.display = canSeeSetup ? 'block' : 'none';
}

// ============================================================================
// DASHBOARD — role-aware, customizable widgets
// ============================================================================
const ALL_WIDGETS = [
  { key:'open_leads',   label:'Open Leads',              table:'leads',     filter:{closure_status:'open'} },
  { key:'open_enquiry', label:'Open Enquiries',          table:'enquiries', filter:{} },
  { key:'po_raised',    label:'P.O. Raised (this month)',table:'enquiries', filter:{pipeline_stage_id:'P.O. Raised'} },
  { key:'order_lost',   label:'Orders Lost (this month)',table:'enquiries', filter:{pipeline_stage_id:'Order Lost'} },
  { key:'unassigned',   label:'Unassigned Mail',         table:'email_threads', filter:{is_assigned:false} },
  { key:'team_size',    label:'Team Members',            table:'app_users', filter:{} }
];
let activeWidgets = JSON.parse(localStorage.getItem('crm_widgets') || 'null') || ['open_leads','open_enquiry','po_raised','unassigned'];

async function renderDashboard(){
  applyRoleVisibility();
  const main = document.getElementById('main');
  main.innerHTML = `
    <div class="page-header">
      <div><h1>Dashboard</h1><div class="page-sub">Scope: ${ROLE_SCOPE[currentRole].label}</div></div>
      <div class="header-actions"><button class="btn secondary small" id="customizeBtn">⚙ Customize widgets</button></div>
    </div>
    <div class="kpi-grid" id="kpiGrid"></div>
    <div class="card">
      <div class="card-title">Pipeline by stage</div>
      <div class="empty-state">Bar/funnel chart renders here from <code>enquiries</code> grouped by <code>pipeline_stage_id</code> —
      wire your preferred chart lib (e.g. Chart.js via CDN) once live data is flowing.</div>
    </div>
  `;
  renderKpiGrid();
  document.getElementById('customizeBtn').onclick = openWidgetPicker;
}

async function renderKpiGrid(){
  const grid = document.getElementById('kpiGrid');
  grid.innerHTML = '';
  for(const key of activeWidgets){
    const w = ALL_WIDGETS.find(x=>x.key===key);
    if(!w) continue;
    const card = el(`
      <div class="kpi-card">
        <button class="kpi-remove" onclick="removeWidget('${key}')">×</button>
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
  grid.appendChild(el(`<div class="add-widget-card" onclick="openWidgetPicker()">+ Add widget</div>`));
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
        <div class="field-picker-item" onclick="addWidget('${w.key}')"><strong>+</strong> ${w.label}</div>
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

// ============================================================================
// COMPANIES
// ============================================================================
async function renderCompanies(){
  const main = document.getElementById('main');
  main.innerHTML = `
    <div class="page-header"><div><h1>Companies</h1><div class="page-sub">Company Master — one-time entry per customer</div></div>
      <button class="btn" id="newCompanyBtn">+ New Company</button></div>
    <div class="table-wrap"><table>
      <thead><tr><th>Code</th><th>Company Name</th><th>Country</th><th>State</th><th>Domestic/Export</th><th></th></tr></thead>
      <tbody id="companyRows"><tr><td colspan="6" class="empty-state">Loading…</td></tr></tbody>
    </table></div>
    ${modalShell('companyModal','New Company', companyFormHtml())}
  `;
  document.getElementById('newCompanyBtn').onclick = ()=> {
    openModal('companyModal');
    populateMasterDropdown('f_country', 'country_master');
    populateStateDropdown('f_state', '');
    document.getElementById('f_country').onchange = (e)=> populateStateDropdown('f_state', e.target.value);
  };
  const { data, error } = await supa.from('company_master').select('*').order('created_at',{ascending:false});
  const rows = document.getElementById('companyRows');
  if(error || !data || !data.length){
    rows.innerHTML = `<tr><td colspan="6" class="empty-state">No companies yet. Add your first company to get started.</td></tr>`; return;
  }
  rows.innerHTML = data.map(c=>`
    <tr><td class="mono">${c.company_code}</td><td>${c.company_name}</td><td>${c.country_id||'–'}</td>
      <td>${c.state_id||'–'}</td><td><span class="pill stage-New">${c.domestic_export||'–'}</span></td>
      <td><button class="btn secondary small" onclick="viewCompany('${c.id}')">View</button></td></tr>`).join('');
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
// LEADS
// ============================================================================
async function renderLeads(){
  const main = document.getElementById('main');
  main.innerHTML = `
    <div class="page-header"><div><h1>Leads</h1><div class="page-sub">Scope: ${ROLE_SCOPE[currentRole].label}</div></div>
      <button class="btn" id="newLeadBtn">+ New Lead</button></div>
    <div class="table-wrap"><table>
      <thead><tr><th>Lead No.</th><th>Company</th><th>Internal Co.</th><th>Source</th><th>Status</th><th></th></tr></thead>
      <tbody id="leadRows"><tr><td colspan="6" class="empty-state">Loading…</td></tr></tbody>
    </table></div>
    ${modalShell('leadModal','New Lead', leadFormHtml())}
  `;
  document.getElementById('newLeadBtn').onclick = ()=> openModal('leadModal');
  const { data, error } = await supa.from('leads').select('*').order('created_at',{ascending:false});
  const rows = document.getElementById('leadRows');
  if(error || !data || !data.length){
    rows.innerHTML = `<tr><td colspan="6" class="empty-state">No leads yet.</td></tr>`; return;
  }
  rows.innerHTML = data.map(l=>`
    <tr><td class="mono">${l.lead_no}</td><td>${l.company_id}</td><td>${l.internal_company_id}</td>
      <td>${l.source_id}</td><td><span class="pill ${pillClass(l.closure_status)}">${l.closure_status||'Open'}</span></td>
      <td><button class="btn secondary small" onclick="viewLead('${l.id}')">View</button>
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
// ENQUIRIES (product-wise)
// ============================================================================
let productLineCount = 0;
async function renderEnquiries(){
  const main = document.getElementById('main');
  main.innerHTML = `
    <div class="page-header"><div><h1>Enquiries</h1><div class="page-sub">Product-wise entry — one line per SF</div></div>
      <button class="btn" id="newEnquiryBtn">+ New Enquiry</button></div>
    <div class="table-wrap"><table>
      <thead><tr><th>Enquiry No.</th><th>Company</th><th>SF (Product)</th><th>Qty</th><th>Amount</th><th>Stage</th><th></th></tr></thead>
      <tbody id="enquiryRows"><tr><td colspan="7" class="empty-state">Loading…</td></tr></tbody>
    </table></div>
    ${modalShell('enquiryModal','New Enquiry — Product-wise Entry', `<div id="productLines"></div>
      <button class="btn secondary small" id="addProductLineBtn">+ Add another product</button>`)}
  `;
  document.getElementById('newEnquiryBtn').onclick = ()=>{
    document.getElementById('productLines').innerHTML=''; productLineCount = 0; addProductLine(); openModal('enquiryModal');
  };
  document.getElementById('addProductLineBtn').onclick = addProductLine;
  const { data, error } = await supa.from('enquiries').select('*').order('created_at',{ascending:false});
  const rows = document.getElementById('enquiryRows');
  if(error || !data || !data.length){ rows.innerHTML = `<tr><td colspan="7" class="empty-state">No enquiries yet.</td></tr>`; return; }
  rows.innerHTML = data.map(e=>`
    <tr><td class="mono">${e.enquiry_no}</td><td>${e.company_id}</td><td>${e.sf_id}</td>
      <td>${e.enquiry_qty||'–'}</td><td>${e.enquiry_amount||'–'}</td>
      <td><span class="pill ${pillClass(e.pipeline_stage_id)}">${e.pipeline_stage_id||'Quotation'}</span></td>
      <td><button class="btn secondary small" onclick="viewEnquiry('${e.id}')">View</button>
      <button class="btn small" onclick="openQuoteBuilder('${e.id}')">Quote</button></td></tr>`).join('');
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
      <div id="pl_po_block_${idx}" style="display:none;margin-top:12px;padding-top:12px;border-top:1px dashed var(--border);">
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
  main.innerHTML = `
    <div class="page-header"><div><h1>SF Master</h1><div class="page-sub">Product / formulation master — the source of truth for every enquiry line</div></div>
      <button class="btn" id="newSFBtn">+ New SF Product</button></div>
    <div class="table-wrap"><table>
      <thead><tr><th>SF Code</th><th>SF Name</th><th>Composition</th><th>Category</th><th>Dosage Form</th><th>Pack Size</th><th>Status</th><th></th></tr></thead>
      <tbody id="sfRows"><tr><td colspan="8" class="empty-state">Loading…</td></tr></tbody>
    </table></div>
    ${modalShell('sfModal','New SF Product', sfFormHtml())}
  `;
  document.getElementById('newSFBtn').onclick = ()=> openModal('sfModal');
  populateMasterDropdown('sf_category', 'category_master');
  populateMasterDropdown('sf_dosage', 'dosage_form_master');
  renderSFCustomFieldInputs();

  const { data, error } = await supa.from('sf_master').select('*').order('created_at',{ascending:false});
  const rows = document.getElementById('sfRows');
  if(error || !data || !data.length){
    rows.innerHTML = `<tr><td colspan="8" class="empty-state">No SF products yet. New products can also be generated on the fly from Enquiry entry.</td></tr>`; return;
  }
  rows.innerHTML = data.map(s=>`
    <tr><td class="mono">${s.sf_code}</td><td>${s.sf_name}</td><td>${s.composition||'–'}</td>
      <td>${s.category_id||'–'}</td><td>${s.dosage_form_id||'–'}</td><td>${s.pack_size||'–'}</td>
      <td><span class="pill stage-${s.status==='new'?'New':'Existing'}">${s.status||'existing'}</span></td>
      <td><button class="btn secondary small" onclick="viewSF('${s.id}')">View</button></td></tr>`).join('');
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
    <div style="margin-top:10px;"><a href="#" onclick="event.preventDefault(); window.__navTo('fields')" style="font-size:12px;color:var(--brand-700);font-weight:600;">+ Add another field to this form (Custom Fields)</a></div>
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
  main.innerHTML = `
    <div class="page-header"><h1>Mail</h1></div>
    <div class="tabs">
      <div class="tab active" data-mailtab="unassigned">Unassigned</div>
      <div class="tab" data-mailtab="assigned">Assigned to Lead/Enquiry</div>
    </div>
    <div id="mailList"><div class="empty-state">Connect a mailbox in Setup → Mail Integration to see messages here.</div></div>`;
  document.querySelectorAll('[data-mailtab]').forEach(t=>{
    t.onclick = ()=>{ document.querySelectorAll('[data-mailtab]').forEach(x=>x.classList.remove('active')); t.classList.add('active'); loadMail(t.dataset.mailtab); };
  });
  loadMail('unassigned');
}
async function loadMail(tab){
  const { data, error } = await supa.from('email_threads').select('*').eq('is_assigned', tab==='assigned');
  const list = document.getElementById('mailList');
  if(error || !data || !data.length){ list.innerHTML = `<div class="empty-state">No ${tab} mail.</div>`; return; }
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
  main.innerHTML = `<div class="page-header"><h1>Quotes</h1></div>
    <div class="table-wrap"><table><thead><tr><th>Quote No.</th><th>Enquiry</th><th>Amount</th><th>Sent</th><th></th></tr></thead>
    <tbody id="quoteRows"><tr><td colspan="5" class="empty-state">Loading…</td></tr></tbody></table></div>`;
  const { data, error } = await supa.from('quotes').select('*').order('created_at',{ascending:false});
  const rows = document.getElementById('quoteRows');
  if(error || !data || !data.length){ rows.innerHTML = `<tr><td colspan="5" class="empty-state">No quotes yet. Build one from an Enquiry row.</td></tr>`; return; }
  rows.innerHTML = data.map(q=>`<tr><td class="mono">${q.quote_no}</td><td>${q.enquiry_id}</td><td>${q.quoted_amount||'–'}</td>
    <td>${q.sent_at?new Date(q.sent_at).toLocaleDateString():'Not sent'}</td><td><button class="btn secondary small">Send</button></td></tr>`).join('');
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
  document.getElementById('main').innerHTML = `<div class="page-header"><h1>Projects</h1><button class="btn">+ New Project</button></div>
    <div class="empty-state">Project boards render here — same pattern as Leads/Enquiries (Supabase tables: projects / project_tasks).</div>`;
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
  main.innerHTML = `
    <div class="page-header"><div><h1>Reports</h1><div class="page-sub">Build a custom report — pick a module, choose columns, run.</div></div></div>
    <div class="report-builder-grid">
      <div class="card">
        <div class="card-title">1. Module</div>
        <select id="reportModule" style="width:100%;margin-bottom:16px;">
          ${Object.keys(REPORT_MODULES).map(m=>`<option value="${m}">${m[0].toUpperCase()+m.slice(1)}</option>`).join('')}
        </select>
        <div class="card-title">2. Columns</div>
        <div class="field-picker-list" id="reportFieldPicker"></div>
        <button class="btn small" style="margin-top:14px;width:100%;" id="runReportBtn">Run report</button>
      </div>
      <div class="card">
        <div class="card-title">Result</div>
        <div id="reportResult" class="empty-state">Choose columns and click "Run report".</div>
      </div>
    </div>`;
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
  if(error || !data || !data.length){ result.innerHTML = `<div class="empty-state">No rows returned.</div>`; return; }
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
  main.innerHTML = `
    <div class="page-header"><h1>Masters</h1></div>
    <div class="tabs" id="masterTabs">${MASTER_TABLES.map((m,i)=>`<div class="tab ${i===0?'active':''}" data-master="${m.key}">${m.label}</div>`).join('')}</div>
    <div class="card">
      <div style="display:flex;gap:8px;margin-bottom:14px;">
        <input id="newMasterValue" placeholder="Add new value...">
        <button class="btn small" id="addMasterBtn">Add</button>
      </div>
      <table><tbody id="masterRows"></tbody></table>
    </div>`;
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
// CUSTOM FIELDS — now covers 'sf' module too
// ============================================================================
async function renderCustomFields(){
  const main = document.getElementById('main');
  main.innerHTML = `
    <div class="page-header"><h1>Custom Fields</h1></div>
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
        <button class="btn" id="addFieldBtn">+ Add Field</button>
      </div>
    </div>
    <div id="fieldChips" style="margin-bottom:14px;"></div>
  `;
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
  main.innerHTML = `
    <div class="page-header"><div><h1>Users & Roles</h1>
      <div class="page-sub">Role hierarchy: User → Manager → Super Manager → Admin. A Manager sees their direct reports' records; a Super Manager sees every team below them.</div></div>
      <button class="btn" id="inviteUserBtn">+ Invite User</button></div>
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
  `;
  document.getElementById('inviteUserBtn').onclick = ()=> openModal('userModal');
  const { data, error } = await supa.from('app_users').select('*').order('created_at',{ascending:false});
  const rows = document.getElementById('userRows');
  if(error || !data || !data.length){ rows.innerHTML = `<tr><td colspan="5" class="empty-state">No users yet.</td></tr>`; return; }
  rows.innerHTML = data.map(u=>`<tr><td>${u.full_name}</td><td>${u.email}</td>
    <td><span class="pill role-pill">${u.role}</span></td><td>${u.reports_to||'–'}</td>
    <td><button class="btn secondary small">Edit</button></td></tr>`).join('');
}

// ============================================================================
// SETTINGS — mail integration
// ============================================================================
async function renderSettings(){
  document.getElementById('main').innerHTML = `
    <div class="page-header"><h1>Mail Integration</h1></div>
    <div class="card">
      <p>Each user connects their own inbox. Once connected, incoming mail is matched to open leads/enquiries by
      sender + thread; anything unmatched appears under <strong>Mail → Unassigned</strong>.</p>
      <div style="margin-top:14px;display:flex;gap:10px;">
        <button class="btn" onclick="connectMailbox('gmail')">Connect Gmail</button>
        <button class="btn secondary" onclick="connectMailbox('outlook')">Connect Outlook</button>
      </div>
      <p style="font-size:12px;color:var(--ink-500);margin-top:14px;">
        Implementation note: wire this button to a Supabase Edge Function that runs the Google/Microsoft OAuth flow
        and stores only a token reference (via Supabase Vault) in <code>connected_mailboxes</code> — never the raw token here.
      </p>
    </div>`;
}
function connectMailbox(provider){ toast(`Wire this button to your OAuth edge function for ${provider}.`); }

// ============================================================================
// SHARED HELPERS
// ============================================================================
function modalShell(id, title, bodyHtml, skipSave){
  let saveFn = "toast('Not wired yet')";
  if(id==='companyModal') saveFn = 'saveCompany()';
  if(id==='leadModal') saveFn = 'saveLead()';
  if(id==='enquiryModal') saveFn = 'saveEnquiry()';
  if(id==='sfModal') saveFn = 'saveSF()';
  return `
    <div class="modal-overlay" id="${id}">
      <div class="modal">
        <h2>${title}</h2>
        ${bodyHtml}
        <div class="modal-footer">
          <button class="btn secondary" onclick="closeModal('${id}')">Cancel</button>
          ${skipSave ? '' : `<button class="btn" onclick="${saveFn}">Save</button>`}
        </div>
      </div>
    </div>`;
}
function openModal(id){ document.getElementById(id).classList.add('open'); }
function closeModal(id){ document.getElementById(id).classList.remove('open'); }

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

function viewCompany(id){ toast('Open company detail view for '+id); }
function viewLead(id){ toast('Open lead detail view for '+id); }
function viewEnquiry(id){ toast('Open enquiry detail view for '+id); }
function viewSF(id){ toast('Open SF product detail view for '+id); }
function startEnquiryFromLead(id){ renderEnquiries(); }
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
