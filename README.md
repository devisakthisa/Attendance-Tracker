
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Attendify | Attendance Tracker</title>
<style>
:root {
  --navy:#172554;
  --blue:#4f46e5;
  --bg:#f5f7fc;
  --text:#1e293b;
  --muted:#64748b;
  --border:#e5eaf2;
  --green:#15803d;
  --red:#dc2626;
}
* { box-sizing:border-box; }
body {
  margin:0;
  font-family:Inter,"Segoe UI",Arial,sans-serif;
  background:var(--bg);
  color:var(--text);
}
button,input,select { font:inherit; }
button { cursor:pointer; }
.layout { display:flex; min-height:100vh; }
.sidebar {
  width:245px; background:var(--navy); color:white;
  padding:28px 18px; flex-shrink:0;
}
.brand { font-size:24px; font-weight:800; margin-bottom:8px; }
.brand span { color:#a5b4fc; }
.tagline { font-size:12px; color:#cbd5e1; margin-bottom:36px; }
.nav-label {
  font-size:11px; color:#94a3b8; letter-spacing:1.5px;
  margin:25px 10px 12px;
}
.nav-item {
  display:block; padding:13px 14px; margin:6px 0;
  color:#cbd5e1; text-decoration:none; border-radius:9px;
  font-size:14px;
}
.nav-item.active,.nav-item:hover { background:#313d73; color:white; }
.sidebar-note {
  margin-top:45px; padding:15px; background:#ffffff12;
  border-radius:12px; font-size:12px; line-height:1.7;
  color:#cbd5e1;
}
main { flex:1; min-width:0; padding:30px; }
.topbar {
  display:flex; align-items:center; justify-content:space-between;
  gap:16px; flex-wrap:wrap; margin-bottom:30px;
}
.eyebrow { color:var(--blue); font-size:12px; font-weight:700; }
h1 { font-size:28px; margin:6px 0; }
.subtitle { color:var(--muted); font-size:14px; }
.date-chip {
  background:white; padding:12px 15px; border:1px solid var(--border);
  border-radius:10px; font-size:13px;
}
.section { margin-bottom:26px; scroll-margin-top:20px; }
.section-heading {
  display:flex; align-items:center; justify-content:space-between;
  gap:12px; flex-wrap:wrap; margin-bottom:15px;
}
h2 { font-size:18px; margin:0; }
.stats {
  display:grid; grid-template-columns:repeat(4,minmax(0,1fr));
  gap:16px; margin-bottom:28px;
}
.card {
  background:white; border:1px solid var(--border);
  border-radius:14px; padding:20px; min-width:0;
}
.stat-label { font-size:13px; color:var(--muted); }
.stat-number { font-size:29px; font-weight:800; margin:14px 0 7px; }
.stat-foot { font-size:12px; color:var(--muted); }
.stat-icon {
  display:flex; align-items:center; justify-content:center;
  width:39px; height:39px; border-radius:11px;
  background:#eef2ff; font-size:20px;
}
.green-bg { background:#dcfce7; }
.red-bg { background:#fee2e2; }
.amber-bg { background:#fef3c7; }
.panel { background:white; border:1px solid var(--border); border-radius:14px; padding:22px; }
.toolbar {
  display:flex; flex-wrap:wrap; gap:10px; margin-bottom:16px;
}
input,select {
  min-width:0; background:white; border:1px solid #dbe2ed;
  border-radius:8px; padding:11px 12px; color:var(--text);
}
input:focus,select:focus {
  outline:2px solid #c7d2fe; border-color:var(--blue);
}
.search { flex:1; min-width:150px; }
.btn {
  border:0; padding:11px 15px; border-radius:8px;
  font-size:13px; font-weight:700;
}
.primary { background:var(--blue); color:white; }
.primary:hover { background:#4338ca; }
.secondary { background:#eef2ff; color:#3730a3; }
.danger { background:#fee2e2; color:#991b1b; }
.table-wrap { overflow-x:auto; }
table { width:100%; border-collapse:collapse; white-space:nowrap; }
th {
  background:#f8fafc; color:var(--muted); text-align:left;
  font-size:11px; letter-spacing:.5px; padding:13px 12px;
}
td { padding:14px 12px; border-bottom:1px solid #edf0f5; font-size:13px; }
tbody tr:hover { background:#fafbff; }
.student-name { font-weight:700; }
.roll { color:var(--muted); font-size:12px; margin-top:4px; }
.status {
  border:0; padding:7px 9px; border-radius:7px;
  font-size:12px; font-weight:700; max-width:125px;
}
.status-present { color:#166534; background:#dcfce7; }
.status-absent { color:#991b1b; background:#fee2e2; }
.status-late { color:#92400e; background:#fef3c7; }
.status-unmarked { color:#475569; background:#f1f5f9; }
.progress {
  height:7px; background:#e9edf5; border-radius:10px;
  overflow:hidden; min-width:70px;
}
.progress div { height:100%; background:var(--blue); border-radius:10px; }
.report-grid { display:grid; grid-template-columns:1fr 1fr; gap:18px; }
.report-row { margin-top:20px; }
.report-label {
  display:flex; justify-content:space-between; gap:10px;
  font-size:13px; margin-bottom:9px;
}
.empty { padding:30px 10px; text-align:center; color:var(--muted); }
footer { text-align:center; color:var(--muted); font-size:12px; padding:20px 0; }
.modal-backdrop {
  display:none; position:fixed; inset:0; z-index:5;
  background:#0f172a88; align-items:center; justify-content:center;
  padding:16px;
}
.modal {
  background:white; width:100%; max-width:420px;
  padding:25px; border-radius:16px;
}
.modal h2 { margin-bottom:20px; }
.field { display:block; font-size:13px; font-weight:600; margin:14px 0; }
.field input { display:block; width:100%; margin-top:7px; }
.modal-actions { display:flex; justify-content:flex-end; gap:10px; margin-top:20px; }
.toast {
  position:fixed; bottom:20px; right:20px; background:#172554;
  color:white; padding:13px 18px; border-radius:10px;
  display:none; z-index:10; font-size:13px;
}
@media(max-width:1050px) {
  .stats { grid-template-columns:repeat(2,minmax(0,1fr)); }
}
@media(max-width:700px) {
  .layout { display:block; }
  .sidebar { width:100%; padding:18px; }
  .brand { font-size:22px; }
  .tagline { margin-bottom:12px; }
  .nav-label,.sidebar-note { display:none; }
  .nav-item { display:inline-block; padding:10px; margin:5px 2px; }
  main { padding:19px 13px; }
  h1 { font-size:24px; }
  .stats { gap:10px; }
  .card { padding:14px; }
  .stat-number { font-size:25px; }
  .panel { padding:14px; }
  .report-grid { grid-template-columns:1fr; }
}
</style>
</head>
<body>

<div class="layout">
  <aside class="sidebar">
    <div class="brand">Attend<span>ify.</span></div>
    <div class="tagline">SMART ATTENDANCE MANAGEMENT</div>

    <div class="nav-label">WORKSPACE</div>
    <a class="nav-item active" href="#dashboard">▦ &nbsp; Dashboard</a>
    <a class="nav-item" href="#attendance">▤ &nbsp; Attendance</a>
    <a class="nav-item" href="#reports">▥ &nbsp; Reports</a>

    <div class="nav-label">MANAGEMENT</div>
    <a class="nav-item" href="#students">♙ &nbsp; Students</a>

    <div class="sidebar-note">
      <strong>Attendance made simple.</strong><br>
      Manage student records, mark daily attendance and review attendance reports in one place.
    </div>
  </aside>

  <main>
    <header class="topbar" id="dashboard">
      <div>
        <div class="eyebrow">ATTENDANCE MANAGEMENT SYSTEM</div>
        <h1>Dashboard Overview</h1>
        <div class="subtitle">Track your class attendance at a glance.</div>
      </div>
      <div class="date-chip">📅 <span id="todayText"></span></div>
    </header>

    <section class="stats">
      <div class="card">
        <div class="stat-icon">♙</div>
        <div class="stat-label">Total Students</div>
        <div class="stat-number" id="totalCount">0</div>
        <div class="stat-foot">Registered students</div>
      </div>
      <div class="card">
        <div class="stat-icon green-bg">✓</div>
        <div class="stat-label">Present Today</div>
        <div class="stat-number" id="presentCount">0</div>
        <div class="stat-foot">Marked present</div>
      </div>
      <div class="card">
        <div class="stat-icon red-bg">✕</div>
        <div class="stat-label">Absent Today</div>
        <div class="stat-number" id="absentCount">0</div>
        <div class="stat-foot">Marked absent</div>
      </div>
      <div class="card">
        <div class="stat-icon amber-bg">◷</div>
        <div class="stat-label">Attendance Rate</div>
        <div class="stat-number" id="rateCount">0%</div>
        <div class="stat-foot">For the selected date</div>
      </div>
    </section>

    <section class="section panel" id="attendance">
      <div class="section-heading">
        <div>
          <h2>Daily Attendance</h2>
          <div class="subtitle" style="margin-top:6px">Select a date and update each student's status.</div>
        </div>
        <button class="btn primary" onclick="openModal()">+ Add Student</button>
      </div>

      <div class="toolbar">
        <input type="date" id="attendanceDate" aria-label="Attendance date">
        <input class="search" type="search" id="searchInput"
          placeholder="Search name or roll number..." aria-label="Search students">
        <select id="statusFilter" aria-label="Filter by status">
          <option value="All">All statuses</option>
          <option value="Present">Present</option>
          <option value="Absent">Absent</option>
          <option value="Late">Late</option>
          <option value="Unmarked">Unmarked</option>
        </select>
      </div>

      <div class="table-wrap">
        <table>
          <thead>
            <tr>
              <th>STUDENT</th>
              <th>ATTENDANCE STATUS</th>
              <th>OVERALL ATTENDANCE</th>
              <th>ACTION</th>
            </tr>
          </thead>
          <tbody id="attendanceBody"></tbody>
        </table>
      </div>
      <div class="empty" id="emptyMessage" hidden>No students found. Add a student to get started.</div>

      <div class="toolbar" style="margin:18px 0 0">
        <button class="btn secondary" onclick="markAll('Present')">Mark All Present</button>
        <button class="btn secondary" onclick="markAll('Absent')">Mark All Absent</button>
        <button class="btn primary" onclick="exportCSV()">Export CSV ↓</button>
      </div>
    </section>

    <section class="section" id="students">
      <div class="section-heading">
        <h2>Student Management</h2>
        <span class="subtitle">Add and manage your class list.</span>
      </div>
      <div class="panel">
        <div class="subtitle">
          Use <strong>+ Add Student</strong> above to register a student.
          Student records are stored in this browser.
        </div>
      </div>
    </section>

    <section class="section" id="reports">
      <div class="section-heading">
        <h2>Attendance Reports</h2>
        <span class="subtitle">Based on all recorded attendance dates.</span>
      </div>
      <div class="report-grid">
        <div class="panel">
          <h2>Class Attendance</h2>
          <div class="subtitle" style="margin-top:7px">Present and late records count as attended.</div>
          <div class="report-row">
            <div class="report-label"><span>Present</span><strong id="reportPresent">0</strong></div>
            <div class="progress"><div id="presentBar" style="width:0%"></div></div>
          </div>
          <div class="report-row">
            <div class="report-label"><span>Absent</span><strong id="reportAbsent">0</strong></div>
            <div class="progress"><div id="absentBar" style="width:0%;background:#ef4444"></div></div>
          </div>
          <div class="report-row">
            <div class="report-label"><span>Late</span><strong id="reportLate">0</strong></div>
            <div class="progress"><div id="lateBar" style="width:0%;background:#f59e0b"></div></div>
          </div>
        </div>
        <div class="panel">
          <h2>Student Summary</h2>
          <div class="subtitle" style="margin-top:7px">Attendance percentage for each student.</div>
          <div class="table-wrap" style="margin-top:14px">
            <table>
              <thead><tr><th>NAME</th><th>ATTENDED</th><th>RATE</th></tr></thead>
              <tbody id="reportBody"></tbody>
            </table>
          </div>
        </div>
      </div>
    </section>

    <footer>Attendify © 2026 · Student Attendance Tracker</footer>
  </main>
</div>

<div class="modal-backdrop" id="modalBackdrop">
  <div class="modal">
    <h2>Add New Student</h2>
    <form id="studentForm">
      <label class="field">Student Name
        <input id="studentName" required maxlength="80" placeholder="Enter full name">
      </label>
      <label class="field">Roll Number
        <input id="studentRoll" required maxlength="30" placeholder="e.g. CSE001">
      </label>
      <div class="modal-actions">
        <button type="button" class="btn secondary" onclick="closeModal()">Cancel</button>
        <button type="submit" class="btn primary">Add Student</button>
      </div>
    </form>
  </div>
</div>
<div class="toast" id="toast" role="status"></div>

<script>
const $ = id => document.getElementById(id);
const today = () => {
  const d = new Date();
  return `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`;
};
const dateInput = $('attendanceDate');
dateInput.value = today();

let students = [];
let records = {};
let toastTimer;

try {
  students = JSON.parse(localStorage.getItem('attendify_students')) || [];
  records = JSON.parse(localStorage.getItem('attendify_records')) || {};
  if (!Array.isArray(students) || !records || typeof records !== 'object') {
    throw new Error('Invalid saved data');
  }
} catch {
  students = [];
  records = {};
}

function save() {
  try {
    localStorage.setItem('attendify_students', JSON.stringify(students));
    localStorage.setItem('attendify_records', JSON.stringify(records));
  } catch {
    notify('Unable to save. Check your browser storage.');
  }
}

function notify(message) {
  $('toast').textContent = message;
  $('toast').style.display = 'block';
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => $('toast').style.display = 'none', 2400);
}

function escapeHTML(value) {
  return String(value).replace(/[&<>"']/g, ch => ({
    '&':'&amp;', '<':'&lt;', '>':'&gt;',
    '"':'&quot;', "'":'&#39;'
  })[ch]);
}

function getStatus(studentId, date = dateInput.value) {
  return records[date]?.[studentId] || 'Unmarked';
}

function setStatus(studentId, status) {
  const date = dateInput.value;
  if (!records[date]) records[date] = {};
  if (status === 'Unmarked') {
    delete records[date][studentId];
  } else {
    records[date][studentId] = status;
  }
  save();
  render();
  notify('Attendance updated successfully.');
}

function studentStats(id) {
  let attended = 0, absent = 0, late = 0;
  Object.values(records).forEach(day => {
    const status = day?.[id];
    if (status === 'Present') attended++;
    if (status === 'Absent') absent++;
    if (status === 'Late') late++;
  });
  const total = attended + absent + late;
  return { attended, absent, late, total, rate: total ? Math.round(attended / total * 100) : 0 };
}

function render() {
  const date = dateInput.value;
  $('todayText').textContent = new Date(date + 'T12:00:00').toLocaleDateString(
    'en-IN', { day:'numeric', month:'short', year:'numeric' }
  );

  const present = students.filter(s => getStatus(s.id) === 'Present').length;
  const absent = students.filter(s => getStatus(s.id) === 'Absent').length;
  const late = students.filter(s => getStatus(s.id) === 'Late').length;
  const marked = present + absent + late;
  const rate = marked ? Math.round((present + late) / marked * 100) : 0;

  $('totalCount').textContent = students.length;
  $('presentCount').textContent = present;
  $('absentCount').textContent = absent;
  $('rateCount').textContent = rate + '%';

  const query = $('searchInput').value.trim().toLowerCase();
  const filter = $('statusFilter').value;

  const visible = students.filter(s => {
    const status = getStatus(s.id);
    const matchesSearch = s.name.toLowerCase().includes(query) ||
      s.roll.toLowerCase().includes(query);
    return matchesSearch && (filter === 'All' || status === filter);
  });

  $('attendanceBody').innerHTML = visible.map(s => {
    const status = getStatus(s.id);
    const stat = studentStats(s.id);
    const className = {
      Present:'status-present', Absent:'status-absent',
      Late:'status-late', Unmarked:'status-unmarked'
    }[status];

    return `<tr>
      <td><div class="student-name">${escapeHTML(s.name)}</div>
          <div class="roll">${escapeHTML(s.roll)}</div></td>
      <td><select class="status ${className}" aria-label="Status for ${escapeHTML(s.name)}"
          onchange="setStatus('${s.id}',this.value)">
          ${['Unmarked','Present','Absent','Late'].map(x =>
            `<option value="${x}" ${status === x ? 'selected' : ''}>${x}</option>`
          ).join('')}
      </select></td>
      <td><div style="font-weight:700;margin-bottom:7px">${stat.rate}%</div>
          <div class="progress"><div style="width:${stat.rate}%"></div></div>
          <div class="roll">${stat.attended} attended / ${stat.total} marked</div></td>
      <td><button class="btn danger" onclick="removeStudent('${s.id}')">Remove</button></td>
    </tr>`;
  }).join('');

  $('emptyMessage').hidden = visible.length > 0;
  $('reportPresent').textContent = present;
  $('reportAbsent').textContent = absent;
  $('reportLate').textContent = late;
  $('presentBar').style.width = (marked ? present / marked * 100 : 0) + '%';
  $('absentBar').style.width = (marked ? absent / marked * 100 : 0) + '%';
  $('lateBar').style.width = (marked ? late / marked * 100 : 0) + '%';

  $('reportBody').innerHTML = students.map(s => {
    const stat = studentStats(s.id);
    return `<tr><td>${escapeHTML(s.name)}</td>
      <td>${stat.attended}/${stat.total}</td><td>${stat.rate}%</td></tr>`;
  }).join('');

  if (!students.length) {
    $('reportBody').innerHTML =
      '<tr><td colspan="3" style="color:#64748b">No student records yet.</td></tr>';
  }
}

function openModal() {
  $('modalBackdrop').style.display = 'flex';
  $('studentName').focus();
}
function closeModal() {
  $('modalBackdrop').style.display = 'none';
  $('studentForm').reset();
}
$('modalBackdrop').addEventListener('click', e => {
  if (e.target === $('modalBackdrop')) closeModal();
});

$('studentForm').addEventListener('submit', e => {
  e.preventDefault();
  const name = $('studentName').value.trim();
  const roll = $('studentRoll').value.trim();

  if (!name || !roll) return;
  if (students.some(s => s.roll.toLowerCase() === roll.toLowerCase())) {
    notify('This roll number already exists.');
    return;
  }

  const student = { id: 's' + Date.now() + Math.random().toString(36).slice(2,7), name, roll };
  students.push(student);
  save();
  closeModal();
  render();
  notify('Student added successfully.');
});

function removeStudent(id) {
  const student = students.find(s => s.id === id);
  if (!student) return;
  if (!confirm(`Remove ${student.name} and their attendance records?`)) return;

  students = students.filter(s => s.id !== id);
  Object.values(records).forEach(day => delete day[id]);
  save();
  render();
  notify('Student removed.');
}

function markAll(status) {
  if (!students.length) {
    notify('Add students first.');
    return;
  }
  if (!confirm(`Mark all ${students.length} students as ${status}?`)) return;
  if (!records[dateInput.value]) records[dateInput.value] = {};
  students.forEach(s => records[dateInput.value][s.id] = status);
  save();
  render();
  notify(`All students marked ${status.toLowerCase()}.`);
}

function exportCSV() {
  const rows = [['Name','Roll Number','Date','Status','Attendance Rate']];
  students.forEach(s => {
    rows.push([s.name, s.roll, dateInput.value, getStatus(s.id), studentStats(s.id).rate + '%']);
  });

  const csv = rows.map(row => row.map(v =>
    '"' + String(v).replace(/"/g, '""') + '"'
  ).join(',')).join('\r\n');

  const blob = new Blob(['\uFEFF' + csv], { type:'text/csv;charset=utf-8;' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'attendance-' + dateInput.value + '.csv';
  a.click();
  URL.revokeObjectURL(url);
  notify('CSV report downloaded.');
}

dateInput.addEventListener('change', render);
$('searchInput').addEventListener('input', render);
$('statusFilter').addEventListener('change', render);

render();
</script>
</body>
</html>
