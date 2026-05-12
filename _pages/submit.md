---
title: "Submit Examples of Heterogeneous Structural Data"
layout: single
permalink: submit/
---

<script>
const CFG = {
  WORKER_URL:       'https://diffuse-website.stephanie-wankowicz.workers.dev',
  SUBMISSIONS_PATH: '_submissions'
};
</script>

<style>
.sf-label { display:block; font-weight:600; margin-bottom:.3em; font-size:.92em; }
.sf-req   { color:#e35821; }
.sf-hint  { font-size:.8em; color:#888; margin-top:.22em; line-height:1.4; }
.sf-group { margin-bottom:1.15em; }

.sf-input {
  width:100%; padding:.55em .75em;
  border:1px solid #ccc; border-radius:5px;
  font-size:.92em; font-family:inherit; box-sizing:border-box;
  transition:border-color .2s, box-shadow .2s;
}
.sf-input:focus { outline:none; border-color:#e35821; box-shadow:0 0 0 3px rgba(227,88,33,.1); }
textarea.sf-input { min-height:88px; resize:vertical; }

.pdb-row          { display:flex; gap:.4em; margin-bottom:.4em; }
.pdb-row input    { flex:1; font-family:monospace; }
.btn-rm-pdb       { background:none; border:1px solid #ddd; border-radius:4px; cursor:pointer; color:#bbb; padding:0 .65em; font-size:1em; transition:.15s; }
.btn-rm-pdb:hover { color:#c0392b; border-color:#c0392b; }
.btn-add-pdb      { background:none; border:1px dashed #bbb; border-radius:5px; cursor:pointer; color:#777; padding:.35em .9em; font-size:.84em; width:100%; margin-top:.15em; transition:.15s; }
.btn-add-pdb:hover { border-color:#e35821; color:#e35821; }

.dz               { position:relative; border:2px dashed #ccc; border-radius:7px; padding:1.75em; text-align:center; cursor:pointer; color:#999; transition:.2s; }
.dz:hover, .dz.over { border-color:#e35821; background:#fff8f5; color:#c94a1a; }
.dz input[type=file] { position:absolute; inset:0; opacity:0; cursor:pointer; width:100%; height:100%; }
.dz-icon { font-size:2em; margin-bottom:.2em; }
.dz-sub  { font-size:.77em; color:#bbb; margin-top:.15em; }

.fi-list { margin-top:.6em; }
.fi      { display:flex; align-items:center; gap:.5em; background:#f8f8f8; border:1px solid #e8e8e8; border-radius:4px; padding:.42em .7em; margin-bottom:.3em; font-size:.86em; }
.fi-ext  { background:#e35821; color:#fff; font-size:.69em; font-weight:700; text-transform:uppercase; padding:.1em .4em; border-radius:3px; flex-shrink:0; }
.fi-name { flex:1; font-family:monospace; color:#333; word-break:break-all; }
.fi-size { color:#bbb; flex-shrink:0; }
.fi-rm   { background:none; border:none; cursor:pointer; color:#ccc; font-size:1em; padding:0; flex-shrink:0; transition:.15s; }
.fi-rm:hover { color:#c0392b; }

.types   { display:flex; flex-wrap:wrap; gap:.5em; }
.t-opt   { display:flex; align-items:center; gap:.4em; padding:.48em .75em; border:1px solid #ddd; border-radius:5px; cursor:pointer; font-size:.87em; transition:.15s; user-select:none; }
.t-opt:hover { border-color:#e35821; }
.t-opt.on    { border-color:#e35821; background:#fff8f5; }
.t-opt input { accent-color:#e35821; flex-shrink:0; }

#sf-status { display:none; margin:1em 0 .5em; }

@keyframes spin { to { transform:rotate(360deg); } }
.spin { display:inline-block; width:1em; height:1em; border:2px solid rgba(255,255,255,.35); border-top-color:#fff; border-radius:50%; animation:spin .65s linear infinite; vertical-align:middle; }
</style>

We are looking for examples where heterogeneity is present and/or biologically important, yet cannot be described in the current encoding strategy of PDBx/mmCIF files. We are hoping to obtain diverse examples from X-ray or cryo-EM, including time-resolved data, multiple maps, or fragment-screening data.

---

<div id="sf-wrap">
<form id="sf" onsubmit="doSubmit(event)" novalidate>

<h3>Your Information</h3>

<div class="sf-group">
  <label class="sf-label" for="f-name">Full Name <span class="sf-req">*</span></label>
  <input id="f-name" type="text" class="sf-input" required placeholder="Your full name">
</div>

<div class="sf-group">
  <label class="sf-label" for="f-email">Email <span class="sf-req">*</span></label>
  <input id="f-email" type="email" class="sf-input" required placeholder="your@gmail.com">
  <div class="sf-hint">Please use a Gmail address so the DiffUSE team can follow up on your submission.</div>
</div>

<h3>Structure Files</h3>

<div class="sf-group">
  <label class="sf-label">PDB Accession Codes</label>
  <div id="pdb-list">
    <div class="pdb-row">
      <input type="text" class="sf-input pdb-code" maxlength="8" placeholder="e.g. 1ABC" autocomplete="off" spellcheck="false">
      <button type="button" class="btn-rm-pdb" onclick="rmPdb(this)" title="Remove">×</button>
    </div>
  </div>
  <button type="button" class="btn-add-pdb" onclick="addPdb()">+ Add another PDB code</button>
  <div class="sf-hint">RCSB accession codes (4–8 characters). Leave blank if uploading files directly.</div>
</div>

<div class="sf-group">
  <label class="sf-label">Upload Structure Files</label>
  <div class="dz" id="dz"
    ondragover="dzOver(event)" ondragleave="dzLeave(event)" ondrop="dzDrop(event)">
    <input type="file" id="f-files" multiple accept=".pdb,.cif,.mmcif" onchange="onPick(event)">
    <div class="dz-icon"><i class="fas fa-cloud-upload-alt"></i></div>
    <div>Drag &amp; drop here, or click to browse</div>
    <div class="dz-sub">Accepted: .pdb · .cif · .mmcif &nbsp;|&nbsp; Max 25 MB per file</div>
  </div>
  <div class="fi-list" id="fi-list"></div>
  <div class="sf-hint">Multiple files welcome — separate conformers or time-points are encouraged. At least one PDB code <em>or</em> uploaded file is required.</div>
</div>

<div class="sf-group">
  <label class="sf-label">Data Type <span class="sf-req">*</span></label>
  <div class="types">
    <label class="t-opt"><input type="checkbox" value="cryo_em"      onchange="tSync(this)"> Cryo-EM</label>
    <label class="t-opt"><input type="checkbox" value="xray"          onchange="tSync(this)"> X-ray</label>
    <label class="t-opt"><input type="checkbox" value="multiple_maps" onchange="tSync(this)"> Multiple Maps</label>
    <label class="t-opt"><input type="checkbox" value="time_resolved" onchange="tSync(this)"> Time-resolved</label>
    <label class="t-opt"><input type="checkbox" value="other"         onchange="tSync(this)"> Other</label>
  </div>
  <div class="sf-hint">Select all that apply.</div>
</div>

<h3>Publication</h3>

<div class="sf-group">
  <label class="sf-label" for="f-doi">DOI</label>
  <input id="f-doi" type="text" class="sf-input" placeholder="e.g. 10.1038/s41586-024-12345-6">
  <div class="sf-hint">Leave blank if not yet published.</div>
</div>

<h3>Heterogeneity Context</h3>

<div class="sf-group">
  <label class="sf-label" for="f-het">Description of Heterogeneity <span class="sf-req">*</span></label>
  <textarea id="f-het" class="sf-input" required
    placeholder="Describe the structural heterogeneity in your data — e.g. disordered loop regions, multiple ligand-binding poses, domain motions, partial occupancy, etc."></textarea>
  <div class="sf-hint">Explain what heterogeneity is present and why it is biologically or structurally meaningful.</div>
</div>

<div class="sf-group">
  <label class="sf-label" for="f-issues">Issues Communicating Heterogeneity <span class="sf-req">*</span></label>
  <textarea id="f-issues" class="sf-input" required
    placeholder="Describe issues communicating, visualizing, and/or refining heterogeneity with structural models."></textarea>
  <div class="sf-hint">Explain what issues arise when trying to represent or communicate this heterogeneity.</div>
</div>

<div class="sf-group">
  <label class="sf-label" for="f-res">Residues of Interest</label>
  <textarea id="f-res" class="sf-input" style="min-height:70px;"
    placeholder="e.g. A:123-145, B:89, C:200-210&#10;Format: Chain:residue or Chain:start-end, comma-separated"></textarea>
  <div class="sf-hint">Residues or ranges that best capture the heterogeneity. Preferred format: <code>Chain:residue</code> or <code>Chain:start-end</code>.</div>
</div>

<div class="sf-group">
  <label class="sf-label" for="f-notes">Additional Notes</label>
  <textarea id="f-notes" class="sf-input" style="min-height:65px;"
    placeholder="Any other context, caveats, or information useful (optional)."></textarea>
</div>

<div id="sf-status"></div>

<div style="text-align:right; margin-top:.5em;">
  <button type="submit" class="btn btn--primary btn--large" id="sf-btn">
    <i class="fas fa-paper-plane"></i> Submit
  </button>
</div>

</form>
</div>

<div class="notice--success" id="sf-done" style="display:none">
  <h4 style="margin-top:0;">Submission received!</h4>
  <p>Thank you for contributing to the DiffUSE Project. Your data has been saved to:</p>
  <p><code id="sf-path"></code></p>
  <p>The team will follow up at <strong id="sf-email"></strong> if there are any questions.</p>
  <p><a href="#" onclick="doReset();return false;">Submit another</a></p>
</div>

<script>
var files = [];

function addPdb() {
  var row = document.createElement('div');
  row.className = 'pdb-row';
  row.innerHTML = '<input type="text" class="sf-input pdb-code" maxlength="8" placeholder="e.g. 2XYZ" autocomplete="off" spellcheck="false">' +
    '<button type="button" class="btn-rm-pdb" onclick="rmPdb(this)" title="Remove">×</button>';
  document.getElementById('pdb-list').appendChild(row);
  row.querySelector('input').focus();
}
function rmPdb(btn) {
  var rows = document.querySelectorAll('.pdb-row');
  if (rows.length > 1) btn.closest('.pdb-row').remove();
  else btn.closest('.pdb-row').querySelector('input').value = '';
}

function dzOver(e)  { e.preventDefault(); document.getElementById('dz').classList.add('over'); }
function dzLeave()  { document.getElementById('dz').classList.remove('over'); }
function dzDrop(e)  { e.preventDefault(); dzLeave(); addFiles(e.dataTransfer.files); }
function onPick(e)  { addFiles(e.target.files); e.target.value = ''; }

function addFiles(list) {
  var errs = [];
  Array.from(list).forEach(function (f) {
    var ext = '.' + f.name.split('.').pop().toLowerCase();
    if (!['.pdb','.cif','.mmcif'].includes(ext))  { errs.push(f.name + ': use .pdb, .cif, or .mmcif'); return; }
    if (f.size > 25 * 1024 * 1024)               { errs.push(f.name + ': exceeds 25 MB'); return; }
    if (files.find(function(x){ return x.name===f.name; })) { errs.push(f.name + ': already added'); return; }
    files.push(f);
  });
  if (errs.length) setStatus('notice--danger', errs.join('<br>')); else clearStatus();
  renderFiles();
}
function renderFiles() {
  document.getElementById('fi-list').innerHTML = files.map(function (f, i) {
    var ext  = f.name.split('.').pop().toUpperCase();
    var size = f.size < 1048576 ? Math.round(f.size/1024)+' KB' : (f.size/1048576).toFixed(1)+' MB';
    return '<div class="fi"><span class="fi-ext">'+ext+'</span><span class="fi-name">'+esc(f.name)+'</span>' +
      '<span class="fi-size">'+size+'</span>' +
      '<button type="button" class="fi-rm" onclick="rmFile('+i+')" title="Remove">✕</button></div>';
  }).join('');
}
function rmFile(i) { files.splice(i,1); renderFiles(); }

function tSync(cb) { cb.closest('.t-opt').classList.toggle('on', cb.checked); }

async function doSubmit(e) {
  e.preventDefault();
  var name      = val('f-name');
  var email     = val('f-email');
  var doi       = val('f-doi');
  var het       = val('f-het');
  var issues    = val('f-issues');
  var residues  = val('f-res');
  var notes     = val('f-notes');
  var pdbCodes  = Array.from(document.querySelectorAll('.pdb-code'))
                    .map(function(el){ return el.value.trim().toUpperCase(); })
                    .filter(function(v){ return v.length >= 4; });
  var dataTypes = Array.from(document.querySelectorAll('.t-opt input:checked'))
                    .map(function(el){ return el.value; });

  if (!name)                             { setStatus('notice--danger','Please enter your full name.'); return; }
  if (!email)                            { setStatus('notice--danger','Please enter your email address.'); return; }
  if (!pdbCodes.length && !files.length) { setStatus('notice--danger','Please provide at least one PDB code or upload a structure file.'); return; }
  if (!dataTypes.length)                 { setStatus('notice--danger','Please select at least one data type.'); return; }
  if (!het)                              { setStatus('notice--danger','Please describe the heterogeneity in your data.'); return; }
  if (!issues)                           { setStatus('notice--danger','Please describe the issues communicating heterogeneity.'); return; }

  var btn = document.getElementById('sf-btn');
  btn.disabled = true;
  btn.innerHTML = '<span class="spin"></span> Submitting…';

  try {
    var ts     = new Date().toISOString().slice(0,19);
    var tsPath = ts.replace(/:/g,'-');
    var safe   = name.replace(/[^a-zA-Z0-9]+/g,'-').replace(/^-+|-+$/g,'').toLowerCase().slice(0,28);
    var folder = CFG.SUBMISSIONS_PATH + '/' + tsPath + '_' + safe;
    var yaml   = buildYaml({name,email,pdbCodes,dataTypes,doi,het,issues,residues,notes,fileNames:files.map(function(f){return f.name;}),ts});

    setStatus('notice--info','Creating submission record…');
    await workerPut(folder+'/metadata.yml', toB64(yaml), 'Add submission from '+name);

    for (var i=0; i<files.length; i++) {
      var f = files[i];
      setStatus('notice--info','Uploading '+esc(f.name)+' ('+(i+2)+'/'+(files.length+1)+')…');
      await workerPut(folder+'/'+f.name, await fileB64(f), 'Add '+f.name+' from '+name);
    }

    document.getElementById('sf-wrap').style.display = 'none';
    clearStatus();
    document.getElementById('sf-path').textContent  = folder + '/';
    document.getElementById('sf-email').textContent = email;
    document.getElementById('sf-done').style.display = 'block';

  } catch (err) {
    setStatus('notice--danger','Submission failed: '+(err.message||err)+'<br>Please try again or email <a href="mailto:diffuse@astera.org">diffuse@astera.org</a>.');
    btn.disabled = false;
    btn.innerHTML = '<i class="fas fa-paper-plane"></i> Submit';
  }
}

async function workerPut(path, content, message) {
  var r = await fetch(CFG.WORKER_URL, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ path, content, message })
  });
  var d = {};
  try { d = await r.json(); } catch(_) {}
  if (!r.ok) throw new Error(d.error || 'HTTP ' + r.status);
  return d;
}

function buildYaml(o) {
  var y  = '---\n';
  y += 'submitted_at: "'+o.ts+'Z"\n';
  y += 'submitter:\n  name: "'+q(o.name)+'"\n  email: "'+q(o.email)+'"\n';
  y += 'structures:\n';
  y += o.pdbCodes.length ? '  pdb_codes:\n'+o.pdbCodes.map(function(c){ return '    - "'+c+'"'; }).join('\n')+'\n' : '  pdb_codes: []\n';
  y += o.fileNames.length ? '  uploaded_files:\n'+o.fileNames.map(function(n){ return '    - "'+q(n)+'"'; }).join('\n')+'\n' : '  uploaded_files: []\n';
  y += 'data_types:\n'+(o.dataTypes.length ? o.dataTypes.map(function(t){ return '  - '+t; }).join('\n')+'\n' : '  []\n');
  y += 'publication:\n  doi: "'+q(o.doi)+'"\n';
  y += 'heterogeneity:\n  description: |\n'+o.het.split('\n').map(function(l){ return '    '+l; }).join('\n')+'\n';
  y += '  issues: |\n'+o.issues.split('\n').map(function(l){ return '    '+l; }).join('\n')+'\n';
  y += '  residues: "'+q(o.residues)+'"\n';
  y += 'notes: "'+q(o.notes)+'"\n---\n';
  return y;
}

function val(id) { return document.getElementById(id).value.trim(); }
function esc(s)  { return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }
function q(s)    { return (s||'').replace(/\\/g,'\\\\').replace(/"/g,'\\"'); }
function toB64(str) { return btoa(unescape(encodeURIComponent(str))); }
function fileB64(f) {
  return new Promise(function(res,rej){
    var r=new FileReader(); r.onload=function(e){res(e.target.result.split(',')[1]);}; r.onerror=rej; r.readAsDataURL(f);
  });
}
function setStatus(cls, html) {
  var el=document.getElementById('sf-status');
  el.className='notice '+cls; el.innerHTML=html; el.style.display='block';
}
function clearStatus() { document.getElementById('sf-status').style.display='none'; }
function doReset() {
  files=[];
  document.getElementById('sf-done').style.display='none';
  document.getElementById('sf-wrap').style.display='block';
  document.getElementById('sf').reset();
  document.getElementById('fi-list').innerHTML='';
  document.querySelector('.pdb-row input').value='';
  document.querySelectorAll('.pdb-row').forEach(function(r,i){if(i>0)r.remove();});
  document.querySelectorAll('.t-opt').forEach(function(el){el.classList.remove('on');});
  clearStatus();
  var btn=document.getElementById('sf-btn');
  btn.disabled=false; btn.innerHTML='<i class="fas fa-paper-plane"></i> Submit';
}
</script>
