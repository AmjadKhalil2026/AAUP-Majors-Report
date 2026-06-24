<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AAUP - Faculty - Report</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
<style>
  :root {
    --c1: #647B7D;
    --c2: #4A5F61;
    --c3: #A78C9B;
    --c4: #7EF1FC;
    --c5: #FC7EC6;
    --c6: #FCEC7E;
    --c7: #7D7A64;
    --white: #F0FEFF;
    --light-bg: #F5FEFF;
    --card-bg: #FFFFFF;
    --border: #C8EDEF;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: 'Segoe UI', Arial, sans-serif; background: var(--light-bg); color: var(--c1); }

  /* ========== LANDING PAGE ========== */
  #landing {
    min-height: 100vh;
    background: linear-gradient(135deg, #3A5254 0%, #647B7D 50%, #7D7A64 100%);
    display: flex; flex-direction: column; align-items: center; justify-content: center;
    text-align: center; padding: 40px 20px;
  }
  .landing-logo-wrap { margin-bottom: 28px; }
  .landing-logo {
    width: 120px; height: 120px; border-radius: 50%;
    background: #FFFFFF;
    display: flex; align-items: center; justify-content: center;
    margin: 0 auto 18px; border: 4px solid var(--c4); box-shadow: 0 0 40px rgba(126,241,252,0.4);
    overflow: hidden; padding: 4px;
  }
  .landing-logo svg { width: 70px; height: 70px; }
  .uni-name {
    color: var(--c4); font-size: 2rem; font-weight: 800; letter-spacing: 1px;
    text-shadow: 0 2px 12px rgba(126,241,252,0.4); line-height: 1.2;
  }
  .uni-sub { color: var(--c4); opacity: 0.7; font-size: 1rem; margin-top: 4px; letter-spacing: 3px; text-transform: uppercase; }
  .divider-line { width: 80px; height: 3px; background: linear-gradient(90deg, var(--c5), var(--c6)); /* pink to cyan */ border-radius: 2px; margin: 24px auto; }
  .report-title-landing { color: #fff; font-size: 1.9rem; font-weight: 700; margin-bottom: 10px; }
  .landing-info { margin: 24px 0; background: rgba(255,255,255,0.07); border-radius: 16px; padding: 22px 36px; border: 1px solid rgba(217,182,163,0.2); display: inline-block; }
  .landing-info p { color: var(--c4); font-size: 1rem; line-height: 2; }
  .landing-info span { color: #fff; font-weight: 600; }
  .btn-view {
    margin-top: 28px;
    background: linear-gradient(135deg, var(--c5), var(--c6));
    color: var(--c1); font-size: 1.1rem; font-weight: 700;
    border: none; border-radius: 50px; padding: 16px 50px;
    cursor: pointer; letter-spacing: 1px; box-shadow: 0 8px 28px rgba(252,126,198,0.35);
    transition: transform .2s, box-shadow .2s;
  }
  .btn-view:hover { transform: translateY(-3px); box-shadow: 0 14px 36px rgba(252,126,198,0.45); }

  /* ========== REPORT PAGE ========== */
  #report { display: none; }
  .report-header {
    background: linear-gradient(135deg, #3A5254 0%, #647B7D 100%);
    padding: 0; position: sticky; top: 0; z-index: 100;
    box-shadow: 0 4px 20px rgba(7,5,13,0.3);
  }
  .header-top {
    display: flex; align-items: center; justify-content: space-between;
    padding: 16px 36px; flex-wrap: wrap; gap: 12px;
  }
  .header-logo-area { display: flex; align-items: center; gap: 16px; }
  .hdr-logo {
    width: 56px; height: 56px; border-radius: 50%;
    background: #FFFFFF;
    display: flex; align-items: center; justify-content: center;
    border: 2px solid var(--c4); flex-shrink: 0;
  }
  .hdr-logo svg { width: 32px; height: 32px; }
  .hdr-uni { color: var(--c4); font-size: 1.05rem; font-weight: 700; line-height: 1.3; }
  .hdr-uni-sub { color: rgba(217,182,163,0.6); font-size: 0.72rem; letter-spacing: 2px; text-transform: uppercase; }
  .hdr-title { color: #fff; font-size: 1.3rem; font-weight: 700; text-align: center; flex: 1; }
  .hdr-actions { display: flex; gap: 10px; flex-wrap: wrap; }
  .btn-back {
    background: transparent; border: 2px solid var(--c4); color: var(--c4);
    font-size: 0.85rem; font-weight: 600; border-radius: 50px; padding: 8px 20px;
    cursor: pointer; transition: all .2s;
  }
  .btn-back:hover { background: var(--c4); color: var(--c1); }
  .btn-desc {
    background: linear-gradient(135deg, var(--c5), var(--c6));
    border: none; color: var(--c1); font-size: 0.85rem; font-weight: 700;
    border-radius: 50px; padding: 8px 20px; cursor: pointer; transition: all .2s;
  }
  .btn-desc:hover { opacity: 0.85; }

  .nav-tabs {
    display: flex; gap: 0; overflow-x: auto;
    padding: 0 36px; border-top: 1px solid rgba(255,255,255,0.08);
  }
  .nav-tab {
    padding: 12px 22px; color: rgba(217,182,163,0.6); font-size: 0.88rem; font-weight: 600;
    cursor: pointer; border-bottom: 3px solid transparent; transition: all .2s;
    white-space: nowrap; letter-spacing: 0.5px;
  }
  .nav-tab:hover { color: var(--c4); }
  .nav-tab.active { color: var(--c4); border-bottom-color: var(--c4); }

  /* ========== CONTENT ========== */
  .report-body { padding: 28px 36px; max-width: 1400px; margin: 0 auto; }
  .section { display: none; }
  .section.active { display: block; }

  /* Stats cards */
  .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 18px; margin-bottom: 30px; }
  .stat-card {
    background: var(--card-bg); border-radius: 16px; padding: 22px 20px;
    border: 1px solid var(--border); text-align: center;
    box-shadow: 0 2px 12px rgba(7,5,13,0.06); transition: transform .2s;
  }
  .stat-card:hover { transform: translateY(-3px); }
  .stat-icon { font-size: 2rem; margin-bottom: 8px; }
  .stat-val { font-size: 2rem; font-weight: 800; color: var(--c5); margin-bottom: 4px; }
  .stat-label { font-size: 0.8rem; color: var(--c3); text-transform: uppercase; letter-spacing: 1px; }

  /* Charts grid */
  .charts-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(420px, 1fr)); gap: 22px; margin-bottom: 28px; }
  .chart-card {
    background: var(--card-bg); border-radius: 16px; padding: 24px;
    border: 1px solid var(--border); box-shadow: 0 2px 12px rgba(7,5,13,0.06);
  }
  .chart-card.wide { grid-column: 1 / -1; }
  .chart-title { font-size: 1rem; font-weight: 700; color: var(--c2); margin-bottom: 18px; display: flex; align-items: center; gap: 8px; }
  .chart-title::before { content: ''; width: 4px; height: 18px; background: linear-gradient(180deg, var(--c5), var(--c4)); border-radius: 2px; }
  .chart-wrap { position: relative; height: 280px; }
  .chart-wrap.tall { height: 400px; }

  /* TABLE */
  .table-controls {
    display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap;
    gap: 14px; margin-bottom: 18px;
  }
  .search-box {
    padding: 10px 18px; border: 2px solid var(--border); border-radius: 50px;
    font-size: 0.9rem; outline: none; min-width: 240px; background: var(--card-bg);
    transition: border-color .2s;
  }
  .search-box:focus { border-color: var(--c5); }
  .filter-select {
    padding: 10px 18px; border: 2px solid var(--border); border-radius: 50px;
    font-size: 0.9rem; outline: none; background: var(--card-bg); cursor: pointer;
    transition: border-color .2s;
  }
  .filter-select:focus { border-color: var(--c5); }
  .btn-add {
    background: linear-gradient(135deg, var(--c5), var(--c6));
    border: none; color: var(--c1); font-size: 0.9rem; font-weight: 700;
    border-radius: 50px; padding: 10px 24px; cursor: pointer; transition: opacity .2s;
  }
  .btn-add:hover { opacity: 0.85; }
  .table-wrap { overflow-x: auto; border-radius: 16px; box-shadow: 0 2px 12px rgba(7,5,13,0.06); }
  table { width: 100%; border-collapse: collapse; background: var(--card-bg); font-size: 0.875rem; }
  thead tr { background: linear-gradient(135deg, #3A5254, #647B7D); }
  thead th {
    padding: 14px 14px; color: var(--c4); font-weight: 700;
    text-align: left; font-size: 0.8rem; letter-spacing: 0.5px; white-space: nowrap;
    cursor: pointer; user-select: none;
  }
  thead th:hover { color: #fff; }
  tbody tr { border-bottom: 1px solid var(--border); transition: background .15s; }
  tbody tr:hover { background: rgba(217,182,163,0.08); }
  tbody td { padding: 12px 14px; color: var(--c1); white-space: nowrap; }
  .badge {
    display: inline-block; padding: 3px 10px; border-radius: 50px; font-size: 0.75rem; font-weight: 600;
  }
  .badge-sci { background: rgba(64,73,89,0.12); color: var(--c3); }
  .badge-all { background: rgba(166,128,114,0.15); color: var(--c5); }
  .badge-bach { background: rgba(21,20,38,0.1); color: var(--c2); }
  .action-btns { display: flex; gap: 6px; }
  .btn-edit, .btn-del {
    padding: 5px 12px; border-radius: 50px; font-size: 0.75rem; font-weight: 600;
    border: none; cursor: pointer; transition: all .15s;
  }
  .btn-edit { background: rgba(217,182,163,0.2); color: var(--c5); }
  .btn-edit:hover { background: var(--c5); color: #fff; }
  .btn-del { background: rgba(220,53,53,0.1); color: #c0392b; }
  .btn-del:hover { background: #c0392b; color: #fff; }

  /* MODAL */
  .modal-overlay {
    position: fixed; inset: 0; background: rgba(7,5,13,0.7); z-index: 1000;
    display: none; align-items: center; justify-content: center; padding: 20px;
  }
  .modal-overlay.open { display: flex; }
  .modal {
    background: var(--card-bg); border-radius: 20px; padding: 32px;
    max-width: 640px; width: 100%; max-height: 90vh; overflow-y: auto;
    box-shadow: 0 24px 80px rgba(7,5,13,0.4);
  }
  .modal-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 24px; }
  .modal-title { font-size: 1.2rem; font-weight: 800; color: var(--c1); }
  .modal-close { background: none; border: none; font-size: 1.5rem; cursor: pointer; color: var(--c3); line-height: 1; }
  .form-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  .form-group { display: flex; flex-direction: column; gap: 6px; }
  .form-group.full { grid-column: 1 / -1; }
  .form-group label { font-size: 0.8rem; font-weight: 600; color: var(--c3); text-transform: uppercase; letter-spacing: 0.5px; }
  .form-group input, .form-group select {
    padding: 10px 14px; border: 2px solid var(--border); border-radius: 10px;
    font-size: 0.9rem; outline: none; transition: border-color .2s;
  }
  .form-group input:focus, .form-group select:focus { border-color: var(--c5); }
  .modal-footer { margin-top: 24px; display: flex; gap: 12px; justify-content: flex-end; }
  .btn-cancel { background: var(--border); border: none; color: var(--c3); font-weight: 600; border-radius: 50px; padding: 10px 24px; cursor: pointer; }
  .btn-save { background: linear-gradient(135deg, var(--c5), var(--c6)); border: none; color: var(--c1); font-weight: 700; border-radius: 50px; padding: 10px 28px; cursor: pointer; }

  /* DESC MODAL */
  .desc-content { line-height: 1.8; color: var(--c3); }
  .desc-content h3 { color: var(--c1); font-size: 1rem; margin: 16px 0 6px; }
  .desc-content ul { padding-left: 20px; }
  .desc-content li { margin-bottom: 6px; }

  /* Pagination */
  .pagination { display: flex; gap: 6px; align-items: center; justify-content: center; margin-top: 18px; }
  .pg-btn {
    padding: 7px 13px; border-radius: 8px; border: 1.5px solid var(--border);
    background: var(--card-bg); cursor: pointer; font-size: 0.85rem; color: var(--c3);
    transition: all .15s;
  }
  .pg-btn.active { background: var(--c5); color: #fff; border-color: var(--c5); }
  .pg-btn:hover:not(.active) { border-color: var(--c5); color: var(--c5); }

  /* Section titles */
  .section-title { font-size: 1.5rem; font-weight: 800; color: var(--c1); margin-bottom: 6px; }
  .section-sub { color: var(--c3); font-size: 0.9rem; margin-bottom: 24px; }

  /* Comparison bars */
  .comp-bar-wrap { margin-bottom: 10px; }
  .comp-bar-label { display: flex; justify-content: space-between; font-size: 0.82rem; color: var(--c3); margin-bottom: 4px; }
  .comp-bar-outer { background: var(--border); border-radius: 50px; height: 10px; overflow: hidden; }
  .comp-bar-inner { height: 100%; border-radius: 50px; background: linear-gradient(90deg, var(--c5), var(--c6)); /* pink to cyan */ transition: width 1s ease; }

  @media (max-width: 768px) {
    .report-body { padding: 16px; }
    .header-top { padding: 14px 16px; }
    .nav-tabs { padding: 0 16px; }
    .charts-grid { grid-template-columns: 1fr; }
    .form-grid { grid-template-columns: 1fr; }
    .uni-name { font-size: 1.4rem; }
  }
</style>
</head>
<body>

<!-- ============= LANDING PAGE ============= -->
<div id="landing">
  <div class="landing-logo-wrap">
    <div class="landing-logo">
      <img src="data:image/png;base64,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" alt="AAUP Logo" style="width:112px;height:112px;object-fit:contain;border-radius:50%;">
    </div>
    <div class="uni-name">Arab American University - AAUP</div>
    <div class="uni-sub">Palestine · Ramallah Campus</div>
  </div>
  <div class="divider-line"></div>
  <div class="report-title-landing">AAUP — Faculty — Report</div>
  <div class="landing-info">
    <p><span>Student:</span> Razan Idris رزان إدريس</p>
    <p><span>Course:</span> Introduction to coding for Journalism</p>
    <p><span>Instructor:</span> Amjad Khalil أمجد خليل</p>
  </div>
  <button class="btn-view" onclick="openReport()">📊 View Report</button>
</div>

<!-- ============= REPORT PAGE ============= -->
<div id="report">
  <div class="report-header">
    <div class="header-top">
      <div class="header-logo-area">
        <div class="hdr-logo">
          <img src="data:image/png;base64,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" alt="AAUP Logo" style="width:52px;height:52px;object-fit:contain;border-radius:50%;">
        </div>
        <div>
          <div class="hdr-uni">Arab American University</div>
          <div class="hdr-uni-sub">Palestine · Ramallah</div>
        </div>
      </div>
      <div class="hdr-title">AAUP — Faculty — Report</div>
      <div class="hdr-actions">
        <button class="btn-desc" onclick="openDesc()">📋 Project Description</button>
        <button class="btn-back" onclick="backToLanding()">← Back to Home</button>
      </div>
    </div>
    <div class="nav-tabs">
      <div class="nav-tab active" onclick="showSection('overview',this)">📊 Overview</div>
      <div class="nav-tab" onclick="showSection('charts',this)">📈 Charts</div>
      <div class="nav-tab" onclick="showSection('comparison',this)">🔍 Comparison</div>
      <div class="nav-tab" onclick="showSection('majors',this)">📋 Majors Table</div>
    </div>
  </div>

  <div class="report-body">

    <!-- OVERVIEW SECTION -->
    <div class="section active" id="sec-overview">
      <div class="section-title">University Overview</div>
      <div class="section-sub">AAUP Ramallah Campus — Academic Data Summary for 45 Majors</div>
      <div class="stats-grid" id="statsGrid"></div>
      <div class="charts-grid">
        <div class="chart-card">
          <div class="chart-title">Students by Faculty</div>
          <div class="chart-wrap"><canvas id="chartFacultyStudents"></canvas></div>
        </div>
        <div class="chart-card">
          <div class="chart-title">High School Stream Distribution</div>
          <div class="chart-wrap"><canvas id="chartStream"></canvas></div>
        </div>
        <div class="chart-card">
          <div class="chart-title">Average Age by Faculty</div>
          <div class="chart-wrap"><canvas id="chartAge"></canvas></div>
        </div>
        <div class="chart-card">
          <div class="chart-title">Employment Rate by Faculty (%)</div>
          <div class="chart-wrap"><canvas id="chartEmploy"></canvas></div>
        </div>
      </div>
    </div>

    <!-- CHARTS SECTION -->
    <div class="section" id="sec-charts">
      <div class="section-title">Detailed Analytics</div>
      <div class="section-sub">In-depth visual analysis of academic data across all majors</div>
      <div class="charts-grid">
        <div class="chart-card wide">
          <div class="chart-title">Students Count per Major (All 45 Majors)</div>
          <div class="chart-wrap tall"><canvas id="chartAllStudents"></canvas></div>
        </div>
        <div class="chart-card wide">
          <div class="chart-title">Graduates Per Year by Major</div>
          <div class="chart-wrap tall"><canvas id="chartGrads"></canvas></div>
        </div>
        <div class="chart-card">
          <div class="chart-title">High School GPA Required vs Employment Rate</div>
          <div class="chart-wrap"><canvas id="chartGpaEmploy"></canvas></div>
        </div>
        <div class="chart-card">
          <div class="chart-title">Male vs Female Students by Faculty</div>
          <div class="chart-wrap"><canvas id="chartGender"></canvas></div>
        </div>
      </div>
    </div>

    <!-- COMPARISON SECTION -->
    <div class="section" id="sec-comparison">
      <div class="section-title">Major Comparison</div>
      <div class="section-sub">Compare any two majors side by side across key metrics</div>
      <div style="display:flex;gap:16px;flex-wrap:wrap;margin-bottom:24px;align-items:center;">
        <select id="cmpA" class="filter-select" onchange="renderComparison()"></select>
        <span style="font-weight:700;color:var(--c5);font-size:1.1rem;">VS</span>
        <select id="cmpB" class="filter-select" onchange="renderComparison()"></select>
      </div>
      <div id="cmpResult"></div>
      <div class="chart-card" style="margin-top:24px;">
        <div class="chart-title">Visual Comparison</div>
        <div class="chart-wrap"><canvas id="chartCmp"></canvas></div>
      </div>
    </div>

    <!-- MAJORS TABLE SECTION -->
    <div class="section" id="sec-majors">
      <div class="section-title">Majors Data Table</div>
      <div class="section-sub">Full editable dataset — add, edit or remove majors</div>
      <div class="table-controls">
        <input type="text" class="search-box" placeholder="🔍 Search majors, faculty…" id="searchInput" oninput="filterTable()">
        <select class="filter-select" id="filterFaculty" onchange="filterTable()">
          <option value="">All Faculties</option>
        </select>
        <select class="filter-select" id="filterStream" onchange="filterTable()">
          <option value="">All Streams</option>
          <option value="Scientific">Scientific</option>
          <option value="All Streams">All Streams</option>
        </select>
        <button class="btn-add" onclick="openModal(null)">+ Add Major</button>
      </div>
      <div class="table-wrap">
        <table>
          <thead>
            <tr>
              <th onclick="sortTable('majoes')">#  Major ↕</th>
              <th onclick="sortTable('Faculty')">Faculty ↕</th>
              <th onclick="sortTable('Degree')">Degree</th>
              <th onclick="sortTable('Average Age')">Avg Age ↕</th>
              <th onclick="sortTable('High School GPA Required')">GPA Req ↕</th>
              <th onclick="sortTable('High School Stream')">HS Stream</th>
              <th onclick="sortTable('Students Count')">Students ↕</th>
              <th onclick="sortTable('Male Students')">Male ↕</th>
              <th onclick="sortTable('Female Students')">Female ↕</th>
              <th onclick="sortTable('Employment Rate %')">Employ% ↕</th>
              <th onclick="sortTable('Graduates Per Year')">Grads/Yr ↕</th>
              <th>Actions</th>
            </tr>
          </thead>
          <tbody id="tableBody"></tbody>
        </table>
      </div>
      <div class="pagination" id="pagination"></div>
    </div>

  </div><!-- end report-body -->
</div><!-- end report -->

<!-- ============= ADD/EDIT MODAL ============= -->
<div class="modal-overlay" id="modalOverlay">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title" id="modalTitle">Add New Major</div>
      <button class="modal-close" onclick="closeModal()">×</button>
    </div>
    <div class="form-grid">
      <div class="form-group full">
        <label>Major Name</label>
        <input type="text" id="f_major" placeholder="e.g. Computer Science">
      </div>
      <div class="form-group">
        <label>Faculty</label>
        <input type="text" id="f_faculty" placeholder="e.g. Engineering">
      </div>
      <div class="form-group">
        <label>Degree</label>
        <select id="f_degree">
          <option>Bachelor</option>
          <option>Master</option>
          <option>PhD</option>
        </select>
      </div>
      <div class="form-group">
        <label>Average Age</label>
        <input type="number" id="f_age" min="17" max="35" placeholder="20">
      </div>
      <div class="form-group">
        <label>HS GPA Required</label>
        <input type="number" id="f_gpa" min="0" max="100" placeholder="75">
      </div>
      <div class="form-group">
        <label>HS Stream</label>
        <select id="f_stream">
          <option>Scientific</option>
          <option>All Streams</option>
          <option>Literary</option>
        </select>
      </div>
      <div class="form-group">
        <label>Students Count</label>
        <input type="number" id="f_students" min="0" placeholder="100">
      </div>
      <div class="form-group">
        <label>Study Years</label>
        <input type="number" id="f_years" min="1" max="10" placeholder="4">
      </div>
      <div class="form-group">
        <label>Male Students</label>
        <input type="number" id="f_male" min="0" placeholder="50">
      </div>
      <div class="form-group">
        <label>Female Students</label>
        <input type="number" id="f_female" min="0" placeholder="50">
      </div>
      <div class="form-group">
        <label>Employment Rate %</label>
        <input type="number" id="f_employ" min="0" max="100" placeholder="80">
      </div>
      <div class="form-group">
        <label>Graduates Per Year</label>
        <input type="number" id="f_grads" min="0" placeholder="80">
      </div>
      <div class="form-group">
        <label>Credit Hours</label>
        <input type="number" id="f_credits" min="0" placeholder="132">
      </div>
      <div class="form-group">
        <label>Cost Per Credit (NIS)</label>
        <input type="number" id="f_cost" min="0" placeholder="180">
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn-cancel" onclick="closeModal()">Cancel</button>
      <button class="btn-save" onclick="saveMajor()">Save Major</button>
    </div>
  </div>
</div>

<!-- ============= DESC MODAL ============= -->
<div class="modal-overlay" id="descOverlay">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">📋 Project Description</div>
      <button class="modal-close" onclick="closeDesc()">×</button>
    </div>
    <div class="desc-content">
      <h3>عن هذا المشروع</h3>
      <p>This interactive academic data report was developed as part of the <strong>Introduction to Programming for Journalistic Purposes</strong> course at the Arab American University (AAUP), Ramallah Campus.</p>
      <h3>Student Information</h3>
      <ul>
        <li><strong>Student:</strong> Razan Idris الطالبة: رزان إدريس</li>
        <li><strong>Course:</strong> Introduction to Coding for Journalism  مدخل في البرمجة لأغراض صحفية</li>
        <li><strong>Instructor:</strong> Amjad J. Khalil  المحاضر: أمجد خليل</li>
        <li><strong>Institution:</strong> Arab American University-AAUP — Ramallah Campus</li>
      </ul>
      <h3>Dataset Overview</h3>
      <ul>
        <li>45 academic majors across 13 faculties</li>
        <li>Over 3,500 students total enrollment</li>
        <li>Data includes: degree type, average student age, high school GPA requirements, school stream, gender breakdown, employment rates, and graduates per year</li>
      </ul>
      <h3>Features</h3>
      <ul>
        <li>Interactive charts: faculty distribution, age, GPA, gender, employment</li>
        <li>Full-text search and faculty/stream filtering</li>
        <li>Add, edit, and delete major records dynamically</li>
        <li>Side-by-side major comparison tool</li>
        <li>Sortable data table with pagination</li>
      </ul>
      <h3>Technologies Used</h3>
      <ul>
        <li>Python, HTML5, JavaScript</li>
        <li>Chart.js for interactive data visualizations</li>
        <li>Data sourced from AAUP Ramallah Campus academic records</li>
      </ul>
    </div>
    <div class="modal-footer">
      <button class="btn-save" onclick="closeDesc()">Close</button>
    </div>
  </div>
</div>

<div class="footer-note" id="footer"></div>
      <footer>
  <footer>
  <div class="ft", align ="center">AAUP — Faculty — Reportتقرير التخصصات في الجامعة الأمريكية - رام الله </div>
  <p align ="center">Introduction to coding for journalists AAUP - Student: Razan Idris</p>
  <p style="margin-top:8px;font-size:1rem;opacity:.7", align ="center">AAUP - Instructor: Amjad Khalil · Faculty of Modern Media</p>
  </footer>
<script>
// ============= DATA =============
let DATA = [{"majoes":"Medicine","Faculty":"Medicine","Degree":"Bachelor","Average Age":22,"High School GPA Required":95,"High School Stream":"Scientific","Students Count":159,"Study Years":6,"Credit Hours":252,"Cost Per Credit (NIS)":480,"Male Students":83,"Female Students":76,"Employment Rate %":92,"Graduates Per Year":120,"Total majors Cost (NIS)":120960},{"majoes":"Dentistry","Faculty":"Dentistry","Degree":"Bachelor","Average Age":22,"High School GPA Required":90,"High School Stream":"Scientific","Students Count":119,"Study Years":5,"Credit Hours":200,"Cost Per Credit (NIS)":450,"Male Students":50,"Female Students":69,"Employment Rate %":88,"Graduates Per Year":90,"Total majors Cost (NIS)":90000},{"majoes":"Pharmacy","Faculty":"Pharmacy","Degree":"Bachelor","Average Age":21,"High School GPA Required":85,"High School Stream":"Scientific","Students Count":139,"Study Years":5,"Credit Hours":160,"Cost Per Credit (NIS)":220,"Male Students":44,"Female Students":95,"Employment Rate %":84,"Graduates Per Year":110,"Total majors Cost (NIS)":35200},{"majoes":"Biomedical Sciences","Faculty":"Medicine","Degree":"Bachelor","Average Age":21,"High School GPA Required":80,"High School Stream":"Scientific","Students Count":70,"Study Years":4,"Credit Hours":141,"Cost Per Credit (NIS)":220,"Male Students":24,"Female Students":46,"Employment Rate %":78,"Graduates Per Year":70,"Total majors Cost (NIS)":31020},{"majoes":"Optometry","Faculty":"Allied Health","Degree":"Bachelor","Average Age":21,"High School GPA Required":80,"High School Stream":"Scientific","Students Count":50,"Study Years":4,"Credit Hours":140,"Cost Per Credit (NIS)":220,"Male Students":18,"Female Students":32,"Employment Rate %":82,"Graduates Per Year":50,"Total majors Cost (NIS)":30800},{"majoes":"Nursing","Faculty":"Nursing","Degree":"Bachelor","Average Age":21,"High School GPA Required":75,"High School Stream":"Scientific","Students Count":99,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":200,"Male Students":30,"Female Students":69,"Employment Rate %":85,"Graduates Per Year":100,"Total majors Cost (NIS)":26400},{"majoes":"Physiotherapy","Faculty":"Allied Health","Degree":"Bachelor","Average Age":21,"High School GPA Required":80,"High School Stream":"Scientific","Students Count":60,"Study Years":4,"Credit Hours":140,"Cost Per Credit (NIS)":220,"Male Students":26,"Female Students":34,"Employment Rate %":86,"Graduates Per Year":60,"Total majors Cost (NIS)":30800},{"majoes":"Medical Imaging","Faculty":"Allied Health","Degree":"Bachelor","Average Age":21,"High School GPA Required":78,"High School Stream":"Scientific","Students Count":56,"Study Years":4,"Credit Hours":135,"Cost Per Credit (NIS)":210,"Male Students":24,"Female Students":32,"Employment Rate %":83,"Graduates Per Year":55,"Total majors Cost (NIS)":28350},{"majoes":"Computer Science","Faculty":"Engineering","Degree":"Bachelor","Average Age":20,"High School GPA Required":75,"High School Stream":"Scientific","Students Count":179,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":180,"Male Students":119,"Female Students":60,"Employment Rate %":89,"Graduates Per Year":180,"Total majors Cost (NIS)":23760},{"majoes":"Software Engineering","Faculty":"Engineering","Degree":"Bachelor","Average Age":20,"High School GPA Required":78,"High School Stream":"Scientific","Students Count":169,"Study Years":4,"Credit Hours":140,"Cost Per Credit (NIS)":190,"Male Students":109,"Female Students":60,"Employment Rate %":91,"Graduates Per Year":170,"Total majors Cost (NIS)":26600},{"majoes":"Artificial Intelligence","Faculty":"Engineering","Degree":"Bachelor","Average Age":20,"High School GPA Required":80,"High School Stream":"Scientific","Students Count":99,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":190,"Male Students":63,"Female Students":36,"Employment Rate %":93,"Graduates Per Year":90,"Total majors Cost (NIS)":25080},{"majoes":"Cybersecurity","Faculty":"Engineering","Degree":"Bachelor","Average Age":20,"High School GPA Required":80,"High School Stream":"Scientific","Students Count":90,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":190,"Male Students":60,"Female Students":30,"Employment Rate %":94,"Graduates Per Year":80,"Total majors Cost (NIS)":25080},{"majoes":"Data Science","Faculty":"Engineering","Degree":"Bachelor","Average Age":20,"High School GPA Required":80,"High School Stream":"Scientific","Students Count":64,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":190,"Male Students":36,"Female Students":28,"Employment Rate %":92,"Graduates Per Year":60,"Total majors Cost (NIS)":25080},{"majoes":"Computer Engineering","Faculty":"Engineering","Degree":"Bachelor","Average Age":20,"High School GPA Required":78,"High School Stream":"Scientific","Students Count":80,"Study Years":5,"Credit Hours":160,"Cost Per Credit (NIS)":200,"Male Students":56,"Female Students":24,"Employment Rate %":88,"Graduates Per Year":70,"Total majors Cost (NIS)":32000},{"majoes":"Civil Engineering","Faculty":"Engineering","Degree":"Bachelor","Average Age":21,"High School GPA Required":75,"High School Stream":"Scientific","Students Count":119,"Study Years":5,"Credit Hours":160,"Cost Per Credit (NIS)":190,"Male Students":83,"Female Students":36,"Employment Rate %":82,"Graduates Per Year":120,"Total majors Cost (NIS)":30400},{"majoes":"Architectural Engineering","Faculty":"Engineering","Degree":"Bachelor","Average Age":21,"High School GPA Required":78,"High School Stream":"Scientific","Students Count":70,"Study Years":5,"Credit Hours":160,"Cost Per Credit (NIS)":200,"Male Students":34,"Female Students":36,"Employment Rate %":80,"Graduates Per Year":65,"Total majors Cost (NIS)":32000},{"majoes":"Electrical Engineering","Faculty":"Engineering","Degree":"Bachelor","Average Age":21,"High School GPA Required":75,"High School Stream":"Scientific","Students Count":84,"Study Years":5,"Credit Hours":160,"Cost Per Credit (NIS)":190,"Male Students":64,"Female Students":20,"Employment Rate %":84,"Graduates Per Year":75,"Total majors Cost (NIS)":30400},{"majoes":"Mechanical Engineering","Faculty":"Engineering","Degree":"Bachelor","Average Age":21,"High School GPA Required":75,"High School Stream":"Scientific","Students Count":76,"Study Years":5,"Credit Hours":160,"Cost Per Credit (NIS)":190,"Male Students":60,"Female Students":16,"Employment Rate %":81,"Graduates Per Year":70,"Total majors Cost (NIS)":30400},{"majoes":"Business Administration","Faculty":"Business","Degree":"Bachelor","Average Age":20,"High School GPA Required":70,"High School Stream":"All Streams","Students Count":199,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":160,"Male Students":103,"Female Students":96,"Employment Rate %":78,"Graduates Per Year":220,"Total majors Cost (NIS)":21120},{"majoes":"Accounting","Faculty":"Business","Degree":"Bachelor","Average Age":20,"High School GPA Required":70,"High School Stream":"All Streams","Students Count":139,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":160,"Male Students":64,"Female Students":75,"Employment Rate %":76,"Graduates Per Year":140,"Total majors Cost (NIS)":21120},{"majoes":"Finance and Banking","Faculty":"Business","Degree":"Bachelor","Average Age":20,"High School GPA Required":72,"High School Stream":"All Streams","Students Count":99,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":160,"Male Students":48,"Female Students":51,"Employment Rate %":79,"Graduates Per Year":90,"Total majors Cost (NIS)":21120},{"majoes":"Marketing","Faculty":"Business","Degree":"Bachelor","Average Age":20,"High School GPA Required":70,"High School Stream":"All Streams","Students Count":90,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":160,"Male Students":38,"Female Students":52,"Employment Rate %":77,"Graduates Per Year":80,"Total majors Cost (NIS)":21120},{"majoes":"Digital Marketing","Faculty":"Business","Degree":"Bachelor","Average Age":20,"High School GPA Required":70,"High School Stream":"All Streams","Students Count":60,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":160,"Male Students":24,"Female Students":36,"Employment Rate %":85,"Graduates Per Year":55,"Total majors Cost (NIS)":21120},{"majoes":"Economics","Faculty":"Business","Degree":"Bachelor","Average Age":20,"High School GPA Required":72,"High School Stream":"All Streams","Students Count":50,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":160,"Male Students":28,"Female Students":22,"Employment Rate %":75,"Graduates Per Year":45,"Total majors Cost (NIS)":21120},{"majoes":"Law","Faculty":"Law","Degree":"Bachelor","Average Age":21,"High School GPA Required":70,"High School Stream":"All Streams","Students Count":129,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":170,"Male Students":71,"Female Students":58,"Employment Rate %":74,"Graduates Per Year":130,"Total majors Cost (NIS)":22440},{"majoes":"Public Relations","Faculty":"Media","Degree":"Bachelor","Average Age":20,"High School GPA Required":70,"High School Stream":"All Streams","Students Count":56,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":150,"Male Students":18,"Female Students":38,"Employment Rate %":82,"Graduates Per Year":50,"Total majors Cost (NIS)":19800},{"majoes":"Journalism","Faculty":"Media","Degree":"Bachelor","Average Age":20,"High School GPA Required":70,"High School Stream":"All Streams","Students Count":52,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":150,"Male Students":22,"Female Students":30,"Employment Rate %":80,"Graduates Per Year":45,"Total majors Cost (NIS)":19800},{"majoes":"Digital Media","Faculty":"Media","Degree":"Bachelor","Average Age":20,"High School GPA Required":70,"High School Stream":"All Streams","Students Count":48,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":150,"Male Students":20,"Female Students":28,"Employment Rate %":84,"Graduates Per Year":40,"Total majors Cost (NIS)":19800},{"majoes":"English Language","Faculty":"Arts","Degree":"Bachelor","Average Age":20,"High School GPA Required":65,"High School Stream":"All Streams","Students Count":80,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":140,"Male Students":24,"Female Students":56,"Employment Rate %":72,"Graduates Per Year":80,"Total majors Cost (NIS)":18480},{"majoes":"Arabic Language","Faculty":"Arts","Degree":"Bachelor","Average Age":20,"High School GPA Required":65,"High School Stream":"All Streams","Students Count":70,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":140,"Male Students":26,"Female Students":44,"Employment Rate %":70,"Graduates Per Year":70,"Total majors Cost (NIS)":18480},{"majoes":"Translation","Faculty":"Arts","Degree":"Bachelor","Average Age":20,"High School GPA Required":68,"High School Stream":"All Streams","Students Count":44,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":140,"Male Students":14,"Female Students":30,"Employment Rate %":78,"Graduates Per Year":35,"Total majors Cost (NIS)":18480},{"majoes":"Graphic Design","Faculty":"Arts","Degree":"Bachelor","Average Age":20,"High School GPA Required":68,"High School Stream":"All Streams","Students Count":60,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":150,"Male Students":24,"Female Students":36,"Employment Rate %":81,"Graduates Per Year":50,"Total majors Cost (NIS)":19800},{"majoes":"Interior Design","Faculty":"Arts","Degree":"Bachelor","Average Age":20,"High School GPA Required":68,"High School Stream":"All Streams","Students Count":44,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":150,"Male Students":14,"Female Students":30,"Employment Rate %":76,"Graduates Per Year":35,"Total majors Cost (NIS)":19800},{"majoes":"Mathematics","Faculty":"Science","Degree":"Bachelor","Average Age":20,"High School GPA Required":70,"High School Stream":"Scientific","Students Count":36,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":145,"Male Students":18,"Female Students":18,"Employment Rate %":73,"Graduates Per Year":30,"Total majors Cost (NIS)":19140},{"majoes":"Physics","Faculty":"Science","Degree":"Bachelor","Average Age":20,"High School GPA Required":70,"High School Stream":"Scientific","Students Count":30,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":145,"Male Students":20,"Female Students":10,"Employment Rate %":71,"Graduates Per Year":25,"Total majors Cost (NIS)":19140},{"majoes":"Chemistry","Faculty":"Science","Degree":"Bachelor","Average Age":20,"High School GPA Required":70,"High School Stream":"Scientific","Students Count":34,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":145,"Male Students":16,"Female Students":18,"Employment Rate %":74,"Graduates Per Year":30,"Total majors Cost (NIS)":19140},{"majoes":"Biotechnology","Faculty":"Science","Degree":"Bachelor","Average Age":20,"High School GPA Required":78,"High School Stream":"Scientific","Students Count":42,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":180,"Male Students":16,"Female Students":26,"Employment Rate %":83,"Graduates Per Year":40,"Total majors Cost (NIS)":23760},{"majoes":"Nutrition","Faculty":"Health Sciences","Degree":"Bachelor","Average Age":20,"High School GPA Required":75,"High School Stream":"Scientific","Students Count":52,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":180,"Male Students":12,"Female Students":40,"Employment Rate %":82,"Graduates Per Year":50,"Total majors Cost (NIS)":23760},{"majoes":"Occupational Therapy","Faculty":"Health Sciences","Degree":"Bachelor","Average Age":21,"High School GPA Required":75,"High School Stream":"Scientific","Students Count":36,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":180,"Male Students":10,"Female Students":26,"Employment Rate %":84,"Graduates Per Year":30,"Total majors Cost (NIS)":23760},{"majoes":"Environmental Sciences","Faculty":"Science","Degree":"Bachelor","Average Age":20,"High School GPA Required":70,"High School Stream":"Scientific","Students Count":32,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":145,"Male Students":18,"Female Students":14,"Employment Rate %":75,"Graduates Per Year":25,"Total majors Cost (NIS)":19140},{"majoes":"Human Resource Management","Faculty":"Business","Degree":"Bachelor","Average Age":20,"High School GPA Required":70,"High School Stream":"All Streams","Students Count":52,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":160,"Male Students":20,"Female Students":32,"Employment Rate %":78,"Graduates Per Year":45,"Total majors Cost (NIS)":21120},{"majoes":"Supply Chain Management","Faculty":"Business","Degree":"Bachelor","Average Age":20,"High School GPA Required":70,"High School Stream":"All Streams","Students Count":36,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":160,"Male Students":18,"Female Students":18,"Employment Rate %":81,"Graduates Per Year":30,"Total majors Cost (NIS)":21120},{"majoes":"E-Commerce","Faculty":"Business","Degree":"Bachelor","Average Age":20,"High School GPA Required":70,"High School Stream":"All Streams","Students Count":40,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":160,"Male Students":18,"Female Students":22,"Employment Rate %":86,"Graduates Per Year":35,"Total majors Cost (NIS)":21120},{"majoes":"Information Systems","Faculty":"Engineering","Degree":"Bachelor","Average Age":20,"High School GPA Required":75,"High School Stream":"Scientific","Students Count":84,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":180,"Male Students":48,"Female Students":36,"Employment Rate %":88,"Graduates Per Year":75,"Total majors Cost (NIS)":23760},{"majoes":"Educational Technology","Faculty":"Education","Degree":"Bachelor","Average Age":20,"High School GPA Required":65,"High School Stream":"All Streams","Students Count":24,"Study Years":4,"Credit Hours":132,"Cost Per Credit (NIS)":140,"Male Students":8,"Female Students":16,"Employment Rate %":76,"Graduates Per Year":25,"Total majors Cost (NIS)":18480}];

// ============= STATE =============
const COLORS = ['#7EF1FC','#FC7EC6','#FCEC7E','#A78C9B','#647B7D','#7D7A64','#5EC8D4','#F06AB0','#E8D86A','#8A7080','#4F6668','#6A6852','#9FD8DE'];
let editIdx = null, currentPage = 1, pageSize = 15, filteredData = [], sortKey = '', sortAsc = true;
let chartInstances = {};

// ============= NAV =============
function openReport() {
  document.getElementById('landing').style.display = 'none';
  document.getElementById('report').style.display = 'block';
  initReport();
}
function backToLanding() {
  document.getElementById('report').style.display = 'none';
  document.getElementById('landing').style.display = 'flex';
}
function showSection(name, el) {
  document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
  document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
  document.getElementById('sec-' + name).classList.add('active');
  el.classList.add('active');
  if (name === 'charts') setTimeout(initDetailCharts, 100);
  if (name === 'comparison') setTimeout(initComparison, 100);
}
function openDesc() { document.getElementById('descOverlay').classList.add('open'); }
function closeDesc() { document.getElementById('descOverlay').classList.remove('open'); }

// ============= INIT =============
let initialized = false;
function initReport() {
  if (initialized) return;
  initialized = true;
  renderStats();
  initOverviewCharts();
  populateFacultyFilter();
  filterTable();
}

// ============= STATS =============
function renderStats() {
  const total = DATA.reduce((s,d) => s + d['Students Count'], 0);
  const avgAge = (DATA.reduce((s,d) => s + d['Average Age'], 0) / DATA.length).toFixed(1);
  const avgGPA = (DATA.reduce((s,d) => s + d['High School GPA Required'], 0) / DATA.length).toFixed(1);
  const avgEmploy = (DATA.reduce((s,d) => s + d['Employment Rate %'], 0) / DATA.length).toFixed(1);
  const totalGrads = DATA.reduce((s,d) => s + d['Graduates Per Year'], 0);
  const faculties = [...new Set(DATA.map(d => d.Faculty))].length;

  const stats = [
    { icon: '🎓', val: DATA.length, label: 'Total Majors' },
    { icon: '👥', val: total.toLocaleString(), label: 'Total Students' },
    { icon: '🏛️', val: faculties, label: 'Faculties' },
    { icon: '📅', val: avgAge, label: 'Avg Student Age' },
    { icon: '📊', val: avgGPA + '%', label: 'Avg GPA Required' },
    { icon: '💼', val: avgEmploy + '%', label: 'Avg Employment' },
    { icon: '🎉', val: totalGrads.toLocaleString(), label: 'Graduates/Year' },
  ];
  document.getElementById('statsGrid').innerHTML = stats.map(s =>
    `<div class="stat-card"><div class="stat-icon">${s.icon}</div><div class="stat-val">${s.val}</div><div class="stat-label">${s.label}</div></div>`
  ).join('');
}

// ============= OVERVIEW CHARTS =============
function destroyChart(id) { if (chartInstances[id]) { chartInstances[id].destroy(); delete chartInstances[id]; } }

function initOverviewCharts() {
  // Faculty students
  const faculties = [...new Set(DATA.map(d => d.Faculty))];
  const facStudents = faculties.map(f => DATA.filter(d => d.Faculty === f).reduce((s,d) => s + d['Students Count'], 0));
  destroyChart('chartFacultyStudents');
  chartInstances['chartFacultyStudents'] = new Chart(document.getElementById('chartFacultyStudents'), {
    type: 'doughnut',
    data: { labels: faculties, datasets: [{ data: facStudents, backgroundColor: COLORS, borderWidth: 2, borderColor: '#fff' }] },
    options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { position: 'right', labels: { font: { size: 11 }, boxWidth: 14 } } } }
  });

  // Stream pie
  const sci = DATA.filter(d => d['High School Stream'] === 'Scientific').length;
  const all = DATA.filter(d => d['High School Stream'] === 'All Streams').length;
  destroyChart('chartStream');
  chartInstances['chartStream'] = new Chart(document.getElementById('chartStream'), {
    type: 'pie',
    data: { labels: ['Scientific Stream', 'All Streams'], datasets: [{ data: [sci, all], backgroundColor: ['#FC7EC6','#7EF1FC'], borderWidth: 2, borderColor: '#fff' }] },
    options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { position: 'bottom' } } }
  });

  // Avg age by faculty
  const avgAges = faculties.map(f => {
    const rows = DATA.filter(d => d.Faculty === f);
    return +(rows.reduce((s,d) => s + d['Average Age'], 0) / rows.length).toFixed(1);
  });
  destroyChart('chartAge');
  chartInstances['chartAge'] = new Chart(document.getElementById('chartAge'), {
    type: 'bar',
    data: { labels: faculties, datasets: [{ label: 'Avg Age', data: avgAges, backgroundColor: '#FC7EC6', borderRadius: 6 }] },
    options: { responsive: true, maintainAspectRatio: false, scales: { y: { min: 18, max: 24 } }, plugins: { legend: { display: false } } }
  });

  // Employment by faculty
  const avgEmploy = faculties.map(f => {
    const rows = DATA.filter(d => d.Faculty === f);
    return +(rows.reduce((s,d) => s + d['Employment Rate %'], 0) / rows.length).toFixed(1);
  });
  destroyChart('chartEmploy');
  chartInstances['chartEmploy'] = new Chart(document.getElementById('chartEmploy'), {
    type: 'bar',
    data: { labels: faculties, datasets: [{ label: 'Employment %', data: avgEmploy, backgroundColor: '#7EF1FC', borderRadius: 6 }] },
    options: { responsive: true, maintainAspectRatio: false, scales: { y: { min: 60, max: 100 } }, plugins: { legend: { display: false } } }
  });
}

// ============= DETAIL CHARTS =============
let detailInited = false;
function initDetailCharts() {
  if (detailInited) return;
  detailInited = true;
  const labels = DATA.map(d => d.majoes);
  const students = DATA.map(d => d['Students Count']);
  const grads = DATA.map(d => d['Graduates Per Year']);

  destroyChart('chartAllStudents');
  chartInstances['chartAllStudents'] = new Chart(document.getElementById('chartAllStudents'), {
    type: 'bar',
    data: { labels, datasets: [{ label: 'Students', data: students, backgroundColor: DATA.map((_,i) => COLORS[i % COLORS.length]), borderRadius: 4 }] },
    options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false } }, scales: { x: { ticks: { maxRotation: 90, font: { size: 10 } } } } }
  });

  destroyChart('chartGrads');
  chartInstances['chartGrads'] = new Chart(document.getElementById('chartGrads'), {
    type: 'bar',
    data: { labels, datasets: [{ label: 'Graduates/Year', data: grads, backgroundColor: '#FC7EC6', borderRadius: 4 }] },
    options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false } }, scales: { x: { ticks: { maxRotation: 90, font: { size: 10 } } } } }
  });

  // Scatter GPA vs Employment
  const scatter = DATA.map(d => ({ x: d['High School GPA Required'], y: d['Employment Rate %'], label: d.majoes }));
  destroyChart('chartGpaEmploy');
  chartInstances['chartGpaEmploy'] = new Chart(document.getElementById('chartGpaEmploy'), {
    type: 'scatter',
    data: { datasets: [{ label: 'Majors', data: scatter, backgroundColor: '#FC7EC6', pointRadius: 7, pointHoverRadius: 9 }] },
    options: { responsive: true, maintainAspectRatio: false, scales: { x: { title: { display: true, text: 'GPA Required' } }, y: { title: { display: true, text: 'Employment %' } } } }
  });

  // Gender by faculty
  const facs = [...new Set(DATA.map(d => d.Faculty))];
  const maleData = facs.map(f => DATA.filter(d => d.Faculty === f).reduce((s,d) => s + d['Male Students'], 0));
  const femaleData = facs.map(f => DATA.filter(d => d.Faculty === f).reduce((s,d) => s + d['Female Students'], 0));
  destroyChart('chartGender');
  chartInstances['chartGender'] = new Chart(document.getElementById('chartGender'), {
    type: 'bar',
    data: { labels: facs, datasets: [
      { label: 'Male', data: maleData, backgroundColor: '#647B7D', borderRadius: 4 },
      { label: 'Female', data: femaleData, backgroundColor: '#7EF1FC', borderRadius: 4 }
    ]},
    options: { responsive: true, maintainAspectRatio: false, scales: { x: { stacked: false } }, plugins: { legend: { position: 'top' } } }
  });
}

// ============= COMPARISON =============
let cmpChart = null;
function initComparison() {
  const selA = document.getElementById('cmpA');
  const selB = document.getElementById('cmpB');
  if (selA.options.length > 0) return;
  DATA.forEach((d, i) => {
    selA.add(new Option(d.majoes, i));
    selB.add(new Option(d.majoes, i));
  });
  selB.selectedIndex = 1;
  renderComparison();
}

function renderComparison() {
  const a = DATA[document.getElementById('cmpA').value];
  const b = DATA[document.getElementById('cmpB').value];
  if (!a || !b) return;
  const metrics = [
    { key: 'Students Count', label: 'Students' },
    { key: 'High School GPA Required', label: 'GPA Required' },
    { key: 'Average Age', label: 'Avg Age' },
    { key: 'Employment Rate %', label: 'Employment %' },
    { key: 'Graduates Per Year', label: 'Graduates/Yr' },
    { key: 'Credit Hours', label: 'Credit Hours' },
    { key: 'Study Years', label: 'Study Years' },
  ];
  const maxVals = { 'Students Count': 250, 'High School GPA Required': 100, 'Average Age': 25, 'Employment Rate %': 100, 'Graduates Per Year': 250, 'Credit Hours': 280, 'Study Years': 7 };
  
  document.getElementById('cmpResult').innerHTML = `
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:20px;margin-bottom:20px;">
      <div class="chart-card" style="padding:20px;">
        <div style="font-size:1.1rem;font-weight:800;color:var(--c5);margin-bottom:12px;">${a.majoes}</div>
        <div style="color:var(--c3);font-size:0.85rem;margin-bottom:4px;">Faculty: <strong>${a.Faculty}</strong></div>
        <div style="color:var(--c3);font-size:0.85rem;margin-bottom:4px;">Stream: <span class="badge ${a['High School Stream']==='Scientific'?'badge-sci':'badge-all'}">${a['High School Stream']}</span></div>
        <div style="color:var(--c3);font-size:0.85rem;">Degree: <span class="badge badge-bach">${a.Degree}</span></div>
      </div>
      <div class="chart-card" style="padding:20px;">
        <div style="font-size:1.1rem;font-weight:800;color:var(--c2);margin-bottom:12px;">${b.majoes}</div>
        <div style="color:var(--c3);font-size:0.85rem;margin-bottom:4px;">Faculty: <strong>${b.Faculty}</strong></div>
        <div style="color:var(--c3);font-size:0.85rem;margin-bottom:4px;">Stream: <span class="badge ${b['High School Stream']==='Scientific'?'badge-sci':'badge-all'}">${b['High School Stream']}</span></div>
        <div style="color:var(--c3);font-size:0.85rem;">Degree: <span class="badge badge-bach">${b.Degree}</span></div>
      </div>
    </div>
    <div class="chart-card" style="padding:20px;margin-bottom:20px;">
      ${metrics.map(m => {
        const av = a[m.key], bv = b[m.key], mx = maxVals[m.key];
        const aw = Math.min(100, (av/mx)*100), bw = Math.min(100, (bv/mx)*100);
        return `<div class="comp-bar-wrap">
          <div class="comp-bar-label"><span style="color:var(--c5);">${a.majoes}: ${av}</span><span style="font-weight:700;">${m.label}</span><span style="color:var(--c2);">${b.majoes}: ${bv}</span></div>
          <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;">
            <div class="comp-bar-outer"><div class="comp-bar-inner" style="width:${aw}%;background:linear-gradient(90deg,#FC7EC6,#7EF1FC);"></div></div>
            <div class="comp-bar-outer"><div class="comp-bar-inner" style="width:${bw}%;background:linear-gradient(90deg,#647B7D,#7D7A64);"></div></div>
          </div>
        </div>`;
      }).join('')}
    </div>`;

  destroyChart('chartCmp');
  const metricLabels = metrics.map(m => m.label);
  const normalize = (d) => metrics.map(m => {
    const max = maxVals[m.key];
    return +((d[m.key]/max)*100).toFixed(1);
  });
  chartInstances['chartCmp'] = new Chart(document.getElementById('chartCmp'), {
    type: 'radar',
    data: {
      labels: metricLabels,
      datasets: [
        { label: a.majoes, data: normalize(a), backgroundColor: 'rgba(252,126,198,0.2)', borderColor: '#FC7EC6', borderWidth: 2, pointBackgroundColor: '#FC7EC6' },
        { label: b.majoes, data: normalize(b), backgroundColor: 'rgba(100,123,125,0.2)', borderColor: '#647B7D', borderWidth: 2, pointBackgroundColor: '#647B7D' }
      ]
    },
    options: { responsive: true, maintainAspectRatio: false, scales: { r: { min: 0, max: 100, ticks: { font: { size: 10 } } } } }
  });
}

// ============= TABLE =============
function populateFacultyFilter() {
  const sel = document.getElementById('filterFaculty');
  [...new Set(DATA.map(d => d.Faculty))].forEach(f => {
    const opt = document.createElement('option'); opt.value = f; opt.textContent = f; sel.appendChild(opt);
  });
}

function filterTable() {
  const q = document.getElementById('searchInput').value.toLowerCase();
  const fac = document.getElementById('filterFaculty').value;
  const str = document.getElementById('filterStream').value;
  filteredData = DATA.filter(d =>
    (!q || d.majoes.toLowerCase().includes(q) || d.Faculty.toLowerCase().includes(q)) &&
    (!fac || d.Faculty === fac) &&
    (!str || d['High School Stream'] === str)
  );
  if (sortKey) {
    filteredData.sort((a,b) => {
      const av = a[sortKey], bv = b[sortKey];
      return (typeof av === 'number' ? av - bv : String(av).localeCompare(String(bv))) * (sortAsc ? 1 : -1);
    });
  }
  currentPage = 1;
  renderTable();
}

function sortTable(key) {
  if (sortKey === key) sortAsc = !sortAsc; else { sortKey = key; sortAsc = true; }
  filterTable();
}

function renderTable() {
  const start = (currentPage - 1) * pageSize;
  const page = filteredData.slice(start, start + pageSize);
  document.getElementById('tableBody').innerHTML = page.map((d, i) => {
    const realIdx = DATA.indexOf(d);
    return `<tr>
      <td><strong>${start+i+1}. ${d.majoes}</strong></td>
      <td>${d.Faculty}</td>
      <td><span class="badge badge-bach">${d.Degree}</span></td>
      <td>${d['Average Age']}</td>
      <td>${d['High School GPA Required']}%</td>
      <td><span class="badge ${d['High School Stream']==='Scientific'?'badge-sci':'badge-all'}">${d['High School Stream']}</span></td>
      <td><strong>${d['Students Count']}</strong></td>
      <td>${d['Male Students']}</td>
      <td>${d['Female Students']}</td>
      <td>${d['Employment Rate %']}%</td>
      <td>${d['Graduates Per Year']}</td>
      <td><div class="action-btns">
        <button class="btn-edit" onclick="openModal(${realIdx})">Edit</button>
        <button class="btn-del" onclick="deleteMajor(${realIdx})">Del</button>
      </div></td>
    </tr>`;
  }).join('');
  renderPagination();
}

function renderPagination() {
  const total = Math.ceil(filteredData.length / pageSize);
  let html = '';
  for (let i = 1; i <= total; i++) {
    html += `<button class="pg-btn ${i===currentPage?'active':''}" onclick="goPage(${i})">${i}</button>`;
  }
  document.getElementById('pagination').innerHTML = html;
}

function goPage(p) { currentPage = p; renderTable(); }

// ============= MODAL =============
function openModal(idx) {
  editIdx = idx;
  document.getElementById('modalTitle').textContent = idx === null ? 'Add New Major' : 'Edit Major';
  const d = idx !== null ? DATA[idx] : {};
  document.getElementById('f_major').value = d.majoes || '';
  document.getElementById('f_faculty').value = d.Faculty || '';
  document.getElementById('f_degree').value = d.Degree || 'Bachelor';
  document.getElementById('f_age').value = d['Average Age'] || '';
  document.getElementById('f_gpa').value = d['High School GPA Required'] || '';
  document.getElementById('f_stream').value = d['High School Stream'] || 'Scientific';
  document.getElementById('f_students').value = d['Students Count'] || '';
  document.getElementById('f_years').value = d['Study Years'] || '';
  document.getElementById('f_male').value = d['Male Students'] || '';
  document.getElementById('f_female').value = d['Female Students'] || '';
  document.getElementById('f_employ').value = d['Employment Rate %'] || '';
  document.getElementById('f_grads').value = d['Graduates Per Year'] || '';
  document.getElementById('f_credits').value = d['Credit Hours'] || '';
  document.getElementById('f_cost').value = d['Cost Per Credit (NIS)'] || '';
  document.getElementById('modalOverlay').classList.add('open');
}
function closeModal() { document.getElementById('modalOverlay').classList.remove('open'); }

function saveMajor() {
  const rec = {
    majoes: document.getElementById('f_major').value.trim(),
    Faculty: document.getElementById('f_faculty').value.trim(),
    Degree: document.getElementById('f_degree').value,
    'Average Age': +document.getElementById('f_age').value,
    'High School GPA Required': +document.getElementById('f_gpa').value,
    'High School Stream': document.getElementById('f_stream').value,
    'Students Count': +document.getElementById('f_students').value,
    'Study Years': +document.getElementById('f_years').value,
    'Male Students': +document.getElementById('f_male').value,
    'Female Students': +document.getElementById('f_female').value,
    'Employment Rate %': +document.getElementById('f_employ').value,
    'Graduates Per Year': +document.getElementById('f_grads').value,
    'Credit Hours': +document.getElementById('f_credits').value,
    'Cost Per Credit (NIS)': +document.getElementById('f_cost').value,
    'Total majors Cost (NIS)': +(document.getElementById('f_credits').value) * +(document.getElementById('f_cost').value)
  };
  if (!rec.majoes) { alert('Major name is required.'); return; }
  if (editIdx !== null) DATA[editIdx] = rec; else DATA.push(rec);
  closeModal();
  filterTable();
  renderStats();
  detailInited = false;
}

function deleteMajor(idx) {
  if (!confirm(`Delete "${DATA[idx].majoes}"?`)) return;
  DATA.splice(idx, 1);
  filterTable();
  renderStats();
  detailInited = false;
}
</script>
</body>
</html>
