<!DOCTYPE html>
<html lang="id" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Proyek Blog Interaktif | Laravel, Filament, Livewire</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    
    <!-- Chosen Palette: Warm Neutrals (Tailwind Stone) -->
    <!-- Application Structure Plan: Desain aplikasi ini menggunakan struktur 'Dashboard Hub' yang dibagi menjadi beberapa bagian tematik (Ringkasan, Fitur, Teknologi, Instalasi). Struktur ini dipilih untuk memfasilitasi eksplorasi non-linear, memungkinkan pengguna dengan kebutuhan berbeda (misalnya, developer vs. manajer) untuk langsung melompat ke bagian yang relevan melalui navigasi yang jelas. Alur pengguna didesain untuk menjadi interaktif, mengubah daftar statis menjadi elemen yang dapat diklik dan panduan langkah-demi-langkah untuk meningkatkan pemahaman dan keterlibatan. -->
    <!-- Visualization & Content Choices: 
        - Ringkasan: Kartu statistik (HTML/CSS) untuk memberikan gambaran tingkat tinggi.
        - Fitur: Layout dua kolom dengan daftar interaktif (JS) dan visualisasi diagram donat (Chart.js) untuk membandingkan cakupan fitur. Tujuannya adalah mengubah daftar panjang menjadi pengalaman eksplorasi yang menarik.
        - Teknologi: Grid visual (HTML/Tailwind) dengan tooltip saat di-hover (JS) untuk menyajikan tumpukan teknologi secara cepat dan menarik.
        - Instalasi: Wizard langkah-demi-langkah (JS) dengan tombol 'copy-to-clipboard' untuk memandu pengguna melalui proses teknis yang kompleks secara terstruktur dan fungsional.
        - Semua pilihan ini dibuat untuk menyajikan konten README yang padat teks menjadi format yang lebih mudah dicerna dan interaktif tanpa menggunakan SVG atau Mermaid.
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f5f5f4; /* stone-100 */
        }
        .chart-container {
            position: relative;
            margin: auto;
            height: 320px;
            width: 100%;
            max-width: 320px;
        }
        .nav-link {
            transition: color 0.3s ease, border-bottom-color 0.3s ease;
            border-bottom: 2px solid transparent;
        }
        .nav-link:hover, .nav-link.active {
            color: #16a34a; /* green-600 */
            border-bottom-color: #16a34a; /* green-600 */
        }
        .feature-item.active {
            background-color: #dcfce7; /* green-100 */
            color: #15803d; /* green-700 */
            font-weight: 600;
        }
        .code-block {
            position: relative;
        }
        .copy-button {
            position: absolute;
            top: 0.5rem;
            right: 0.5rem;
            background-color: #44403c; /* stone-700 */
            color: #e7e5e4; /* stone-200 */
            border: none;
            padding: 0.25rem 0.5rem;
            border-radius: 0.25rem;
            cursor: pointer;
            opacity: 0.5;
            transition: opacity 0.2s;
        }
        .code-block:hover .copy-button {
            opacity: 1;
        }
    </style>

</head>
<body class="text-stone-800 antialiased">

    <header id="header" class="bg-white/80 backdrop-blur-lg sticky top-0 z-50 shadow-sm">
        <nav class="container mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <div class="flex-shrink-0">
                    <a href="#" class="text-xl font-bold text-stone-900">🚀 Proyek Blog Modern</a>
                </div>
                <div class="hidden md:block">
                    <div class="ml-10 flex items-baseline space-x-4">
                        <a href="#overview" class="nav-link px-3 py-2 rounded-md text-sm font-medium text-stone-600">Ringkasan</a>
                        <a href="#features" class="nav-link px-3 py-2 rounded-md text-sm font-medium text-stone-600">Fitur</a>
                        <a href="#tech-stack" class="nav-link px-3 py-2 rounded-md text-sm font-medium text-stone-600">Teknologi</a>
                        <a href="#installation" class="nav-link px-3 py-2 rounded-md text-sm font-medium text-stone-600">Instalasi</a>
                    </div>
                </div>
                 <div class="md:hidden">
                    <button id="mobile-menu-button" class="inline-flex items-center justify-center p-2 rounded-md text-stone-500 hover:text-stone-700 hover:bg-stone-200 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-stone-100 focus:ring-green-500">
                        <span class="sr-only">Buka menu</span>
                        <span id="menu-icon-open">☰</span>
                        <span id="menu-icon-close" class="hidden">✕</span>
                    </button>
                </div>
            </div>
             <div id="mobile-menu" class="hidden md:hidden pb-3">
                <a href="#overview" class="mobile-nav-link block nav-link px-3 py-2 rounded-md text-base font-medium text-stone-600">Ringkasan</a>
                <a href="#features" class="mobile-nav-link block nav-link px-3 py-2 rounded-md text-base font-medium text-stone-600">Fitur</a>
                <a href="#tech-stack" class="mobile-nav-link block nav-link px-3 py-2 rounded-md text-base font-medium text-stone-600">Teknologi</a>
                <a href="#installation" class="mobile-nav-link block nav-link px-3 py-2 rounded-md text-base font-medium text-stone-600">Instalasi</a>
            </div>
        </nav>
    </header>

    <main class="container mx-auto px-4 sm:px-6 lg:px-8 py-8 md:py-12">

        <section id="overview" class="scroll-mt-20">
            <div class="text-center">
                <h1 class="text-4xl md:text-5xl font-extrabold text-stone-900 tracking-tight">Bangun Blog Impian Anda</h1>
                <p class="mt-4 max-w-2xl mx-auto text-lg text-stone-600">
                    Ini adalah proyek starter untuk membangun sistem blog atau CMS pribadi yang modern dan kaya fitur. Dirancang untuk memberikan pengalaman terbaik bagi penulis dan pembaca dengan teknologi terbaru dari ekosistem Laravel.
                </p>
            </div>

            <div class="mt-10 grid grid-cols-1 md:grid-cols-3 gap-6 text-center">
                <div class="bg-white p-6 rounded-xl shadow-md">
                    <h3 class="text-3xl font-bold text-green-600">Laravel 11</h3>
                    <p class="mt-2 text-stone-500">Framework PHP yang kokoh dan elegan sebagai fondasi.</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow-md">
                    <h3 class="text-3xl font-bold text-green-600">Filament 3</h3>
                    <p class="mt-2 text-stone-500">Panel admin yang cantik dan kuat untuk manajemen konten.</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow-md">
                    <h3 class="text-3xl font-bold text-green-600">Livewire 3</h3>
                    <p class="mt-2 text-stone-500">Frontend dinamis dan interaktif tanpa menulis banyak JavaScript.</p>
                </div>
            </div>
        </section>

        <section id="features" class="mt-20 scroll-mt-20">
            <div class="text-center">
                <h2 class="text-3xl font-bold text-stone-900">Fitur Unggulan</h2>
                <p class="mt-3 max-w-xl mx-auto text-stone-600">Jelajahi berbagai fitur interaktif yang dirancang untuk memperkaya pengalaman pembaca dan memudahkan penulis.</p>
            </div>

            <div class="mt-10 grid grid-cols-1 lg:grid-cols-3 gap-8">
                <div class="lg:col-span-1">
                    <div class="bg-white p-4 rounded-xl shadow-md">
                        <div class="chart-container">
                            <canvas id="featureChart"></canvas>
                        </div>
                        <p class="text-center mt-4 text-sm text-stone-500">Distribusi fitur antara Frontend dan Backend.</p>
                    </div>
                </div>

                <div class="lg:col-span-2">
                    <div class="bg-white rounded-xl shadow-md overflow-hidden">
                        <div class="grid grid-cols-1 md:grid-cols-2">
                             <div id="feature-list" class="border-r border-stone-200">
                            </div>
                            <div id="feature-details" class="p-6 bg-stone-50 min-h-[300px]">
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="tech-stack" class="mt-20 scroll-mt-20">
            <div class="text-center">
                <h2 class="text-3xl font-bold text-stone-900">Tumpukan Teknologi & Plugin</h2>
                <p class="mt-3 max-w-xl mx-auto text-stone-600">Dibangun dengan alat-alat modern dan didukung oleh plugin pilihan untuk fungsionalitas maksimal.</p>
            </div>

            <div class="mt-10">
                <h3 class="text-xl font-semibold text-center text-stone-700 mb-6">Teknologi Inti</h3>
                 <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-6 gap-6 text-center">
                    <div class="bg-white p-4 rounded-lg shadow-sm"><strong>Laravel 11</strong></div>
                    <div class="bg-white p-4 rounded-lg shadow-sm"><strong>Filament 3</strong></div>
                    <div class="bg-white p-4 rounded-lg shadow-sm"><strong>Livewire 3</strong></div>
                    <div class="bg-white p-4 rounded-lg shadow-sm"><strong>Tailwind CSS</strong></div>
                    <div class="bg-white p-4 rounded-lg shadow-sm"><strong>Alpine.js</strong></div>
                    <div class="bg-white p-4 rounded-lg shadow-sm"><strong>MySQL/PgSQL</strong></div>
                </div>

                <h3 class="text-xl font-semibold text-center text-stone-700 mb-6 mt-12">Plugin Filament Pilihan</h3>
                <div id="plugin-list" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                </div>
            </div>
        </section>

        <section id="installation" class="mt-20 scroll-mt-20">
            <div class="text-center">
                <h2 class="text-3xl font-bold text-stone-900">Panduan Instalasi</h2>
                <p class="mt-3 max-w-xl mx-auto text-stone-600">Ikuti langkah-langkah terstruktur ini untuk menjalankan proyek di lingkungan lokal Anda.</p>
            </div>

            <div class="mt-10 max-w-4xl mx-auto bg-white rounded-xl shadow-md p-6 md:p-8">
                <div id="installation-steps-container">
                </div>
                <div class="mt-6 flex justify-between items-center">
                    <button id="prev-step" class="bg-stone-200 text-stone-700 font-semibold py-2 px-4 rounded-lg transition hover:bg-stone-300 disabled:opacity-50 disabled:cursor-not-allowed">Sebelumnya</button>
                    <div id="step-indicator" class="text-sm text-stone-500"></div>
                    <button id="next-step" class="bg-green-600 text-white font-semibold py-2 px-4 rounded-lg transition hover:bg-green-700 disabled:opacity-50">Selanjutnya</button>
                </div>
            </div>
        </section>

    </main>

    <footer class="bg-stone-800 text-stone-300 mt-20">
        <div class="container mx-auto px-4 sm:px-6 lg:px-8 py-6 text-center">
            <p>&copy; 2025 Proyek Blog Modern. Dibuat dengan ❤ dan kode.</p>
            <p class="text-sm mt-1">Proyek ini berada di bawah Lisensi MIT.</p>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const features = {
                frontend: [
                    { name: 'Pencarian Real-time', desc: 'Kotak pencarian global yang menampilkan hasil secara instan saat pengguna mengetik, memberikan pengalaman navigasi yang cepat.' },
                    { name: 'Mode Gelap (Dark Mode)', desc: 'Pilihan tema terang dan gelap yang nyaman di mata, preferensinya disimpan di browser untuk kunjungan berikutnya.' },
                    { name: 'Sistem Komentar Interaktif', desc: 'Pengguna bisa berkomentar, membalas komentar lain, dengan sorotan visual untuk komentar dari penulis artikel.' },
                    { name: 'Tombol Suka / "Claps"', desc: 'Cara sederhana bagi pembaca untuk menunjukkan apresiasi pada sebuah artikel, meningkatkan interaksi pengguna.' },
                    { name: 'Bookmark / "Baca Nanti"', desc: 'Fitur bagi pengguna terdaftar untuk menyimpan artikel favorit mereka untuk dibaca di kemudian hari.' },
                    { name: 'Reading Progress Bar', desc: 'Indikator visual yang menunjukkan progres membaca sebuah artikel, meningkatkan user experience.' },
                    { name: 'Berbagi ke Media Sosial', desc: 'Tombol untuk membagikan artikel dengan mudah ke platform seperti Twitter, Facebook, dan WhatsApp.' },
                    { name: 'Desain Responsif', desc: 'Tampilan yang optimal di semua perangkat, dari desktop hingga mobile, untuk jangkauan audiens yang luas.' }
                ],
                backend: [
                    { name: 'Manajemen Postingan (CRUD)', desc: 'Antarmuka yang elegan untuk membuat, membaca, memperbarui, dan menghapus postingan dengan mudah.' },
                    { name: 'Editor Teks Superior', desc: 'Menggunakan Tiptap Editor untuk pengalaman menulis yang kaya fitur, mirip dengan editor modern seperti Notion.' },
                    { name: 'Manajemen Kategori & Tag', desc: 'Mengelompokkan dan melabeli postingan dengan mudah untuk organisasi konten yang lebih baik.' },
                    { name: 'Moderasi Komentar', desc: 'Admin dapat menyetujui atau menolak komentar sebelum ditampilkan, menjaga kualitas diskusi.' },
                    { name: 'Manajemen SEO', desc: 'Field khusus untuk meta title dan description dengan pratinjau Google SERP untuk optimasi mesin pencari.' },
                    { name: 'Pustaka Media Terpusat', desc: 'Mengelola semua file yang diunggah di satu tempat menggunakan integrasi Spatie Media Library.' },
                    { name: 'Manajemen Pengguna & Hak Akses', desc: 'Sistem peran (Roles & Permissions) untuk membedakan hak akses antara Admin dan Penulis.' },
                    { name: 'Dashboard Analitik', desc: 'Widget yang menampilkan data dari Google Analytics langsung di dashboard admin untuk memantau performa.' }
                ]
            };

            const plugins = [
                { name: 'Tiptap Editor', desc: 'Editor teks WYSIWYG yang modern dan bisa dikustomisasi.', icon: '✍️' },
                { name: 'Filament SEO', desc: 'Mengelola meta tags dan pratinjau SERP dengan mudah.', icon: '🔍' },
                { name: 'Spatie Media Library', desc: 'Integrasi pustaka media yang kuat untuk manajemen file.', icon: '🖼️' },
                { name: 'Google Analytics', desc: 'Menampilkan data analitik langsung di dashboard Filament.', icon: '📊' },
                { name: 'Filament Shield', desc: 'Manajemen Peran & Hak Akses yang intuitif.', icon: '🛡️' },
            ];

            const installationSteps = [
                { title: 'Langkah 1: Clone Repository', desc: 'Salin repositori proyek ke mesin lokal Anda menggunakan Git.', code: 'git clone https://github.com/username/nama-repo.git\ncd nama-repo' },
                { title: 'Langkah 2: Install Dependensi', desc: 'Install semua paket PHP yang dibutuhkan oleh proyek melalui Composer.', code: 'composer install' },
                { title: 'Langkah 3: Konfigurasi Environment', desc: 'Salin file `.env.example` menjadi `.env` dan generate kunci aplikasi baru.', code: 'cp .env.example .env\nphp artisan key:generate' },
                { title: 'Langkah 4: Setup Database', desc: 'Buka file `.env` dan sesuaikan pengaturan koneksi database Anda.', code: 'DB_DATABASE=nama_database_anda\nDB_USERNAME=root\nDB_PASSWORD=' },
                { title: 'Langkah 5: Migrasi & Seeding', desc: 'Jalankan migrasi untuk membuat struktur tabel dan seeder untuk mengisi data awal.', code: 'php artisan migrate --seed' },
                { title: 'Langkah 6: Storage Link & User Admin', desc: 'Buat symbolic link untuk storage dan buat pengguna admin pertama Anda.', code: 'php artisan storage:link\nphp artisan make:filament-user' },
                { title: 'Langkah 7: Compile Assets & Jalankan', desc: 'Install dependensi frontend dan jalankan server development Laravel.', code: 'npm install\nnpm run dev\nphp artisan serve' },
                { title: 'Selesai!', desc: 'Anda berhasil! Sekarang akses website di <strong>http://127.0.0.1:8000</strong> dan admin di <strong>http://127.0.0.1:8000/admin</strong>.', code: '🎉 Selamat Datang di Proyek Blog Modern Anda! 🎉' }
            ];

            const featureListEl = document.getElementById('feature-list');
            const featureDetailsEl = document.getElementById('feature-details');
            const pluginListEl = document.getElementById('plugin-list');
            const installationStepsContainerEl = document.getElementById('installation-steps-container');
            const prevStepBtn = document.getElementById('prev-step');
            const nextStepBtn = document.getElementById('next-step');
            const stepIndicatorEl = document.getElementById('step-indicator');

            let currentStepIndex = 0;
            const allFeatures = [
                ...features.frontend.map(f => ({...f, type: 'Frontend'})),
                ...features.backend.map(f => ({...f, type: 'Backend'}))
            ];

            function renderFeatures() {
                featureListEl.innerHTML = '';
                allFeatures.forEach((feature, index) => {
                    const item = document.createElement('div');
                    item.className = 'feature-item p-4 cursor-pointer hover:bg-stone-100 transition';
                    item.innerHTML = `<span class="font-semibold text-sm ${feature.type === 'Frontend' ? 'text-green-600' : 'text-stone-600'}">${feature.type}</span><p class="text-stone-800">${feature.name}</p>`;
                    item.addEventListener('click', () => showFeatureDetails(index));
                    featureListEl.appendChild(item);
                });
            }

            function showFeatureDetails(index) {
                const feature = allFeatures[index];
                featureDetailsEl.innerHTML = `
                    <h4 class="font-bold text-lg text-stone-900">${feature.name}</h4>
                    <span class="inline-block mt-1 text-xs font-semibold ${feature.type === 'Frontend' ? 'bg-green-100 text-green-700' : 'bg-stone-200 text-stone-700'} px-2 py-1 rounded-full">${feature.type}</span>
                    <p class="mt-4 text-stone-600">${feature.desc}</p>
                `;
                document.querySelectorAll('.feature-item').forEach((el, i) => {
                    el.classList.toggle('active', i === index);
                });
            }

            function renderPlugins() {
                pluginListEl.innerHTML = plugins.map(plugin => `
                    <div class="bg-white p-6 rounded-xl shadow-md flex items-start space-x-4">
                        <div class="text-4xl">${plugin.icon}</div>
                        <div>
                            <h4 class="font-bold text-stone-900">${plugin.name}</h4>
                            <p class="text-stone-600 mt-1">${plugin.desc}</p>
                        </div>
                    </div>
                `).join('');
            }

            function copyToClipboard(text, button) {
                const textarea = document.createElement('textarea');
                textarea.value = text;
                document.body.appendChild(textarea);
                textarea.select();
                try {
                    document.execCommand('copy');
                    button.textContent = 'Disalin!';
                    setTimeout(() => { button.textContent = 'Salin'; }, 2000);
                } catch (err) {
                    console.error('Gagal menyalin teks: ', err);
                }
                document.body.removeChild(textarea);
            }

            function renderCurrentStep() {
                const step = installationSteps[currentStepIndex];
                installationStepsContainerEl.innerHTML = `
                    <h4 class="text-xl font-bold text-stone-900 mb-2">${step.title}</h4>
                    <p class="text-stone-600 mb-4">${step.desc}</p>
                    <div class="code-block bg-stone-800 text-stone-200 rounded-lg p-4 font-mono text-sm overflow-x-auto">
                        <button class="copy-button">Salin</button>
                        <pre><code>${step.code}</code></pre>
                    </div>
                `;
                const copyButton = installationStepsContainerEl.querySelector('.copy-button');
                if(copyButton) {
                    copyButton.addEventListener('click', (e) => {
                       e.stopPropagation();
                       copyToClipboard(step.code, copyButton);
                    });
                }

                stepIndicatorEl.textContent = `Langkah ${currentStepIndex + 1} dari ${installationSteps.length}`;
                prevStepBtn.disabled = currentStepIndex === 0;
                nextStepBtn.disabled = currentStepIndex === installationSteps.length - 1;
                if (currentStepIndex === installationSteps.length - 1) {
                    nextStepBtn.textContent = 'Selesai';
                } else {
                    nextStepBtn.textContent = 'Selanjutnya';
                }
            }

            prevStepBtn.addEventListener('click', () => {
                if (currentStepIndex > 0) {
                    currentStepIndex--;
                    renderCurrentStep();
                }
            });

            nextStepBtn.addEventListener('click', () => {
                if (currentStepIndex < installationSteps.length - 1) {
                    currentStepIndex++;
                    renderCurrentStep();
                }
            });

            const mobileMenuButton = document.getElementById('mobile-menu-button');
            const mobileMenu = document.getElementById('mobile-menu');
            const menuIconOpen = document.getElementById('menu-icon-open');
            const menuIconClose = document.getElementById('menu-icon-close');

            mobileMenuButton.addEventListener('click', () => {
                mobileMenu.classList.toggle('hidden');
                menuIconOpen.classList.toggle('hidden');
                menuIconClose.classList.toggle('hidden');
            });

            document.querySelectorAll('.mobile-nav-link').forEach(link => {
                link.addEventListener('click', () => {
                    mobileMenu.classList.add('hidden');
                    menuIconOpen.classList.remove('hidden');
                    menuIconClose.classList.add('hidden');
                });
            });

            const sections = document.querySelectorAll('section');
            const navLinks = document.querySelectorAll('.nav-link');

            window.addEventListener('scroll', () => {
                let current = '';
                sections.forEach(section => {
                    const sectionTop = section.offsetTop;
                    if (pageYOffset >= sectionTop - 80) {
                        current = section.getAttribute('id');
                    }
                });

                navLinks.forEach(link => {
                    link.classList.remove('active');
                    if (link.getAttribute('href').includes(current)) {
                        link.classList.add('active');
                    }
                });
            });

            const ctx = document.getElementById('featureChart').getContext('2d');
            new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: ['Frontend', 'Backend'],
                    datasets: [{
                        data: [features.frontend.length, features.backend.length],
                        backgroundColor: ['#16a34a', '#44403c'],
                        borderColor: '#f5f5f4',
                        borderWidth: 4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { position: 'bottom', labels: { color: '#57534e', font: { family: 'Inter', size: 14 } } } },
                    cutout: '60%'
                }
            });

            renderFeatures();
            showFeatureDetails(0);
            renderPlugins();
            renderCurrentStep();
        });
    </script>

</body>
</html>
