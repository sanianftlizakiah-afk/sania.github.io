<!DOCTYPE html>
<html lang="id" class="light">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pendidikan Bahasa Arab - Premium LMS</title>
    
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Amiri:ital,wght@0,400;0,700;1,400&family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <!-- Tailwind CSS (Script Version for Config) -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <style>
        /* Custom Styles & Overrides */
        body { font-family: 'Poppins', sans-serif; }
        .font-arabic { font-family: 'Amiri', serif; direction: rtl; }
        
        /* Glassmorphism Classes */
        .glass { background: rgba(255, 255, 255, 0.7); backdrop-filter: blur(10px); -webkit-backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.3); }
        .dark .glass { background: rgba(31, 41, 55, 0.7); border: 1px solid rgba(255, 255, 255, 0.1); }
        
        /* Custom Scrollbar */
        ::-webkit-scrollbar { width: 6px; height: 6px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: #d946ef; border-radius: 10px; }
        ::-webkit-scrollbar-thumb:hover { background: #c026d3; }

        /* Loader Animation */
        .loader { border: 3px solid #f3f3f3; border-radius: 50%; border-top: 3px solid #d946ef; width: 24px; height: 24px; -webkit-animation: spin 1s linear infinite; animation: spin 1s linear infinite; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

        /* Hide elements dynamically */
        .hidden-app { display: none !important; }
        
        /* Smooth Transitions */
        .transition-all { transition-property: all; transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1); transition-duration: 300ms; }
    </style>

    <script>
        // Tailwind Configuration via Interval to ensure window.tailwind is ready
        let twInterval = setInterval(() => {
            if (window.tailwind) {
                clearInterval(twInterval);
                tailwind.config = {
                    darkMode: 'class',
                    theme: {
                        extend: {
                            colors: {
                                primary: '#d946ef',   // fuchsia-500
                                secondary: '#ec4899', // pink-500
                                accent: '#f472b6',    // pink-400
                                bgLight: '#fdf4ff',   // fuchsia-50
                                bgDark: '#111827',    // gray-900
                                cardDark: '#1f2937'   // gray-800
                            }
                        }
                    }
                };
            }
        }, 50);
    </script>
</head>
<body class="bg-bgLight dark:bg-bgDark text-gray-800 dark:text-gray-200 transition-colors duration-300 antialiased overflow-hidden">

    <!-- Toast Notification Container -->
    <div id="toast-container" class="fixed top-5 right-5 z-50 flex flex-col gap-2 pointer-events-none"></div>

    <!-- Full Screen Loader -->
    <div id="global-loader" class="fixed inset-0 bg-white/80 dark:bg-gray-900/80 backdrop-blur-sm z-[100] flex flex-col items-center justify-center transition-opacity duration-300">
        <div class="loader mb-4" style="width: 50px; height: 50px; border-width: 5px;"></div>
        <h2 class="text-xl font-semibold text-primary">Memuat Sistem...</h2>
        <p class="text-sm text-gray-500 dark:text-gray-400 mt-2" id="loader-text">Menghubungkan ke server</p>
    </div>

    <!-- ================= LOGIN SCREEN ================= -->
    <div id="login-screen" class="hidden-app h-screen w-full flex items-center justify-center bg-gradient-to-br from-fuchsia-100 to-pink-100 dark:from-gray-900 dark:to-gray-800 p-4">
        <div class="glass dark:bg-cardDark p-8 rounded-3xl shadow-2xl w-full max-w-md transform transition-all hover:scale-[1.01]">
            <div class="text-center mb-8">
                <div class="w-20 h-20 bg-gradient-to-tr from-primary to-secondary rounded-full flex items-center justify-center mx-auto mb-4 shadow-lg">
                    <i class="fas fa-book-quran text-white text-3xl"></i>
                </div>
                <h1 class="text-2xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-primary to-secondary">Pendidikan Bahasa Arab</h1>
                <p class="text-sm text-gray-500 dark:text-gray-400 mt-1">Sistem Manajemen Pembelajaran</p>
            </div>
            <form id="login-form" class="space-y-5">
                <div class="bg-blue-50 dark:bg-blue-900/20 p-3 rounded-xl border border-blue-100 dark:border-blue-800 mb-4 text-center">
                    <p class="text-xs text-blue-600 dark:text-blue-400 font-medium"><i class="fas fa-info-circle"></i> Gunakan Akun Admin (admin / admin123) atau Akun Guru & Siswa yang telah didaftarkan.</p>
                </div>
                <div>
                    <label class="block text-sm font-medium mb-1">Username / ID Pengguna</label>
                    <div class="relative">
                        <i class="fas fa-user absolute left-3 top-3 text-gray-400"></i>
                        <input type="text" id="login-username" required autocomplete="off" class="w-full pl-10 pr-4 py-2 border rounded-xl focus:ring-2 focus:ring-primary focus:border-primary outline-none dark:bg-gray-700 dark:border-gray-600">
                    </div>
                </div>
                <div>
                    <label class="block text-sm font-medium mb-1">Password Masuk</label>
                    <div class="relative">
                        <i class="fas fa-lock absolute left-3 top-3 text-gray-400"></i>
                        <input type="password" id="login-password" required autocomplete="off" class="w-full pl-10 pr-4 py-2 border rounded-xl focus:ring-2 focus:ring-primary focus:border-primary outline-none dark:bg-gray-700 dark:border-gray-600">
                    </div>
                </div>
                <button type="submit" class="w-full py-3 bg-gradient-to-r from-primary to-secondary hover:from-secondary hover:to-primary text-white rounded-xl font-semibold shadow-lg shadow-pink-500/30 transition-all flex justify-center items-center gap-2">
                    <span>Masuk Aplikasi</span>
                    <i class="fas fa-arrow-right"></i>
                </button>
            </form>
            <div id="login-error" class="mt-4 text-center text-red-500 text-sm hidden-app font-medium bg-red-50 dark:bg-red-900/20 p-2 rounded-xl"></div>
            
            <div class="mt-6 text-center text-xs text-gray-400">
                <p id="network-status" class="flex items-center justify-center gap-1">
                    <i class="fas fa-circle text-green-500 text-[8px]"></i> Cloud Database Connected
                </p>
            </div>
        </div>
    </div>

    <!-- ================= MAIN APP LAYOUT ================= -->
    <div id="app-screen" class="hidden-app h-screen w-full flex overflow-hidden">
        
        <!-- Sidebar -->
        <aside id="sidebar" class="w-64 bg-white dark:bg-cardDark border-r border-gray-200 dark:border-gray-700 flex flex-col transition-all duration-300 absolute md:relative z-40 h-full -translate-x-full md:translate-x-0">
            <!-- Logo Area -->
            <div class="h-16 flex items-center px-6 border-b border-gray-200 dark:border-gray-700 justify-between shrink-0">
                <div class="flex items-center gap-3 font-bold text-lg bg-clip-text text-transparent bg-gradient-to-r from-primary to-secondary">
                    <i class="fas fa-book-quran text-primary"></i> <span class="truncate">LMS Arab</span>
                </div>
                <button id="close-sidebar-mobile" class="md:hidden text-gray-500"><i class="fas fa-times"></i></button>
            </div>

            <!-- User Info -->
            <div class="p-4 border-b border-gray-200 dark:border-gray-700 flex items-center gap-3 shrink-0">
                <img id="user-avatar" src="" alt="Avatar" class="w-10 h-10 rounded-full border-2 border-primary">
                <div class="overflow-hidden">
                    <p id="user-name" class="text-sm font-semibold truncate">Nama Pengguna</p>
                    <p id="user-role-badge" class="text-[10px] uppercase font-bold bg-primary/10 text-primary px-2 py-0.5 rounded-full inline-block mt-0.5 tracking-wider">Role</p>
                </div>
            </div>

            <!-- Navigation -->
            <nav class="flex-1 overflow-y-auto p-4 space-y-1 custom-scrollbar" id="nav-menu">
                <!-- Injected via JS -->
            </nav>

            <!-- Bottom Actions -->
            <div class="p-4 border-t border-gray-200 dark:border-gray-700 shrink-0">
                <button onclick="logout()" class="flex items-center gap-3 w-full p-3 text-red-500 hover:bg-red-50 dark:hover:bg-red-900/20 rounded-xl transition-colors text-sm font-medium">
                    <i class="fas fa-sign-out-alt"></i> Keluar Akun
                </button>
            </div>
        </aside>

        <!-- Main Content Area -->
        <main class="flex-1 flex flex-col h-full relative">
            <!-- Mobile Overlay -->
            <div id="mobile-overlay" class="fixed inset-0 bg-black/50 z-30 hidden md:hidden"></div>

            <!-- Topbar -->
            <header class="h-16 glass dark:bg-cardDark/90 border-b border-gray-200 dark:border-gray-700 flex items-center justify-between px-4 lg:px-8 z-20 shrink-0">
                <div class="flex items-center gap-4">
                    <button id="open-sidebar" class="md:hidden text-gray-600 dark:text-gray-300 hover:text-primary"><i class="fas fa-bars text-xl"></i></button>
                    <h2 id="page-title" class="text-xl font-semibold hidden sm:block">Dashboard</h2>
                </div>
                
                <div class="flex items-center gap-4">
                    <div id="status-indicator" class="hidden sm:flex items-center gap-2 px-3 py-1 rounded-full bg-green-100 dark:bg-green-900/30 text-green-600 text-xs font-medium">
                        <span class="relative flex h-2 w-2"><span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-green-400 opacity-75"></span><span class="relative inline-flex rounded-full h-2 w-2 bg-green-500"></span></span>
                        Realtime Sinkron
                    </div>
                    
                    <button id="theme-toggle" class="w-10 h-10 rounded-full bg-gray-100 dark:bg-gray-700 flex items-center justify-center text-gray-600 dark:text-gray-300 hover:text-primary transition-colors">
                        <i class="fas fa-moon" id="theme-icon"></i>
                    </button>
                </div>
            </header>

            <!-- Dynamic View Container -->
            <div id="content-area" class="flex-1 overflow-y-auto p-4 lg:p-8 bg-gray-50 dark:bg-bgDark custom-scrollbar relative">
                <!-- Content injected here -->
            </div>
        </main>
    </div>

    <!-- ================= MODALS & TEMPLATES ================= -->
    
    <!-- Confirm Dialog -->
    <div id="confirm-dialog" class="fixed inset-0 bg-black/60 z-[60] flex items-center justify-center hidden-app backdrop-blur-sm opacity-0 transition-opacity">
        <div class="bg-white dark:bg-cardDark p-6 rounded-2xl shadow-xl w-full max-w-sm transform scale-95 transition-transform" id="confirm-box">
            <h3 class="text-lg font-semibold mb-2" id="confirm-title">Konfirmasi Tindakan</h3>
            <p class="text-sm text-gray-600 dark:text-gray-400 mb-6" id="confirm-msg">Apakah Anda yakin?</p>
            <div class="flex justify-end gap-3">
                <button id="confirm-cancel" class="px-4 py-2 rounded-lg bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 text-sm font-medium transition-colors">Batal</button>
                <button id="confirm-ok" class="px-4 py-2 rounded-lg bg-red-500 hover:bg-red-600 text-white text-sm font-medium transition-colors">Ya, Lanjutkan</button>
            </div>
        </div>
    </div>

    <!-- Generic Form Modal Container -->
    <div id="form-modal" class="fixed inset-0 bg-black/60 z-[50] flex items-center justify-center hidden-app backdrop-blur-sm">
        <div class="bg-white dark:bg-cardDark rounded-2xl shadow-2xl w-full max-w-xl max-h-[90vh] flex flex-col overflow-hidden transform transition-all slide-down">
            <div class="flex justify-between items-center p-5 border-b border-gray-100 dark:border-gray-700 bg-gradient-to-r from-primary/10 to-transparent shrink-0">
                <h3 class="font-bold text-lg text-primary" id="modal-title">Form</h3>
                <button onclick="closeModal()" class="text-gray-400 hover:text-red-500 transition-colors"><i class="fas fa-times text-xl"></i></button>
            </div>
            <div class="p-5 overflow-y-auto custom-scrollbar" id="modal-content">
                <!-- Form fields injected here -->
            </div>
        </div>
    </div>

    <!-- AI Tutor Floating Button & Chatbox -->
    <button onclick="toggleAITutor()" class="fixed bottom-6 left-6 z-[45] w-14 h-14 bg-gradient-to-tr from-purple-600 to-indigo-500 text-white rounded-full shadow-[0_10px_25px_rgba(124,58,237,0.5)] flex items-center justify-center hover:scale-110 transition-transform hover:rotate-12 group">
        <i class="fas fa-robot text-2xl group-hover:animate-pulse"></i>
    </button>
    <div id="ai-tutor-modal" class="fixed bottom-24 left-6 z-[45] w-80 bg-white dark:bg-cardDark rounded-3xl shadow-2xl border border-purple-100 dark:border-purple-800/50 flex flex-col hidden-app transition-all overflow-hidden h-[450px]">
        <div class="bg-gradient-to-r from-purple-600 to-indigo-500 p-4 text-white flex justify-between items-center shrink-0">
            <div class="flex items-center gap-3">
                <div class="w-8 h-8 bg-white/20 rounded-full flex items-center justify-center"><i class="fas fa-magic"></i></div>
                <div>
                    <h4 class="font-bold text-sm">Ustadz AI</h4>
                    <p class="text-[10px] text-purple-100">Asisten Pintar Bahasa Arab</p>
                </div>
            </div>
            <button onclick="toggleAITutor()" class="text-white hover:text-purple-200"><i class="fas fa-times"></i></button>
        </div>
        <div id="ai-chat-box" class="flex-1 overflow-y-auto p-4 space-y-3 bg-gray-50 dark:bg-gray-900 custom-scrollbar text-sm">
            <div class="flex items-start gap-2 max-w-[90%]">
                <div class="w-6 h-6 rounded-full bg-purple-500 text-white flex items-center justify-center shrink-0 text-xs"><i class="fas fa-robot"></i></div>
                <div class="p-2.5 rounded-xl bg-white dark:bg-gray-800 border border-gray-100 dark:border-gray-700 shadow-sm text-gray-700 dark:text-gray-300">Ahlan wa Sahlan! Saya Asisten AI yang bisa membantu Anda menerjemahkan kalimat, menjelaskan Nahwu/Sharaf, atau membuat contoh paragraf bahasa Arab. Ada yang bisa saya bantu?</div>
            </div>
        </div>
        <form onsubmit="sendAITutor(event)" class="p-3 bg-white dark:bg-cardDark border-t border-gray-100 dark:border-gray-700 flex gap-2 shrink-0">
            <input type="text" id="ai-chat-input" placeholder="Tanya tentang bahasa Arab..." class="flex-1 bg-gray-100 dark:bg-gray-800 dark:text-white px-4 py-2 rounded-xl text-sm outline-none focus:ring-1 focus:ring-purple-500">
            <button type="submit" class="w-10 h-10 bg-purple-500 hover:bg-purple-600 text-white rounded-xl shadow transition-colors flex items-center justify-center shrink-0"><i class="fas fa-paper-plane"></i></button>
        </form>
    </div>

    <!-- Virtual Arabic Keyboard Overlay -->
    <div id="arabic-keyboard" class="fixed bottom-0 left-0 right-0 bg-white dark:bg-gray-800 border-t border-gray-200 dark:border-gray-700 p-2 shadow-[0_-10px_40px_rgba(0,0,0,0.1)] z-[45] hidden-app transform translate-y-full transition-transform duration-300">
        <div class="max-w-3xl mx-auto flex flex-col gap-1">
            <div class="flex justify-between items-center mb-1 px-2">
                <span class="text-xs font-semibold text-primary">Virtual Keyboard - Maharah Kitabah</span>
                <button onclick="toggleKeyboard()" class="text-gray-500 hover:text-red-500"><i class="fas fa-chevron-down"></i></button>
            </div>
            <!-- Rows of Keyboard -->
            <div class="flex justify-center gap-1">
                <button class="kbd-btn" onclick="insertChar('ض')">ض</button><button class="kbd-btn" onclick="insertChar('ص')">ص</button><button class="kbd-btn" onclick="insertChar('ث')">ث</button><button class="kbd-btn" onclick="insertChar('ق')">ق</button><button class="kbd-btn" onclick="insertChar('ف')">ف</button><button class="kbd-btn" onclick="insertChar('غ')">غ</button><button class="kbd-btn" onclick="insertChar('ع')">ع</button><button class="kbd-btn" onclick="insertChar('ه')">ه</button><button class="kbd-btn" onclick="insertChar('خ')">خ</button><button class="kbd-btn" onclick="insertChar('ح')">ح</button><button class="kbd-btn" onclick="insertChar('ج')">ج</button><button class="kbd-btn" onclick="insertChar('د')">د</button>
            </div>
            <div class="flex justify-center gap-1">
                <button class="kbd-btn" onclick="insertChar('ش')">ش</button><button class="kbd-btn" onclick="insertChar('س')">س</button><button class="kbd-btn" onclick="insertChar('ي')">ي</button><button class="kbd-btn" onclick="insertChar('ب')">ب</button><button class="kbd-btn" onclick="insertChar('ل')">ل</button><button class="kbd-btn" onclick="insertChar('ا')">ا</button><button class="kbd-btn" onclick="insertChar('ت')">ت</button><button class="kbd-btn" onclick="insertChar('ن')">ن</button><button class="kbd-btn" onclick="insertChar('م')">م</button><button class="kbd-btn" onclick="insertChar('ك')">ك</button><button class="kbd-btn" onclick="insertChar('ط')">ط</button>
            </div>
            <div class="flex justify-center gap-1 mt-1">
                <button class="kbd-btn text-blue-500 font-bold" onclick="insertChar('َ')">Fathah</button><button class="kbd-btn text-blue-500 font-bold" onclick="insertChar('ِ')">Kasrah</button><button class="kbd-btn text-blue-500 font-bold" onclick="insertChar('ُ')">Dhammah</button><button class="kbd-btn" onclick="insertChar('ئ')">ئ</button><button class="kbd-btn" onclick="insertChar('ء')">ء</button><button class="kbd-btn" onclick="insertChar('ؤ')">ؤ</button><button class="kbd-btn" onclick="insertChar('ر')">ر</button><button class="kbd-btn" onclick="insertChar('لا')">لا</button><button class="kbd-btn" onclick="insertChar('ى')">ى</button><button class="kbd-btn" onclick="insertChar('ة')">ة</button><button class="kbd-btn" onclick="insertChar('و')">و</button><button class="kbd-btn" onclick="insertChar('ز')">ز</button><button class="kbd-btn" onclick="insertChar('ظ')">ظ</button>
            </div>
            <div class="flex justify-center gap-1 mt-1">
                <button class="kbd-btn flex-grow max-w-[200px]" onclick="insertChar(' ')">Spasi</button>
            </div>
        </div>
        <style>
            .kbd-btn { padding: 8px; background: #f3f4f6; border-radius: 6px; font-family: 'Amiri', serif; font-size: 1.1rem; border: 1px solid #e5e7eb; transition: all 0.2s; cursor: pointer;}
            .dark .kbd-btn { background: #374151; border-color: #4b5563; color: white; }
            .kbd-btn:hover { background: #d946ef; color: white; border-color: #d946ef; }
            
            /* Chat message animation */
            @keyframes msgPop { 0% { transform: scale(0.95) translateY(10px); opacity: 0; } 100% { transform: scale(1) translateY(0); opacity: 1; } }
            .msg-animate { animation: msgPop 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards; }
        </style>
    </div>

    <!-- Firebase SDKs -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, collection, doc, setDoc, getDocs, onSnapshot, addDoc, updateDoc, deleteDoc, query, where } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // ============================================================================
        // GLOBAL STATE & UTILITIES
        // ============================================================================
        const AppState = {
            user: null, 
            isOffline: !navigator.onLine,
            data: {
                users: [], classes: [], subjects: [], materials: [], 
                attendance: [], assignments: [], announcements: [], schedules: [],
                messages: [], grades: [] // Data Chat & Nilai ditambahkan
            },
            unsubscribes: [],
            activeTargetInput: null,
            scheduleMode: 'my', // 'my' atau 'all'
            activeChat: 'group', // default chat target ('group' atau userId)
            currentParam: null, // Parameter navigasi submenu
            history: [] // Untuk back button
        };

        const Subjects = ["Maharah Istima'", "Maharah Kalam", "Maharah Qira'ah", "Maharah Kitabah", "Mufradat", "Tarkib"];
        const Days = ["Senin", "Selasa", "Rabu", "Kamis", "Jumat", "Sabtu"];

        const D = (id) => document.getElementById(id);
        const hide = (id) => { if(D(id)) D(id).classList.add('hidden-app'); };
        const show = (id) => { if(D(id)) D(id).classList.remove('hidden-app'); };
        
        window.escapeHTML = (str) => {
            if (!str) return '';
            return String(str).replace(/[&<>'"]/g, tag => ({
                '&': '&amp;', '<': '&lt;', '>': '&gt;', "'": '&#39;', '"': '&quot;'
            }[tag]));
        };

        window.showToast = (message, type = 'info') => {
            const container = D('toast-container');
            const id = 'toast-' + Date.now();
            const colors = { success: 'bg-green-500', error: 'bg-red-500', info: 'bg-blue-500', warning: 'bg-yellow-500' };
            const icons = { success: 'fa-check-circle', error: 'fa-exclamation-circle', info: 'fa-info-circle', warning: 'fa-exclamation-triangle' };
            
            const el = document.createElement('div');
            el.id = id;
            el.className = `flex items-center p-4 mb-2 text-white rounded-xl shadow-lg transform transition-all duration-300 translate-x-full opacity-0 ${colors[type]} glass border-none z-[100]`;
            el.innerHTML = `<i class="fas ${icons[type]} mr-3 text-lg"></i> <span class="text-sm font-medium">${escapeHTML(message)}</span>`;
            container.appendChild(el);
            
            setTimeout(() => { el.classList.remove('translate-x-full', 'opacity-0'); }, 10);
            setTimeout(() => {
                el.classList.add('translate-x-full', 'opacity-0');
                setTimeout(() => el.remove(), 300);
            }, 3000);
        };

        window.setLoading = (isLoading, text = 'Memuat...') => {
            if(isLoading) { D('loader-text').innerText = text; show('global-loader'); } 
            else { hide('global-loader'); }
        };

        const updateNetworkStatus = () => {
            AppState.isOffline = !navigator.onLine;
            const ind = D('status-indicator');
            if (AppState.isOffline) {
                if(ind) ind.innerHTML = `<i class="fas fa-wifi-slash"></i> Offline Mode`;
                if(ind) ind.className = 'hidden sm:flex items-center gap-2 px-3 py-1 rounded-full bg-red-100 text-red-600 text-xs font-medium';
                showToast("Koneksi terputus. Beralih ke Mode Offline.", "warning");
            } else {
                if(ind) ind.innerHTML = `<span class="relative flex h-2 w-2"><span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-green-400 opacity-75"></span><span class="relative inline-flex rounded-full h-2 w-2 bg-green-500"></span></span> Realtime Aktif`;
                if(ind) ind.className = 'hidden sm:flex items-center gap-2 px-3 py-1 rounded-full bg-green-100 text-green-600 text-xs font-medium';
            }
        };
        window.addEventListener('online', updateNetworkStatus);
        window.addEventListener('offline', updateNetworkStatus);

        window.confirmAction = (message, onConfirm) => {
            D('confirm-msg').innerText = message;
            show('confirm-dialog');
            setTimeout(() => { D('confirm-dialog').classList.remove('opacity-0'); D('confirm-box').classList.remove('scale-95'); }, 10);
            
            const cancelBtn = D('confirm-cancel');
            const okBtn = D('confirm-ok');
            
            const cleanup = () => {
                D('confirm-dialog').classList.add('opacity-0'); D('confirm-box').classList.add('scale-95');
                setTimeout(() => hide('confirm-dialog'), 300);
                cancelBtn.onclick = null; okBtn.onclick = null;
            };
            cancelBtn.onclick = cleanup;
            okBtn.onclick = () => { cleanup(); onConfirm(); };
        };

        const setupTheme = () => {
            const isDark = localStorage.getItem('theme') === 'dark' || (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches);
            if (isDark) document.documentElement.classList.add('dark');
            D('theme-icon').className = isDark ? 'fas fa-sun' : 'fas fa-moon';

            D('theme-toggle').addEventListener('click', () => {
                document.documentElement.classList.toggle('dark');
                const darkNow = document.documentElement.classList.contains('dark');
                localStorage.setItem('theme', darkNow ? 'dark' : 'light');
                D('theme-icon').className = darkNow ? 'fas fa-sun' : 'fas fa-moon';
            });
        };

        D('open-sidebar').addEventListener('click', () => { D('sidebar').classList.remove('-translate-x-full'); show('mobile-overlay'); });
        D('close-sidebar-mobile').addEventListener('click', () => { D('sidebar').classList.add('-translate-x-full'); hide('mobile-overlay'); });
        D('mobile-overlay').addEventListener('click', () => { D('sidebar').classList.add('-translate-x-full'); hide('mobile-overlay'); });

        // ============================================================================
        // FIREBASE INITIALIZATION & DB HELPERS
        // ============================================================================
        let app, auth, db, appId;

        const initFirebase = async () => {
            try {
                const configStr = typeof __firebase_config !== 'undefined' ? __firebase_config : '{}';
                const firebaseConfig = JSON.parse(configStr);
                if (!firebaseConfig.projectId) throw new Error("Firebase config not found.");
                
                appId = typeof __app_id !== 'undefined' ? __app_id : 'lms-arab-default';
                app = initializeApp(firebaseConfig);
                auth = getAuth(app);
                db = getFirestore(app);
                return true;
            } catch (error) {
                console.error("Firebase Init Error:", error);
                AppState.isOffline = true;
                updateNetworkStatus();
                return false;
            }
        };

        const dbHelper = {
            getColRef: (colName) => collection(db, 'artifacts', appId, 'public', 'data', colName),
            getDocRef: (colName, docId) => doc(db, 'artifacts', appId, 'public', 'data', colName, docId)
        };

        // ============================================================================
        // AUTHENTICATION & INITIALIZATION
        // ============================================================================
        window.logout = async () => {
            confirmAction("Anda yakin ingin keluar dari sistem?", async () => {
                setLoading(true, "Mengeluarkan akun...");
                AppState.unsubscribes.forEach(unsub => unsub());
                AppState.unsubscribes = [];
                AppState.user = null;
                AppState.history = [];
                localStorage.removeItem('lms_session');
                D('login-username').value = '';
                D('login-password').value = '';
                hide('app-screen');
                show('login-screen');
                setLoading(false);
            });
        };

        const initApp = async () => {
            setupTheme();
            updateNetworkStatus();
            
            const isFbReady = await initFirebase();
            
            if (isFbReady && !AppState.isOffline) {
                setLoading(true, 'Menyiapkan Jalur Keamanan...');
                try {
                    if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                        try { await signInWithCustomToken(auth, __initial_auth_token); } 
                        catch(e) { await signInAnonymously(auth); }
                    } else {
                        await signInAnonymously(auth);
                    }
                    
                    onAuthStateChanged(auth, async (firebaseUser) => {
                        if (firebaseUser) {
                            const localSession = JSON.parse(localStorage.getItem('lms_session'));
                            if (localSession) {
                                AppState.user = localSession;
                                finishLoginSetup();
                            } else {
                                hide('app-screen'); show('login-screen'); setLoading(false);
                            }
                        } else {
                            hide('app-screen'); show('login-screen'); setLoading(false);
                        }
                    });
                } catch (e) {
                    AppState.isOffline = true; updateNetworkStatus();
                    checkLocalSession();
                }
            } else {
                checkLocalSession();
            }
        };

        const checkLocalSession = () => {
            const localSession = JSON.parse(localStorage.getItem('lms_session'));
            if (localSession) { AppState.user = localSession; finishLoginSetup(); } 
            else { hide('app-screen'); show('login-screen'); setLoading(false); }
        };

        D('login-form').addEventListener('submit', async (e) => {
            e.preventDefault();
            const u = D('login-username').value.trim();
            const p = D('login-password').value.trim();
            const err = D('login-error');
            hide(err.id);
            setLoading(true, 'Memeriksa Kredensial Pengguna...');

            if (u === 'admin' && p === 'admin123') {
                AppState.user = { uid: 'admin_sys_id', username: 'admin', role: 'admin', name: 'Administrator Pusat' };
                processSuccessfulLogin();
                return;
            }

            if (AppState.isOffline) {
                err.innerText = "Mode Offline Aktif: Hanya Admin Utama yang dapat login tanpa koneksi internet."; show(err.id);
                setLoading(false); return;
            }

            try {
                const usersRef = dbHelper.getColRef('users');
                const querySnapshot = await getDocs(usersRef); 
                
                let found = false;
                querySnapshot.forEach((doc) => {
                    const userData = doc.data();
                    if (userData.username === u && userData.password === p) {
                        AppState.user = { uid: doc.id, ...userData };
                        found = true;
                    }
                });

                if (found) { 
                    processSuccessfulLogin(); 
                } else { 
                    err.innerHTML = `<i class="fas fa-exclamation-triangle"></i> Username atau Password tidak cocok dengan database.`; 
                    show(err.id); 
                    setLoading(false); 
                }
            } catch (error) {
                console.error("Login Error:", error);
                err.innerText = "Terjadi kendala jaringan saat memverifikasi akun ke Server Database."; show(err.id); setLoading(false);
            }
        });

        const processSuccessfulLogin = () => {
            localStorage.setItem('lms_session', JSON.stringify(AppState.user));
            finishLoginSetup();
        };

        const finishLoginSetup = () => {
            hide('login-screen');
            show('app-screen');
            D('user-name').innerText = escapeHTML(AppState.user.name);
            D('user-role-badge').innerText = AppState.user.role;
            
            let bg = AppState.user.role === 'admin' ? 'd946ef' : (AppState.user.role === 'guru' ? 'ec4899' : '3b82f6');
            D('user-avatar').src = `https://ui-avatars.com/api/?name=${encodeURIComponent(AppState.user.name)}&background=${bg}&color=fff&bold=true`;

            // Reset view state
            AppState.scheduleMode = AppState.user.role === 'admin' ? 'all' : 'my';
            AppState.history = [];

            buildNavigation();
            
            if (!AppState.isOffline) setupRealtimeSync();
            else loadLocalData();

            renderView('dashboard');
            setLoading(false);
        };

        // ============================================================================
        // REALTIME SYNC & OPTIMISTIC DATA
        // ============================================================================
        const setupRealtimeSync = () => {
            AppState.unsubscribes.forEach(unsub => unsub());
            AppState.unsubscribes = [];

            // Sinkronisasi data utama termasuk Grades
            const collectionsToSync = ['users', 'classes', 'materials', 'attendance', 'announcements', 'schedules', 'assignments', 'messages', 'grades'];
            
            collectionsToSync.forEach(colName => {
                const colRef = dbHelper.getColRef(colName);
                const unsub = onSnapshot(colRef, 
                    (snapshot) => {
                        const dataArray = [];
                        snapshot.forEach(doc => dataArray.push({ id: doc.id, ...doc.data() }));
                        AppState.data[colName] = dataArray;
                        localStorage.setItem(`offline_data_${colName}`, JSON.stringify(dataArray));
                        
                        if (AppState.currentView) renderView(AppState.currentView, true, AppState.currentParam);
                    },
                    (error) => { console.error(`Sync error on ${colName}:`, error); }
                );
                AppState.unsubscribes.push(unsub);
            });
        };

        const loadLocalData = () => {
            ['users', 'classes', 'materials', 'attendance', 'announcements', 'schedules', 'assignments', 'messages', 'grades'].forEach(colName => {
                const stored = localStorage.getItem(`offline_data_${colName}`);
                AppState.data[colName] = stored ? JSON.parse(stored) : [];
            });
        };

        // ============================================================================
        // ROUTING & RENDERING
        // ============================================================================
        const buildNavigation = () => {
            const menu = D('nav-menu');
            menu.innerHTML = '';
            const role = AppState.user.role;

            const items = [
                { id: 'dashboard', icon: 'fa-chart-pie', text: 'Dashboard', roles: ['admin', 'guru', 'siswa'] },
                { id: 'users', icon: 'fa-users', text: 'Data Pengguna', roles: ['admin'] },
                { id: 'classes', icon: 'fa-building', text: 'Manajemen Kelas', roles: ['admin'] },
                { id: 'schedules', icon: 'fa-calendar-alt', text: 'Jadwal Pelajaran', roles: ['admin', 'guru', 'siswa'] },
                { id: 'myclasses', icon: 'fa-chalkboard-user', text: 'Ruang Kelas & Anggota', roles: ['guru', 'siswa'] },
                { id: 'materials', icon: 'fa-book-open', text: 'Materi Belajar', roles: ['guru', 'siswa'] },
                { id: 'assignments', icon: 'fa-tasks', text: 'Tugas & Evaluasi', roles: ['guru', 'siswa'] },
                { id: 'grades_view', icon: 'fa-star', text: 'Manajemen Nilai', roles: ['guru', 'siswa'] },
                { id: 'attendance', icon: 'fa-clipboard-user', text: 'Absensi Realtime', roles: ['guru', 'siswa'] },
                { id: 'chat', icon: 'fa-comments', text: 'Pesan & Diskusi', roles: ['admin', 'guru', 'siswa'] }
            ];

            items.forEach(item => {
                if (item.roles.includes(role)) {
                    const a = document.createElement('a');
                    a.href = '#';
                    a.className = 'nav-item flex items-center gap-3 p-3 rounded-xl text-sm font-medium text-gray-600 dark:text-gray-400 hover:bg-primary/10 hover:text-primary transition-colors';
                    a.innerHTML = `<div class="w-6 text-center"><i class="fas ${item.icon}"></i></div> <span>${item.text}</span>`;
                    a.onclick = (e) => {
                        e.preventDefault();
                        document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('bg-gradient-to-r', 'from-primary', 'to-secondary', 'text-white', 'shadow-md'));
                        a.classList.add('bg-gradient-to-r', 'from-primary', 'to-secondary', 'text-white', 'shadow-md');
                        a.classList.remove('text-gray-600', 'dark:text-gray-400', 'hover:bg-primary/10', 'hover:text-primary');
                        renderView(item.id);
                        if(window.innerWidth < 768) D('close-sidebar-mobile').click();
                    };
                    menu.appendChild(a);
                    if(item.id === 'dashboard') a.click(); 
                }
            });
        };

        // Fungsi Global Navigasi (Back Button)
        window.goBack = () => {
            if (AppState.history.length > 1) {
                AppState.history.pop(); // buang state saat ini
                const prev = AppState.history[AppState.history.length - 1]; // intip yang sebelumnya
                // Panggil render tanpa menyimpan ke history lagi
                executeRender(prev.viewId, false, prev.param, true); 
            } else {
                renderView('dashboard');
            }
        };

        window.renderView = (viewId, isUpdate = false, param = null) => {
            executeRender(viewId, isUpdate, param, false);
        };

        const executeRender = (viewId, isUpdate = false, param = null, isBackAction = false) => {
            AppState.currentView = viewId;
            AppState.currentParam = param;
            
            // Simpan history untuk navigasi "Kembali" jika bukan update atau aksi back
            if (!isUpdate && !isBackAction) {
                // Hindari duplikasi beruntun
                if (AppState.history.length === 0 || AppState.history[AppState.history.length - 1].viewId !== viewId || AppState.history[AppState.history.length - 1].param !== param) {
                    AppState.history.push({ viewId, param });
                }
            }

            const content = D('content-area');
            const titles = {
                'dashboard': 'Dashboard Utama', 'users': 'Manajemen Guru & Siswa', 'classes': 'Manajemen Kelas',
                'schedules': 'Jadwal Pelajaran', 'myclasses': 'Ruang Kelas', 'classDetail': 'Detail Kelas', 'materials': 'Materi Pembelajaran', 
                'attendance': 'Sistem Absensi', 'assignments': 'Tugas & Evaluasi', 'chat': 'Pesan & Diskusi Interaktif', 'grades_view': 'Manajemen Nilai'
            };
            D('page-title').innerText = titles[viewId] || 'LMS System';
            
            if(!isUpdate) {
                content.innerHTML = `
                    <div class="animate-pulse space-y-4 h-full">
                        <div class="h-8 bg-gray-200 dark:bg-gray-700 rounded w-1/4 mb-6"></div>
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                            <div class="h-32 bg-gray-200 dark:bg-gray-700 rounded-2xl"></div>
                            <div class="h-32 bg-gray-200 dark:bg-gray-700 rounded-2xl"></div>
                            <div class="h-32 bg-gray-200 dark:bg-gray-700 rounded-2xl"></div>
                        </div>
                    </div>
                `;
            }

            setTimeout(() => {
                // Wrapper Header Navigasi Umum (Jika bukan dashboard)
                let headerHTML = '';
                if (viewId !== 'dashboard' && AppState.history.length > 1) {
                    headerHTML = `
                        <div class="mb-4">
                            <button onclick="goBack()" class="text-sm font-medium text-gray-500 hover:text-primary transition-colors flex items-center gap-2 bg-gray-100 hover:bg-gray-200 dark:bg-gray-800 dark:hover:bg-gray-700 px-3 py-1.5 rounded-lg w-max">
                                <i class="fas fa-arrow-left"></i> Kembali Sebelumnya
                            </button>
                        </div>
                    `;
                }

                // Temporary container untuk dirender
                const tempDiv = document.createElement('div');

                switch(viewId) {
                    case 'dashboard': renderDashboard(tempDiv); break;
                    case 'users': renderUsers(tempDiv); break;
                    case 'classes': renderClassesAdmin(tempDiv); break;
                    case 'schedules': renderSchedules(tempDiv); break;
                    case 'myclasses': renderMyClasses(tempDiv); break;
                    case 'classDetail': renderClassDetail(tempDiv, param); break;
                    case 'materials': renderMaterials(tempDiv); break;
                    case 'attendance': renderAttendance(tempDiv); break;
                    case 'assignments': renderAssignments(tempDiv); break;
                    case 'chat': renderChat(tempDiv); break;
                    case 'grades_view': renderGrades(tempDiv); break;
                    default: tempDiv.innerHTML = '<p class="text-gray-500">Modul sedang dalam pengembangan.</p>';
                }

                content.innerHTML = headerHTML + tempDiv.innerHTML;

                // Special handling for chat scroll after render
                if (viewId === 'chat') {
                    const chatBox = D('chat-messages-box');
                    if(chatBox) chatBox.scrollTop = chatBox.scrollHeight;
                }

            }, isUpdate ? 0 : 50);
        };

        // --- FILTER HELPERS ---
        const getMyClasses = () => {
            const role = AppState.user.role;
            const uid = AppState.user.uid;
            if(role === 'admin') return AppState.data.classes;
            if(role === 'guru') return AppState.data.classes.filter(c => c.teacherId === uid);
            if(role === 'siswa') return AppState.data.classes.filter(c => (c.students || []).includes(uid));
            return [];
        };

        // ============================================================================
        // VIEWS IMPLEMENTATION
        // ============================================================================

        // --- DASHBOARD ---
        const renderDashboard = (container) => {
            const role = AppState.user.role;
            const u = AppState.data.users || [];
            const c = AppState.data.classes || [];
            const myClasses = getMyClasses();
            
            let html = `
                <div class="glass dark:bg-cardDark rounded-2xl p-6 mb-6 relative overflow-hidden shadow-sm border border-primary/10">
                    <div class="absolute right-0 top-0 w-64 h-64 bg-gradient-to-bl from-primary/20 to-transparent rounded-full -translate-y-1/2 translate-x-1/4 pointer-events-none"></div>
                    <h2 class="text-2xl font-bold mb-2">Ahlan wa Sahlan, ${escapeHTML(AppState.user.name)}! 👋</h2>
                    <p class="text-gray-600 dark:text-gray-400">Selamat datang di Sistem Manajemen Pembelajaran Bahasa Arab.</p>
                </div>
            `;

            if (role === 'admin') {
                html += `
                    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4 mb-6">
                        ${createStatCard('Total Guru', u.filter(x => x.role === 'guru').length, 'fa-chalkboard-user', 'bg-blue-500', 'users')}
                        ${createStatCard('Total Siswa', u.filter(x => x.role === 'siswa').length, 'fa-user-graduate', 'bg-green-500', 'users')}
                        ${createStatCard('Total Kelas', c.length, 'fa-building', 'bg-purple-500', 'classes')}
                        ${createStatCard('Total Materi', AppState.data.materials.length, 'fa-book-open', 'bg-pink-500', 'materials')}
                    </div>
                `;
            } else if (role === 'guru') {
                 html += `
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                        ${createStatCard('Kelas Diampu', myClasses.length, 'fa-building', 'bg-purple-500', 'myclasses')}
                        ${createStatCard('Sesi Absensi Aktif', AppState.data.attendance?.filter(x => x.status === 'active' && x.createdBy === AppState.user.uid)?.length || 0, 'fa-clock', 'bg-yellow-500', 'attendance')}
                        ${createStatCard('Tugas Diberikan', AppState.data.assignments?.filter(x => x.authorId === AppState.user.uid)?.length || 0, 'fa-tasks', 'bg-green-500', 'assignments')}
                    </div>
                `;
            } else if (role === 'siswa') {
                html += `
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                        ${createStatCard('Kelas Diikuti', myClasses.length, 'fa-chalkboard-user', 'bg-blue-500', 'myclasses')}
                        ${createStatCard('Materi Tersedia', AppState.data.materials?.filter(m => myClasses.some(c=>c.id===m.classId)).length || 0, 'fa-book-open', 'bg-pink-500', 'materials')}
                        ${createStatCard('Tugas Aktif', AppState.data.assignments?.filter(a => myClasses.some(c=>c.id===a.classId)).length || 0, 'fa-pencil-alt', 'bg-orange-500', 'assignments')}
                    </div>
                `;
            }
            container.innerHTML = html;
        };

        const createStatCard = (title, value, icon, colorClass, targetView) => `
            <div onclick="${targetView ? `renderView('${targetView}')` : ''}" class="glass dark:bg-cardDark rounded-2xl p-5 flex items-center gap-4 shadow-sm transition-transform hover:-translate-y-1 duration-300 ${targetView ? 'cursor-pointer hover:shadow-md hover:border-primary/50 border border-transparent' : ''}">
                <div class="w-12 h-12 rounded-xl ${colorClass} text-white flex items-center justify-center text-xl shadow-lg shrink-0">
                    <i class="fas ${icon}"></i>
                </div>
                <div class="overflow-hidden">
                    <p class="text-sm text-gray-500 dark:text-gray-400 font-medium truncate">${title}</p>
                    <h3 class="text-2xl font-bold">${value}</h3>
                </div>
            </div>
        `;

        // --- MANAJEMEN PENGGUNA (Admin) ---
        const renderUsers = (container) => {
            const users = AppState.data.users || [];
            const gurus = users.filter(u => u.role === 'guru');
            const siswas = users.filter(u => u.role === 'siswa');

            let html = `
                <div class="flex justify-between items-center mb-6 flex-wrap gap-4">
                    <h2 class="text-xl font-bold">Data Guru & Siswa</h2>
                    <div class="flex gap-2">
                        <!-- Import CSV Tool -->
                        <button onclick="downloadCSVTemplate()" class="px-4 py-2 bg-gray-100 hover:bg-gray-200 dark:bg-gray-700 dark:hover:bg-gray-600 text-gray-700 dark:text-gray-200 rounded-xl shadow-sm text-sm font-medium transition-colors flex items-center gap-2">
                            <i class="fas fa-file-download"></i> Template CSV
                        </button>
                        <button onclick="D('csv-upload').click()" class="px-4 py-2 bg-blue-500 hover:bg-blue-600 text-white rounded-xl shadow-md text-sm font-medium transition-colors flex items-center gap-2">
                            <i class="fas fa-file-excel"></i> Import CSV
                        </button>
                        <input type="file" id="csv-upload" class="hidden" accept=".csv" onchange="handleCSVImport(event)">

                        <button onclick="openModal('Tambah Pengguna Baru', userFormHTML(), saveUser)" class="px-5 py-2 bg-gradient-to-r from-primary to-secondary text-white rounded-xl shadow-lg text-sm font-medium hover:scale-105 transition-transform flex items-center gap-2 ml-2">
                            <i class="fas fa-user-plus"></i> Tambah Manual
                        </button>
                    </div>
                </div>
            `;

            // Helper Tabel
            const renderTable = (list, title, icon, colorBase) => `
                <div class="mb-8 glass dark:bg-cardDark rounded-2xl overflow-hidden shadow-sm border border-gray-100 dark:border-gray-700">
                    <div class="px-5 py-4 border-b border-gray-100 dark:border-gray-700 bg-${colorBase}-50 dark:bg-${colorBase}-900/20 flex items-center gap-3">
                        <div class="w-8 h-8 rounded-full bg-${colorBase}-500 text-white flex items-center justify-center shadow"><i class="fas ${icon}"></i></div>
                        <h3 class="font-bold text-lg text-gray-800 dark:text-gray-100">${title} <span class="text-sm font-medium text-gray-500">(${list.length} Orang)</span></h3>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-sm whitespace-nowrap">
                            <thead class="bg-gray-50/50 dark:bg-gray-800/50 text-gray-500 dark:text-gray-400 font-medium border-b border-gray-100 dark:border-gray-700">
                                <tr>
                                    <th class="p-4">Nama Lengkap</th>
                                    <th class="p-4">Username Login</th>
                                    <th class="p-4">Sandi Akses Masuk</th>
                                    <th class="p-4 text-center">Tindakan</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-gray-100 dark:divide-gray-700">
                                ${list.map(u => `
                                    <tr class="hover:bg-gray-50 dark:hover:bg-gray-700/30 transition-colors">
                                        <td class="p-4 font-medium flex items-center gap-3">
                                            <div class="w-8 h-8 rounded-full bg-${colorBase}-100 text-${colorBase}-600 dark:bg-${colorBase}-900/50 dark:text-${colorBase}-300 flex items-center justify-center font-bold text-xs shrink-0">${u.name.charAt(0).toUpperCase()}</div>
                                            ${escapeHTML(u.name)}
                                        </td>
                                        <td class="p-4 font-bold text-gray-700 dark:text-gray-300">${escapeHTML(u.username)}</td>
                                        <td class="p-4 font-mono text-xs text-blue-600 bg-blue-50 dark:bg-blue-900/30 rounded px-3 py-1 m-2 select-all inline-block border border-blue-200 dark:border-blue-800">${escapeHTML(u.password)}</td>
                                        <td class="p-4 text-center">
                                            <button onclick="editUser('${u.id}')" class="text-blue-500 hover:bg-blue-100 dark:hover:bg-blue-900/30 p-2 rounded-lg transition" title="Edit Data"><i class="fas fa-edit"></i></button>
                                            <button onclick="deleteUser('${u.id}')" class="text-red-500 hover:bg-red-100 dark:hover:bg-red-900/30 p-2 rounded-lg transition" title="Hapus Permanen"><i class="fas fa-trash-alt"></i></button>
                                        </td>
                                    </tr>
                                `).join('')}
                                ${list.length === 0 ? `<tr><td colspan="4" class="p-8 text-center text-gray-400">Belum ada data ${title.toLowerCase()} yang didaftarkan.</td></tr>` : ''}
                            </tbody>
                        </table>
                    </div>
                </div>
            `;

            html += renderTable(gurus, 'Daftar Guru Pengajar', 'fa-chalkboard-teacher', 'blue');
            html += renderTable(siswas, 'Daftar Siswa / Murid', 'fa-user-graduate', 'green');

            container.innerHTML = html;
        };

        window.downloadCSVTemplate = () => {
            const csv = "Nama Lengkap,Username,Password,Role\nBudi Santoso,budis,budi123,siswa\nAhmad Guru,ahmadg,guru123,guru\n";
            const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
            const link = document.createElement("a");
            link.href = URL.createObjectURL(blob);
            link.download = "Template_Import_LMS.csv";
            link.style.display = "none";
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            showToast("Template CSV berhasil diunduh.", "info");
        };

        window.handleCSVImport = (e) => {
            const file = e.target.files[0];
            if (!file) return;
            const reader = new FileReader();
            reader.onload = async (event) => {
                const text = event.target.result;
                const rows = text.split('\n').map(row => row.trim()).filter(row => row.length > 0);
                
                if (rows.length < 2) {
                    showToast("File CSV kosong atau format tidak sesuai.", "error");
                    return;
                }

                showToast(`Memproses ${rows.length - 1} data dari CSV...`, "info");
                let successCount = 0;
                
                // Mulai dari 1 karena 0 adalah header
                for (let i = 1; i < rows.length; i++) {
                    const cols = rows[i].split(',');
                    if (cols.length >= 4) {
                        const [name, username, password, role] = cols.map(c => c.trim());
                        // Simple validation
                        if (name && username && password && (role.toLowerCase() === 'guru' || role.toLowerCase() === 'siswa')) {
                            // Check duplikat lokal (bisa dimaksimalkan dengan check DB if needed)
                            if (!AppState.data.users.find(u => u.username === username)) {
                                await addDoc(dbHelper.getColRef('users'), { name, username, password, role: role.toLowerCase() });
                                successCount++;
                            }
                        }
                    }
                }
                showToast(`Import Selesai! ${successCount} data pengguna baru ditambahkan.`, "success");
                e.target.value = ''; // reset
            };
            reader.readAsText(file);
        };

        window.userFormHTML = (user = null) => `
            <form id="add-user-form" class="space-y-4">
                <input type="hidden" id="f-id" value="${user ? user.id : ''}">
                <div><label class="block text-sm font-medium mb-1">Nama Lengkap</label><input type="text" id="f-name" value="${user ? escapeHTML(user.name) : ''}" required class="w-full p-2.5 border rounded-xl dark:bg-gray-800 dark:border-gray-600 outline-none focus:border-primary focus:ring-1 focus:ring-primary transition"></div>
                <div><label class="block text-sm font-medium mb-1">Username (ID Login)</label><input type="text" id="f-user" value="${user ? escapeHTML(user.username) : ''}" required class="w-full p-2.5 border rounded-xl dark:bg-gray-800 dark:border-gray-600 outline-none focus:border-primary focus:ring-1 focus:ring-primary transition"></div>
                <div><label class="block text-sm font-medium mb-1">Password</label><input type="text" id="f-pass" value="${user ? escapeHTML(user.password) : ''}" required class="w-full p-2.5 border rounded-xl dark:bg-gray-800 dark:border-gray-600 outline-none focus:border-primary focus:ring-1 focus:ring-primary transition"></div>
                <div><label class="block text-sm font-medium mb-1">Pilih Peran/Jabatan</label>
                    <select id="f-role" class="w-full p-2.5 border rounded-xl dark:bg-gray-800 dark:border-gray-600 outline-none focus:border-primary focus:ring-1 focus:ring-primary transition">
                        <option value="guru" ${user && user.role === 'guru' ? 'selected' : ''}>Guru Pengampu</option>
                        <option value="siswa" ${user && user.role === 'siswa' ? 'selected' : ''}>Siswa / Murid</option>
                    </select>
                </div>
                <div class="pt-5 flex justify-end">
                    <button type="submit" class="px-5 py-2.5 bg-gradient-to-r from-primary to-secondary hover:shadow-lg text-white rounded-xl transition-all font-medium">Simpan Identitas</button>
                </div>
            </form>
        `;

        window.saveUser = async (e) => {
            e.preventDefault();
            const id = D('f-id').value;
            const data = { 
                name: D('f-name').value.trim(), 
                username: D('f-user').value.trim(), 
                password: D('f-pass').value.trim(), 
                role: D('f-role').value 
            };
            
            closeModal();
            showToast("Memproses penyimpanan data...", "info");
            
            try {
                if (id) {
                    await updateDoc(dbHelper.getDocRef('users', id), data);
                    showToast("Pembaruan data berhasil!", "success");
                } else {
                    const existing = AppState.data.users.find(u => u.username === data.username);
                    if(existing) {
                        showToast("Peringatan: Username sudah dipakai, buat yang berbeda!", "warning");
                        return;
                    }
                    await addDoc(dbHelper.getColRef('users'), data);
                    showToast("Pengguna baru sukses ditambahkan!", "success");
                }
            } catch (err) {
                console.error("Gagal simpan:", err);
                showToast("Kesalahan sistem. Periksa koneksi internet Anda.", "error");
            }
        };

        window.editUser = (id) => {
            const user = AppState.data.users.find(u => u.id === id);
            if(user) openModal('Edit Identitas Pengguna', userFormHTML(user), saveUser);
        };

        window.deleteUser = (id) => {
            confirmAction("Konfirmasi: Apakah Anda sangat yakin ingin menghapus akun pengguna ini secara permanen dari sistem database?", async () => { 
                showToast("Memproses penghapusan...", "info");
                try {
                    await deleteDoc(dbHelper.getDocRef('users', id)); 
                    showToast("Akun telah terhapus permanen.", "success"); 
                } catch(err) {
                    showToast("Gagal menghapus data.", "error");
                }
            });
        };

        // --- MANAJEMEN KELAS (Admin) ---
        const renderClassesAdmin = (container) => {
            const classes = AppState.data.classes || [];
            const users = AppState.data.users || [];
            const gurus = users.filter(u => u.role === 'guru');

            let html = `
                <div class="flex justify-between items-center mb-6 flex-wrap gap-4">
                    <h2 class="text-xl font-bold">Data Struktur Kelas</h2>
                    <button onclick="openModal('Pembuatan Kelas Baru', classFormHTML(), saveClass)" class="px-5 py-2 bg-purple-500 hover:bg-purple-600 text-white rounded-xl shadow-lg text-sm font-medium transition-colors flex items-center gap-2">
                        <i class="fas fa-layer-group"></i> Tambah Kelas
                    </button>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-5">
                    ${classes.map(c => {
                        const guru = gurus.find(g => g.id === c.teacherId);
                        return `
                        <div class="glass dark:bg-cardDark p-6 rounded-2xl shadow-sm border-t-4 border-purple-500 hover:shadow-md transition-shadow relative">
                            <div class="absolute top-4 right-4 text-purple-500/20 text-4xl"><i class="fas fa-building"></i></div>
                            <h3 class="font-bold text-xl mb-3 text-gray-800 dark:text-gray-100 pr-10">${escapeHTML(c.name)}</h3>
                            <div class="space-y-2 mb-5">
                                <p class="text-sm text-gray-600 dark:text-gray-400 flex items-center gap-2"><i class="fas fa-chalkboard-teacher w-4 text-purple-500"></i> <span class="font-medium">${guru ? escapeHTML(guru.name) : '<span class="text-red-400 italic">Belum Ada Guru</span>'}</span></p>
                                <p class="text-sm text-gray-600 dark:text-gray-400 flex items-center gap-2"><i class="fas fa-users w-4 text-blue-500"></i> ${c.students ? c.students.length : 0} Siswa Berpartisipasi</p>
                            </div>
                            <div class="flex gap-3 mt-auto pt-4 border-t border-gray-100 dark:border-gray-700">
                                <button onclick="editClass('${c.id}')" class="text-xs font-semibold text-blue-500 bg-blue-50 dark:bg-blue-900/20 px-3 py-1.5 rounded-lg hover:bg-blue-100 transition"><i class="fas fa-edit mr-1"></i> Edit Anggota & Guru</button>
                                <button onclick="deleteClass('${c.id}')" class="text-xs font-semibold text-red-500 bg-red-50 dark:bg-red-900/20 px-3 py-1.5 rounded-lg hover:bg-red-100 transition"><i class="fas fa-trash-alt mr-1"></i> Hapus</button>
                            </div>
                        </div>
                        `;
                    }).join('')}
                    ${classes.length === 0 ? '<div class="col-span-full p-10 text-center text-gray-400 border-2 border-dashed border-gray-200 dark:border-gray-700 rounded-2xl"><i class="fas fa-door-open text-4xl mb-3 block"></i>Belum ada kelas yang didirikan. Silakan buat kelas pertama Anda.</div>' : ''}
                </div>
            `;
            container.innerHTML = html;
        };

        window.classFormHTML = (classData = null) => {
            const gurus = (AppState.data.users || []).filter(u => u.role === 'guru');
            const siswas = (AppState.data.users || []).filter(u => u.role === 'siswa');
            const enrolled = classData ? (classData.students || []) : [];

            return `
                <form id="add-class-form" class="space-y-4">
                    <input type="hidden" id="c-id" value="${classData ? classData.id : ''}">
                    <p class="text-xs text-gray-500 dark:text-gray-400 mb-4 bg-yellow-50 dark:bg-yellow-900/20 p-2 rounded">Pilih Guru Pengampu dan centang siswa yang berhak mengakses kelas ini secara eksklusif.</p>
                    
                    <div><label class="block text-sm font-medium mb-1">Nama Kelompok Kelas (Misal: X Bahasa Arab)</label><input type="text" id="c-name" value="${classData ? escapeHTML(classData.name) : ''}" required class="w-full p-2.5 border rounded-xl dark:bg-gray-800 outline-none focus:border-purple-500 focus:ring-1 focus:ring-purple-500"></div>
                    <div>
                        <label class="block text-sm font-medium mb-1">Pilih Guru Wali / Pengampu Utama</label>
                        <select id="c-teacher" class="w-full p-2.5 border rounded-xl dark:bg-gray-800 outline-none focus:border-purple-500 focus:ring-1 focus:ring-purple-500" required>
                            <option value="">-- Pilih Guru --</option>
                            ${gurus.map(g => `<option value="${g.id}" ${classData && classData.teacherId === g.id ? 'selected' : ''}>${escapeHTML(g.name)}</option>`).join('')}
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-medium mb-1">Daftarkan Siswa ke Kelas Ini (Centang kotak)</label>
                        <div class="h-48 overflow-y-auto border rounded-xl p-3 dark:bg-gray-800 dark:border-gray-600 shadow-inner bg-gray-50 dark:bg-gray-900/50">
                            ${siswas.map(s => `
                                <label class="flex items-center gap-3 p-2 hover:bg-white dark:hover:bg-gray-700 rounded-lg cursor-pointer transition border border-transparent hover:border-gray-200 dark:hover:border-gray-600 mb-1">
                                    <input type="checkbox" value="${s.id}" class="c-student-cb w-4 h-4 text-purple-600 rounded" ${enrolled.includes(s.id) ? 'checked' : ''}> 
                                    <span class="text-sm font-medium text-gray-700 dark:text-gray-200">${escapeHTML(s.name)}</span>
                                </label>
                            `).join('') || '<div class="text-center text-xs text-gray-400 mt-10">Data siswa kosong. Tambahkan di menu Data Pengguna.</div>'}
                        </div>
                    </div>
                    <div class="pt-5 flex justify-end"><button type="submit" class="px-5 py-2.5 bg-purple-500 hover:bg-purple-600 text-white font-medium rounded-xl shadow-md transition">${classData ? 'Simpan Perubahan' : 'Bentuk Kelas'}</button></div>
                </form>
            `;
        };

        window.saveClass = async (e) => {
            e.preventDefault();
            const id = D('c-id').value;
            const studentChecks = document.querySelectorAll('.c-student-cb:checked');
            const students = Array.from(studentChecks).map(cb => cb.value);
            const teacherId = D('c-teacher').value;
            
            if(!teacherId) { showToast("Pilih guru pengampu terlebih dahulu!", "warning"); return; }
            
            const data = { name: D('c-name').value, teacherId: teacherId, students: students };
            
            closeModal();
            showToast("Menyinkronkan data kelas...", "info");

            try {
                if (id) {
                    await updateDoc(dbHelper.getDocRef('classes', id), data);
                    showToast("Perubahan anggota kelas berhasil disimpan!", "success");
                } else {
                    await addDoc(dbHelper.getColRef('classes'), data);
                    showToast("Struktur Kelas baru berhasil dibangun!", "success");
                }
            } catch (err) {
                showToast("Gagal menyimpan data kelas.", "error");
            }
        };

        window.editClass = (id) => {
            const classData = AppState.data.classes.find(c => c.id === id);
            if(classData) openModal('Modifikasi Ruang Kelas', classFormHTML(classData), saveClass);
        };

        window.deleteClass = (id) => {
            confirmAction("Pembubaran Kelas: Yakin ingin menghapus ruang kelas ini? Seluruh kaitan materi dan tugas akan kehilangan referensi kelas.", async () => { 
                await deleteDoc(dbHelper.getDocRef('classes', id)); 
                showToast("Ruang kelas telah dibubarkan.", "success"); 
            });
        };

        // --- KELAS SAYA (Guru & Siswa) ---
        const renderMyClasses = (container) => {
            const myClasses = getMyClasses();
            const users = AppState.data.users || [];

            let html = `
                <h2 class="text-xl font-bold mb-6 flex items-center gap-2"><i class="fas fa-door-open text-blue-500"></i> Ruang Kelas Anda</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5">
            `;
            
            myClasses.forEach(c => {
                const guru = users.find(u => u.id === c.teacherId);
                const enrolledStudents = users.filter(u => u.role === 'siswa' && (c.students || []).includes(u.id));

                html += `
                    <!-- Clickable Card untuk masuk ke Detail Kelas -->
                    <div onclick="renderView('classDetail', false, '${c.id}')" class="glass dark:bg-cardDark p-6 rounded-2xl shadow-sm border-t-4 border-blue-500 hover:-translate-y-1 transition-transform relative group cursor-pointer hover:shadow-md">
                        <div class="absolute top-4 right-4 text-blue-500/20 group-hover:text-blue-500/40 transition-colors"><i class="fas fa-external-link-alt"></i></div>
                        <h3 class="font-bold text-xl mb-3 text-gray-800 dark:text-gray-100 pr-6">${escapeHTML(c.name)}</h3>
                        <div class="p-3 bg-blue-50 dark:bg-blue-900/20 rounded-xl mb-4 border border-blue-100 dark:border-blue-800">
                            <p class="text-xs font-semibold text-blue-800 dark:text-blue-300 uppercase tracking-wider mb-1">Pengajar Utama</p>
                            <p class="text-sm text-gray-800 dark:text-gray-200 flex items-center gap-2">
                                <img src="https://ui-avatars.com/api/?name=${guru ? encodeURIComponent(guru.name) : 'A'}&background=3b82f6&color=fff" class="w-6 h-6 rounded-full">
                                ${guru ? escapeHTML(guru.name) : '-'}
                            </p>
                        </div>
                        <div class="flex items-center justify-between mt-auto">
                            <span class="text-sm font-medium text-gray-600 dark:text-gray-400 bg-gray-100 dark:bg-gray-800 px-3 py-1.5 rounded-lg">
                                <i class="fas fa-user-graduate text-blue-500 mr-1"></i> ${enrolledStudents.length} Siswa Tergabung
                            </span>
                        </div>
                    </div>
                `;
            });
            if(myClasses.length === 0) html += `<div class="col-span-full p-10 text-center text-gray-400 bg-gray-50 dark:bg-gray-800 rounded-2xl border border-gray-200 dark:border-gray-700">Anda belum dilibatkan di kelas manapun. Menunggu instruksi Admin.</div>`;
            html += `</div>`;
            container.innerHTML = html;
        };

        // --- DETAIL KELAS ---
        const renderClassDetail = (container, classId) => {
            const cls = AppState.data.classes.find(c => c.id === classId);
            if (!cls) { container.innerHTML = '<p>Kelas tidak ditemukan.</p>'; return; }
            
            const users = AppState.data.users || [];
            const guru = users.find(u => u.id === cls.teacherId);
            const enrolledStudents = users.filter(u => u.role === 'siswa' && (cls.students || []).includes(u.id));

            let html = `
                <div class="glass dark:bg-cardDark p-6 rounded-2xl mb-6 shadow-sm border-l-4 border-blue-500 flex justify-between items-center flex-wrap gap-4">
                    <div>
                        <h2 class="text-2xl font-bold text-gray-800 dark:text-gray-100">${escapeHTML(cls.name)}</h2>
                        <p class="text-gray-600 dark:text-gray-400 mt-1"><i class="fas fa-chalkboard-teacher text-blue-500"></i> Guru Pengampu: ${guru ? escapeHTML(guru.name) : '-'}</p>
                    </div>
                    ${AppState.user.role === 'guru' || AppState.user.role === 'admin' ? `
                        <button onclick="downloadClassRekap('${cls.id}')" class="px-5 py-2.5 bg-blue-500 hover:bg-blue-600 text-white rounded-xl font-bold text-sm shadow-md transition-colors flex items-center gap-2">
                            <i class="fas fa-file-csv"></i> Unduh Daftar Siswa
                        </button>
                    ` : ''}
                </div>

                <div class="bg-white dark:bg-cardDark rounded-2xl shadow-sm overflow-hidden border border-gray-100 dark:border-gray-700">
                    <div class="px-5 py-4 border-b border-gray-100 dark:border-gray-700 bg-gray-50/50 dark:bg-gray-800/50 flex items-center gap-3">
                        <div class="w-8 h-8 rounded-full bg-blue-100 text-blue-600 dark:bg-blue-900/50 dark:text-blue-400 flex items-center justify-center"><i class="fas fa-users"></i></div>
                        <h3 class="font-bold text-lg text-gray-800 dark:text-gray-100">Anggota Kelas <span class="text-sm text-gray-500">(${enrolledStudents.length} Siswa)</span></h3>
                    </div>
                    <div class="p-4 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-3">
                        ${enrolledStudents.map((s, idx) => `
                            <div class="flex items-center gap-3 p-3 rounded-xl hover:bg-gray-50 dark:hover:bg-gray-800 transition-colors border border-transparent hover:border-gray-200 dark:hover:border-gray-700">
                                <div class="w-8 h-8 rounded-full bg-blue-100 text-blue-600 dark:bg-blue-900/50 dark:text-blue-400 flex items-center justify-center font-bold text-xs shrink-0">${idx + 1}</div>
                                <div>
                                    <p class="font-bold text-sm text-gray-800 dark:text-gray-200">${escapeHTML(s.name)}</p>
                                    <p class="text-[10px] text-gray-500 uppercase tracking-wider">Siswa</p>
                                </div>
                            </div>
                        `).join('')}
                        ${enrolledStudents.length === 0 ? '<div class="col-span-full p-6 text-center text-gray-500">Belum ada siswa yang tergabung.</div>' : ''}
                    </div>
                </div>
            `;
            container.innerHTML = html;
        };

        window.downloadClassRekap = (classId) => {
            const cls = AppState.data.classes.find(c => c.id === classId);
            const enrolledStudents = AppState.data.users.filter(u => u.role === 'siswa' && (cls.students || []).includes(u.id));
            
            let csv = `Data Siswa Kelas ${cls.name}\nNo,Nama Lengkap,Username\n`;
            enrolledStudents.forEach((s, i) => {
                csv += `${i+1},"${s.name}","${s.username}"\n`;
            });
            
            const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
            const link = document.createElement("a");
            link.href = URL.createObjectURL(blob);
            link.download = `Rekap_Siswa_${cls.name.replace(/ /g, '_')}.csv`;
            link.style.display = "none";
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            showToast("Berhasil mendownload data siswa CSV.", "success");
        };


        // --- JADWAL PELAJARAN (REKAPITULASI GLOBAL/LOKAL) ---
        window.toggleScheduleMode = (mode) => {
            AppState.scheduleMode = mode;
            renderView('schedules', true);
        };

        const renderSchedules = (container) => {
            const role = AppState.user.role;
            const schedules = AppState.data.schedules || [];
            const classes = AppState.data.classes || [];
            const users = AppState.data.users || [];

            // Filter
            let viewSchedules = schedules;
            if(AppState.scheduleMode === 'my' && role !== 'admin') {
                if (role === 'guru') {
                    viewSchedules = schedules.filter(s => s.teacherId === AppState.user.uid);
                } else if (role === 'siswa') {
                    const myClassIds = getMyClasses().map(c => c.id);
                    viewSchedules = schedules.filter(s => myClassIds.includes(s.classId));
                }
            }

            let html = `
                <div class="flex justify-between items-center mb-6 flex-wrap gap-4">
                    <h2 class="text-xl font-bold flex items-center gap-2"><i class="fas fa-calendar-alt text-teal-500"></i> Kalender Pelajaran</h2>
                    <div class="flex items-center gap-3">
                        <!-- Toggle Mode Khusus Guru -->
                        ${role === 'guru' ? `
                            <div class="bg-gray-100 dark:bg-gray-800 p-1 rounded-xl flex font-medium text-sm">
                                <button onclick="toggleScheduleMode('my')" class="px-4 py-1.5 rounded-lg transition-colors ${AppState.scheduleMode === 'my' ? 'bg-white dark:bg-gray-700 shadow text-teal-600 dark:text-teal-400' : 'text-gray-500 hover:text-gray-700 dark:hover:text-gray-300'}">Jadwal Saya</button>
                                <button onclick="toggleScheduleMode('all')" class="px-4 py-1.5 rounded-lg transition-colors ${AppState.scheduleMode === 'all' ? 'bg-white dark:bg-gray-700 shadow text-teal-600 dark:text-teal-400' : 'text-gray-500 hover:text-gray-700 dark:hover:text-gray-300'}">Semua Jadwal (Global)</button>
                            </div>
                        ` : ''}
                        ${role === 'admin' ? `<button onclick="openModal('Penyusunan Jadwal', scheduleFormHTML(), saveSchedule)" class="px-5 py-2 bg-teal-500 hover:bg-teal-600 text-white rounded-xl shadow-lg text-sm font-medium transition flex items-center gap-2"><i class="fas fa-calendar-plus"></i> Tambah Jadwal</button>` : ''}
                    </div>
                </div>
                
                ${AppState.scheduleMode === 'all' && role === 'guru' ? '<p class="text-xs text-gray-500 mb-4 bg-blue-50 dark:bg-blue-900/20 p-2 rounded border border-blue-100 dark:border-blue-800"><i class="fas fa-info-circle text-blue-500"></i> Menampilkan rekapitulasi jadwal seluruh guru dan kelas di sistem.</p>' : ''}
                
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
            `;

            viewSchedules.sort((a,b) => Days.indexOf(a.day) - Days.indexOf(b.day)).forEach(s => {
                const c = classes.find(x => x.id === s.classId);
                const g = users.find(x => x.id === s.teacherId);
                html += `
                    <div class="glass dark:bg-cardDark p-5 rounded-2xl shadow-sm border border-gray-100 dark:border-gray-700 hover:border-teal-300 transition-colors flex flex-col h-full relative overflow-hidden">
                        <div class="absolute -right-4 -bottom-4 opacity-5 text-6xl"><i class="fas fa-clock"></i></div>
                        <div class="flex justify-between items-center mb-3">
                            <span class="bg-teal-100 text-teal-700 dark:bg-teal-900/50 dark:text-teal-300 px-3 py-1 rounded-lg text-xs font-bold shadow-sm uppercase tracking-wider">${escapeHTML(s.day)}</span>
                            <span class="text-xs font-bold text-gray-500 bg-white dark:bg-gray-800 px-2 py-1 rounded shadow-sm border border-gray-100 dark:border-gray-700"><i class="far fa-clock text-teal-500 mr-1"></i> ${s.timeStart} - ${s.timeEnd}</span>
                        </div>
                        <h4 class="font-bold text-lg text-gray-800 dark:text-gray-100 mb-3">${escapeHTML(s.subject)}</h4>
                        <div class="space-y-1 mt-auto z-10">
                            <p class="text-xs text-gray-600 dark:text-gray-400 flex items-center gap-2 bg-gray-50 dark:bg-gray-800/50 p-1.5 rounded"><i class="fas fa-building w-4 text-purple-400"></i> ${c ? escapeHTML(c.name) : '-'}</p>
                            <p class="text-xs text-gray-600 dark:text-gray-400 flex items-center gap-2 bg-gray-50 dark:bg-gray-800/50 p-1.5 rounded"><i class="fas fa-user-tie w-4 text-blue-400"></i> ${g ? escapeHTML(g.name) : '-'}</p>
                        </div>
                        ${role === 'admin' ? `<button onclick="deleteSchedule('${s.id}')" class="absolute top-4 right-4 text-gray-300 hover:text-red-500 transition-colors"><i class="fas fa-times-circle text-lg"></i></button>` : ''}
                    </div>
                `;
            });

            if(viewSchedules.length === 0) html += `<div class="col-span-full text-center p-10 bg-gray-50 dark:bg-gray-800 rounded-2xl text-gray-500 border border-dashed border-gray-300 dark:border-gray-700">Agenda pembelajaran masih kosong.</div>`;
            html += `</div>`;
            container.innerHTML = html;
        };

        window.scheduleFormHTML = () => {
            const classes = AppState.data.classes || [];
            const gurus = (AppState.data.users || []).filter(u => u.role === 'guru');
            return `
                <form id="add-schedule-form" class="space-y-4">
                    <div>
                        <label class="block text-sm font-medium mb-1">Pilih Kelas</label>
                        <select id="s-class" class="w-full p-2.5 border rounded-xl dark:bg-gray-800 outline-none focus:border-teal-500" required>
                            <option value="">-- Tentukan Kelas --</option>
                            ${classes.map(c => `<option value="${c.id}">${escapeHTML(c.name)}</option>`).join('')}
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-medium mb-1">Mata Pelajaran (Kurikulum)</label>
                        <select id="s-subject" class="w-full p-2.5 border rounded-xl dark:bg-gray-800 outline-none focus:border-teal-500" required>
                            ${Subjects.map(s => `<option value="${s}">${s}</option>`).join('')}
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-medium mb-1">Guru Pengajar (Penyaji Materi)</label>
                        <select id="s-teacher" class="w-full p-2.5 border rounded-xl dark:bg-gray-800 outline-none focus:border-teal-500" required>
                            <option value="">-- Tentukan Guru --</option>
                            ${gurus.map(g => `<option value="${g.id}">${escapeHTML(g.name)}</option>`).join('')}
                        </select>
                    </div>
                    <div class="grid grid-cols-2 gap-3 bg-gray-50 dark:bg-gray-800/50 p-3 rounded-xl border border-gray-100 dark:border-gray-700">
                        <div class="col-span-2">
                            <label class="block text-sm font-medium mb-1">Hari Pertemuan</label>
                            <select id="s-day" class="w-full p-2.5 border rounded-xl dark:bg-gray-800 outline-none focus:border-teal-500">
                                ${Days.map(d => `<option value="${d}">${d}</option>`).join('')}
                            </select>
                        </div>
                        <div><label class="block text-sm font-medium mb-1">Jam Mulai</label><input type="time" id="s-start" required class="w-full p-2.5 border rounded-xl dark:bg-gray-800 outline-none focus:border-teal-500"></div>
                        <div><label class="block text-sm font-medium mb-1">Jam Selesai</label><input type="time" id="s-end" required class="w-full p-2.5 border rounded-xl dark:bg-gray-800 outline-none focus:border-teal-500"></div>
                    </div>
                    <div class="pt-4 flex justify-end"><button type="submit" class="px-5 py-2.5 bg-teal-500 hover:bg-teal-600 text-white rounded-xl shadow-md font-medium transition">Simpan Jadwal</button></div>
                </form>
            `;
        };

        window.saveSchedule = async (e) => {
            e.preventDefault();
            const data = {
                classId: D('s-class').value, subject: D('s-subject').value, teacherId: D('s-teacher').value,
                day: D('s-day').value, timeStart: D('s-start').value, timeEnd: D('s-end').value
            };
            closeModal();
            try {
                await addDoc(dbHelper.getColRef('schedules'), data);
                showToast("Penyusunan jadwal sukses direkam!", "success");
            } catch(e) {
                showToast("Terjadi kegagalan menyimpan jadwal.", "error");
            }
        };
        window.deleteSchedule = (id) => confirmAction("Hapus data jadwal ujian/pelajaran ini?", async () => await deleteDoc(dbHelper.getDocRef('schedules', id)));

        // --- MATERI PEMBELAJARAN ---
        const renderMaterials = (container) => {
            const role = AppState.user.role;
            const myClassIds = getMyClasses().map(c => c.id);
            const materials = (AppState.data.materials || []).filter(m => role === 'admin' || myClassIds.includes(m.classId));
            const classes = AppState.data.classes || [];

            let html = `
                <div class="flex justify-between items-center mb-6 flex-wrap gap-4">
                    <h2 class="text-xl font-bold flex items-center gap-2"><i class="fas fa-book-open text-pink-500"></i> Perpustakaan Materi</h2>
                    ${role === 'guru' ? `<button onclick="openModal('Penyebaran Materi Baru', materialFormHTML(), saveMaterial)" class="px-5 py-2 bg-pink-500 hover:bg-pink-600 text-white rounded-xl shadow-lg text-sm font-medium transition flex items-center gap-2"><i class="fas fa-cloud-upload-alt"></i> Unggah Materi</button>` : ''}
                </div>
                <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-6">
                    ${materials.map(m => {
                        const c = classes.find(x => x.id === m.classId);
                        return `
                        <div class="bg-white dark:bg-cardDark rounded-2xl overflow-hidden shadow-sm hover:shadow-lg transition-all flex flex-col h-full border border-gray-100 dark:border-gray-700 group">
                            <div class="h-2 bg-gradient-to-r from-pink-400 to-primary w-full opacity-70 group-hover:opacity-100 transition-opacity"></div>
                            <div class="p-5 flex-1 flex flex-col">
                                <span class="text-[10px] font-bold tracking-wider bg-pink-50 text-pink-600 dark:bg-pink-900/30 dark:text-pink-300 px-2 py-1 rounded uppercase w-max mb-3">${escapeHTML(m.subject)}</span>
                                <h3 class="font-bold text-lg mb-1 leading-snug text-gray-800 dark:text-gray-100">${escapeHTML(m.title)}</h3>
                                <p class="text-xs text-gray-400 mb-3 flex items-center gap-1"><i class="fas fa-building text-gray-300"></i> ${c ? escapeHTML(c.name) : '-'}</p>
                                
                                <div class="bg-gray-50 dark:bg-gray-800/50 p-3 rounded-xl mb-4 flex-1">
                                    <p class="text-sm text-gray-700 dark:text-gray-300 ${/[\u0600-\u06FF]/.test(m.desc) ? 'font-arabic text-right text-xl leading-loose' : 'line-clamp-4 leading-relaxed'}">${escapeHTML(m.desc)}</p>
                                </div>
                                
                                <div class="flex items-center justify-between pt-2">
                                    <span class="text-xs font-medium text-gray-400 flex items-center gap-1"><i class="far fa-calendar-alt"></i> ${new Date(m.date).toLocaleDateString('id-ID')}</span>
                                    <button onclick="downloadMaterialFile('${m.id}')" class="text-sm text-pink-500 font-bold hover:text-pink-600 bg-pink-50 hover:bg-pink-100 dark:bg-pink-900/20 dark:hover:bg-pink-900/40 px-3 py-1.5 rounded-lg transition-colors flex items-center gap-2 cursor-pointer">
                                        Unduh File <i class="fas fa-download"></i>
                                    </button>
                                </div>
                                ${m.fileName ? `
                                    <div class="mt-2 text-xs text-gray-500 bg-gray-100 dark:bg-gray-800 px-2 py-1 rounded truncate"><i class="fas fa-paperclip"></i> ${escapeHTML(m.fileName)}</div>
                                ` : ''}
                            </div>
                        </div>`;
                    }).join('')}
                </div>
                ${materials.length === 0 ? `<div class="col-span-full p-12 text-center bg-white dark:bg-cardDark rounded-3xl border-2 border-dashed border-gray-200 dark:border-gray-700 text-gray-400"><i class="fas fa-folder-open text-5xl mb-4 text-gray-300 dark:text-gray-600 block"></i>Belum ada silabus atau materi yang dibagikan untuk kelas ini.</div>` : ''}
            `;
            container.innerHTML = html;
        };

        window.downloadMaterialFile = (id) => {
            const m = AppState.data.materials.find(x => x.id === id);
            if(!m) return;
            const c = AppState.data.classes.find(x => x.id === m.classId);
            const className = c ? c.name : 'Unknown';
            const content = `Judul Dokumen: ${m.title}\nMata Pelajaran: ${m.subject}\nKelas: ${className}\nTanggal Upload: ${new Date(m.date).toLocaleString('id-ID')}\nLampiran: ${m.fileName || 'Tidak ada'}\n\n=========================================\nISI MATERI:\n\n${m.desc}\n=========================================`;
            const blob = new Blob([content], { type: 'text/plain;charset=utf-8;' });
            const link = document.createElement("a");
            const url = URL.createObjectURL(blob);
            link.setAttribute("href", url);
            link.setAttribute("download", `Materi_${m.title.replace(/ /g, '_')}.txt`);
            link.style.visibility = 'hidden';
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            showToast(`File materi "${m.title}" berhasil diunduh.`, "success");
        };

        window.materialFormHTML = () => {
            const myClasses = getMyClasses();
            
            // Validasi Blokir Akses Jika Guru Belum Punya Kelas
            if (myClasses.length === 0) {
                return `<div class="p-8 text-center text-red-500 bg-red-50 dark:bg-red-900/20 rounded-xl border border-red-100 dark:border-red-800"><i class="fas fa-exclamation-triangle text-3xl mb-3"></i><p class="font-bold text-lg">Akses Ditolak</p><p class="text-sm mt-1">Anda belum ditugaskan untuk mengajar di kelas manapun oleh Admin. Silakan hubungi Administrator Pusat untuk penugasan kelas terlebih dahulu.</p></div>`;
            }

            return `
                <form id="add-material-form" class="space-y-4">
                    <div>
                        <label class="block text-sm font-medium mb-1">Target Penyebaran (Kelas yang Anda Ampu)</label>
                        <select id="m-class" class="w-full p-2.5 border rounded-xl dark:bg-gray-800 outline-none focus:border-pink-500" required>
                            <option value="">-- Tentukan Kelas --</option>
                            ${myClasses.map(c => `<option value="${c.id}">${escapeHTML(c.name)}</option>`).join('')}
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-medium mb-1">Kategori / Mata Pelajaran</label>
                        <select id="m-subject" class="w-full p-2.5 border rounded-xl dark:bg-gray-800 outline-none focus:border-pink-500">
                            ${Subjects.map(s => `<option value="${s}">${s}</option>`).join('')}
                        </select>
                    </div>
                    <div><label class="block text-sm font-medium mb-1">Judul / Topik Materi</label><input type="text" id="m-title" required class="w-full p-2.5 border rounded-xl dark:bg-gray-800 outline-none focus:border-pink-500"></div>
                    <div>
                        <label class="block text-sm font-medium mb-1 flex justify-between items-center">
                            Isi Teks Materi
                            <div class="flex gap-2">
                                <button type="button" onclick="generateMateriAI()" class="text-xs font-bold text-purple-600 bg-purple-100 hover:bg-purple-200 px-2 py-1 rounded shadow-sm transition"><i class="fas fa-magic"></i> Generate AI</button>
                                <button type="button" onclick="toggleKeyboard('m-desc')" class="text-xs font-bold text-pink-600 bg-pink-100 hover:bg-pink-200 px-2 py-1 rounded shadow-sm transition"><i class="fas fa-keyboard"></i> Buka Keyboard Arab</button>
                            </div>
                        </label>
                        <textarea id="m-desc" rows="5" class="w-full p-3 border rounded-xl dark:bg-gray-800 outline-none focus:border-pink-500 focus:ring-1 focus:ring-pink-500 transition leading-relaxed"></textarea>
                    </div>
                    <div class="pt-4 flex justify-end"><button type="submit" class="px-5 py-2.5 bg-pink-500 hover:bg-pink-600 text-white rounded-xl shadow-md font-medium transition">Tebarkan Materi</button></div>
                </form>
            `;
        };

        window.saveMaterial = async (e) => {
            e.preventDefault();
            const fileInput = D('m-file');
            const fileName = fileInput.files.length > 0 ? fileInput.files[0].name : '';

            const data = {
                classId: D('m-class').value, subject: D('m-subject').value, title: D('m-title').value, desc: D('m-desc').value,
                fileName: fileName, date: new Date().toISOString(), authorId: AppState.user.uid
            };
            closeModal();
            try {
                await addDoc(dbHelper.getColRef('materials'), data);
                showToast("Notifikasi: Dokumen berhasil disiarkan ke kelas target!", "success");
            } catch(e) { showToast("Gagal mengunggah materi.", "error"); }
        };

        // --- TUGAS & KUIS (Assignments) ---
        const renderAssignments = (container) => {
            const role = AppState.user.role;
            const myClassIds = getMyClasses().map(c => c.id);
            const assignments = (AppState.data.assignments || []).filter(a => role === 'admin' || myClassIds.includes(a.classId));
            const classes = AppState.data.classes || [];

            let html = `
                <div class="flex justify-between items-center mb-6 flex-wrap gap-4">
                    <h2 class="text-xl font-bold flex items-center gap-2"><i class="fas fa-tasks text-orange-500"></i> Evaluasi & Penugasan</h2>
                    ${role === 'guru' ? `<button onclick="openModal('Pemberian Tugas Baru', assignmentFormHTML(), saveAssignment)" class="px-5 py-2 bg-orange-500 hover:bg-orange-600 text-white rounded-xl shadow-lg text-sm font-medium transition flex items-center gap-2"><i class="fas fa-edit"></i> Buat Tugas Baru</button>` : ''}
                </div>
                <div class="grid grid-cols-1 lg:grid-cols-2 xl:grid-cols-3 gap-5">
                    ${assignments.map(a => {
                        const c = classes.find(x => x.id === a.classId);
                        const isExpired = new Date(a.deadline) < new Date();
                        const mySubmission = role === 'siswa' ? (a.submissions || []).find(s => s.uid === AppState.user.uid) : null;
                        
                        return `
                        <div class="bg-white dark:bg-cardDark p-6 rounded-2xl shadow-sm border-l-4 ${isExpired ? 'border-red-500 opacity-80' : 'border-orange-500'} flex flex-col hover:shadow-md transition-shadow relative">
                            ${isExpired ? '<div class="absolute top-2 right-2 text-[10px] bg-red-100 text-red-700 px-2 py-0.5 rounded-full font-bold uppercase tracking-widest border border-red-200">Ditutup</div>' : '<div class="absolute top-2 right-2 text-[10px] bg-green-100 text-green-700 px-2 py-0.5 rounded-full font-bold uppercase tracking-widest border border-green-200">Aktif</div>'}
                            
                            <h3 class="font-bold text-lg text-gray-800 dark:text-gray-100 mb-1 pr-14">${escapeHTML(a.title)}</h3>
                            <p class="text-xs font-medium text-gray-500 mb-3 flex items-center gap-1"><i class="fas fa-building w-3"></i> ${c ? escapeHTML(c.name) : '-'}</p>
                            
                            <div class="bg-orange-50/50 dark:bg-orange-900/10 p-3 rounded-lg mb-4 flex-1 border border-orange-100/50 dark:border-orange-800/30">
                                <p class="text-sm text-gray-700 dark:text-gray-300 ${/[\u0600-\u06FF]/.test(a.desc) ? 'font-arabic text-right text-xl' : 'line-clamp-3'}">${escapeHTML(a.desc)}</p>
                            </div>
                            
                            ${a.fileName ? `<div class="mb-3 text-xs font-medium text-gray-500"><i class="fas fa-paperclip"></i> Dokumen Soal: ${escapeHTML(a.fileName)}</div>` : ''}

                            <div class="flex items-center justify-between mb-4">
                                <span class="text-xs font-semibold ${isExpired ? 'text-red-500' : 'text-orange-600 dark:text-orange-400'} flex items-center gap-1 bg-gray-50 dark:bg-gray-800 px-2 py-1 rounded"><i class="fas fa-hourglass-half"></i> Deadline: ${new Date(a.deadline).toLocaleDateString('id-ID')}</span>
                                ${mySubmission ? `<span class="text-[10px] bg-green-100 text-green-700 px-2 py-1 rounded-lg font-bold"><i class="fas fa-check"></i> Dikumpulkan</span>` : ''}
                            </div>
                            
                            <div class="mt-auto pt-3 border-t border-gray-100 dark:border-gray-700 flex gap-2">
                                ${role === 'siswa' 
                                    ? `<button onclick="openSubmitAssignment('${a.id}')" class="px-4 py-2.5 ${mySubmission ? 'bg-green-500 hover:bg-green-600' : (isExpired ? 'bg-gray-300 text-gray-600 cursor-not-allowed' : 'bg-gradient-to-r from-orange-400 to-orange-500 hover:scale-[1.02]')} text-white rounded-xl text-xs font-bold w-full text-center transition-transform shadow">
                                            ${mySubmission ? '<i class="fas fa-eye"></i> Lihat Jawaban Saya' : (isExpired ? '<i class="fas fa-lock"></i> Waktu Habis' : 'Kumpulkan Jawaban')}
                                       </button>` 
                                    : `<button onclick="renderView('classDetail', false, '${a.classId}')" class="px-4 py-2.5 bg-orange-100 text-orange-700 dark:bg-orange-900/30 dark:text-orange-300 rounded-xl text-xs font-bold w-full text-center hover:bg-orange-200 dark:hover:bg-orange-900/50 transition">
                                            <i class="fas fa-users"></i> Lihat Siswa
                                       </button>
                                       <button onclick="viewSubmissions('${a.id}')" class="px-4 py-2.5 bg-gray-800 text-white rounded-xl text-xs font-bold w-full text-center hover:bg-gray-700 transition">
                                            <i class="fas fa-inbox"></i> Jawaban Masuk (${a.submissions ? a.submissions.length : 0})
                                       </button>`}
                            </div>
                        </div>`;
                    }).join('')}
                </div>
                ${assignments.length === 0 ? `<div class="text-center p-10 bg-white dark:bg-cardDark rounded-3xl border border-dashed border-gray-200 text-gray-400"><i class="fas fa-clipboard-check text-4xl mb-3 block opacity-50"></i>Belum ada instruksi tugas baru.</div>` : ''}
            `;
            container.innerHTML = html;
        };

        window.openSubmitAssignment = (id) => {
            const assignment = AppState.data.assignments.find(a => a.id === id);
            const mySubmission = (assignment.submissions || []).find(s => s.uid === AppState.user.uid);
            const isExpired = new Date(assignment.deadline) < new Date();
            
            if (isExpired && !mySubmission) {
                showToast("Maaf, batas waktu pengumpulan tugas ini telah berakhir.", "error");
                return;
            }

            const formHTML = `
                <form id="submit-assignment-form" class="space-y-4">
                    <input type="hidden" id="sub-assignment-id" value="${id}">
                    <div class="bg-orange-50 dark:bg-orange-900/20 p-3 rounded-xl border border-orange-100 dark:border-orange-800">
                        <p class="text-xs text-orange-600 dark:text-orange-400 font-bold uppercase tracking-wider mb-1">Topik Penugasan</p>
                        <p class="text-sm font-medium text-gray-800 dark:text-gray-200">${escapeHTML(assignment.title)}</p>
                    </div>
                    <div>
                        <label class="block text-sm font-medium mb-2 flex justify-between items-center">
                            Lembar Jawaban Teks
                            ${!mySubmission ? `<button type="button" onclick="toggleKeyboard('sub-answer')" class="text-xs bg-gray-100 dark:bg-gray-700 text-gray-600 dark:text-gray-300 px-2 py-1 rounded shadow-sm hover:text-primary transition"><i class="fas fa-keyboard"></i> Keyboard Arab</button>` : ''}
                        </label>
                        <textarea id="sub-answer" rows="5" class="w-full p-4 border rounded-xl dark:bg-gray-800 outline-none focus:border-orange-500 focus:ring-1 focus:ring-orange-500 transition leading-relaxed ${/[\u0600-\u06FF]/.test(mySubmission?.answer || '') ? 'font-arabic text-xl text-right' : ''}" ${mySubmission ? 'disabled bg-gray-50 dark:bg-gray-900' : ''} placeholder="Ketik jawaban Anda di sini...">${mySubmission ? escapeHTML(mySubmission.answer) : ''}</textarea>
                    </div>
                    ${!mySubmission ? `
                        <div>
                            <label class="block text-sm font-medium mb-1">Upload File (Jika Ada)</label>
                            <input type="file" id="sub-file" class="w-full p-2 border rounded-xl dark:bg-gray-800 dark:border-gray-600 text-sm">
                        </div>
                    ` : (mySubmission.fileName ? `
                        <div class="p-3 bg-gray-100 dark:bg-gray-800 rounded-xl text-sm font-medium"><i class="fas fa-paperclip"></i> Dokumen Dilampirkan: ${escapeHTML(mySubmission.fileName)}</div>
                    ` : '')}

                    ${mySubmission ? `
                        <div class="p-4 bg-green-50 dark:bg-green-900/20 text-green-700 dark:text-green-300 rounded-xl border border-green-200 dark:border-green-800 flex justify-between items-center">
                            <div>
                                <p class="font-bold text-sm"><i class="fas fa-check-circle"></i> Berhasil Terkirim</p>
                                <p class="text-xs mt-1">Pada: ${new Date(mySubmission.date).toLocaleString('id-ID')}</p>
                            </div>
                        </div>
                    ` : `
                        <div class="pt-2 flex justify-end">
                            <button type="submit" class="px-6 py-3 bg-gradient-to-r from-orange-500 to-orange-400 hover:from-orange-600 hover:to-orange-500 text-white rounded-xl shadow-lg font-bold transition-transform hover:scale-105 flex items-center gap-2">
                                <i class="fas fa-paper-plane"></i> Kirim Jawaban Sekarang
                            </button>
                        </div>
                    `}
                </form>
            `;
            openModal("Pengumpulan Lembar Kerja", formHTML, saveSubmission);
        };

        window.saveSubmission = async (e) => {
            e.preventDefault();
            const id = D('sub-assignment-id').value;
            const answer = D('sub-answer').value.trim();
            const fileInput = D('sub-file');
            const fileName = fileInput && fileInput.files.length > 0 ? fileInput.files[0].name : '';

            if(!answer && !fileName) { showToast("Anda harus mengisi teks jawaban atau melampirkan file!", "warning"); return; }

            const assignment = AppState.data.assignments.find(a => a.id === id);
            const newSub = { uid: AppState.user.uid, name: AppState.user.name, answer: answer, fileName: fileName, date: new Date().toISOString() };
            const updatedSubs = [...(assignment.submissions || []), newSub];
            
            closeModal();
            showToast("Mengirim lembar jawaban ke meja guru...", "info");
            try {
                await updateDoc(dbHelper.getDocRef('assignments', id), { submissions: updatedSubs });
                showToast("Berhasil! Jawaban Anda telah dikumpulkan.", "success");
            } catch(err) {
                showToast("Gagal mengirim jawaban, cek koneksi internet.", "error");
            }
        };

        window.viewSubmissions = (id) => {
            const assignment = AppState.data.assignments.find(a => a.id === id);
            const subs = assignment.submissions || [];
            
            let html = `
                <div class="bg-gray-50 dark:bg-gray-900 p-3 rounded-xl mb-4 border border-gray-200 dark:border-gray-700">
                    <p class="text-xs text-gray-500 font-bold uppercase tracking-wider mb-1">Tugas:</p>
                    <p class="text-sm font-medium">${escapeHTML(assignment.title)}</p>
                </div>
                <div class="space-y-4 max-h-[55vh] overflow-y-auto pr-2 custom-scrollbar">
                    ${subs.map((s) => `
                        <div class="p-4 bg-white dark:bg-gray-800 rounded-xl border border-gray-200 dark:border-gray-700 shadow-sm flex flex-col">
                            <div class="flex justify-between items-center mb-3 border-b border-gray-100 dark:border-gray-700 pb-2">
                                <span class="font-bold text-gray-800 dark:text-gray-100 flex items-center gap-2"><i class="fas fa-user-circle text-blue-400 text-lg"></i> ${escapeHTML(s.name)}</span>
                                <span class="text-[10px] text-gray-500 bg-gray-100 dark:bg-gray-900 px-2 py-1 rounded"><i class="far fa-clock"></i> ${new Date(s.date).toLocaleString('id-ID')}</span>
                            </div>
                            <div class="p-3 bg-gray-50 dark:bg-gray-900 rounded-lg text-sm mb-4 border border-gray-100 dark:border-gray-700 whitespace-pre-wrap ${/[\u0600-\u06FF]/.test(s.answer) ? 'font-arabic text-xl text-right leading-loose' : 'leading-relaxed'}">${escapeHTML(s.answer)}</div>
                            
                            <div id="ai-feedback-${id}-${s.uid}" class="hidden-app bg-purple-50 dark:bg-purple-900/20 p-3 rounded-lg text-sm text-purple-800 dark:text-purple-300 mb-3 border border-purple-200 dark:border-purple-800 whitespace-pre-wrap"></div>
                            
                            <div class="flex items-center gap-2 mt-auto flex-wrap">
                                <button type="button" onclick="evaluateAnswerAI('${id}', '${s.uid}', '${escapeJS(s.answer)}', '${escapeJS(assignment.title)}')" class="px-3 py-2 bg-purple-100 text-purple-700 dark:bg-purple-900/50 dark:text-purple-300 rounded-lg text-xs font-bold hover:bg-purple-200 transition flex items-center gap-1">
                                    <i class="fas fa-magic"></i> Analisis AI
                                </button>
                                <div class="ml-auto flex items-center gap-2">
                                    <span class="text-xs font-bold uppercase text-gray-500">Nilai:</span>
                                    <input type="number" id="score-${id}-${s.uid}" value="${s.score !== null && s.score !== undefined ? s.score : ''}" placeholder="0-100" class="w-24 p-2 border rounded-lg text-sm font-bold text-center dark:bg-gray-900 dark:border-gray-600 focus:border-orange-500 outline-none">
                                    <button type="button" onclick="saveScore('${id}', '${s.uid}', 'score-${id}-${s.uid}')" class="px-4 py-2 bg-green-500 text-white rounded-lg text-sm font-bold hover:bg-green-600 transition flex items-center gap-2">
                                        <i class="fas fa-save"></i> Simpan
                                    </button>
                                </div>
                            </div>
                        </div>
                    `).join('')}
                    ${subs.length === 0 ? `
                        <div class="flex flex-col items-center justify-center py-10 opacity-50 text-gray-500">
                            <i class="fas fa-inbox text-5xl mb-3"></i>
                            <p class="text-sm font-medium">Belum ada lembar kerja yang dikumpulkan oleh siswa.</p>
                        </div>
                    ` : ''}
                </div>
            `;
            openModal("Monitoring Nilai Siswa", html, null);
        };

        window.saveScore = async (assignmentId, studentUid, inputId) => {
            const scoreVal = D(inputId).value;
            if(scoreVal === '') { showToast("Nilai tidak boleh kosong!", "warning"); return; }
            
            const assignment = AppState.data.assignments.find(a => a.id === assignmentId);
            if(!assignment) return;
            
            const subs = [...(assignment.submissions || [])];
            const subIndex = subs.findIndex(s => s.uid === studentUid);
            
            if(subIndex > -1) {
                subs[subIndex].score = parseInt(scoreVal);
                
                const btn = D(inputId).nextElementSibling;
                const oldHTML = btn.innerHTML;
                btn.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Menyimpan...';
                
                try {
                    // 1. Update di Tugas
                    await updateDoc(dbHelper.getDocRef('assignments', assignmentId), { submissions: subs });
                    
                    // 2. Sync ke Manajemen Nilai (Harian)
                    const classId = assignment.classId;
                    const gradesData = AppState.data.grades || [];
                    const existingGrade = gradesData.find(g => g.classId === classId && g.uid === studentUid);
                    
                    if (existingGrade) {
                        let currentHarian = existingGrade.harian || '';
                        let newHarian = currentHarian ? currentHarian + ', ' + scoreVal : scoreVal;
                        await updateDoc(dbHelper.getDocRef('grades', existingGrade.id), { harian: newHarian });
                    } else {
                        await addDoc(dbHelper.getColRef('grades'), {
                            classId: classId,
                            uid: studentUid,
                            harian: scoreVal.toString(),
                            formatif: null,
                            sumatif: null
                        });
                    }

                    btn.innerHTML = '<i class="fas fa-check"></i> Tersimpan';
                    btn.classList.replace('bg-green-500', 'bg-blue-500');
                    setTimeout(() => { 
                        btn.innerHTML = oldHTML; 
                        btn.classList.replace('bg-blue-500', 'bg-green-500'); 
                    }, 2000);
                    showToast("Nilai berhasil disinkronkan ke Manajemen Nilai!", "success");
                } catch(e) {
                    btn.innerHTML = oldHTML;
                    showToast("Gagal menyimpan nilai", "error");
                }
            }
        };

        window.assignmentFormHTML = () => {
            const myClasses = getMyClasses();
            
            // Validasi Blokir Akses Jika Guru Belum Punya Kelas
            if (myClasses.length === 0) {
                return `<div class="p-8 text-center text-red-500 bg-red-50 dark:bg-red-900/20 rounded-xl border border-red-100 dark:border-red-800"><i class="fas fa-exclamation-triangle text-3xl mb-3"></i><p class="font-bold text-lg">Akses Ditolak</p><p class="text-sm mt-1">Anda belum ditugaskan untuk mengajar di kelas manapun oleh Admin. Silakan hubungi Administrator Pusat untuk penugasan kelas terlebih dahulu.</p></div>`;
            }

            return `
                <form id="add-assignment-form" class="space-y-4">
                    <div>
                        <label class="block text-sm font-medium mb-1">Berlaku Untuk Kelas (Yang Anda Ampu)</label>
                        <select id="a-class" class="w-full p-2.5 border rounded-xl dark:bg-gray-800 outline-none focus:border-orange-500" required>
                            <option value="">-- Pilih Target Kelas --</option>
                            ${myClasses.map(c => `<option value="${c.id}">${escapeHTML(c.name)}</option>`).join('')}
                        </select>
                    </div>
                    <div><label class="block text-sm font-medium mb-1">Judul Ujian/Tugas</label><input type="text" id="a-title" required class="w-full p-2.5 border rounded-xl dark:bg-gray-800 outline-none focus:border-orange-500"></div>
                    <div>
                        <label class="block text-sm font-medium mb-1 flex justify-between items-center">
                            Soal Instruksi
                            <button type="button" onclick="toggleKeyboard('a-desc')" class="text-xs bg-orange-100 text-orange-700 font-bold px-2 py-1 rounded shadow-sm"><i class="fas fa-keyboard"></i> Arab</button>
                        </label>
                        <textarea id="a-desc" rows="4" class="w-full p-3 border rounded-xl dark:bg-gray-800 outline-none focus:border-orange-500 focus:ring-1 focus:ring-orange-500"></textarea>
                    </div>
                    <div>
                        <label class="block text-sm font-medium mb-1">Upload Dokumen Soal (PDF/Docs)</label>
                        <input type="file" id="a-file" class="w-full p-2 border rounded-xl dark:bg-gray-800 dark:border-gray-600 text-sm">
                    </div>
                    <div><label class="block text-sm font-medium mb-1">Batas Pengumpulan Akhir (Deadline)</label><input type="date" id="a-deadline" required class="w-full p-2.5 border rounded-xl dark:bg-gray-800 outline-none focus:border-orange-500"></div>
                    <div class="pt-5 flex justify-end"><button type="submit" class="px-5 py-2.5 bg-orange-500 hover:bg-orange-600 text-white rounded-xl shadow-md font-medium transition">Tugaskan Sekarang</button></div>
                </form>
            `;
        };

        window.saveAssignment = async (e) => {
            e.preventDefault();
            const fileInput = D('a-file');
            const fileName = fileInput.files.length > 0 ? fileInput.files[0].name : '';

            const data = {
                classId: D('a-class').value, title: D('a-title').value, desc: D('a-desc').value, fileName: fileName,
                deadline: D('a-deadline').value, authorId: AppState.user.uid, date: new Date().toISOString(), submissions: []
            };
            closeModal();
            try {
                await addDoc(dbHelper.getColRef('assignments'), data);
                showToast("Berhasil disiarkan langsung ke seluruh siswa target!", "success");
            } catch(e) { showToast("Gagal membagikan tugas.", "error"); }
        };

        // --- MANAJEMEN NILAI (Grades) ---
        const renderGrades = (container) => {
            const role = AppState.user.role;
            const myClasses = getMyClasses();
            const users = AppState.data.users || [];
            const gradesData = AppState.data.grades || [];

            // Selector Kelas
            let html = `
                <div class="mb-6 flex flex-wrap justify-between items-end gap-4">
                    <div>
                        <h2 class="text-xl font-bold flex items-center gap-2"><i class="fas fa-star text-yellow-500"></i> Rekapitulasi Nilai Siswa</h2>
                        <p class="text-sm text-gray-500 mt-1">Kelola Nilai Formatif (Harian) & Sumatif (Ujian) per Kelas</p>
                    </div>
                    ${role === 'guru' ? `
                        <div class="w-full md:w-64">
                            <label class="block text-xs font-bold mb-1 uppercase tracking-wider text-gray-500">Pilih Kelas</label>
                            <select id="grade-class-selector" class="w-full p-2 border rounded-xl dark:bg-gray-800 outline-none focus:border-yellow-500 font-medium" onchange="renderView('grades_view', false, this.value)">
                                <option value="">-- Pilih Ruang Kelas --</option>
                                ${myClasses.map(c => `<option value="${c.id}" ${AppState.currentParam === c.id ? 'selected' : ''}>${escapeHTML(c.name)}</option>`).join('')}
                            </select>
                        </div>
                    ` : ''}
                </div>
            `;

            if (role === 'guru' && AppState.currentParam) {
                // Tampilkan form nilai untuk guru
                const selectedClass = myClasses.find(c => c.id === AppState.currentParam);
                if(selectedClass) {
                    const enrolledStudents = users.filter(u => u.role === 'siswa' && (selectedClass.students || []).includes(u.id));
                    
                    html += `
                        <div class="glass dark:bg-cardDark rounded-2xl overflow-hidden shadow-sm border border-gray-100 dark:border-gray-700">
                            <div class="overflow-x-auto">
                                <table class="w-full text-left text-sm whitespace-nowrap">
                                    <thead class="bg-gray-50/80 dark:bg-gray-800/80 text-gray-600 dark:text-gray-300 font-semibold border-b border-gray-100 dark:border-gray-700">
                                        <tr>
                                            <th class="p-4">Nama Siswa</th>
                                            <th class="p-4 text-center w-48">Nilai Harian (Koma)</th>
                                            <th class="p-4 text-center w-24">Rata Harian</th>
                                            <th class="p-4 text-center w-32">Nilai Formatif</th>
                                            <th class="p-4 text-center w-32">Nilai Sumatif</th>
                                            <th class="p-4 text-center w-32">Aksi</th>
                                        </tr>
                                    </thead>
                                    <tbody class="divide-y divide-gray-100 dark:divide-gray-700">
                                        ${enrolledStudents.map(s => {
                                            // Cari data nilai spesifik (kombinasi classId dan uid)
                                            const sGrade = gradesData.find(g => g.classId === selectedClass.id && g.uid === s.id) || { harian: '', formatif: '', sumatif: '' };
                                            
                                            // Kalkulasi Rata-rata Harian
                                            let avgHarian = '-';
                                            if (sGrade.harian) {
                                                const harianArr = sGrade.harian.split(',').map(x => Number(x.trim())).filter(x => !isNaN(x));
                                                if(harianArr.length > 0) {
                                                    avgHarian = (harianArr.reduce((a,b)=>a+b, 0) / harianArr.length).toFixed(1);
                                                }
                                            }

                                            return `
                                            <tr class="hover:bg-yellow-50/30 dark:hover:bg-yellow-900/10 transition-colors">
                                                <td class="p-4 font-bold text-gray-700 dark:text-gray-200">${escapeHTML(s.name)}</td>
                                                <td class="p-4">
                                                    <input type="text" id="hr-${s.id}" value="${sGrade.harian || ''}" placeholder="80, 85, 90" class="w-full p-2 border rounded-lg text-center font-mono text-sm dark:bg-gray-800 dark:border-gray-600 focus:border-yellow-500 outline-none" title="Pisahkan setiap nilai dengan koma (,)">
                                                </td>
                                                <td class="p-4 text-center font-bold text-yellow-600 dark:text-yellow-400">
                                                    ${avgHarian}
                                                </td>
                                                <td class="p-4">
                                                    <input type="number" id="fmt-${s.id}" value="${sGrade.formatif}" placeholder="0-100" class="w-full p-2 border rounded-lg text-center font-bold dark:bg-gray-800 dark:border-gray-600 focus:border-yellow-500 outline-none">
                                                </td>
                                                <td class="p-4">
                                                    <input type="number" id="smt-${s.id}" value="${sGrade.sumatif}" placeholder="0-100" class="w-full p-2 border rounded-lg text-center font-bold dark:bg-gray-800 dark:border-gray-600 focus:border-yellow-500 outline-none">
                                                </td>
                                                <td class="p-4 text-center">
                                                    <button onclick="saveStudentGrade('${selectedClass.id}', '${s.id}', '${sGrade.id || ''}')" class="px-3 py-1.5 bg-yellow-500 hover:bg-yellow-600 text-white rounded-lg font-bold text-xs shadow-sm transition">
                                                        <i class="fas fa-save"></i> Simpan
                                                    </button>
                                                </td>
                                            </tr>
                                            `;
                                        }).join('')}
                                        ${enrolledStudents.length === 0 ? '<tr><td colspan="6" class="p-8 text-center text-gray-500">Belum ada siswa di kelas ini.</td></tr>' : ''}
                                    </tbody>
                                </table>
                            </div>
                        </div>
                    `;
                }
            } else if (role === 'siswa') {
                // Tampilan untuk Siswa
                html += `
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        ${myClasses.map(c => {
                            const myGrade = gradesData.find(g => g.classId === c.id && g.uid === AppState.user.uid) || { harian: '', formatif: '--', sumatif: '--' };
                            
                            let avgHarian = '-';
                            if (myGrade.harian) {
                                const harianArr = myGrade.harian.split(',').map(x => Number(x.trim())).filter(x => !isNaN(x));
                                if(harianArr.length > 0) avgHarian = (harianArr.reduce((a,b)=>a+b, 0) / harianArr.length).toFixed(1);
                            }

                            return `
                                <div class="glass dark:bg-cardDark p-5 rounded-2xl shadow-sm border border-gray-100 dark:border-gray-700">
                                    <h3 class="font-bold text-lg text-gray-800 dark:text-gray-200 mb-4">${escapeHTML(c.name)}</h3>
                                    
                                    <div class="mb-4 bg-gray-50 dark:bg-gray-800 p-3 rounded-xl border border-gray-200 dark:border-gray-700">
                                        <p class="text-xs font-bold text-gray-500 uppercase tracking-wider mb-2 flex justify-between items-center">
                                            <span>Riwayat Nilai Harian</span>
                                            <span class="text-yellow-600 dark:text-yellow-400">Rata-rata: ${avgHarian}</span>
                                        </p>
                                        <p class="font-mono text-sm text-gray-700 dark:text-gray-300 leading-loose">${myGrade.harian ? myGrade.harian.split(',').map(v => `<span class="inline-block bg-white dark:bg-gray-900 px-2 py-1 rounded shadow-sm mr-1 border border-gray-100 dark:border-gray-600">${v.trim()}</span>`).join('') : '<span class="italic text-gray-400 text-xs">Belum ada data nilai harian</span>'}</p>
                                    </div>

                                    <div class="flex gap-4">
                                        <div class="flex-1 bg-blue-50 dark:bg-blue-900/20 p-4 rounded-xl text-center border border-blue-100 dark:border-blue-800">
                                            <p class="text-xs font-bold text-blue-500 uppercase tracking-wider mb-1">Formatif</p>
                                            <p class="text-3xl font-extrabold text-blue-600 dark:text-blue-400">${myGrade.formatif}</p>
                                        </div>
                                        <div class="flex-1 bg-green-50 dark:bg-green-900/20 p-4 rounded-xl text-center border border-green-100 dark:border-green-800">
                                            <p class="text-xs font-bold text-green-500 uppercase tracking-wider mb-1">Sumatif</p>
                                            <p class="text-3xl font-extrabold text-green-600 dark:text-green-400">${myGrade.sumatif}</p>
                                        </div>
                                    </div>
                                </div>
                            `;
                        }).join('')}
                    </div>
                `;
            } else {
                if (role === 'guru') html += `<div class="p-10 text-center text-gray-500 bg-white dark:bg-cardDark rounded-3xl border-2 border-dashed border-gray-200 dark:border-gray-700"><i class="fas fa-hand-pointer text-4xl mb-3 text-gray-300"></i><p>Silakan pilih kelas pada dropdown di atas untuk mengelola nilai.</p></div>`;
            }

            container.innerHTML = html;
        };

        window.saveStudentGrade = async (classId, studentId, gradeDocId) => {
            const hVal = D(`hr-${studentId}`).value;
            const fVal = D(`fmt-${studentId}`).value;
            const sVal = D(`smt-${studentId}`).value;
            
            const data = {
                classId: classId,
                uid: studentId,
                harian: hVal ? hVal.trim() : null,
                formatif: fVal ? parseInt(fVal) : null,
                sumatif: sVal ? parseInt(sVal) : null
            };

            showToast("Menyimpan nilai...", "info");
            try {
                if (gradeDocId) {
                    await updateDoc(dbHelper.getDocRef('grades', gradeDocId), data);
                } else {
                    await addDoc(dbHelper.getColRef('grades'), data);
                }
                showToast("Nilai berhasil direkam!", "success");
            } catch(e) {
                showToast("Gagal menyimpan nilai.", "error");
            }
        };

        // --- ABSENSI REALTIME ---
        const renderAttendance = (container) => {
            const role = AppState.user.role;
            const att = AppState.data.attendance || [];
            const activeSession = att.find(a => a.status === 'active');
            const closedSessions = att.filter(a => a.status === 'closed' && (role === 'admin' || a.createdBy === AppState.user.uid)).sort((a,b) => new Date(b.date) - new Date(a.date));

            let html = `
                <div class="mb-6">
                    <h2 class="text-xl font-bold flex items-center gap-2"><i class="fas fa-broadcast-tower text-green-500"></i> Radar Presensi Kehadiran</h2>
                    <p class="text-sm text-gray-500 mt-1">Laporan sinkron otomatis ketika siswa melakukan absensi di perangkat mereka.</p>
                </div>
            `;

            if (role === 'guru' || role === 'admin') {
                if (activeSession) {
                    html += `
                        <div class="bg-gradient-to-r from-green-500 to-emerald-500 text-white p-8 rounded-3xl shadow-xl shadow-green-500/20 mb-6 relative overflow-hidden">
                            <i class="fas fa-satellite-dish absolute -right-6 -bottom-6 text-9xl opacity-20 transform -rotate-12"></i>
                            <div class="relative z-10 flex justify-between items-center flex-wrap gap-4">
                                <div>
                                    <div class="flex items-center gap-2 mb-2">
                                        <span class="relative flex h-3 w-3"><span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-white opacity-75"></span><span class="relative inline-flex rounded-full h-3 w-3 bg-white"></span></span>
                                        <span class="bg-white/20 backdrop-blur text-white text-xs font-bold px-3 py-1 rounded-full uppercase tracking-widest border border-white/30">Siaran Sedang Berjalan</span>
                                    </div>
                                    <h3 class="text-3xl font-extrabold tracking-tight">Sistem Merekam...</h3>
                                    <p class="text-green-50 mt-1 opacity-90">Siswa yang menekan tombol kehadiran akan langsung terdata tanpa perlu muat ulang halaman.</p>
                                </div>
                                <button onclick="tutupAbsensi('${activeSession.id}')" class="bg-white text-green-700 hover:bg-green-50 px-6 py-3 rounded-2xl font-extrabold shadow-lg transition-transform hover:scale-105">
                                    <i class="fas fa-stop-circle mr-2"></i> Kunci Sesi
                                </button>
                            </div>
                        </div>
                        
                        <div class="bg-white dark:bg-cardDark rounded-3xl p-6 shadow-sm border border-gray-100 dark:border-gray-700 relative mb-8">
                            <div class="flex items-center justify-between mb-5 pb-4 border-b border-gray-100 dark:border-gray-700">
                                <h4 class="font-bold text-lg text-gray-800 dark:text-gray-100"><i class="fas fa-list-ol text-green-500 mr-2"></i> Aliran Log Kehadiran</h4>
                                <span class="bg-green-100 text-green-700 px-3 py-1 rounded-full text-xs font-bold">${activeSession.records ? activeSession.records.length : 0} Entri Masuk</span>
                            </div>
                            
                            <div class="space-y-3 max-h-96 overflow-y-auto custom-scrollbar pr-2">
                                ${(activeSession.records || []).slice().reverse().map((r, i) => `
                                    <div class="p-4 flex justify-between items-center bg-gray-50 dark:bg-gray-800/50 rounded-xl border-l-4 ${r.status==='Hadir'?'border-green-500':(r.status==='Izin'?'border-blue-500':'border-yellow-500')} animate-[slideIn_0.3s_ease-out_forwards]">
                                        <div class="flex items-center gap-4">
                                            <div class="w-8 h-8 rounded-full bg-white dark:bg-gray-700 shadow-sm flex items-center justify-center font-bold text-gray-500 text-xs">${activeSession.records.length - i}</div>
                                            <span class="font-bold text-gray-800 dark:text-gray-200">${escapeHTML(r.name)}</span>
                                        </div>
                                        <div class="flex flex-col items-end">
                                            <span class="text-xs font-extrabold uppercase px-2 py-0.5 rounded ${r.status==='Hadir'?'text-green-600 bg-green-100':(r.status==='Izin'?'text-blue-600 bg-blue-100':'text-yellow-600 bg-yellow-100')}">${r.status}</span>
                                            <span class="text-[10px] text-gray-400 mt-1"><i class="far fa-clock"></i> Pukul ${r.time}</span>
                                        </div>
                                    </div>
                                `).join('')}
                                ${!(activeSession.records && activeSession.records.length > 0) ? `
                                    <div class="flex flex-col items-center justify-center py-10 opacity-50">
                                        <i class="fas fa-satellite-dish text-6xl text-gray-300 dark:text-gray-600 mb-4 animate-pulse"></i>
                                        <p class="text-sm font-medium">Menunggu data sinyal presensi dari gawai siswa...</p>
                                    </div>
                                ` : ''}
                            </div>
                        </div>
                    `;
                } else {
                    html += `
                        <div class="bg-white dark:bg-cardDark p-10 rounded-3xl text-center shadow-sm border-2 border-dashed border-gray-200 dark:border-gray-700 max-w-2xl mx-auto mt-6 mb-10 relative overflow-hidden">
                            <div class="w-20 h-20 bg-green-50 dark:bg-green-900/20 text-green-500 rounded-full flex items-center justify-center text-4xl mx-auto mb-5">
                                <i class="fas fa-play"></i>
                            </div>
                            <h3 class="font-extrabold text-2xl text-gray-800 dark:text-gray-100 mb-2">Pusat Kendali Presensi Mati</h3>
                            <p class="text-gray-500 text-sm mb-8 leading-relaxed max-w-md mx-auto">Klik tombol di bawah ini jika Anda ingin memulai pendataan siswa di kelas secara langsung dan seketika (realtime).</p>
                            <button onclick="bukaAbsensi()" class="bg-gradient-to-r from-green-500 to-emerald-500 text-white px-8 py-4 rounded-2xl font-bold shadow-xl shadow-green-500/30 hover:scale-105 transition-transform text-lg flex items-center gap-3 mx-auto">
                                <i class="fas fa-power-off"></i> Mulai Penyiaran Sesi
                            </button>
                        </div>
                    `;
                }
                
                html += `
                    <div class="mt-4 pt-8 border-t border-gray-200 dark:border-gray-700">
                        <h3 class="font-bold text-lg mb-5 flex items-center gap-2"><i class="fas fa-history text-gray-400"></i> Riwayat & Laporan Presensi Kelas</h3>
                        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4">
                            ${closedSessions.map(s => `
                                <div class="bg-white dark:bg-cardDark p-5 rounded-2xl shadow-sm border border-gray-100 dark:border-gray-700 flex flex-col hover:shadow-md transition-shadow">
                                    <div class="flex justify-between items-center mb-3">
                                        <span class="bg-gray-100 text-gray-600 dark:bg-gray-800 dark:text-gray-400 px-2 py-0.5 rounded text-[10px] font-bold uppercase tracking-wider">Sesi Ditutup</span>
                                        <span class="text-xs font-medium text-gray-500"><i class="far fa-calendar-alt"></i> ${new Date(s.date).toLocaleDateString('id-ID')}</span>
                                    </div>
                                    <div class="mb-4">
                                        <p class="font-bold text-gray-800 dark:text-gray-100 text-lg">${s.records ? s.records.filter(r=>r.status==='Hadir').length : 0} Hadir</p>
                                        <p class="text-xs text-gray-500">Total partisipan: ${s.records ? s.records.length : 0} siswa</p>
                                    </div>
                                    <button onclick="exportAbsensiCSV('${s.id}')" class="mt-auto px-4 py-2.5 bg-green-50 text-green-700 hover:bg-green-100 dark:bg-green-900/30 dark:text-green-400 dark:hover:bg-green-900/50 font-bold text-xs rounded-xl transition flex items-center justify-center gap-2 cursor-pointer w-full">
                                        <i class="fas fa-file-csv text-base"></i> Export Excel (CSV)
                                    </button>
                                </div>
                            `).join('')}
                            ${closedSessions.length === 0 ? '<div class="col-span-full p-8 text-center text-gray-400 bg-gray-50 dark:bg-gray-800 rounded-2xl border border-dashed border-gray-300 dark:border-gray-700">Belum ada riwayat sesi absensi yang tersimpan.</div>' : ''}
                        </div>
                    </div>
                `;
            } else if (role === 'siswa') {
                if (activeSession) {
                    const myRecord = (activeSession.records || []).find(r => r.uid === AppState.user.uid);
                    if(myRecord) {
                         html += `
                            <div class="bg-green-50 dark:bg-green-900/10 text-green-700 dark:text-green-400 p-8 rounded-3xl text-center border-2 border-green-200 dark:border-green-800/50 mt-10 shadow-sm max-w-md mx-auto">
                                <i class="fas fa-check-circle text-6xl mb-4 text-green-500 animate-bounce"></i>
                                <h3 class="font-extrabold text-xl mb-1">Berhasil Disinkronisasi!</h3>
                                <p class="text-sm">Laporan terkirim ke meja guru: <b class="bg-green-200 dark:bg-green-800 px-2 py-0.5 rounded ml-1">${myRecord.status}</b></p>
                            </div>
                         `;
                    } else {
                        html += `
                            <div class="bg-white dark:bg-cardDark p-8 rounded-3xl text-center border border-primary/20 shadow-xl max-w-lg mx-auto relative mt-10">
                                <div class="absolute inset-0 bg-gradient-to-t from-primary/5 to-transparent rounded-3xl pointer-events-none"></div>
                                <div class="flex justify-center mb-4">
                                    <span class="flex items-center gap-2 bg-red-100 text-red-600 px-3 py-1 rounded-full text-xs font-bold animate-pulse"><i class="fas fa-circle text-[8px]"></i> WAKTU BERJALAN</span>
                                </div>
                                <h3 class="font-extrabold text-2xl mb-2 text-gray-800 dark:text-gray-100">Panggilan Presensi!</h3>
                                <p class="text-sm text-gray-500 mb-8">Guru sedang mengabsen kelas Anda sekarang. Segera klik konfirmasi status kehadiran Anda.</p>
                                
                                <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 relative z-10">
                                    <button onclick="isiAbsensi('${activeSession.id}', 'Hadir')" class="flex flex-col items-center justify-center p-5 border-2 border-green-500 rounded-2xl bg-white dark:bg-gray-800 text-green-600 hover:bg-green-50 dark:hover:bg-green-900/20 transition-all hover:scale-105 group shadow-sm">
                                        <i class="fas fa-hand-sparkles text-3xl mb-2 group-hover:-translate-y-1 transition-transform"></i>
                                        <span class="font-extrabold text-sm">Hadir</span>
                                    </button>
                                    <button onclick="isiAbsensi('${activeSession.id}', 'Izin')" class="flex flex-col items-center justify-center p-5 border-2 border-blue-500 rounded-2xl bg-white dark:bg-gray-800 text-blue-600 hover:bg-blue-50 dark:hover:bg-blue-900/20 transition-all hover:scale-105 group shadow-sm">
                                        <i class="fas fa-envelope-open-text text-3xl mb-2 group-hover:-translate-y-1 transition-transform"></i>
                                        <span class="font-extrabold text-sm">Izin</span>
                                    </button>
                                    <button onclick="isiAbsensi('${activeSession.id}', 'Sakit')" class="flex flex-col items-center justify-center p-5 border-2 border-yellow-500 rounded-2xl bg-white dark:bg-gray-800 text-yellow-600 hover:bg-yellow-50 dark:hover:bg-yellow-900/20 transition-all hover:scale-105 group shadow-sm">
                                        <i class="fas fa-procedures text-3xl mb-2 group-hover:-translate-y-1 transition-transform"></i>
                                        <span class="font-extrabold text-sm">Sakit</span>
                                    </button>
                                </div>
                            </div>
                        `;
                    }
                } else {
                     html += `
                        <div class="bg-gray-50 dark:bg-gray-800 p-10 rounded-3xl text-center max-w-lg mx-auto mt-10 border border-gray-100 dark:border-gray-700">
                            <i class="fas fa-mug-hot text-5xl text-gray-300 dark:text-gray-600 mb-4"></i>
                            <h3 class="font-bold text-lg mb-1 text-gray-700 dark:text-gray-300">Belum Ada Panggilan</h3>
                            <p class="text-gray-500 text-sm">Silakan tunggu, guru pengampu belum menyalakan sesi pendaftaran hadir.</p>
                        </div>
                     `;
                }
            }
            container.innerHTML = html;
        };

        window.bukaAbsensi = async () => {
            try {
                await addDoc(dbHelper.getColRef('attendance'), { status: 'active', date: new Date().toISOString(), records: [], createdBy: AppState.user.uid });
                showToast("Berhasil! Sinyal presensi telah disiarkan ke dashboard siswa.", "success");
            } catch(e) { showToast("Gagal memulai sesi", "error"); }
        };
        window.tutupAbsensi = async (id) => {
            try {
                await updateDoc(dbHelper.getDocRef('attendance', id), { status: 'closed' }); 
                showToast("Kunci presensi aktif. Pendataan dihentikan.", "info");
            } catch(e) {}
        };
        window.isiAbsensi = async (sessionId, status) => {
            const sessionData = AppState.data.attendance.find(a => a.id === sessionId);
            if(sessionData) {
                showToast("Sedang mengirim sinyal kehadiran...", "info");
                const newRecord = { uid: AppState.user.uid, name: AppState.user.name, status: status, time: new Date().toLocaleTimeString('id-ID', {hour: '2-digit', minute:'2-digit'}) };
                try {
                    await updateDoc(dbHelper.getDocRef('attendance', sessionId), { records: [...(sessionData.records || []), newRecord] });
                    showToast(`Sistem menerima input: ${status}`, "success");
                } catch(e) { showToast("Gagal menyinkronkan data.", "error"); }
            }
        };

        window.exportAbsensiCSV = (sessionId) => {
            const session = AppState.data.attendance.find(a => a.id === sessionId);
            if(!session || !session.records || session.records.length === 0) {
                showToast("Tidak ada data presensi yang bisa diekspor pada sesi ini.", "warning"); return;
            }
            
            let csv = "Nama Lengkap Siswa,Status Kehadiran,Waktu Input\n";
            session.records.forEach(r => {
                csv += `"${r.name}","${r.status}","${r.time}"\n`;
            });
            
            const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
            const link = document.createElement("a");
            const url = URL.createObjectURL(blob);
            link.setAttribute("href", url);
            const dateStr = new Date(session.date).toISOString().split('T')[0];
            link.setAttribute("download", `Rekap_Absensi_LMS_${dateStr}.csv`);
            link.style.visibility = 'hidden';
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            
            showToast("Berhasil mendownload format Excel (CSV).", "success");
        };

        // --- SISTEM CHAT (Pesan & Diskusi) ---
        window.setActiveChat = (chatId) => {
            // Gunakan render subview agar tidak terstack di history berlebihan
            executeRender('chat', true, chatId, true); 
        };

        const renderChat = (container) => {
            const myUid = AppState.user.uid;
            const users = AppState.data.users || [];
            
            // Atur active chat dari param (jika ada), kalau null gunakan default
            if(AppState.currentParam) AppState.activeChat = AppState.currentParam;
            else if (!AppState.activeChat) AppState.activeChat = 'group';

            // Susun Daftar Kontak
            const sysAdmin = { id: 'admin_sys_id', name: 'Admin Pusat (Sekolah)', role: 'admin' };
            let contacts = [sysAdmin, ...users].filter(u => u.id !== myUid);
            
            const getChatName = (id) => {
                if(id === 'group') return 'Grup Diskusi Global';
                const u = contacts.find(x => x.id === id);
                return u ? u.name : 'Pengguna Tidak Diketahui';
            };

            const getChatRole = (id) => {
                if(id === 'group') return 'Semua Anggota';
                const u = contacts.find(x => x.id === id);
                return u ? u.role : '';
            };

            // Filter pesan
            const allMessages = AppState.data.messages || [];
            const activeMsgs = allMessages.filter(m => {
                if (AppState.activeChat === 'group') return m.receiverId === 'group';
                return (m.senderId === myUid && m.receiverId === AppState.activeChat) || 
                       (m.senderId === AppState.activeChat && m.receiverId === myUid);
            }).sort((a,b) => new Date(a.timestamp) - new Date(b.timestamp));

            let html = `
                <div class="h-[75vh] flex flex-col md:flex-row gap-4 -m-2 md:-m-4">
                    
                    <!-- Sidebar Kontak -->
                    <div class="w-full md:w-1/3 lg:w-1/4 bg-white dark:bg-cardDark rounded-2xl flex flex-col h-48 md:h-full border border-gray-100 dark:border-gray-700 shadow-sm shrink-0">
                        <div class="p-4 border-b border-gray-100 dark:border-gray-700">
                            <h3 class="font-bold text-lg"><i class="fas fa-users text-primary mr-2"></i> Kontak Pesan</h3>
                        </div>
                        <div class="flex-1 overflow-y-auto custom-scrollbar p-2 space-y-1">
                            <!-- Grup Utama -->
                            <div onclick="setActiveChat('group')" class="p-3 rounded-xl cursor-pointer transition-colors flex items-center gap-3 ${AppState.activeChat === 'group' ? 'bg-primary/10 border border-primary/20' : 'hover:bg-gray-50 dark:hover:bg-gray-800'}">
                                <div class="w-10 h-10 rounded-full bg-gradient-to-r from-primary to-secondary text-white flex items-center justify-center shrink-0"><i class="fas fa-globe"></i></div>
                                <div class="overflow-hidden">
                                    <p class="font-bold text-sm text-gray-800 dark:text-gray-100 truncate">Grup Diskusi Global</p>
                                    <p class="text-xs text-gray-500 truncate">Papan informasi & obrolan umum</p>
                                </div>
                            </div>
                            <hr class="border-gray-100 dark:border-gray-700 my-2">
                            <!-- Daftar Individu -->
                            <p class="text-[10px] font-bold text-gray-400 px-3 uppercase tracking-wider mb-1 mt-2">Chat Pribadi (Japri)</p>
                            ${contacts.map(c => `
                                <div onclick="setActiveChat('${c.id}')" class="p-3 rounded-xl cursor-pointer transition-colors flex items-center gap-3 ${AppState.activeChat === c.id ? 'bg-primary/10 border border-primary/20' : 'hover:bg-gray-50 dark:hover:bg-gray-800'}">
                                    <div class="w-10 h-10 rounded-full flex items-center justify-center font-bold text-xs shrink-0 text-white ${c.role==='admin'?'bg-purple-500':(c.role==='guru'?'bg-blue-500':'bg-green-500')}">${c.name.charAt(0).toUpperCase()}</div>
                                    <div class="overflow-hidden">
                                        <p class="font-bold text-sm text-gray-800 dark:text-gray-100 truncate">${escapeHTML(c.name)}</p>
                                        <p class="text-[10px] bg-gray-100 dark:bg-gray-700 text-gray-600 dark:text-gray-400 px-2 rounded-full w-max uppercase mt-0.5">${c.role}</p>
                                    </div>
                                </div>
                            `).join('')}
                        </div>
                    </div>

                    <!-- Area Chat Utama -->
                    <div class="flex-1 bg-white dark:bg-cardDark rounded-2xl flex flex-col h-[50vh] md:h-full border border-gray-100 dark:border-gray-700 shadow-sm">
                        <!-- Chat Header -->
                        <div class="h-16 border-b border-gray-100 dark:border-gray-700 flex items-center px-5 gap-4 shrink-0 bg-gray-50 dark:bg-gray-800/50 rounded-t-2xl">
                            <div class="w-10 h-10 rounded-full bg-gray-200 dark:bg-gray-700 flex items-center justify-center text-gray-500"><i class="${AppState.activeChat === 'group' ? 'fas fa-globe' : 'fas fa-user'}"></i></div>
                            <div>
                                <h3 class="font-bold text-gray-800 dark:text-gray-100">${getChatName(AppState.activeChat)}</h3>
                                <p class="text-xs text-primary font-medium uppercase tracking-wider">${getChatRole(AppState.activeChat)}</p>
                            </div>
                        </div>

                        <!-- Ruang Pesan -->
                        <div id="chat-messages-box" class="flex-1 overflow-y-auto p-5 space-y-4 bg-[url('https://www.transparenttextures.com/patterns/arabesque.png')] dark:bg-none relative custom-scrollbar">
                            ${activeMsgs.map(m => {
                                const isMe = m.senderId === myUid;
                                return `
                                <div class="flex flex-col ${isMe ? 'items-end' : 'items-start'} msg-animate">
                                    <div class="flex items-end gap-2 max-w-[85%] ${isMe ? 'flex-row-reverse' : 'flex-row'}">
                                        <div class="w-8 h-8 rounded-full flex items-center justify-center text-[10px] font-bold shrink-0 shadow-sm text-white ${isMe ? 'bg-primary' : (m.senderRole==='admin'?'bg-purple-500':(m.senderRole==='guru'?'bg-blue-500':'bg-green-500'))}">
                                            ${m.senderName.charAt(0).toUpperCase()}
                                        </div>
                                        <div class="flex flex-col ${isMe ? 'items-end' : 'items-start'}">
                                            ${!isMe && AppState.activeChat === 'group' ? `<span class="text-[10px] text-gray-500 font-bold ml-1 mb-0.5">${escapeHTML(m.senderName)} <span class="uppercase border border-gray-200 dark:border-gray-600 px-1 rounded ml-1">${m.senderRole}</span></span>` : ''}
                                            <div class="p-3 rounded-2xl text-sm shadow-sm ${isMe ? 'bg-gradient-to-tr from-primary to-secondary text-white rounded-br-sm' : 'bg-white dark:bg-gray-700 border border-gray-100 dark:border-gray-600 text-gray-800 dark:text-gray-200 rounded-bl-sm'} ${/[\u0600-\u06FF]/.test(m.text) ? 'font-arabic text-xl' : ''}">
                                                ${escapeHTML(m.text)}
                                            </div>
                                        </div>
                                    </div>
                                    <span class="text-[9px] text-gray-400 mt-1 mx-10">${new Date(m.timestamp).toLocaleTimeString('id-ID', {hour:'2-digit', minute:'2-digit'})}</span>
                                </div>
                                `;
                            }).join('')}
                            ${activeMsgs.length === 0 ? `<div class="h-full flex flex-col items-center justify-center text-gray-400 opacity-50"><i class="far fa-comments text-5xl mb-3"></i><p class="text-sm">Belum ada percakapan. Mulai sapa sekarang!</p></div>` : ''}
                        </div>

                        <!-- Chat Input Form -->
                        <div class="p-4 bg-white dark:bg-gray-800 border-t border-gray-100 dark:border-gray-700 rounded-b-2xl shrink-0">
                            <form id="chat-form" onsubmit="sendChatMessage(event)" class="flex items-end gap-2 relative">
                                <button type="button" onclick="toggleKeyboard('chat-input')" class="p-3 text-gray-400 hover:text-primary transition-colors h-[46px] rounded-xl bg-gray-50 dark:bg-gray-700" title="Keyboard Arab"><i class="fas fa-keyboard text-lg"></i></button>
                                <textarea id="chat-input" rows="1" required placeholder="Tulis pesan..." class="flex-1 p-3 border border-gray-200 dark:border-gray-600 rounded-xl outline-none focus:border-primary focus:ring-1 focus:ring-primary dark:bg-gray-700 resize-none max-h-32 min-h-[46px] transition-all custom-scrollbar"></textarea>
                                <button type="submit" class="w-12 h-[46px] bg-primary hover:bg-secondary text-white rounded-xl flex items-center justify-center shadow-md transition-colors shrink-0">
                                    <i class="fas fa-paper-plane"></i>
                                </button>
                            </form>
                        </div>
                    </div>
                </div>
            `;
            container.innerHTML = html;

            setTimeout(() => {
                const chatBox = D('chat-messages-box');
                if(chatBox) chatBox.scrollTop = chatBox.scrollHeight;
                
                const input = D('chat-input');
                if(input) {
                    input.addEventListener('keydown', function(e) {
                        if (e.key === 'Enter' && !e.shiftKey) { e.preventDefault(); sendChatMessage(new Event('submit')); }
                    });
                }
            }, 50);
        };

        window.sendChatMessage = async (e) => {
            e.preventDefault();
            const input = D('chat-input');
            const text = input.value.trim();
            if(!text) return;

            const msgData = {
                senderId: AppState.user.uid,
                senderName: AppState.user.name,
                senderRole: AppState.user.role,
                receiverId: AppState.activeChat,
                text: text,
                timestamp: new Date().toISOString()
            };

            const chatBox = D('chat-messages-box');
            if(chatBox) {
                if(chatBox.innerHTML.includes('Belum ada percakapan')) chatBox.innerHTML = '';
                chatBox.innerHTML += `
                    <div class="flex flex-col items-end msg-animate opacity-50">
                        <div class="flex items-end gap-2 max-w-[85%] flex-row-reverse">
                            <div class="w-8 h-8 rounded-full flex items-center justify-center text-[10px] font-bold shrink-0 shadow-sm text-white bg-primary">${AppState.user.name.charAt(0).toUpperCase()}</div>
                            <div class="p-3 rounded-2xl text-sm shadow-sm bg-gradient-to-tr from-primary to-secondary text-white rounded-br-sm ${/[\u0600-\u06FF]/.test(text) ? 'font-arabic text-xl' : ''}">
                                ${escapeHTML(text)}
                            </div>
                        </div>
                        <span class="text-[9px] text-gray-400 mt-1 mx-10">Mengirim...</span>
                    </div>
                `;
                chatBox.scrollTop = chatBox.scrollHeight;
            }
            
            input.value = '';
            try { await addDoc(dbHelper.getColRef('messages'), msgData); } 
            catch(e) { showToast("Gagal mengirim pesan.", "error"); }
        };

        // --- ARABIC VIRTUAL KEYBOARD ---
        window.toggleKeyboard = (inputId = null) => {
            const kb = D('arabic-keyboard');
            if (inputId) {
                AppState.activeTargetInput = D(inputId);
                kb.classList.remove('translate-y-full', 'hidden-app');
                AppState.activeTargetInput.classList.add('font-arabic');
                AppState.activeTargetInput.dir = 'rtl';
            } else {
                kb.classList.add('translate-y-full');
                setTimeout(() => kb.classList.add('hidden-app'), 300);
                AppState.activeTargetInput = null;
            }
        };

        window.insertChar = (char) => {
            const el = AppState.activeTargetInput;
            if (el) {
                const start = el.selectionStart, end = el.selectionEnd;
                el.value = el.value.substring(0, start) + char + el.value.substring(end);
                el.selectionStart = el.selectionEnd = start + char.length; el.focus();
            }
        };

        // --- MODAL SYSTEM ---
        window.openModal = (title, contentHTML, onSubmit) => {
            D('modal-title').innerText = title; D('modal-content').innerHTML = contentHTML; show('form-modal');
            setTimeout(() => { const form = D('modal-content').querySelector('form'); if (form && onSubmit) form.onsubmit = onSubmit; }, 50);
        };
        window.closeModal = () => hide('form-modal');

        // ============================================================================
        // GEMINI AI INTEGRATION (LLM)
        // ============================================================================
        
        window.callGeminiAPI = async (promptText, systemPrompt = "") => {
            const apiKey = ""; // API Key disuntikkan secara dinamis oleh Canvas environment
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${apiKey}`;
            
            const payload = {
                contents: [{ parts: [{ text: promptText }] }]
            };

            if (systemPrompt) {
                payload.systemInstruction = { parts: [{ text: systemPrompt }] };
            }

            try {
                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });
                const result = await response.json();
                if (result.candidates && result.candidates[0].content && result.candidates[0].content.parts) {
                    return result.candidates[0].content.parts[0].text;
                }
                throw new Error("Format respons AI tidak dikenali.");
            } catch (error) {
                console.error("Gemini API Error:", error);
                return "Maaf, terjadi kesalahan saat menghubungi server AI. Pastikan koneksi stabil atau coba beberapa saat lagi.";
            }
        };

        // Fitur 1: AI Chat Tutor Global
        window.toggleAITutor = () => {
            const modal = D('ai-tutor-modal');
            if(modal.classList.contains('hidden-app')) {
                modal.classList.remove('hidden-app');
            } else {
                modal.classList.add('hidden-app');
            }
        };

        window.sendAITutor = async (e) => {
            e.preventDefault();
            const input = D('ai-chat-input');
            const message = input.value.trim();
            if(!message) return;

            const chatBox = D('ai-chat-box');
            // Tambahkan pesan User
            chatBox.innerHTML += `
                <div class="flex items-start gap-2 max-w-[90%] self-end flex-row-reverse ml-auto">
                    <div class="w-6 h-6 rounded-full bg-blue-500 text-white flex items-center justify-center shrink-0 text-xs"><i class="fas fa-user"></i></div>
                    <div class="p-2.5 rounded-xl bg-blue-500 text-white shadow-sm">${escapeHTML(message)}</div>
                </div>
            `;
            input.value = '';
            
            // Tambahkan indicator loading AI
            const loadingId = 'ai-load-' + Date.now();
            chatBox.innerHTML += `
                <div id="${loadingId}" class="flex items-start gap-2 max-w-[90%]">
                    <div class="w-6 h-6 rounded-full bg-purple-500 text-white flex items-center justify-center shrink-0 text-xs"><i class="fas fa-robot"></i></div>
                    <div class="p-2.5 rounded-xl bg-white dark:bg-gray-800 border border-gray-100 dark:border-gray-700 shadow-sm text-gray-400 italic">Berpikir...</div>
                </div>
            `;
            chatBox.scrollTop = chatBox.scrollHeight;

            const sysInstruction = "Anda adalah Ustadz/Ustadzah AI, asisten virtual LMS Pendidikan Bahasa Arab. Jawablah pertanyaan seputar terjemahan, nahwu, sharaf, atau konsep bahasa Arab dengan bahasa Indonesia yang ramah, ringkas, jelas, dan edukatif.";
            const responseText = await window.callGeminiAPI(message, sysInstruction);

            const loadEl = D(loadingId);
            if(loadEl) {
                // Menampilkan teks respons. Mengonversi baris baru menjadi tag <br> untuk HTML
                const formattedResponse = escapeHTML(responseText).replace(/\n/g, '<br>');
                loadEl.innerHTML = `
                    <div class="w-6 h-6 rounded-full bg-purple-500 text-white flex items-center justify-center shrink-0 text-xs"><i class="fas fa-robot"></i></div>
                    <div class="p-2.5 rounded-xl bg-white dark:bg-gray-800 border border-gray-100 dark:border-gray-700 shadow-sm text-gray-700 dark:text-gray-300 ${/[\u0600-\u06FF]/.test(responseText) ? 'font-arabic text-lg' : ''}">${formattedResponse}</div>
                `;
                chatBox.scrollTop = chatBox.scrollHeight;
            }
        };

        // Fitur 2: AI Generate Materi
        window.generateMateriAI = async () => {
            const titleInput = D('m-title');
            const subjectSelect = D('m-subject');
            const descArea = D('m-desc');

            if (!titleInput.value.trim()) {
                showToast("Isi kolom Judul/Topik Materi terlebih dahulu agar AI bisa menyesuaikan konteks.", "warning");
                titleInput.focus();
                return;
            }

            showToast("AI sedang menyusun draf materi pembelajaran...", "info");
            const btn = document.querySelector('button[onclick="generateMateriAI()"]');
            const originalText = btn.innerHTML;
            btn.innerHTML = `<i class="fas fa-spinner fa-spin"></i> Memproses...`;
            btn.disabled = true;

            const prompt = `Buatkan materi pelajaran Bahasa Arab yang komprehensif namun padat mengenai mata pelajaran '${subjectSelect.value}' dengan topik/judul '${titleInput.value}'. Sediakan teks Arab (berharakat lengkap) untuk contoh atau penjelasan, lalu sertakan terjemahan dan penjelasan singkatnya dalam bahasa Indonesia. Jangan gunakan formatting markdown bold/italic yang rumit, cukup teks biasa yang rapi.`;
            const sysInstruction = "Anda adalah pakar pembuat kurikulum Bahasa Arab. Hasilkan materi edukatif yang jelas dan langsung dapat disalin ke form LMS.";

            const response = await window.callGeminiAPI(prompt, sysInstruction);
            
            descArea.value = response;
            
            btn.innerHTML = originalText;
            btn.disabled = false;
            showToast("Draf AI berhasil dimuat! Anda dapat mengeditnya jika perlu.", "success");
        };

        // Fitur 3: AI Submission Grader
        window.evaluateAnswerAI = async (assignmentId, studentUid, answer, assignmentTitle) => {
            const feedbackDiv = D(`ai-feedback-${assignmentId}-${studentUid}`);
            const btn = event.currentTarget;
            
            if (!feedbackDiv) return;
            
            showToast("AI sedang menganalisis jawaban siswa...", "info");
            const oldHtml = btn.innerHTML;
            btn.innerHTML = `<i class="fas fa-spinner fa-spin"></i> Menganalisis...`;
            btn.disabled = true;
            feedbackDiv.classList.remove('hidden-app');
            feedbackDiv.innerHTML = "<em>Memeriksa struktur bahasa dan keakuratan jawaban...</em>";

            const prompt = `Berikut adalah jawaban seorang siswa untuk tugas Bahasa Arab dengan judul "${assignmentTitle}".
            
            Jawaban Siswa: 
            "${answer}"
            
            Tolong lakukan evaluasi:
            1. Periksa apakah ada kesalahan tata bahasa (Nahwu/Sharaf) atau kosakata, serta ejaannya jika menggunakan teks Arab.
            2. Berikan kritik dan saran membangun maksimal 3 kalimat.
            3. Di akhir, berikan saran rentang nilai dari 0 hingga 100 (misalnya "Saran Nilai: 85").`;
            
            const sysInstruction = "Anda adalah guru penilai tugas bahasa Arab. Berikan ulasan singkat, ramah, jujur dan objektif, fokus pada kebenaran tulisan/jawaban yang diberikan siswa.";

            const response = await window.callGeminiAPI(prompt, sysInstruction);

            feedbackDiv.innerHTML = `<b><i class="fas fa-robot"></i> Laporan Asisten AI:</b><br>${escapeHTML(response).replace(/\n/g, '<br>')}`;
            
            btn.innerHTML = oldHtml;
            btn.disabled = false;
        };

        // Style untuk animasi Absensi realtime khusus
        const style = document.createElement('style');
        style.innerHTML = `@keyframes slideIn { from { opacity: 0; transform: translateX(20px); } to { opacity: 1; transform: translateX(0); } }`;
        document.head.appendChild(style);

        document.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>
