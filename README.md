# afyabakena
based on health
<!doctype html>
<html lang="en" class="h-full">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>eHMS - Hospital Management System</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <script src="/_sdk/data_sdk.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700&amp;display=swap" rel="stylesheet">
  <style>
    body {
      box-sizing: border-box;
      font-family: 'Plus Jakarta Sans', sans-serif;
    }
    
    .gradient-bg {
      background: linear-gradient(135deg, #1e3a5f 0%, #0d1b2a 100%);
    }
    
    .card-gradient {
      background: linear-gradient(145deg, #ffffff 0%, #f8fafc 100%);
    }
    
    .dept-card {
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    }
    
    .dept-card:hover {
      transform: translateY(-4px);
      box-shadow: 0 20px 40px rgba(0,0,0,0.15);
    }
    
    .table-row {
      transition: background-color 0.2s ease;
    }
    
    .table-row:hover {
      background-color: #f1f5f9;
    }
    
    .status-pending { background: #fef3c7; color: #92400e; }
    .status-inprogress { background: #dbeafe; color: #1e40af; }
    .status-completed { background: #d1fae5; color: #065f46; }
    .status-urgent { background: #fee2e2; color: #991b1b; }
    
    .priority-high { border-left: 4px solid #ef4444; }
    .priority-medium { border-left: 4px solid #f59e0b; }
    .priority-low { border-left: 4px solid #10b981; }
    
    .modal-overlay {
      background: rgba(0, 0, 0, 0.6);
      backdrop-filter: blur(4px);
    }
    
    .pulse-dot {
      animation: pulse 2s infinite;
    }
    
    @keyframes pulse {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.5; }
    }
    
    .sidebar-item {
      transition: all 0.2s ease;
    }
    
    .sidebar-item:hover {
      background: rgba(255,255,255,0.1);
      padding-left: 1.5rem;
    }
    
    .sidebar-item.active {
      background: rgba(59, 130, 246, 0.3);
      border-right: 3px solid #3b82f6;
    }
    
    ::-webkit-scrollbar {
      width: 8px;
      height: 8px;
    }
    
    ::-webkit-scrollbar-track {
      background: #f1f5f9;
    }
    
    ::-webkit-scrollbar-thumb {
      background: #94a3b8;
      border-radius: 4px;
    }
    
    ::-webkit-scrollbar-thumb:hover {
      background: #64748b;
    }
  </style>
  <style>@view-transition { navigation: auto; }</style>
 </head>
 <body class="h-full bg-slate-100">
  <div id="app" class="h-full flex overflow-hidden"><!-- Sidebar -->
   <aside id="sidebar" class="gradient-bg w-64 flex-shrink-0 flex flex-col text-white">
    <div class="p-6 border-b border-white/10">
     <div class="flex items-center gap-3">
      <div class="w-10 h-10 bg-blue-500 rounded-lg flex items-center justify-center">
       <svg class="w-6 h-6" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4" />
       </svg>
      </div>
      <div>
       <h1 id="hospital-name" class="font-bold text-lg">City Hospital</h1>
       <p id="system-title" class="text-xs text-blue-300">eHMS System v2.0</p>
      </div>
     </div>
    </div><!-- Network Status -->
    <div class="px-6 py-3 border-b border-white/10">
     <div class="flex items-center gap-2 text-xs"><span class="pulse-dot w-2 h-2 bg-green-400 rounded-full"></span> <span class="text-slate-300">Network: 122.333.44.5</span>
     </div>
    </div><!-- Navigation -->
    <nav class="flex-1 py-4 overflow-y-auto">
     <div class="px-4 mb-2 text-xs font-semibold text-slate-400 uppercase tracking-wider">
      Main Menu
     </div><button onclick="switchView('dashboard')" class="sidebar-item active w-full flex items-center gap-3 px-4 py-3 text-left" data-view="dashboard">
      <svg class="w-5 h-5" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2V6zM14 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2v-2zM14 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z" />
      </svg><span>Dashboard</span> </button> <button onclick="switchView('reception')" class="sidebar-item w-full flex items-center gap-3 px-4 py-3 text-left" data-view="reception">
      <svg class="w-5 h-5" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M18 9v3m0 0v3m0-3h3m-3 0h-3m-2-5a4 4 0 11-8 0 4 4 0 018 0zM3 20a6 6 0 0112 0v1H3v-1z" />
      </svg><span>Reception</span> </button>
     <div class="px-4 mt-4 mb-2 text-xs font-semibold text-slate-400 uppercase tracking-wider">
      Departments
     </div><button onclick="switchView('laboratory')" class="sidebar-item w-full flex items-center gap-3 px-4 py-3 text-left" data-view="laboratory">
      <svg class="w-5 h-5" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z" />
      </svg><span>Laboratory</span> </button> <button onclick="switchView('radiology')" class="sidebar-item w-full flex items-center gap-3 px-4 py-3 text-left" data-view="radiology">
      <svg class="w-5 h-5" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 3v2m6-2v2M9 19v2m6-2v2M5 9H3m2 6H3m18-6h-2m2 6h-2M7 19h10a2 2 0 002-2V7a2 2 0 00-2-2H7a2 2 0 00-2 2v10a2 2 0 002 2zM9 9h6v6H9V9z" />
      </svg><span>Radiology</span> </button> <button onclick="switchView('pharmacy')" class="sidebar-item w-full flex items-center gap-3 px-4 py-3 text-left" data-view="pharmacy">
      <svg class="w-5 h-5" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z" />
      </svg><span>Pharmacy</span> </button> <button onclick="switchView('medical')" class="sidebar-item w-full flex items-center gap-3 px-4 py-3 text-left" data-view="medical">
      <svg class="w-5 h-5" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" />
      </svg><span>Medical Doctors</span> </button> <button onclick="switchView('dental')" class="sidebar-item w-full flex items-center gap-3 px-4 py-3 text-left" data-view="dental">
      <svg class="w-5 h-5" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14.828 14.828a4 4 0 01-5.656 0M9 10h.01M15 10h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
      </svg><span>Dental</span> </button> <button onclick="switchView('nursing')" class="sidebar-item w-full flex items-center gap-3 px-4 py-3 text-left" data-view="nursing">
      <svg class="w-5 h-5" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z" />
      </svg><span>Nursing</span> </button>
    </nav><!-- User Info -->
    <div class="p-4 border-t border-white/10">
     <div class="flex items-center gap-3">
      <div class="w-10 h-10 bg-blue-600 rounded-full flex items-center justify-center font-semibold">
       AD
      </div>
      <div class="flex-1">
       <p class="text-sm font-medium">Admin User</p>
       <p class="text-xs text-slate-400">System Administrator</p>
      </div>
     </div>
    </div>
   </aside><!-- Main Content -->
   <main class="flex-1 flex flex-col overflow-hidden"><!-- Top Bar -->
    <header class="bg-white shadow-sm px-6 py-4 flex items-center justify-between">
     <div>
      <h2 id="current-view-title" class="text-xl font-bold text-slate-800">Dashboard</h2>
      <p id="current-date" class="text-sm text-slate-500"></p>
     </div>
     <div class="flex items-center gap-4"><!-- Search -->
      <div class="relative"><input type="text" id="global-search" placeholder="Search patients..." class="pl-10 pr-4 py-2 w-64 border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent" oninput="handleGlobalSearch(this.value)">
       <svg class="absolute left-3 top-1/2 -translate-y-1/2 w-5 h-5 text-slate-400" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
       </svg>
      </div><!-- Notifications --> <button class="relative p-2 text-slate-600 hover:bg-slate-100 rounded-lg">
       <svg class="w-6 h-6" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
       </svg><span id="notification-badge" class="hidden absolute -top-1 -right-1 w-5 h-5 bg-red-500 text-white text-xs rounded-full flex items-center justify-center">0</span> </button>
     </div>
    </header><!-- Content Area -->
    <div id="content-area" class="flex-1 overflow-y-auto p-6"><!-- Dashboard View -->
     <div id="view-dashboard" class="view-content"><!-- Stats Cards -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
       <div class="card-gradient rounded-xl p-6 shadow-lg border border-slate-100">
        <div class="flex items-center justify-between">
         <div>
          <p class="text-slate-500 text-sm">Total Patients</p>
          <p id="stat-total" class="text-3xl font-bold text-slate-800 mt-1">0</p>
         </div>
         <div class="w-12 h-12 bg-blue-100 rounded-xl flex items-center justify-center">
          <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z" />
          </svg>
         </div>
        </div>
       </div>
       <div class="card-gradient rounded-xl p-6 shadow-lg border border-slate-100">
        <div class="flex items-center justify-between">
         <div>
          <p class="text-slate-500 text-sm">Pending</p>
          <p id="stat-pending" class="text-3xl font-bold text-amber-600 mt-1">0</p>
         </div>
         <div class="w-12 h-12 bg-amber-100 rounded-xl flex items-center justify-center">
          <svg class="w-6 h-6 text-amber-600" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
         </div>
        </div>
       </div>
       <div class="card-gradient rounded-xl p-6 shadow-lg border border-slate-100">
        <div class="flex items-center justify-between">
         <div>
          <p class="text-slate-500 text-sm">In Progress</p>
          <p id="stat-inprogress" class="text-3xl font-bold text-blue-600 mt-1">0</p>
         </div>
         <div class="w-12 h-12 bg-blue-100 rounded-xl flex items-center justify-center">
          <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
          </svg>
         </div>
        </div>
       </div>
       <div class="card-gradient rounded-xl p-6 shadow-lg border border-slate-100">
        <div class="flex items-center justify-between">
         <div>
          <p class="text-slate-500 text-sm">Completed</p>
          <p id="stat-completed" class="text-3xl font-bold text-emerald-600 mt-1">0</p>
         </div>
         <div class="w-12 h-12 bg-emerald-100 rounded-xl flex items-center justify-center">
          <svg class="w-6 h-6 text-emerald-600" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
         </div>
        </div>
       </div>
      </div><!-- Department Overview -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-6 mb-8">
       <div class="bg-white rounded-xl p-6 shadow-lg">
        <h3 class="text-lg font-semibold text-slate-800 mb-4">Department Activity</h3>
        <div id="dept-activity" class="space-y-3"><!-- Department bars will be inserted here -->
        </div>
       </div>
       <div class="bg-white rounded-xl p-6 shadow-lg">
        <h3 class="text-lg font-semibold text-slate-800 mb-4">Recent Activity</h3>
        <div id="recent-activity" class="space-y-3 max-h-64 overflow-y-auto">
         <p class="text-slate-500 text-center py-4">No recent activity</p>
        </div>
       </div>
      </div><!-- Recent Patients Table -->
      <div class="bg-white rounded-xl shadow-lg overflow-hidden">
       <div class="p-6 border-b border-slate-100">
        <h3 class="text-lg font-semibold text-slate-800">Recent Patients</h3>
       </div>
       <div class="overflow-x-auto">
        <table class="w-full">
         <thead class="bg-slate-50">
          <tr>
           <th class="px-6 py-3 text-left text-xs font-semibold text-slate-600 uppercase tracking-wider">Patient ID</th>
           <th class="px-6 py-3 text-left text-xs font-semibold text-slate-600 uppercase tracking-wider">Name</th>
           <th class="px-6 py-3 text-left text-xs font-semibold text-slate-600 uppercase tracking-wider">Department</th>
           <th class="px-6 py-3 text-left text-xs font-semibold text-slate-600 uppercase tracking-wider">Status</th>
           <th class="px-6 py-3 text-left text-xs font-semibold text-slate-600 uppercase tracking-wider">Date</th>
          </tr>
         </thead>
         <tbody id="dashboard-table-body" class="divide-y divide-slate-100">
          <tr>
           <td colspan="5" class="px-6 py-8 text-center text-slate-500">No patients registered yet</td>
          </tr>
         </tbody>
        </table>
       </div>
      </div>
     </div><!-- Reception View -->
     <div id="view-reception" class="view-content hidden">
      <div class="bg-white rounded-xl shadow-lg p-6 mb-6">
       <h3 class="text-lg font-semibold text-slate-800 mb-4">Register New Patient</h3>
       <form id="patient-form" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
        <div><label for="patient-id-input" class="block text-sm font-medium text-slate-700 mb-1">Patient ID</label> <input type="text" id="patient-id-input" required class="w-full px-4 py-2 border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" placeholder="e.g., PAT-001">
        </div>
        <div><label for="patient-name-input" class="block text-sm font-medium text-slate-700 mb-1">Patient Name</label> <input type="text" id="patient-name-input" required class="w-full px-4 py-2 border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" placeholder="Full name">
        </div>
        <div><label for="patient-age-input" class="block text-sm font-medium text-slate-700 mb-1">Age</label> <input type="number" id="patient-age-input" required min="0" max="150" class="w-full px-4 py-2 border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" placeholder="Age">
        </div>
        <div><label for="patient-gender-input" class="block text-sm font-medium text-slate-700 mb-1">Gender</label> <select id="patient-gender-input" required class="w-full px-4 py-2 border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"> <option value="">Select gender</option> <option value="Male">Male</option> <option value="Female">Female</option> <option value="Other">Other</option> </select>
        </div>
        <div><label for="patient-contact-input" class="block text-sm font-medium text-slate-700 mb-1">Contact</label> <input type="tel" id="patient-contact-input" required class="w-full px-4 py-2 border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" placeholder="Phone number">
        </div>
        <div><label for="patient-department-input" class="block text-sm font-medium text-slate-700 mb-1">Send to Department</label> <select id="patient-department-input" required class="w-full px-4 py-2 border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"> <option value="">Select department</option> <option value="laboratory">Laboratory</option> <option value="radiology">Radiology</option> <option value="pharmacy">Pharmacy</option> <option value="medical">Medical Doctors</option> <option value="dental">Dental</option> <option value="nursing">Nursing</option> </select>
        </div>
        <div><label for="patient-priority-input" class="block text-sm font-medium text-slate-700 mb-1">Priority</label> <select id="patient-priority-input" required class="w-full px-4 py-2 border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"> <option value="low">Low</option> <option value="medium">Medium</option> <option value="high">High - Urgent</option> </select>
        </div>
        <div class="md:col-span-2"><label for="patient-notes-input" class="block text-sm font-medium text-slate-700 mb-1">Initial Notes</label> <textarea id="patient-notes-input" rows="2" class="w-full px-4 py-2 border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" placeholder="Reason for visit, symptoms, etc."></textarea>
        </div>
        <div class="flex items-end"><button type="submit" id="submit-patient-btn" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-6 rounded-lg transition-colors"> Register &amp; Send </button>
        </div>
       </form>
      </div><!-- Reception Patient List -->
      <div class="bg-white rounded-xl shadow-lg overflow-hidden">
       <div class="p-6 border-b border-slate-100 flex flex-wrap items-center justify-between gap-4">
        <h3 class="text-lg font-semibold text-slate-800">All Registered Patients</h3>
        <div class="flex flex-wrap gap-2"><input type="text" id="reception-search-name" placeholder="Search by name..." class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-blue-500" oninput="filterReceptionTable()"> <input type="text" id="reception-search-id" placeholder="Search by ID..." class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-blue-500" oninput="filterReceptionTable()"> <input type="date" id="reception-search-date" class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-blue-500" oninput="filterReceptionTable()">
        </div>
       </div>
       <div class="overflow-x-auto">
        <table class="w-full">
         <thead class="bg-slate-50">
          <tr>
           <th class="px-4 py-3 text-left text-xs font-semibold text-slate-600 uppercase tracking-wider">Patient ID</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-slate-600 uppercase tracking-wider">Name</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-slate-600 uppercase tracking-wider">Age/Gender</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-slate-600 uppercase tracking-wider">Contact</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-slate-600 uppercase tracking-wider">Department</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-slate-600 uppercase tracking-wider">Priority</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-slate-600 uppercase tracking-wider">Status</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-slate-600 uppercase tracking-wider">Date</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-slate-600 uppercase tracking-wider">Actions</th>
          </tr>
         </thead>
         <tbody id="reception-table-body" class="divide-y divide-slate-100">
          <tr>
           <td colspan="9" class="px-6 py-8 text-center text-slate-500">No patients registered yet</td>
          </tr>
         </tbody>
        </table>
       </div>
      </div>
     </div><!-- Laboratory View -->
     <div id="view-laboratory" class="view-content hidden">
      <div class="bg-white rounded-xl shadow-lg overflow-hidden">
       <div class="p-6 border-b border-slate-100">
        <div class="flex flex-wrap items-center justify-between gap-4">
         <div class="flex items-center gap-3">
          <div class="w-10 h-10 bg-purple-100 rounded-lg flex items-center justify-center">
           <svg class="w-5 h-5 text-purple-600" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z" />
           </svg>
          </div>
          <div>
           <h3 class="text-lg font-semibold text-slate-800">Laboratory Department</h3>
           <p class="text-sm text-slate-500">Manage lab tests and results</p>
          </div>
         </div>
         <div class="flex flex-wrap gap-2"><input type="text" id="lab-search-name" placeholder="Patient name..." class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-purple-500" oninput="filterDepartmentTable('laboratory')"> <input type="text" id="lab-search-id" placeholder="Patient ID..." class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-purple-500" oninput="filterDepartmentTable('laboratory')"> <input type="date" id="lab-search-date" class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-purple-500" oninput="filterDepartmentTable('laboratory')">
         </div>
        </div>
       </div>
       <div class="overflow-x-auto">
        <table class="w-full">
         <thead class="bg-purple-50">
          <tr>
           <th class="px-4 py-3 text-left text-xs font-semibold text-purple-800 uppercase tracking-wider">Patient ID</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-purple-800 uppercase tracking-wider">Name</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-purple-800 uppercase tracking-wider">Age/Gender</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-purple-800 uppercase tracking-wider">Priority</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-purple-800 uppercase tracking-wider">Notes</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-purple-800 uppercase tracking-wider">Lab Results</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-purple-800 uppercase tracking-wider">Status</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-purple-800 uppercase tracking-wider">Updated</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-purple-800 uppercase tracking-wider">Actions</th>
          </tr>
         </thead>
         <tbody id="laboratory-table-body" class="divide-y divide-slate-100">
          <tr>
           <td colspan="9" class="px-6 py-8 text-center text-slate-500">No patients assigned to Laboratory</td>
          </tr>
         </tbody>
        </table>
       </div>
      </div>
     </div><!-- Radiology View -->
     <div id="view-radiology" class="view-content hidden">
      <div class="bg-white rounded-xl shadow-lg overflow-hidden mb-6">
       <div class="p-6 border-b border-slate-100">
        <div class="flex flex-wrap items-center justify-between gap-4">
         <div class="flex items-center gap-3">
          <div class="w-10 h-10 bg-cyan-100 rounded-lg flex items-center justify-center">
           <svg class="w-5 h-5 text-cyan-600" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 3v2m6-2v2M9 19v2m6-2v2M5 9H3m2 6H3m18-6h-2m2 6h-2M7 19h10a2 2 0 002-2V7a2 2 0 00-2-2H7a2 2 0 00-2 2v10a2 2 0 002 2zM9 9h6v6H9V9z" />
           </svg>
          </div>
          <div>
           <h3 class="text-lg font-semibold text-slate-800">Radiology Department</h3>
           <p class="text-sm text-slate-500">X-Ray, CT, MRI imaging and reports</p>
          </div>
         </div>
         <div class="flex flex-wrap gap-2"><input type="text" id="rad-search-name" placeholder="Patient name..." class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-cyan-500" oninput="filterDepartmentTable('radiology')"> <input type="text" id="rad-search-id" placeholder="Patient ID..." class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-cyan-500" oninput="filterDepartmentTable('radiology')"> <input type="date" id="rad-search-date" class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-cyan-500" oninput="filterDepartmentTable('radiology')">
         </div>
        </div>
       </div><!-- Radiographer Image Transfer Panel -->
       <div class="p-6 bg-gradient-to-r from-cyan-50 to-blue-50 border-b border-slate-100">
        <h4 class="font-semibold text-slate-800 mb-3 flex items-center gap-2">
         <svg class="w-5 h-5 text-cyan-600" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
         </svg> Radiographer Image Transfer System</h4>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
         <div><label class="block text-sm font-medium text-slate-700 mb-1">Select Patient</label> <select id="rad-patient-select" class="w-full px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-cyan-500"> <option value="">Choose patient...</option> </select>
         </div>
         <div><label class="block text-sm font-medium text-slate-700 mb-1">Image Type</label> <select id="rad-image-type" class="w-full px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-cyan-500"> <option value="X-Ray">X-Ray</option> <option value="CT Scan">CT Scan</option> <option value="MRI">MRI</option> <option value="Ultrasound">Ultrasound</option> <option value="Mammography">Mammography</option> </select>
         </div>
         <div><label class="block text-sm font-medium text-slate-700 mb-1">Send To Doctor</label> <select id="rad-doctor-select" class="w-full px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-cyan-500"> <option value="Dr. Smith">Dr. Smith</option> <option value="Dr. Johnson">Dr. Johnson</option> <option value="Dr. Williams">Dr. Williams</option> <option value="Dr. Brown">Dr. Brown</option> </select>
         </div>
         <div class="md:col-span-2"><label class="block text-sm font-medium text-slate-700 mb-1">Image Reference / Notes</label> <input type="text" id="rad-image-ref" placeholder="Enter image reference or findings..." class="w-full px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-cyan-500">
         </div>
         <div class="flex items-end"><button onclick="sendImageToDoctor()" class="w-full bg-cyan-600 hover:bg-cyan-700 text-white font-semibold py-2 px-4 rounded-lg transition-colors flex items-center justify-center gap-2">
           <svg class="w-4 h-4" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 19l9 2-9-18-9 18 9-2zm0 0v-8" />
           </svg> Send to Doctor </button>
         </div>
        </div>
        <p class="text-xs text-slate-500 mt-2"><span class="font-medium">Network:</span> Images transmitted via IP 122.333.44.5</p>
       </div>
       <div class="overflow-x-auto">
        <table class="w-full">
         <thead class="bg-cyan-50">
          <tr>
           <th class="px-4 py-3 text-left text-xs font-semibold text-cyan-800 uppercase tracking-wider">Patient ID</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-cyan-800 uppercase tracking-wider">Name</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-cyan-800 uppercase tracking-wider">Age/Gender</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-cyan-800 uppercase tracking-wider">Imaging Type</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-cyan-800 uppercase tracking-wider">Radiology Notes</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-cyan-800 uppercase tracking-wider">Sent To</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-cyan-800 uppercase tracking-wider">Status</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-cyan-800 uppercase tracking-wider">Updated</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-cyan-800 uppercase tracking-wider">Actions</th>
          </tr>
         </thead>
         <tbody id="radiology-table-body" class="divide-y divide-slate-100">
          <tr>
           <td colspan="9" class="px-6 py-8 text-center text-slate-500">No patients assigned to Radiology</td>
          </tr>
         </tbody>
        </table>
       </div>
      </div>
     </div><!-- Pharmacy View -->
     <div id="view-pharmacy" class="view-content hidden">
      <div class="bg-white rounded-xl shadow-lg overflow-hidden">
       <div class="p-6 border-b border-slate-100">
        <div class="flex flex-wrap items-center justify-between gap-4">
         <div class="flex items-center gap-3">
          <div class="w-10 h-10 bg-green-100 rounded-lg flex items-center justify-center">
           <svg class="w-5 h-5 text-green-600" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z" />
           </svg>
          </div>
          <div>
           <h3 class="text-lg font-semibold text-slate-800">Pharmacy Department</h3>
           <p class="text-sm text-slate-500">Medication dispensing and prescriptions</p>
          </div>
         </div>
         <div class="flex flex-wrap gap-2"><input type="text" id="pharm-search-name" placeholder="Patient name..." class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-green-500" oninput="filterDepartmentTable('pharmacy')"> <input type="text" id="pharm-search-id" placeholder="Patient ID..." class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-green-500" oninput="filterDepartmentTable('pharmacy')"> <input type="date" id="pharm-search-date" class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-green-500" oninput="filterDepartmentTable('pharmacy')">
         </div>
        </div>
       </div>
       <div class="overflow-x-auto">
        <table class="w-full">
         <thead class="bg-green-50">
          <tr>
           <th class="px-4 py-3 text-left text-xs font-semibold text-green-800 uppercase tracking-wider">Patient ID</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-green-800 uppercase tracking-wider">Name</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-green-800 uppercase tracking-wider">Age/Gender</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-green-800 uppercase tracking-wider">Prescription</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-green-800 uppercase tracking-wider">Notes</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-green-800 uppercase tracking-wider">Status</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-green-800 uppercase tracking-wider">Updated</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-green-800 uppercase tracking-wider">Actions</th>
          </tr>
         </thead>
         <tbody id="pharmacy-table-body" class="divide-y divide-slate-100">
          <tr>
           <td colspan="8" class="px-6 py-8 text-center text-slate-500">No patients assigned to Pharmacy</td>
          </tr>
         </tbody>
        </table>
       </div>
      </div>
     </div><!-- Medical Doctors View -->
     <div id="view-medical" class="view-content hidden">
      <div class="bg-white rounded-xl shadow-lg overflow-hidden">
       <div class="p-6 border-b border-slate-100">
        <div class="flex flex-wrap items-center justify-between gap-4">
         <div class="flex items-center gap-3">
          <div class="w-10 h-10 bg-red-100 rounded-lg flex items-center justify-center">
           <svg class="w-5 h-5 text-red-600" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" />
           </svg>
          </div>
          <div>
           <h3 class="text-lg font-semibold text-slate-800">Medical Doctors</h3>
           <p class="text-sm text-slate-500">Patient consultations and diagnoses</p>
          </div>
         </div>
         <div class="flex flex-wrap gap-2"><input type="text" id="med-search-name" placeholder="Patient name..." class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-red-500" oninput="filterDepartmentTable('medical')"> <input type="text" id="med-search-id" placeholder="Patient ID..." class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-red-500" oninput="filterDepartmentTable('medical')"> <input type="date" id="med-search-date" class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-red-500" oninput="filterDepartmentTable('medical')">
         </div>
        </div>
       </div>
       <div class="overflow-x-auto">
        <table class="w-full">
         <thead class="bg-red-50">
          <tr>
           <th class="px-4 py-3 text-left text-xs font-semibold text-red-800 uppercase tracking-wider">Patient ID</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-red-800 uppercase tracking-wider">Name</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-red-800 uppercase tracking-wider">Age/Gender</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-red-800 uppercase tracking-wider">Priority</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-red-800 uppercase tracking-wider">Diagnosis</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-red-800 uppercase tracking-wider">Notes</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-red-800 uppercase tracking-wider">Radiology</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-red-800 uppercase tracking-wider">Status</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-red-800 uppercase tracking-wider">Updated</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-red-800 uppercase tracking-wider">Actions</th>
          </tr>
         </thead>
         <tbody id="medical-table-body" class="divide-y divide-slate-100">
          <tr>
           <td colspan="10" class="px-6 py-8 text-center text-slate-500">No patients assigned to Medical Doctors</td>
          </tr>
         </tbody>
        </table>
       </div>
      </div>
     </div><!-- Dental View -->
     <div id="view-dental" class="view-content hidden">
      <div class="bg-white rounded-xl shadow-lg overflow-hidden">
       <div class="p-6 border-b border-slate-100">
        <div class="flex flex-wrap items-center justify-between gap-4">
         <div class="flex items-center gap-3">
          <div class="w-10 h-10 bg-indigo-100 rounded-lg flex items-center justify-center">
           <svg class="w-5 h-5 text-indigo-600" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14.828 14.828a4 4 0 01-5.656 0M9 10h.01M15 10h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
           </svg>
          </div>
          <div>
           <h3 class="text-lg font-semibold text-slate-800">Dental Department</h3>
           <p class="text-sm text-slate-500">Dental care and procedures</p>
          </div>
         </div>
         <div class="flex flex-wrap gap-2"><input type="text" id="dent-search-name" placeholder="Patient name..." class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500" oninput="filterDepartmentTable('dental')"> <input type="text" id="dent-search-id" placeholder="Patient ID..." class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500" oninput="filterDepartmentTable('dental')"> <input type="date" id="dent-search-date" class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500" oninput="filterDepartmentTable('dental')">
         </div>
        </div>
       </div>
       <div class="overflow-x-auto">
        <table class="w-full">
         <thead class="bg-indigo-50">
          <tr>
           <th class="px-4 py-3 text-left text-xs font-semibold text-indigo-800 uppercase tracking-wider">Patient ID</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-indigo-800 uppercase tracking-wider">Name</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-indigo-800 uppercase tracking-wider">Age/Gender</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-indigo-800 uppercase tracking-wider">Priority</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-indigo-800 uppercase tracking-wider">Diagnosis</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-indigo-800 uppercase tracking-wider">Notes</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-indigo-800 uppercase tracking-wider">Status</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-indigo-800 uppercase tracking-wider">Updated</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-indigo-800 uppercase tracking-wider">Actions</th>
          </tr>
         </thead>
         <tbody id="dental-table-body" class="divide-y divide-slate-100">
          <tr>
           <td colspan="9" class="px-6 py-8 text-center text-slate-500">No patients assigned to Dental</td>
          </tr>
         </tbody>
        </table>
       </div>
      </div>
     </div><!-- Nursing View -->
     <div id="view-nursing" class="view-content hidden">
      <div class="bg-white rounded-xl shadow-lg overflow-hidden">
       <div class="p-6 border-b border-slate-100">
        <div class="flex flex-wrap items-center justify-between gap-4">
         <div class="flex items-center gap-3">
          <div class="w-10 h-10 bg-pink-100 rounded-lg flex items-center justify-center">
           <svg class="w-5 h-5 text-pink-600" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z" />
           </svg>
          </div>
          <div>
           <h3 class="text-lg font-semibold text-slate-800">Nursing Department</h3>
           <p class="text-sm text-slate-500">Patient care and monitoring</p>
          </div>
         </div>
         <div class="flex flex-wrap gap-2"><input type="text" id="nurs-search-name" placeholder="Patient name..." class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-pink-500" oninput="filterDepartmentTable('nursing')"> <input type="text" id="nurs-search-id" placeholder="Patient ID..." class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-pink-500" oninput="filterDepartmentTable('nursing')"> <input type="date" id="nurs-search-date" class="px-3 py-2 border border-slate-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-pink-500" oninput="filterDepartmentTable('nursing')">
         </div>
        </div>
       </div>
       <div class="overflow-x-auto">
        <table class="w-full">
         <thead class="bg-pink-50">
          <tr>
           <th class="px-4 py-3 text-left text-xs font-semibold text-pink-800 uppercase tracking-wider">Patient ID</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-pink-800 uppercase tracking-wider">Name</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-pink-800 uppercase tracking-wider">Age/Gender</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-pink-800 uppercase tracking-wider">Priority</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-pink-800 uppercase tracking-wider">Care Notes</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-pink-800 uppercase tracking-wider">Assigned To</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-pink-800 uppercase tracking-wider">Status</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-pink-800 uppercase tracking-wider">Updated</th>
           <th class="px-4 py-3 text-left text-xs font-semibold text-pink-800 uppercase tracking-wider">Actions</th>
          </tr>
         </thead>
         <tbody id="nursing-table-body" class="divide-y divide-slate-100">
          <tr>
           <td colspan="9" class="px-6 py-8 text-center text-slate-500">No patients assigned to Nursing</td>
          </tr>
         </tbody>
        </table>
       </div>
      </div>
     </div>
    </div>
   </main>
  </div><!-- Toast Notification -->
  <div id="toast" class="fixed bottom-4 right-4 transform translate-y-20 opacity-0 transition-all duration-300 z-50">
   <div class="bg-slate-800 text-white px-6 py-3 rounded-lg shadow-lg flex items-center gap-3"><span id="toast-message">Notification</span>
   </div>
  </div><!-- Edit Modal -->
  <div id="edit-modal" class="fixed inset-0 modal-overlay hidden z-50 flex items-center justify-center p-4">
   <div class="bg-white rounded-xl shadow-2xl w-full max-w-lg max-h-[90%] overflow-y-auto">
    <div class="p-6 border-b border-slate-100 flex items-center justify-between">
     <h3 class="text-lg font-semibold text-slate-800">Edit Patient Record</h3><button onclick="closeEditModal()" class="text-slate-400 hover:text-slate-600">
      <svg class="w-6 h-6" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
      </svg></button>
    </div>
    <form id="edit-form" class="p-6 space-y-4"><input type="hidden" id="edit-record-id">
     <div><label for="edit-status" class="block text-sm font-medium text-slate-700 mb-1">Status</label> <select id="edit-status" class="w-full px-4 py-2 border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"> <option value="pending">Pending</option> <option value="in-progress">In Progress</option> <option value="completed">Completed</option> </select>
     </div>
     <div><label for="edit-notes" class="block text-sm font-medium text-slate-700 mb-1">Notes</label> <textarea id="edit-notes" rows="3" class="w-full px-4 py-2 border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"></textarea>
     </div>
     <div id="edit-diagnosis-field"><label for="edit-diagnosis" class="block text-sm font-medium text-slate-700 mb-1">Diagnosis</label> <textarea id="edit-diagnosis" rows="2" class="w-full px-4 py-2 border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"></textarea>
     </div>
     <div id="edit-prescription-field"><label for="edit-prescription" class="block text-sm font-medium text-slate-700 mb-1">Prescription</label> <textarea id="edit-prescription" rows="2" class="w-full px-4 py-2 border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"></textarea>
     </div>
     <div id="edit-lab-results-field"><label for="edit-lab-results" class="block text-sm font-medium text-slate-700 mb-1">Lab Results</label> <textarea id="edit-lab-results" rows="2" class="w-full px-4 py-2 border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"></textarea>
     </div>
     <div id="edit-radiology-field"><label for="edit-radiology-notes" class="block text-sm font-medium text-slate-700 mb-1">Radiology Notes</label> <textarea id="edit-radiology-notes" rows="2" class="w-full px-4 py-2 border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"></textarea>
     </div>
     <div id="edit-assigned-field"><label for="edit-assigned" class="block text-sm font-medium text-slate-700 mb-1">Assigned To</label> <input type="text" id="edit-assigned" class="w-full px-4 py-2 border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
     </div>
     <div class="flex gap-3 pt-4"><button type="button" onclick="closeEditModal()" class="flex-1 bg-slate-100 hover:bg-slate-200 text-slate-700 font-semibold py-2 px-4 rounded-lg transition-colors"> Cancel </button> <button type="submit" id="edit-submit-btn" class="flex-1 bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-4 rounded-lg transition-colors"> Save Changes </button>
     </div>
    </form>
   </div>
  </div><!-- Transfer Modal -->
  <div id="transfer-modal" class="fixed inset-0 modal-overlay hidden z-50 flex items-center justify-center p-4">
   <div class="bg-white rounded-xl shadow-2xl w-full max-w-md">
    <div class="p-6 border-b border-slate-100 flex items-center justify-between">
     <h3 class="text-lg font-semibold text-slate-800">Transfer Patient</h3><button onclick="closeTransferModal()" class="text-slate-400 hover:text-slate-600">
      <svg class="w-6 h-6" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
      </svg></button>
    </div>
    <form id="transfer-form" class="p-6 space-y-4"><input type="hidden" id="transfer-record-id">
     <div><label for="transfer-department" class="block text-sm font-medium text-slate-700 mb-1">Transfer to Department</label> <select id="transfer-department" required class="w-full px-4 py-2 border border-slate-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"> <option value="">Select department</option> <option value="laboratory">Laboratory</option> <option value="radiology">Radiology</option> <option value="pharmacy">Pharmacy</option> <option value="medical">Medical Doctors</option> <option value="dental">Dental</option> <option value="nursing">Nursing</option> </select>
     </div>
     <div class="flex gap-3 pt-4"><button type="button" onclick="closeTransferModal()" class="flex-1 bg-slate-100 hover:bg-slate-200 text-slate-700 font-semibold py-2 px-4 rounded-lg transition-colors"> Cancel </button> <button type="submit" id="transfer-submit-btn" class="flex-1 bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-4 rounded-lg transition-colors"> Transfer </button>
     </div>
    </form>
   </div>
  </div>
  <script>
    // Application State
    let allPatients = [];
    let currentView = 'dashboard';
    let editingPatient = null;
    
    const defaultConfig = {
      hospital_name: 'City Hospital',
      system_title: 'eHMS System v2.0'
    };
    
    // Department colors for styling
    const deptColors = {
      laboratory: { bg: 'purple', light: 'purple-100', text: 'purple-600' },
      radiology: { bg: 'cyan', light: 'cyan-100', text: 'cyan-600' },
      pharmacy: { bg: 'green', light: 'green-100', text: 'green-600' },
      medical: { bg: 'red', light: 'red-100', text: 'red-600' },
      dental: { bg: 'indigo', light: 'indigo-100', text: 'indigo-600' },
      nursing: { bg: 'pink', light: 'pink-100', text: 'pink-600' }
    };
    
    const deptNames = {
      laboratory: 'Laboratory',
      radiology: 'Radiology',
      pharmacy: 'Pharmacy',
      medical: 'Medical Doctors',
      dental: 'Dental',
      nursing: 'Nursing'
    };

    // Data Handler for SDK
    const dataHandler = {
      onDataChanged(data) {
        allPatients = data.sort((a, b) => new Date(b.updated_at) - new Date(a.updated_at));
        renderAllViews();
      }
    };
    
    // Initialize Application
    async function initApp() {
      // Set current date
      document.getElementById('current-date').textContent = new Date().toLocaleDateString('en-US', {
        weekday: 'long', year: 'numeric', month: 'long', day: 'numeric'
      });
      
      // Initialize Element SDK
      if (window.elementSdk) {
        window.elementSdk.init({
          defaultConfig,
          onConfigChange: async (config) => {
            document.getElementById('hospital-name').textContent = config.hospital_name || defaultConfig.hospital_name;
            document.getElementById('system-title').textContent = config.system_title || defaultConfig.system_title;
          },
          mapToCapabilities: (config) => ({
            recolorables: [],
            borderables: [],
            fontEditable: undefined,
            fontSizeable: undefined
          }),
          mapToEditPanelValues: (config) => new Map([
            ['hospital_name', config.hospital_name || defaultConfig.hospital_name],
            ['system_title', config.system_title || defaultConfig.system_title]
          ])
        });
      }
      
      // Initialize Data SDK
      if (window.dataSdk) {
        const result = await window.dataSdk.init(dataHandler);
        if (!result.isOk) {
          showToast('Failed to initialize data connection');
        }
      }
      
      // Setup form handlers
      setupFormHandlers();
    }
    
    function setupFormHandlers() {
      // Patient registration form
      document.getElementById('patient-form').addEventListener('submit', async (e) => {
        e.preventDefault();
        
        if (allPatients.length >= 999) {
          showToast('Maximum patient limit (999) reached. Please archive old records.');
          return;
        }
        
        const btn = document.getElementById('submit-patient-btn');
        btn.disabled = true;
        btn.textContent = 'Registering...';
        
        const now = new Date().toISOString();
        const patientData = {
          id: Date.now().toString(),
          patient_id: document.getElementById('patient-id-input').value,
          patient_name: document.getElementById('patient-name-input').value,
          age: parseInt(document.getElementById('patient-age-input').value),
          gender: document.getElementById('patient-gender-input').value,
          contact: document.getElementById('patient-contact-input').value,
          department: document.getElementById('patient-department-input').value,
          priority: document.getElementById('patient-priority-input').value,
          notes: document.getElementById('patient-notes-input').value,
          status: 'pending',
          created_at: now,
          updated_at: now,
          assigned_to: '',
          image_url: '',
          diagnosis: '',
          prescription: '',
          lab_results: '',
          radiology_notes: ''
        };
        
        if (window.dataSdk) {
          const result = await window.dataSdk.create(patientData);
          if (result.isOk) {
            showToast(`Patient sent to ${deptNames[patientData.department]}`);
            e.target.reset();
          } else {
            showToast('Failed to register patient');
          }
        }
        
        btn.disabled = false;
        btn.textContent = 'Register & Send';
      });
      
      // Edit form
      document.getElementById('edit-form').addEventListener('submit', async (e) => {
        e.preventDefault();
        
        if (!editingPatient) return;
        
        const btn = document.getElementById('edit-submit-btn');
        btn.disabled = true;
        btn.textContent = 'Saving...';
        
        const updatedPatient = {
          ...editingPatient,
          status: document.getElementById('edit-status').value,
          notes: document.getElementById('edit-notes').value,
          diagnosis: document.getElementById('edit-diagnosis').value,
          prescription: document.getElementById('edit-prescription').value,
          lab_results: document.getElementById('edit-lab-results').value,
          radiology_notes: document.getElementById('edit-radiology-notes').value,
          assigned_to: document.getElementById('edit-assigned').value,
          updated_at: new Date().toISOString()
        };
        
        if (window.dataSdk) {
          const result = await window.dataSdk.update(updatedPatient);
          if (result.isOk) {
            showToast('Patient record updated');
            closeEditModal();
          } else {
            showToast('Failed to update record');
          }
        }
        
        btn.disabled = false;
        btn.textContent = 'Save Changes';
      });
      
      // Transfer form
      document.getElementById('transfer-form').addEventListener('submit', async (e) => {
        e.preventDefault();
        
        const recordId = document.getElementById('transfer-record-id').value;
        const newDept = document.getElementById('transfer-department').value;
        
        const patient = allPatients.find(p => p.__backendId === recordId);
        if (!patient) return;
        
        const btn = document.getElementById('transfer-submit-btn');
        btn.disabled = true;
        btn.textContent = 'Transferring...';
        
        const updatedPatient = {
          ...patient,
          department: newDept,
          status: 'pending',
          updated_at: new Date().toISOString()
        };
        
        if (window.dataSdk) {
          const result = await window.dataSdk.update(updatedPatient);
          if (result.isOk) {
            showToast(`Patient transferred to ${deptNames[newDept]}`);
            closeTransferModal();
          } else {
            showToast('Failed to transfer patient');
          }
        }
        
        btn.disabled = false;
        btn.textContent = 'Transfer';
      });
    }
    
    // View switching
    function switchView(view) {
      currentView = view;
      
      // Update sidebar
      document.querySelectorAll('.sidebar-item').forEach(item => {
        item.classList.remove('active');
        if (item.dataset.view === view) {
          item.classList.add('active');
        }
      });
      
      // Update view title
      const titles = {
        dashboard: 'Dashboard',
        reception: 'Reception Portal',
        laboratory: 'Laboratory Department',
        radiology: 'Radiology Department',
        pharmacy: 'Pharmacy Department',
        medical: 'Medical Doctors',
        dental: 'Dental Department',
        nursing: 'Nursing Department'
      };
      document.getElementById('current-view-title').textContent = titles[view] || 'Dashboard';
      
      // Show/hide views
      document.querySelectorAll('.view-content').forEach(v => v.classList.add('hidden'));
      document.getElementById(`view-${view}`).classList.remove('hidden');
      
      // Update radiology patient select if needed
      if (view === 'radiology') {
        updateRadiologyPatientSelect();
      }
    }
    
    // Render all views
    function renderAllViews() {
      renderDashboard();
      renderReceptionTable();
      renderDepartmentTable('laboratory');
      renderDepartmentTable('radiology');
      renderDepartmentTable('pharmacy');
      renderDepartmentTable('medical');
      renderDepartmentTable('dental');
      renderDepartmentTable('nursing');
      updateRadiologyPatientSelect();
      updateNotificationBadge();
    }
    
    // Dashboard rendering
    function renderDashboard() {
      const total = allPatients.length;
      const pending = allPatients.filter(p => p.status === 'pending').length;
      const inProgress = allPatients.filter(p => p.status === 'in-progress').length;
      const completed = allPatients.filter(p => p.status === 'completed').length;
      
      document.getElementById('stat-total').textContent = total;
      document.getElementById('stat-pending').textContent = pending;
      document.getElementById('stat-inprogress').textContent = inProgress;
      document.getElementById('stat-completed').textContent = completed;
      
      // Department activity
      const deptActivity = document.getElementById('dept-activity');
      const deptCounts = {};
      Object.keys(deptNames).forEach(d => deptCounts[d] = 0);
      allPatients.forEach(p => {
        if (deptCounts[p.department] !== undefined) {
          deptCounts[p.department]++;
        }
      });
      
      const maxCount = Math.max(...Object.values(deptCounts), 1);
      
      deptActivity.innerHTML = Object.entries(deptCounts).map(([dept, count]) => {
        const color = deptColors[dept];
        const percentage = (count / maxCount) * 100;
        return `
          <div class="flex items-center gap-3">
            <span class="w-32 text-sm text-slate-600">${deptNames[dept]}</span>
            <div class="flex-1 bg-slate-100 rounded-full h-3 overflow-hidden">
              <div class="bg-${color.text} h-full rounded-full transition-all duration-500" style="width: ${percentage}%"></div>
            </div>
            <span class="w-8 text-sm font-semibold text-slate-700">${count}</span>
          </div>
        `;
      }).join('');
      
      // Recent activity
      const recentActivity = document.getElementById('recent-activity');
      const recentPatients = allPatients.slice(0, 5);
      
      if (recentPatients.length === 0) {
        recentActivity.innerHTML = '<p class="text-slate-500 text-center py-4">No recent activity</p>';
      } else {
        recentActivity.innerHTML = recentPatients.map(p => `
          <div class="flex items-center gap-3 p-2 rounded-lg hover:bg-slate-50">
            <div class="w-8 h-8 bg-${deptColors[p.department]?.light || 'slate-100'} rounded-full flex items-center justify-center">
              <span class="text-xs font-semibold text-${deptColors[p.department]?.text || 'slate-600'}">${p.patient_name.charAt(0)}</span>
            </div>
            <div class="flex-1 min-w-0">
              <p class="text-sm font-medium text-slate-700 truncate">${p.patient_name}</p>
              <p class="text-xs text-slate-500">${deptNames[p.department] || p.department}</p>
            </div>
            <span class="px-2 py-1 text-xs rounded-full status-${p.status === 'in-progress' ? 'inprogress' : p.status}">${p.status}</span>
          </div>
        `).join('');
      }
      
      // Dashboard table
      const dashboardTable = document.getElementById('dashboard-table-body');
      if (allPatients.length === 0) {
        dashboardTable.innerHTML = '<tr><td colspan="5" class="px-6 py-8 text-center text-slate-500">No patients registered yet</td></tr>';
      } else {
        dashboardTable.innerHTML = allPatients.slice(0, 10).map(p => `
          <tr class="table-row">
            <td class="px-6 py-4 text-sm font-medium text-slate-700">${p.patient_id}</td>
            <td class="px-6 py-4 text-sm text-slate-600">${p.patient_name}</td>
            <td class="px-6 py-4">
              <span class="px-2 py-1 text-xs rounded-full bg-${deptColors[p.department]?.light || 'slate-100'} text-${deptColors[p.department]?.text || 'slate-600'}">
                ${deptNames[p.department] || p.department}
              </span>
            </td>
            <td class="px-6 py-4">
              <span class="px-2 py-1 text-xs rounded-full status-${p.status === 'in-progress' ? 'inprogress' : p.status}">${p.status}</span>
            </td>
            <td class="px-6 py-4 text-sm text-slate-500">${formatDate(p.created_at)}</td>
          </tr>
        `).join('');
      }
    }
    
    // Reception table
    function renderReceptionTable() {
      const tbody = document.getElementById('reception-table-body');
      const filtered = filterPatients(allPatients, 'reception');
      
      if (filtered.length === 0) {
        tbody.innerHTML = '<tr><td colspan="9" class="px-6 py-8 text-center text-slate-500">No patients registered yet</td></tr>';
        return;
      }
      
      tbody.innerHTML = filtered.map(p => `
        <tr class="table-row priority-${p.priority}">
          <td class="px-4 py-3 text-sm font-medium text-slate-700">${p.patient_id}</td>
          <td class="px-4 py-3 text-sm text-slate-600">${p.patient_name}</td>
          <td class="px-4 py-3 text-sm text-slate-500">${p.age} / ${p.gender}</td>
          <td class="px-4 py-3 text-sm text-slate-500">${p.contact}</td>
          <td class="px-4 py-3">
            <span class="px-2 py-1 text-xs rounded-full bg-${deptColors[p.department]?.light || 'slate-100'} text-${deptColors[p.department]?.text || 'slate-600'}">
              ${deptNames[p.department] || p.department}
            </span>
          </td>
          <td class="px-4 py-3">
            <span class="px-2 py-1 text-xs rounded-full ${p.priority === 'high' ? 'bg-red-100 text-red-700' : p.priority === 'medium' ? 'bg-amber-100 text-amber-700' : 'bg-green-100 text-green-700'}">
              ${p.priority}
            </span>
          </td>
          <td class="px-4 py-3">
            <span class="px-2 py-1 text-xs rounded-full status-${p.status === 'in-progress' ? 'inprogress' : p.status}">${p.status}</span>
          </td>
          <td class="px-4 py-3 text-sm text-slate-500">${formatDate(p.created_at)}</td>
          <td class="px-4 py-3">
            <div class="flex gap-1">
              <button onclick="openTransferModal('${p.__backendId}')" class="p-1 text-blue-600 hover:bg-blue-50 rounded" title="Transfer">
                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7h12m0 0l-4-4m4 4l-4 4m0 6H4m0 0l4 4m-4-4l4-4"/>
                </svg>
              </button>
            </div>
          </td>
        </tr>
      `).join('');
    }
    
    // Department table rendering
    function renderDepartmentTable(dept) {
      const tbody = document.getElementById(`${dept}-table-body`);
      const deptPatients = allPatients.filter(p => p.department === dept);
      const filtered = filterPatients(deptPatients, dept);
      
      if (filtered.length === 0) {
        const colSpan = dept === 'radiology' ? 9 : dept === 'medical' ? 10 : dept === 'pharmacy' ? 8 : 9;
        tbody.innerHTML = `<tr><td colspan="${colSpan}" class="px-6 py-8 text-center text-slate-500">No patients assigned to ${deptNames[dept]}</td></tr>`;
        return;
      }
      
      tbody.innerHTML = filtered.map(p => generateDepartmentRow(p, dept)).join('');
    }
    
    function generateDepartmentRow(p, dept) {
      const baseRow = `
        <td class="px-4 py-3 text-sm font-medium text-slate-700">${p.patient_id}</td>
        <td class="px-4 py-3 text-sm text-slate-600">${p.patient_name}</td>
        <td class="px-4 py-3 text-sm text-slate-500">${p.age} / ${p.gender}</td>
      `;
      
      const priorityCell = `
        <td class="px-4 py-3">
          <span class="px-2 py-1 text-xs rounded-full ${p.priority === 'high' ? 'bg-red-100 text-red-700' : p.priority === 'medium' ? 'bg-amber-100 text-amber-700' : 'bg-green-100 text-green-700'}">
            ${p.priority}
          </span>
        </td>
      `;
      
      const statusCell = `
        <td class="px-4 py-3">
          <span class="px-2 py-1 text-xs rounded-full status-${p.status === 'in-progress' ? 'inprogress' : p.status}">${p.status}</span>
        </td>
      `;
      
      const updatedCell = `<td class="px-4 py-3 text-sm text-slate-500">${formatDate(p.updated_at)}</td>`;
      
      const actionsCell = `
        <td class="px-4 py-3">
          <div class="flex gap-1">
            <button onclick="openEditModal('${p.__backendId}', '${dept}')" class="p-1 text-blue-600 hover:bg-blue-50 rounded" title="Edit">
              <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"/>
              </svg>
            </button>
            <button onclick="openTransferModal('${p.__backendId}')" class="p-1 text-green-600 hover:bg-green-50 rounded" title="Transfer">
              <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7h12m0 0l-4-4m4 4l-4 4m0 6H4m0 0l4 4m-4-4l4-4"/>
              </svg>
            </button>
          </div>
        </td>
      `;
      
      // Department-specific columns
      if (dept === 'laboratory') {
        return `
          <tr class="table-row priority-${p.priority}">
            ${baseRow}
            ${priorityCell}
            <td class="px-4 py-3 text-sm text-slate-500 max-w-xs truncate">${p.notes || '-'}</td>
            <td class="px-4 py-3 text-sm text-slate-500 max-w-xs truncate">${p.lab_results || '-'}</td>
            ${statusCell}
            ${updatedCell}
            ${actionsCell}
          </tr>
        `;
      }
      
      if (dept === 'radiology') {
        return `
          <tr class="table-row priority-${p.priority}">
            ${baseRow}
            <td class="px-4 py-3 text-sm text-slate-500">${p.image_url || '-'}</td>
            <td class="px-4 py-3 text-sm text-slate-500 max-w-xs truncate">${p.radiology_notes || '-'}</td>
            <td class="px-4 py-3 text-sm text-slate-500">${p.assigned_to || '-'}</td>
            ${statusCell}
            ${updatedCell}
            ${actionsCell}
          </tr>
        `;
      }
      
      if (dept === 'pharmacy') {
        return `
          <tr class="table-row priority-${p.priority}">
            ${baseRow}
            <td class="px-4 py-3 text-sm text-slate-500 max-w-xs truncate">${p.prescription || '-'}</td>
            <td class="px-4 py-3 text-sm text-slate-500 max-w-xs truncate">${p.notes || '-'}</td>
            ${statusCell}
            ${updatedCell}
            ${actionsCell}
          </tr>
        `;
      }
      
      if (dept === 'medical') {
        return `
          <tr class="table-row priority-${p.priority}">
            ${baseRow}
            ${priorityCell}
            <td class="px-4 py-3 text-sm text-slate-500 max-w-xs truncate">${p.diagnosis || '-'}</td>
            <td class="px-4 py-3 text-sm text-slate-500 max-w-xs truncate">${p.notes || '-'}</td>
            <td class="px-4 py-3 text-sm text-slate-500 max-w-xs truncate">${p.radiology_notes || '-'}</td>
            ${statusCell}
            ${updatedCell}
            ${actionsCell}
          </tr>
        `;
      }
      
      // Default for dental, nursing
      return `
        <tr class="table-row priority-${p.priority}">
          ${baseRow}
          ${priorityCell}
          <td class="px-4 py-3 text-sm text-slate-500 max-w-xs truncate">${p.diagnosis || '-'}</td>
          <td class="px-4 py-3 text-sm text-slate-500 max-w-xs truncate">${p.notes || '-'}</td>
          ${dept === 'nursing' ? `<td class="px-4 py-3 text-sm text-slate-500">${p.assigned_to || '-'}</td>` : ''}
          ${statusCell}
          ${updatedCell}
          ${actionsCell}
        </tr>
      `;
    }
    
    // Filtering
    function filterPatients(patients, section) {
      let searchName = '', searchId = '', searchDate = '';
      
      if (section === 'reception') {
        searchName = document.getElementById('reception-search-name')?.value?.toLowerCase() || '';
        searchId = document.getElementById('reception-search-id')?.value?.toLowerCase() || '';
        searchDate = document.getElementById('reception-search-date')?.value || '';
      } else {
        const prefixes = { laboratory: 'lab', radiology: 'rad', pharmacy: 'pharm', medical: 'med', dental: 'dent', nursing: 'nurs' };
        const prefix = prefixes[section];
        if (prefix) {
          searchName = document.getElementById(`${prefix}-search-name`)?.value?.toLowerCase() || '';
          searchId = document.getElementById(`${prefix}-search-id`)?.value?.toLowerCase() || '';
          searchDate = document.getElementById(`${prefix}-search-date`)?.value || '';
        }
      }
      
      return patients.filter(p => {
        const matchName = !searchName || p.patient_name.toLowerCase().includes(searchName);
        const matchId = !searchId || p.patient_id.toLowerCase().includes(searchId);
        const matchDate = !searchDate || p.created_at.startsWith(searchDate);
        return matchName && matchId && matchDate;
      });
    }
    
    function filterReceptionTable() {
      renderReceptionTable();
    }
    
    function filterDepartmentTable(dept) {
      renderDepartmentTable(dept);
    }
    
    function handleGlobalSearch(query) {
      // Global search affects current view
      if (currentView === 'reception') {
        document.getElementById('reception-search-name').value = query;
        filterReceptionTable();
      } else if (deptNames[currentView]) {
        const prefixes = { laboratory: 'lab', radiology: 'rad', pharmacy: 'pharm', medical: 'med', dental: 'dent', nursing: 'nurs' };
        const prefix = prefixes[currentView];
        if (prefix) {
          document.getElementById(`${prefix}-search-name`).value = query;
          filterDepartmentTable(currentView);
        }
      }
    }
    
    // Modal handlers
    function openEditModal(recordId, dept) {
      editingPatient = allPatients.find(p => p.__backendId === recordId);
      if (!editingPatient) return;
      
      document.getElementById('edit-record-id').value = recordId;
      document.getElementById('edit-status').value = editingPatient.status;
      document.getElementById('edit-notes').value = editingPatient.notes || '';
      document.getElementById('edit-diagnosis').value = editingPatient.diagnosis || '';
      document.getElementById('edit-prescription').value = editingPatient.prescription || '';
      document.getElementById('edit-lab-results').value = editingPatient.lab_results || '';
      document.getElementById('edit-radiology-notes').value = editingPatient.radiology_notes || '';
      document.getElementById('edit-assigned').value = editingPatient.assigned_to || '';
      
      // Show/hide fields based on department
      document.getElementById('edit-diagnosis-field').classList.toggle('hidden', !['medical', 'dental'].includes(dept));
      document.getElementById('edit-prescription-field').classList.toggle('hidden', dept !== 'pharmacy' && dept !== 'medical');
      document.getElementById('edit-lab-results-field').classList.toggle('hidden', dept !== 'laboratory');
      document.getElementById('edit-radiology-field').classList.toggle('hidden', dept !== 'radiology');
      document.getElementById('edit-assigned-field').classList.toggle('hidden', !['radiology', 'nursing'].includes(dept));
      
      document.getElementById('edit-modal').classList.remove('hidden');
    }
    
    function closeEditModal() {
      document.getElementById('edit-modal').classList.add('hidden');
      editingPatient = null;
    }
    
    function openTransferModal(recordId) {
      document.getElementById('transfer-record-id').value = recordId;
      const patient = allPatients.find(p => p.__backendId === recordId);
      if (patient) {
        document.getElementById('transfer-department').value = '';
      }
      document.getElementById('transfer-modal').classList.remove('hidden');
    }
    
    function closeTransferModal() {
      document.getElementById('transfer-modal').classList.add('hidden');
    }
    
    // Radiology specific
    function updateRadiologyPatientSelect() {
      const select = document.getElementById('rad-patient-select');
      const radPatients = allPatients.filter(p => p.department === 'radiology');
      
      select.innerHTML = '<option value="">Choose patient...</option>' + 
        radPatients.map(p => `<option value="${p.__backendId}">${p.patient_id} - ${p.patient_name}</option>`).join('');
    }
    
    async function sendImageToDoctor() {
      const patientId = document.getElementById('rad-patient-select').value;
      const imageType = document.getElementById('rad-image-type').value;
      const doctor = document.getElementById('rad-doctor-select').value;
      const imageRef = document.getElementById('rad-image-ref').value;
      
      if (!patientId) {
        showToast('Please select a patient');
        return;
      }
      
      const patient = allPatients.find(p => p.__backendId === patientId);
      if (!patient) return;
      
      const updatedPatient = {
        ...patient,
        image_url: imageType,
        radiology_notes: imageRef || `${imageType} sent to ${doctor}`,
        assigned_to: doctor,
        status: 'in-progress',
        updated_at: new Date().toISOString()
      };
      
      if (window.dataSdk) {
        const result = await window.dataSdk.update(updatedPatient);
        if (result.isOk) {
          showToast(`${imageType} sent to ${doctor} via IP 122.333.44.5`);
          document.getElementById('rad-patient-select').value = '';
          document.getElementById('rad-image-ref').value = '';
        } else {
          showToast('Failed to send image');
        }
      }
    }
    
    // Notification badge
    function updateNotificationBadge() {
      const urgentCount = allPatients.filter(p => p.priority === 'high' && p.status === 'pending').length;
      const badge = document.getElementById('notification-badge');
      
      if (urgentCount > 0) {
        badge.textContent = urgentCount;
        badge.classList.remove('hidden');
        badge.classList.add('flex');
      } else {
        badge.classList.add('hidden');
        badge.classList.remove('flex');
      }
    }
    
    // Utilities
    function formatDate(dateStr) {
      if (!dateStr) return '-';
      const date = new Date(dateStr);
      return date.toLocaleDateString('en-US', { 
        month: 'short', 
        day: 'numeric',
        hour: '2-digit',
        minute: '2-digit'
      });
    }
    
    function showToast(message) {
      const toast = document.getElementById('toast');
      document.getElementById('toast-message').textContent = message;
      toast.classList.remove('translate-y-20', 'opacity-0');
      toast.classList.add('translate-y-0', 'opacity-100');
      
      setTimeout(() => {
        toast.classList.add('translate-y-20', 'opacity-0');
        toast.classList.remove('translate-y-0', 'opacity-100');
      }, 3000);
    }
    
    // Initialize
    initApp();
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9f1dd4200490071c',t:'MTc3NzEyNTE1MS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
