---
title: "Submit Structural Data"
layout: single
permalink: /submit/
---

<!--
=======================================================================
  PORTAL CONFIGURATION — Set these two values before deploying
=======================================================================

  GOOGLE_CLIENT_ID
  ─────────────────
  1. Go to https://console.cloud.google.com/
  2. Create or select a project (e.g. "DiffUSE Portal")
  3. Navigate to: APIs & Services → Credentials
  4. Click "Create Credentials" → "OAuth 2.0 Client ID"
  5. Application type: Web application
  6. Name: DiffUSE Submit Portal
  7. Authorized JavaScript origins:
       https://diff-use.github.io
       http://localhost:4000   ← for local testing
  8. Save and copy the Client ID (ends in .apps.googleusercontent.com)

  GITHUB_TOKEN
  ─────────────
  1. Go to https://github.com/settings/personal-access-tokens/new
  2. Token name: diffuse-submit-portal
  3. Expiration: set a reasonable date (90 days, then rotate)
  4. Resource owner: diff-use
  5. Repository access: Only selected → diff-use.github.io
  6. Permissions:
       Repository permissions → Contents → Access: Read and Write
  7. Generate and copy the token (starts with github_pat_)

  SECURITY NOTE: This token is visible in page source. It is scoped to
  write-only to this one repository's _submissions/ path. Rotate it
  regularly. Anyone with the token can create files in _submissions/.
=======================================================================
-->
<script>
const PORTAL_CONFIG = {
  GOOGLE_CLIENT_ID: 'YOUR_GOOGLE_CLIENT_ID.apps.googleusercontent.com',
  GITHUB_TOKEN:     'github_pat_REPLACE_WITH_YOUR_TOKEN',
  GITHUB_OWNER:     'diff-use',
  GITHUB_REPO:      'diff-use.github.io',
  SUBMISSIONS_PATH: '_submissions'
};
</script>

<style>
/* ── Banner ── */
.portal-banner {
  background: linear-gradient(135deg, #e35821 0%, #b83e12 100%);
  color: #fff;
  border-radius: 10px;
  padding: 1.75em 2em;
  margin-bottom: 1.75em;
}
.portal-banner h2 {
  margin: 0 0 0.45em 0;
  font-size: 1.35em;
  color: #fff;
  border: none;
}
.portal-banner p { margin: 0; opacity: .92; font-size: .93em; line-height: 1.55; }
.portal-banner .encouraged {
  display: inline-block;
  background: rgba(255,255,255,.22);
  border-radius: 4px;
  padding: .1em .5em;
  font-weight: 700;
  font-size: .88em;
}

/* ── Config warning ── */
.cfg-warn {
  display: none;
  background: #fffbe6;
  border: 1px solid #f0c030;
  border-radius: 7px;
  padding: .9em 1.2em;
  margin-bottom: 1.5em;
  font-size: .87em;
  color: #5a3f00;
}
.cfg-warn code {
  background: rgba(0,0,0,.06);
  padding: .1em .35em;
  border-radius: 3px;
}

/* ── Cards ── */
.p-card {
  background: #fff;
  border: 1px solid #e4e4e4;
  border-radius: 9px;
  padding: 1.5em 1.6em;
  margin-bottom: 1.5em;
  box-shadow: 0 1px 5px rgba(0,0,0,.06);
}
.p-card-title {
  display: flex;
  align-items: center;
  gap: .55em;
  font-size: 1.02em;
  font-weight: 700;
  color: #1e3a5f;
  margin: 0 0 1.2em 0;
  padding-bottom: .55em;
  border-bottom: 2px solid #e35821;
}
.p-card-title i { color: #e35821; }

/* ── Sign-in step ── */
#step-signin { text-align: center; padding: 1.5em 0 2em; }
.signin-intro { color: #555; font-size: .93em; margin-bottom: 1.4em; line-height: 1.5; }
#google-btn-wrap { display: inline-block; }
.gmail-note { margin-top: .9em; font-size: .82em; color: #888; }
#signin-err {
  display: none;
  background: #fef2f2;
  border-left: 3px solid #e74c3c;
  color: #7a1a1a;
  border-radius: 5px;
  padding: .7em 1em;
  font-size: .87em;
  margin-top: 1em;
  text-align: left;
}

/* ── User badge ── */
.user-badge {
  display: inline-flex;
  align-items: center;
  gap: .55em;
  background: #f0f9f0;
  border: 1px solid #b8ddb8;
  border-radius: 20px;
  padding: .38em .95em;
  font-size: .88em;
  color: #1e5e1e;
  margin-bottom: 1.4em;
}
.badge-signout {
  background: none;
  border: none;
  cursor: pointer;
  color: #aaa;
  font-size: .9em;
  margin-left: .35em;
  padding: 0;
  transition: color .2s;
}
.badge-signout:hover { color: #c0392b; }

/* ── Form elements ── */
.p-group { margin-bottom: 1.2em; }
.p-group label {
  display: block;
  font-weight: 600;
  margin-bottom: .38em;
  color: #333;
  font-size: .91em;
}
.p-group label .req { color: #e35821; margin-left: 2px; }
.hint { font-size: .79em; color: #888; margin-top: .22em; line-height: 1.4; }

.p-input {
  width: 100%;
  padding: .6em .8em;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: .91em;
  font-family: inherit;
  box-sizing: border-box;
  transition: border-color .2s, box-shadow .2s;
}
.p-input:focus {
  outline: none;
  border-color: #e35821;
  box-shadow: 0 0 0 3px rgba(227,88,33,.1);
}
.p-input[readonly] { background: #f6f6f6; color: #777; cursor: default; }
textarea.p-input { min-height: 90px; resize: vertical; }

/* ── PDB code rows ── */
.pdb-row { display: flex; gap: .45em; margin-bottom: .45em; }
.pdb-row input { flex: 1; font-family: monospace; letter-spacing: .05em; }
.btn-rm-pdb {
  background: none;
  border: 1px solid #ccc;
  border-radius: 4px;
  cursor: pointer;
  color: #aaa;
  padding: 0 .65em;
  font-size: 1em;
  transition: color .2s, border-color .2s;
  flex-shrink: 0;
}
.btn-rm-pdb:hover { color: #c0392b; border-color: #c0392b; }
.btn-add-pdb {
  background: none;
  border: 1px dashed #bbb;
  border-radius: 5px;
  cursor: pointer;
  color: #666;
  padding: .38em .9em;
  font-size: .84em;
  width: 100%;
  margin-top: .2em;
  transition: border-color .2s, color .2s;
}
.btn-add-pdb:hover { border-color: #e35821; color: #e35821; }

/* ── Drop zone ── */
.drop-zone {
  position: relative;
  border: 2px dashed #ccc;
  border-radius: 8px;
  padding: 1.8em;
  text-align: center;
  cursor: pointer;
  color: #888;
  transition: border-color .2s, background .2s, color .2s;
}
.drop-zone:hover, .drop-zone.over {
  border-color: #e35821;
  background: #fff8f5;
  color: #c94a1a;
}
.drop-zone input[type="file"] {
  position: absolute; inset: 0;
  opacity: 0; cursor: pointer;
  width: 100%; height: 100%;
}
.drop-icon { font-size: 2.1em; margin-bottom: .25em; }
.drop-label { font-size: .9em; }
.drop-sub { font-size: .76em; color: #aaa; margin-top: .2em; }

.file-list { margin-top: .65em; }
.file-item {
  display: flex;
  align-items: center;
  gap: .55em;
  background: #f8f8f8;
  border: 1px solid #e6e6e6;
  border-radius: 5px;
  padding: .45em .7em;
  margin-bottom: .35em;
  font-size: .86em;
}
.file-ext {
  background: #e35821;
  color: #fff;
  font-size: .7em;
  font-weight: 700;
  text-transform: uppercase;
  padding: .12em .42em;
  border-radius: 3px;
  flex-shrink: 0;
}
.file-name { flex: 1; font-family: monospace; color: #333; word-break: break-all; }
.file-size { color: #bbb; font-size: .82em; flex-shrink: 0; }
.file-rm {
  background: none; border: none; cursor: pointer;
  color: #ccc; font-size: 1.05em; padding: 0; flex-shrink: 0;
  transition: color .2s;
}
.file-rm:hover { color: #c0392b; }

/* ── Data type grid ── */
.type-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(155px, 1fr));
  gap: .55em;
}
.type-opt {
  display: flex;
  align-items: center;
  gap: .45em;
  padding: .55em .75em;
  border: 1px solid #ddd;
  border-radius: 6px;
  cursor: pointer;
  font-size: .87em;
  transition: border-color .18s, background .18s;
  user-select: none;
}
.type-opt:hover { border-color: #e35821; }
.type-opt.sel { border-color: #e35821; background: #fff8f5; }
.type-opt input[type="checkbox"] { accent-color: #e35821; flex-shrink: 0; }
.type-opt .t-icon { font-size: 1.05em; }
.type-hot {
  background: linear-gradient(135deg, #fff4f0, #fff8f5);
  border-color: #f0a070 !important;
}
.enc-badge {
  font-size: .68em;
  background: #e35821;
  color: #fff;
  padding: .1em .38em;
  border-radius: 3px;
  margin-left: auto;
  font-weight: 700;
  flex-shrink: 0;
}

/* ── Status bar ── */
.p-status {
  display: none;
  border-radius: 6px;
  padding: .75em 1em;
  font-size: .89em;
  margin-top: .9em;
  line-height: 1.45;
}
.p-status.info  { background:#eef4ff; border-left:3px solid #4a90d9; color:#1a3a70; }
.p-status.ok    { background:#f0f9f0; border-left:3px solid #27ae60; color:#145a20; }
.p-status.err   { background:#fef2f2; border-left:3px solid #e74c3c; color:#7a1a1a; }

/* ── Submit row ── */
.submit-row {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  gap: 1em;
  margin-top: .6em;
}
.btn-submit {
  background: linear-gradient(135deg, #e35821, #b83e12);
  color: #fff;
  border: none;
  border-radius: 6px;
  padding: .75em 2em;
  font-size: .97em;
  font-weight: 700;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  gap: .5em;
  transition: opacity .2s, transform .1s;
}
.btn-submit:hover:not(:disabled) { opacity: .9; transform: translateY(-1px); }
.btn-submit:disabled { opacity: .5; cursor: not-allowed; transform: none; }

/* ── Success ── */
#step-success { text-align: center; padding: 2.5em 1em; }
.success-check { font-size: 3.5em; color: #27ae60; margin-bottom: .2em; }
#step-success h2 { color: #145a20; }
.success-path {
  background: #f4f4f4;
  border-radius: 5px;
  padding: .55em 1em;
  font-family: monospace;
  font-size: .83em;
  color: #444;
  margin: .9em auto;
  max-width: 480px;
  word-break: break-all;
  text-align: left;
}
.btn-again {
  background: none;
  border: 2px solid #e35821;
  color: #e35821;
  border-radius: 6px;
  padding: .55em 1.4em;
  font-weight: 700;
  cursor: pointer;
  font-size: .9em;
  margin-top: .8em;
  transition: background .2s, color .2s;
}
.btn-again:hover { background: #e35821; color: #fff; }

/* ── Spinner ── */
@keyframes spin { to { transform: rotate(360deg); } }
.spinner {
  display: inline-block;
  width: 1em; height: 1em;
  border: 2px solid rgba(255,255,255,.35);
  border-top-color: #fff;
  border-radius: 50%;
  animation: spin .65s linear infinite;
}
</style>

<!-- Config warning (shown if tokens are placeholders) -->
<div class="cfg-warn" id="cfg-warn">
  <strong>⚠ Portal not configured.</strong>
  Open <code>_pages/submit.md</code> and replace <code>PORTAL_CONFIG.GOOGLE_CLIENT_ID</code>
  and <code>PORTAL_CONFIG.GITHUB_TOKEN</code> with real values.
  Setup instructions are in the comments at the top of that file.
</div>

<!-- Banner -->
<div class="portal-banner">
  <h2><i class="fas fa-database"></i> Submit Structural Data</h2>
  <p>
    Contribute PDB or mmCIF structures to the DiffUSE heterogeneity dataset.
    We especially encourage submissions featuring
    <span class="encouraged">cryo-EM</span> and
    <span class="encouraged">time-resolved</span> data.
    All submissions are reviewed by the DiffUSE team before incorporation.
  </p>
</div>

<!-- ══════════════════════════════════════════
     STEP 1 — Sign In
══════════════════════════════════════════ -->
<div id="step-signin">
  <div class="p-card" style="max-width:440px;margin:0 auto;">
    <div class="p-card-title">
      <i class="fab fa-google"></i> Sign In with Google
    </div>
    <p class="signin-intro">
      A Google account is required to submit data.
      Only <strong>@gmail.com</strong> addresses are accepted so the DiffUSE team
      can follow up about your submission.
    </p>
    <div id="google-btn-wrap"></div>
    <p class="gmail-note">
      <i class="fas fa-lock"></i>
      We only store your name and email address alongside your submission.
    </p>
    <div id="signin-err"></div>
  </div>
</div>

<!-- ══════════════════════════════════════════
     STEP 2 — Submission Form
══════════════════════════════════════════ -->
<div id="step-form" style="display:none;">

  <div class="user-badge">
    <i class="fas fa-check-circle"></i>
    <span id="badge-label">Signed in</span>
    <button class="badge-signout" onclick="doSignOut()" title="Sign out">✕</button>
  </div>

  <form id="sub-form" onsubmit="handleSubmit(event)" novalidate>

    <!-- ─── Your Information ─── -->
    <div class="p-card">
      <div class="p-card-title"><i class="fas fa-user"></i> Your Information</div>

      <div class="p-group">
        <label for="f-name">Full Name <span class="req">*</span></label>
        <input id="f-name" type="text" class="p-input" required
          placeholder="Your full name">
      </div>

      <div class="p-group">
        <label>Gmail Address</label>
        <input id="f-email" type="email" class="p-input" readonly>
        <div class="hint">Verified via Google Sign-In. Cannot be changed.</div>
      </div>
    </div>

    <!-- ─── Structure Files ─── -->
    <div class="p-card">
      <div class="p-card-title"><i class="fas fa-atom"></i> Structure Files</div>

      <!-- PDB codes -->
      <div class="p-group">
        <label>PDB Accession Codes</label>
        <div id="pdb-list">
          <div class="pdb-row">
            <input type="text" class="p-input pdb-code" maxlength="8"
              placeholder="e.g. 1ABC" autocomplete="off" spellcheck="false">
            <button type="button" class="btn-rm-pdb" onclick="rmPdb(this)" title="Remove">×</button>
          </div>
        </div>
        <button type="button" class="btn-add-pdb" onclick="addPdb()">
          <i class="fas fa-plus"></i> Add another PDB code
        </button>
        <div class="hint">
          RCSB PDB accession codes (4–8 characters). Leave blank if uploading files directly.
        </div>
      </div>

      <!-- File upload -->
      <div class="p-group">
        <label>Upload Structure Files</label>
        <div class="drop-zone" id="drop-zone"
          ondragover="onDragOver(event)"
          ondragleave="onDragLeave(event)"
          ondrop="onDrop(event)">
          <input type="file" id="file-input" multiple
            accept=".pdb,.cif,.mmcif"
            onchange="onFilePick(event)">
          <div class="drop-icon"><i class="fas fa-cloud-upload-alt"></i></div>
          <div class="drop-label">Drag &amp; drop here, or click to browse</div>
          <div class="drop-sub">Accepted: .pdb · .cif · .mmcif &nbsp;|&nbsp; Max 25 MB per file</div>
        </div>
        <div class="file-list" id="file-list"></div>
        <div class="hint">
          Upload one or more files. Multiple conformers or time-points as separate files are welcome.
          At least one PDB code <em>or</em> one uploaded file is required.
        </div>
      </div>

      <!-- Data type -->
      <div class="p-group">
        <label>Data Type <span class="req">*</span></label>
        <div class="type-grid">
          <label class="type-opt type-hot">
            <input type="checkbox" value="cryo_em" onchange="syncType(this)">
            <span class="t-icon">🔬</span> Cryo-EM
            <span class="enc-badge">encouraged</span>
          </label>
          <label class="type-opt type-hot">
            <input type="checkbox" value="time_resolved" onchange="syncType(this)">
            <span class="t-icon">⏱</span> Time-resolved
            <span class="enc-badge">encouraged</span>
          </label>
          <label class="type-opt">
            <input type="checkbox" value="xray" onchange="syncType(this)">
            <span class="t-icon">⚡</span> X-ray
          </label>
          <label class="type-opt">
            <input type="checkbox" value="nmr" onchange="syncType(this)">
            <span class="t-icon">🧲</span> NMR
          </label>
          <label class="type-opt">
            <input type="checkbox" value="md_simulation" onchange="syncType(this)">
            <span class="t-icon">💻</span> MD / Simulation
          </label>
          <label class="type-opt">
            <input type="checkbox" value="other" onchange="syncType(this)">
            <span class="t-icon">📋</span> Other
          </label>
        </div>
        <div class="hint">Select all that apply. Cryo-EM and time-resolved datasets are especially encouraged.</div>
      </div>
    </div>

    <!-- ─── Publication ─── -->
    <div class="p-card">
      <div class="p-card-title"><i class="fas fa-book-open"></i> Publication</div>

      <div class="p-group">
        <label for="f-doi">DOI</label>
        <input id="f-doi" type="text" class="p-input"
          placeholder="e.g. 10.1038/s41586-024-12345-6">
        <div class="hint">
          Digital Object Identifier for the associated paper.
          Leave blank if not yet published.
        </div>
      </div>
    </div>

    <!-- ─── Heterogeneity Context ─── -->
    <div class="p-card">
      <div class="p-card-title"><i class="fas fa-project-diagram"></i> Heterogeneity Context</div>

      <div class="p-group">
        <label for="f-het">Description of Heterogeneity <span class="req">*</span></label>
        <textarea id="f-het" class="p-input" required
          placeholder="Describe the structural heterogeneity present in your data. For example: conformational switching between two states, disordered loop regions, multiple ligand-binding modes, domain motions captured across time-points, partial occupancy, etc."></textarea>
        <div class="hint">
          Explain what heterogeneity is present, what you believe drives it, and
          why it is biologically or structurally meaningful.
        </div>
      </div>

      <div class="p-group">
        <label for="f-res">Residues of Interest</label>
        <textarea id="f-res" class="p-input" style="min-height:70px;"
          placeholder="e.g. A:123-145, B:89, C:200-210&#10;(Chain:residue or Chain:start-end format)"></textarea>
        <div class="hint">
          List residues or ranges that best capture the heterogeneity.
          Preferred format: <code>Chain:residue</code> or <code>Chain:start-end</code>,
          comma-separated.
        </div>
      </div>

      <div class="p-group">
        <label for="f-notes">Additional Notes</label>
        <textarea id="f-notes" class="p-input" style="min-height:65px;"
          placeholder="Any other context, known caveats, or information useful to the DiffUSE team (optional)."></textarea>
      </div>
    </div>

    <!-- ─── Submit ─── -->
    <div class="p-status" id="sub-status"></div>
    <div class="submit-row">
      <button type="submit" class="btn-submit" id="sub-btn">
        <i class="fas fa-paper-plane"></i> Submit
      </button>
    </div>

  </form>
</div>

<!-- ══════════════════════════════════════════
     STEP 3 — Success
══════════════════════════════════════════ -->
<div id="step-success" style="display:none;">
  <div class="p-card" style="max-width:520px;margin:0 auto;text-align:center;">
    <div class="success-check">✓</div>
    <h2>Submission received!</h2>
    <p>
      Thank you for contributing to the DiffUSE Project.
      Your data has been saved and will be reviewed by the team.
    </p>
    <div class="success-path" id="suc-path"></div>
    <p style="font-size:.87em;color:#555;">
      <i class="fas fa-envelope"></i>
      We will follow up at <strong id="suc-email"></strong> if we have any questions.
    </p>
    <button class="btn-again" onclick="doReset()">Submit Another</button>
  </div>
</div>

<!-- Google Identity Services SDK -->
<script src="https://accounts.google.com/gsi/client" async defer></script>

<script>
// ── State ──────────────────────────────────────────────────────────
let gUser      = null;   // { name, email }
let fileQueue  = [];     // File objects staged for upload

// ── Initialise ─────────────────────────────────────────────────────
document.addEventListener('DOMContentLoaded', function () {

  // Warn if config is still placeholder
  const uncfg = PORTAL_CONFIG.GOOGLE_CLIENT_ID.includes('YOUR_') ||
                PORTAL_CONFIG.GITHUB_TOKEN.includes('YOUR_') ||
                PORTAL_CONFIG.GITHUB_TOKEN.includes('REPLACE_');
  if (uncfg) document.getElementById('cfg-warn').style.display = 'block';

  // Wait for Google Identity Services to load, then render Sign-In button
  waitGSI(initGSI);
});

function waitGSI(cb, tries) {
  tries = tries || 0;
  if (typeof google !== 'undefined' && google.accounts && google.accounts.id) {
    cb();
  } else if (tries < 60) {
    setTimeout(function () { waitGSI(cb, tries + 1); }, 100);
  } else {
    document.getElementById('google-btn-wrap').innerHTML =
      '<p style="color:#c0392b;font-size:.88em;">' +
      'Google Sign-In failed to load. Disable any ad-blockers and reload the page.</p>';
  }
}

function initGSI() {
  google.accounts.id.initialize({
    client_id:            PORTAL_CONFIG.GOOGLE_CLIENT_ID,
    callback:             onGoogleCred,
    auto_select:          false,
    cancel_on_tap_outside: true
  });
  google.accounts.id.renderButton(
    document.getElementById('google-btn-wrap'),
    { theme: 'outline', size: 'large', text: 'sign_in_with', width: 300 }
  );
}

// ── Google Sign-In callback ─────────────────────────────────────────
function onGoogleCred(resp) {
  try {
    // Decode JWT payload (client-side — sufficient for UI gating)
    var b64 = resp.credential.split('.')[1].replace(/-/g, '+').replace(/_/g, '/');
    var payload = JSON.parse(decodeURIComponent(atob(b64).split('').map(function (c) {
      return '%' + ('00' + c.charCodeAt(0).toString(16)).slice(-2);
    }).join('')));

    var email = payload.email || '';
    if (!email.toLowerCase().endsWith('@gmail.com')) {
      showSigninErr('Please sign in with a @gmail.com address. ' +
        'Google Workspace accounts (e.g. @university.edu) are not accepted.');
      return;
    }
    gUser = { name: payload.name || '', email: email };
    document.getElementById('f-name').value  = gUser.name;
    document.getElementById('f-email').value = gUser.email;
    document.getElementById('badge-label').textContent =
      gUser.name + ' (' + gUser.email + ')';

    document.getElementById('step-signin').style.display = 'none';
    document.getElementById('step-form').style.display   = 'block';
    document.getElementById('signin-err').style.display  = 'none';

  } catch (e) {
    showSigninErr('Could not parse sign-in response. Please try again.');
  }
}

function showSigninErr(msg) {
  var el = document.getElementById('signin-err');
  el.textContent = msg;
  el.style.display = 'block';
}

function doSignOut() {
  gUser = null;
  fileQueue = [];
  document.getElementById('step-form').style.display    = 'none';
  document.getElementById('step-success').style.display = 'none';
  document.getElementById('step-signin').style.display  = 'block';
  document.getElementById('sub-form').reset();
  document.getElementById('file-list').innerHTML = '';
  resetPdbList();
  clearStatus();
  if (typeof google !== 'undefined') google.accounts.id.disableAutoSelect();
}

// ── PDB code rows ───────────────────────────────────────────────────
function addPdb() {
  var row = document.createElement('div');
  row.className = 'pdb-row';
  row.innerHTML =
    '<input type="text" class="p-input pdb-code" maxlength="8" ' +
    'placeholder="e.g. 2XYZ" autocomplete="off" spellcheck="false">' +
    '<button type="button" class="btn-rm-pdb" onclick="rmPdb(this)" title="Remove">×</button>';
  document.getElementById('pdb-list').appendChild(row);
  row.querySelector('input').focus();
}

function rmPdb(btn) {
  var rows = document.querySelectorAll('.pdb-row');
  if (rows.length > 1) { btn.closest('.pdb-row').remove(); }
  else { btn.closest('.pdb-row').querySelector('input').value = ''; }
}

function resetPdbList() {
  document.getElementById('pdb-list').innerHTML =
    '<div class="pdb-row">' +
    '<input type="text" class="p-input pdb-code" maxlength="8" ' +
    'placeholder="e.g. 1ABC" autocomplete="off" spellcheck="false">' +
    '<button type="button" class="btn-rm-pdb" onclick="rmPdb(this)" title="Remove">×</button>' +
    '</div>';
}

// ── File upload ─────────────────────────────────────────────────────
var MAX_MB = 25;

function onDragOver(e)  { e.preventDefault(); document.getElementById('drop-zone').classList.add('over'); }
function onDragLeave(e) { document.getElementById('drop-zone').classList.remove('over'); }
function onDrop(e) {
  e.preventDefault();
  document.getElementById('drop-zone').classList.remove('over');
  addFiles(e.dataTransfer.files);
}
function onFilePick(e) {
  addFiles(e.target.files);
  e.target.value = '';
}

function addFiles(list) {
  var allowed = ['.pdb', '.cif', '.mmcif'];
  var errors  = [];
  Array.from(list).forEach(function (f) {
    var ext = '.' + f.name.split('.').pop().toLowerCase();
    if (!allowed.includes(ext)) {
      errors.push(f.name + ': unsupported type. Use .pdb, .cif, or .mmcif.');
      return;
    }
    if (f.size > MAX_MB * 1024 * 1024) {
      errors.push(f.name + ': exceeds ' + MAX_MB + ' MB limit.');
      return;
    }
    if (fileQueue.find(function (x) { return x.name === f.name; })) {
      errors.push(f.name + ': already added.');
      return;
    }
    fileQueue.push(f);
  });
  if (errors.length) setStatus('err', errors.join('<br>'));
  else clearStatus();
  renderFileList();
}

function renderFileList() {
  document.getElementById('file-list').innerHTML = fileQueue.map(function (f, i) {
    var ext  = f.name.split('.').pop().toUpperCase();
    var size = f.size < 1024 * 1024
      ? Math.round(f.size / 1024) + ' KB'
      : (f.size / 1024 / 1024).toFixed(1) + ' MB';
    return '<div class="file-item">' +
      '<span class="file-ext">' + ext + '</span>' +
      '<span class="file-name">' + escHtml(f.name) + '</span>' +
      '<span class="file-size">' + size + '</span>' +
      '<button type="button" class="file-rm" onclick="rmFile(' + i + ')" title="Remove">✕</button>' +
      '</div>';
  }).join('');
}

function rmFile(i) { fileQueue.splice(i, 1); renderFileList(); }

// ── Data type checkboxes ────────────────────────────────────────────
function syncType(cb) {
  cb.closest('.type-opt').classList.toggle('sel', cb.checked);
}

// ── Form submission ─────────────────────────────────────────────────
async function handleSubmit(e) {
  e.preventDefault();

  var name     = document.getElementById('f-name').value.trim();
  var email    = document.getElementById('f-email').value.trim();
  var doi      = document.getElementById('f-doi').value.trim();
  var het      = document.getElementById('f-het').value.trim();
  var residues = document.getElementById('f-res').value.trim();
  var notes    = document.getElementById('f-notes').value.trim();

  var pdbCodes = Array.from(document.querySelectorAll('.pdb-code'))
    .map(function (el) { return el.value.trim().toUpperCase(); })
    .filter(function (v) { return v.length >= 4; });

  var dataTypes = Array.from(document.querySelectorAll('.type-opt input:checked'))
    .map(function (el) { return el.value; });

  // Validate
  if (!name)                             { setStatus('err', 'Please enter your full name.'); return; }
  if (!pdbCodes.length && !fileQueue.length) {
    setStatus('err', 'Please provide at least one PDB code or upload a structure file.'); return;
  }
  if (!dataTypes.length)                 { setStatus('err', 'Please select at least one data type.'); return; }
  if (!het)                              { setStatus('err', 'Please describe the heterogeneity in your data.'); return; }

  var btn = document.getElementById('sub-btn');
  btn.disabled = true;
  btn.innerHTML = '<span class="spinner"></span> Submitting…';

  try {
    var now       = new Date();
    var isoStamp  = now.toISOString().slice(0, 19); // 2026-05-08T14:30:00
    var fileStamp = isoStamp.replace('T', 'T').replace(/:/g, '-');  // 2026-05-08T14-30-00
    var safeName  = name.replace(/[^a-zA-Z0-9]+/g, '-').replace(/^-+|-+$/g, '').toLowerCase().slice(0, 28);
    var folder    = PORTAL_CONFIG.SUBMISSIONS_PATH + '/' + fileStamp + '_' + safeName;

    // 1. Metadata YAML
    var yaml = buildYaml({ name, email, pdbCodes, dataTypes, doi, het, residues, notes,
      fileNames: fileQueue.map(function (f) { return f.name; }),
      timestamp: isoStamp });

    setStatus('info', 'Creating submission record…');
    await ghPut(folder + '/metadata.yml', yamlToB64(yaml),
      'Add submission metadata from ' + name);

    // 2. Structure files
    for (var i = 0; i < fileQueue.length; i++) {
      var f = fileQueue[i];
      setStatus('info', 'Uploading ' + escHtml(f.name) + ' (' + (i + 2) + ' / ' + (fileQueue.length + 1) + ')…');
      var b64 = await fileToB64(f);
      await ghPut(folder + '/' + f.name, b64, 'Add ' + f.name + ' from ' + name);
    }

    // 3. Show success
    document.getElementById('step-form').style.display    = 'none';
    document.getElementById('step-success').style.display = 'block';
    document.getElementById('suc-path').textContent = folder + '/';
    document.getElementById('suc-email').textContent = email;

  } catch (err) {
    console.error(err);
    setStatus('err',
      'Submission failed: ' + (err.message || err) +
      '<br>Please try again or email <a href="mailto:diffuse@astera.org">diffuse@astera.org</a>.');
    btn.disabled = false;
    btn.innerHTML = '<i class="fas fa-paper-plane"></i> Submit';
  }
}

// ── YAML builder ────────────────────────────────────────────────────
function buildYaml(o) {
  var y = '---\n';
  y += 'submitted_at: "' + o.timestamp + 'Z"\n';
  y += 'submitter:\n';
  y += '  name: "' + esc(o.name) + '"\n';
  y += '  email: "' + esc(o.email) + '"\n';
  y += 'structures:\n';
  if (o.pdbCodes.length) {
    y += '  pdb_codes:\n';
    o.pdbCodes.forEach(function (c) { y += '    - "' + c + '"\n'; });
  } else {
    y += '  pdb_codes: []\n';
  }
  if (o.fileNames.length) {
    y += '  uploaded_files:\n';
    o.fileNames.forEach(function (fn) { y += '    - "' + esc(fn) + '"\n'; });
  } else {
    y += '  uploaded_files: []\n';
  }
  y += 'data_types:\n';
  if (o.dataTypes.length) {
    o.dataTypes.forEach(function (t) { y += '  - ' + t + '\n'; });
  } else {
    y += '  []\n';
  }
  y += 'publication:\n';
  y += '  doi: "' + esc(o.doi) + '"\n';
  y += 'heterogeneity:\n';
  y += '  description: |\n';
  o.het.split('\n').forEach(function (line) { y += '    ' + line + '\n'; });
  y += '  residues: "' + esc(o.residues) + '"\n';
  y += 'notes: "' + esc(o.notes) + '"\n';
  y += '---\n';
  return y;
}
function esc(s)   { return (s || '').replace(/\\/g, '\\\\').replace(/"/g, '\\"'); }
function escHtml(s) { return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }
function yamlToB64(str) { return btoa(unescape(encodeURIComponent(str))); }

// ── GitHub Contents API ─────────────────────────────────────────────
async function ghPut(path, base64Content, message) {
  var url = 'https://api.github.com/repos/' +
    PORTAL_CONFIG.GITHUB_OWNER + '/' + PORTAL_CONFIG.GITHUB_REPO +
    '/contents/' + path;
  var resp = await fetch(url, {
    method: 'PUT',
    headers: {
      'Authorization':       'Bearer ' + PORTAL_CONFIG.GITHUB_TOKEN,
      'Content-Type':        'application/json',
      'X-GitHub-Api-Version': '2022-11-28'
    },
    body: JSON.stringify({ message: message, content: base64Content })
  });
  if (!resp.ok) {
    var data = {};
    try { data = await resp.json(); } catch (_) {}
    throw new Error(data.message || 'HTTP ' + resp.status);
  }
  return resp.json();
}

// ── File to base64 ──────────────────────────────────────────────────
function fileToB64(file) {
  return new Promise(function (resolve, reject) {
    var r = new FileReader();
    r.onload  = function (e) { resolve(e.target.result.split(',')[1]); };
    r.onerror = reject;
    r.readAsDataURL(file);
  });
}

// ── Status helpers ──────────────────────────────────────────────────
function setStatus(type, html) {
  var el = document.getElementById('sub-status');
  el.className = 'p-status ' + type;
  el.innerHTML = html;
  el.style.display = 'block';
  el.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
}
function clearStatus() {
  document.getElementById('sub-status').style.display = 'none';
}

// ── Reset portal for another submission ────────────────────────────
function doReset() {
  fileQueue = [];
  document.getElementById('step-success').style.display = 'none';
  document.getElementById('step-form').style.display    = 'block';
  document.getElementById('sub-form').reset();
  document.getElementById('file-list').innerHTML = '';
  resetPdbList();
  clearStatus();
  // Re-fill user fields
  document.getElementById('f-name').value  = gUser ? gUser.name  : '';
  document.getElementById('f-email').value = gUser ? gUser.email : '';
  // Re-tick type highlights off
  document.querySelectorAll('.type-opt').forEach(function (el) {
    el.classList.remove('sel');
  });
  var btn = document.getElementById('sub-btn');
  btn.disabled = false;
  btn.innerHTML = '<i class="fas fa-paper-plane"></i> Submit';
}
</script>
