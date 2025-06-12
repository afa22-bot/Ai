# Ai


<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Editor Video Shorts AI</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .glass-card {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        .btn-primary {
            background-color: #8A2BE2; /* BlueViolet */
            color: white;
            transition: background-color 0.3s ease;
        }
        .btn-primary:hover {
            background-color: #9932CC; /* MediumOrchid */
        }
        .loader {
            border: 4px solid rgba(255, 255, 255, 0.2);
            border-left-color: #8A2BE2;
            border-radius: 50%;
            width: 32px;
            height: 32px;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            to {
                transform: rotate(360deg);
            }
        }
        .gemini-btn {
            background: linear-gradient(90deg, #4f46e5, #c026d3);
            transition: all 0.3s ease;
        }
        .gemini-btn:hover {
            transform: scale(1.03);
            box-shadow: 0 0 15px rgba(192, 38, 211, 0.5);
        }
    </style>
</head>
<body class="bg-gray-900 text-white min-h-screen flex flex-col items-center p-4 sm:p-6 lg:p-8">

    <div class="w-full max-w-6xl">
        <!-- Header -->
        <header class="text-center mb-8">
            <h1 class="text-4xl sm:text-5xl font-bold tracking-tight bg-clip-text text-transparent bg-gradient-to-r from-purple-400 to-pink-600">
                Editor Video Shorts AI
            </h1>
            <p class="text-gray-400 mt-2 text-lg">Ubah video YouTube menjadi Shorts viral dengan kekuatan Gemini.</p>
        </header>

        <!-- Main Content -->
        <main class="space-y-8">
            <!-- 1. Input URL YouTube -->
            <section id="url-input-section" class="glass-card rounded-xl p-6 shadow-lg">
                <h2 class="text-2xl font-semibold mb-4 flex items-center">
                    <i data-lucide="youtube" class="w-6 h-6 mr-3 text-red-500"></i>
                    Langkah 1: Masukkan URL Video YouTube
                </h2>
                <div class="flex flex-col sm:flex-row gap-4">
                    <input id="youtube-url-input" type="text" placeholder="https://www.youtube.com/watch?v=..." class="w-full bg-gray-800 border border-gray-700 rounded-lg px-4 py-3 focus:outline-none focus:ring-2 focus:ring-purple-500 transition-all">
                    <button id="process-video-btn" class="btn-primary font-semibold rounded-lg px-6 py-3 flex items-center justify-center whitespace-nowrap">
                        <i data-lucide="arrow-right" class="w-5 h-5 mr-2"></i>
                        Proses Video
                    </button>
                </div>
            </section>

            <!-- Video Player and Clipping -->
            <section id="clipping-section" class="hidden glass-card rounded-xl p-6 shadow-lg">
                 <h2 class="text-2xl font-semibold mb-4 flex items-center">
                    <i data-lucide="scissors" class="w-6 h-6 mr-3 text-purple-400"></i>
                    Langkah 2: Potong Klip Video Anda
                </h2>
                <div class="bg-black rounded-lg overflow-hidden aspect-video mb-4 border border-gray-700">
                     <div id="player-container" class="w-full h-full flex items-center justify-center bg-gray-800">
                        <p class="text-gray-500">Pratinjau video akan muncul di sini</p>
                    </div>
                </div>
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    <div>
                        <label for="start-time" class="block text-sm font-medium text-gray-400 mb-1">Waktu Mulai</label>
                        <input id="start-time" type="text" value="00:15" class="w-full bg-gray-800 border border-gray-700 rounded-lg px-4 py-2">
                    </div>
                    <div>
                        <label for="end-time" class="block text-sm font-medium text-gray-400 mb-1">Waktu Selesai</label>
                        <input id="end-time" type="text" value="00:55" class="w-full bg-gray-800 border border-gray-700 rounded-lg px-4 py-2">
                    </div>
                </div>
                 <p class="text-xs text-gray-500 mt-2">Format: MM:SS. Durasi direkomendasikan di bawah 60 detik.</p>
            </section>

            <!-- AI Features -->
            <section id="ai-features-section" class="hidden">
                <h2 class="text-2xl font-semibold mb-4 flex items-center">
                    <i data-lucide="sparkles" class="w-6 h-6 mr-3 text-yellow-400"></i>
                    Langkah 3: Gunakan Keajaiban AI
                </h2>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <!-- Auto Subtitle Card -->
                    <div class="glass-card rounded-xl p-6 shadow-lg flex flex-col">
                        <h3 class="text-xl font-semibold mb-3 flex items-center"><i data-lucide="captions" class="w-5 h-5 mr-2 text-blue-400"></i>Subtitle Otomatis</h3>
                        <p class="text-gray-400 mb-4 flex-grow">Buat subtitle secara otomatis dari transkrip video Anda.</p>
                        <button id="generate-subtitles-btn" class="gemini-btn mt-auto w-full text-white font-semibold rounded-lg px-6 py-3">Buat Subtitle ✨</button>
                        <div id="subtitles-output" class="mt-4 hidden"><div class="flex justify-center items-center p-4"><div class="loader"></div></div></div>
                    </div>

                    <!-- Trending Analysis Card -->
                    <div class="glass-card rounded-xl p-6 shadow-lg flex flex-col">
                        <h3 class="text-xl font-semibold mb-3 flex items-center"><i data-lucide="trending-up" class="w-5 h-5 mr-2 text-green-400"></i>Analisis Potensi Trending</h3>
                        <p class="text-gray-400 mb-4 flex-grow">Dapatkan wawasan viral dan rekomendasi hashtag.</p>
                        <button id="analyze-trending-btn" class="gemini-btn mt-auto w-full text-white font-semibold rounded-lg px-6 py-3">Analisis Potensi ✨</button>
                        <div id="trending-output" class="mt-4 hidden"><div class="flex justify-center items-center p-4"><div class="loader"></div></div></div>
                    </div>

                    <!-- Viral Title Generator Card -->
                    <div class="glass-card rounded-xl p-6 shadow-lg flex flex-col">
                        <h3 class="text-xl font-semibold mb-3 flex items-center"><i data-lucide="lightbulb" class="w-5 h-5 mr-2 text-yellow-400"></i>Generator Judul Viral</h3>
                        <p class="text-gray-400 mb-4 flex-grow">Hasilkan 5 ide judul yang menarik untuk video Anda.</p>
                        <button id="generate-titles-btn" class="gemini-btn mt-auto w-full text-white font-semibold rounded-lg px-6 py-3">Buat Judul Viral ✨</button>
                        <div id="titles-output" class="mt-4 hidden"><div class="flex justify-center items-center p-4"><div class="loader"></div></div></div>
                    </div>
                </div>
            </section>
            
             <!-- Preview and Download -->
            <section id="preview-section" class="hidden glass-card rounded-xl p-6 shadow-lg">
                <h2 class="text-2xl font-semibold mb-4 flex items-center">
                    <i data-lucide="film" class="w-6 h-6 mr-3 text-pink-400"></i>
                    Langkah 4: Pratinjau & Unduh
                </h2>
                <div class="flex flex-col lg:flex-row gap-6">
                    <div class="flex-1 lg:w-1/3">
                        <h3 class="text-lg font-semibold mb-2">Pratinjau Video Shorts</h3>
                        <div class="aspect-[9/16] bg-black rounded-lg border border-gray-700 flex items-center justify-center">
                            <p class="text-gray-500 text-center p-4">Pratinjau akhir dengan subtitle akan ditampilkan di sini.</p>
                        </div>
                    </div>
                    <div class="flex-1 lg:w-2/3 space-y-4">
                        <div>
                            <h3 class="text-lg font-semibold mb-2">Hasil Analisis Tren</h3>
                             <div id="final-analysis-results" class="text-gray-300 p-4 bg-gray-800/50 rounded-lg min-h-[100px] max-h-48 overflow-y-auto">Belum ada analisis.</div>
                        </div>
                        <div>
                            <h3 class="text-lg font-semibold mb-2">Judul yang Dihasilkan</h3>
                             <div id="final-titles-results" class="text-gray-300 p-4 bg-gray-800/50 rounded-lg min-h-[100px] max-h-48 overflow-y-auto">Belum ada judul yang dibuat.</div>
                        </div>
                        <div>
                            <h3 class="text-lg font-semibold mb-2">Subtitle yang Dihasilkan</h3>
                            <div id="final-subtitles-display" class="text-gray-300 p-4 bg-gray-800/50 rounded-lg min-h-[150px] max-h-48 overflow-y-auto">Belum ada subtitle.</div>
                        </div>
                    </div>
                </div>
                 <button class="w-full mt-6 btn-primary font-bold rounded-lg px-6 py-4 text-lg flex items-center justify-center">
                    <i data-lucide="download" class="w-6 h-6 mr-3"></i>
                    Unduh Video Shorts
                </button>
                <p class="text-xs text-center text-gray-500 mt-3">Fitur unduh akan diaktifkan dalam versi mendatang.</p>
            </section>
        </main>

        <footer class="text-center mt-12 py-6 border-t border-gray-800">
            <p class="text-gray-500">&copy; 2024 Editor Video Shorts AI. Dibuat dengan ❤️ dan Gemini.</p>
        </footer>

    </div>

    <script>
        lucide.createIcons();
        
        // --- DOM Elements ---
        const youtubeUrlInput = document.getElementById('youtube-url-input');
        const processVideoBtn = document.getElementById('process-video-btn');
        const clippingSection = document.getElementById('clipping-section');
        const playerContainer = document.getElementById('player-container');
        const aiFeaturesSection = document.getElementById('ai-features-section');
        const previewSection = document.getElementById('preview-section');
        
        // AI Feature Elements
        const generateSubtitlesBtn = document.getElementById('generate-subtitles-btn');
        const subtitlesOutput = document.getElementById('subtitles-output');
        const analyzeTrendingBtn = document.getElementById('analyze-trending-btn');
        const trendingOutput = document.getElementById('trending-output');
        const generateTitlesBtn = document.getElementById('generate-titles-btn');
        const titlesOutput = document.getElementById('titles-output');

        // Final Preview Elements
        const finalAnalysisResults = document.getElementById('final-analysis-results');
        const finalTitlesResults = document.getElementById('final-titles-results');
        const finalSubtitlesDisplay = document.getElementById('final-subtitles-display');

        // --- Simulated Data (will be replaced by actual logic) ---
        const videoData = {
            title: "Perjalanan Epik ke Puncak Gunung Rinjani",
            transcript: "Halo semua, selamat datang kembali. Hari ini kita akan memulai petualangan luar biasa mendaki salah satu gunung terindah di Indonesia, yaitu Gunung Rinjani. Pemandangan dari sini sungguh menakjubkan. Lihatlah lautan awan di bawah kita. Perjalanan ini sangat melelahkan, tapi setiap langkahnya, setiap tetes keringat, sangat sepadan ketika kita melihat keindahan alam seperti ini. Kita akhirnya berhasil mencapai puncak! Sebuah perasaan yang tidak bisa diungkapkan dengan kata-kata. Terima kasih sudah mengikuti perjalanan kami."
        };
        
        // --- Functions ---
        
        function processVideo() {
            const url = youtubeUrlInput.value;
            if (!url.includes('youtube.com/watch?v=') && !url.includes('youtu.be/')) {
                alert('Silakan masukkan URL YouTube yang valid.');
                return;
            }
            
            processVideoBtn.innerHTML = '<div class="loader !w-6 !h-6"></div>';
            
            setTimeout(() => {
                processVideoBtn.innerHTML = '<i data-lucide="check" class="w-5 h-5 mr-2"></i> Video Diproses';
                lucide.createIcons();

                clippingSection.classList.remove('hidden');
                aiFeaturesSection.classList.remove('hidden');
                previewSection.classList.remove('hidden');

                playerContainer.innerHTML = `
                    <div class="w-full h-full bg-black flex flex-col items-center justify-center text-center">
                        <i data-lucide="video" class="w-16 h-16 text-gray-600 mb-4"></i>
                        <p class="text-white font-semibold">${videoData.title}</p>
                        <p class="text-xs text-gray-400">(Ini adalah pratinjau simulasi)</p>
                    </div>
                `;
                lucide.createIcons();
                clippingSection.scrollIntoView({ behavior: 'smooth' });

            }, 1500);
        }

        async function callGeminiAPI(prompt, responseSchema) {
            const apiKey = ""; // API key is handled by the environment
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;
            
            const payload = {
                contents: [{ role: "user", parts: [{ text: prompt }] }],
                generationConfig: {
                    responseMimeType: "application/json",
                    responseSchema: responseSchema
                }
            };

            const response = await fetch(apiUrl, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(payload)
            });

            if (!response.ok) {
                throw new Error(`API call failed with status: ${response.status}`);
            }

            const result = await response.json();
             if (result.candidates && result.candidates.length > 0) {
                const text = result.candidates[0].content.parts[0].text;
                return JSON.parse(text);
            } else {
                throw new Error("Invalid API response structure.");
            }
        }
        
        async function generateSubtitles() {
            subtitlesOutput.innerHTML = '<div class="flex justify-center items-center p-4"><div class="loader"></div></div>';
            subtitlesOutput.classList.remove('hidden');

            const prompt = `Anda adalah editor video profesional. Berdasarkan transkrip berikut, buat file subtitle dalam format JSON. Setiap entri harus memiliki "start" (waktu mulai dalam detik, sebagai float) dan "text" (teks subtitle). Buat subtitle yang ringkas dan mudah dibaca untuk video pendek (Shorts). Transkrip: "${videoData.transcript}"`;
            
            const schema = {
                type: "ARRAY",
                items: {
                    type: "OBJECT",
                    properties: {
                        start: { type: "NUMBER", description: "Waktu mulai dalam detik" },
                        text: { type: "STRING" }
                    },
                    required: ["start", "text"]
                }
            };

            try {
                const apiResponse = await callGeminiAPI(prompt, schema);
                
                let subtitleHtml = '<div class="bg-gray-800/50 p-3 rounded-lg text-sm space-y-2 max-h-48 overflow-y-auto">';
                apiResponse.forEach(sub => {
                    subtitleHtml += `<p><span class="font-mono text-purple-300">${sub.start.toFixed(1)}s:</span> ${sub.text}</p>`;
                });
                subtitleHtml += '</div>';

                subtitlesOutput.innerHTML = subtitleHtml;
                finalSubtitlesDisplay.innerHTML = subtitleHtml;

            } catch (error) {
                console.error("Error generating subtitles:", error);
                const errorHtml = `<div class="bg-red-900/50 p-3 rounded-lg text-sm text-red-300">Gagal membuat subtitle. Silakan coba lagi.</div>`;
                subtitlesOutput.innerHTML = errorHtml;
                finalSubtitlesDisplay.innerHTML = "Gagal memuat.";
            }
        }
        
        async function analyzeTrendingPotential() {
            trendingOutput.innerHTML = '<div class="flex justify-center items-center p-4"><div class="loader"></div></div>';
            trendingOutput.classList.remove('hidden');

            const prompt = `Anda adalah Analis Video Viral untuk YouTube. Berdasarkan judul dan transkrip video ini, berikan analisis potensi viral. Judul: "${videoData.title}". Transkrip: "${videoData.transcript}". Berikan respons dalam format JSON dengan: sebuah 'score' (angka 1-100), sebuah 'analysis' (penjelasan singkat 2-3 kalimat), dan sebuah array 'hashtags' (5 hashtag relevan).`;
            
            const schema = {
                type: "OBJECT",
                properties: {
                    score: { type: "INTEGER" },
                    analysis: { type: "STRING" },
                    hashtags: { type: "ARRAY", items: { type: "STRING" } }
                },
                required: ["score", "analysis", "hashtags"]
            };

            try {
                const apiResponse = await callGeminiAPI(prompt, schema);

                let trendingHtml = `
                    <div class="bg-gray-800/50 p-4 rounded-lg space-y-3">
                        <div class="text-center">
                            <p class="text-lg text-gray-400">Skor Potensi Tren</p>
                            <p class="text-5xl font-bold text-green-400">${apiResponse.score}/100</p>
                        </div>
                        <div>
                            <p class="font-semibold text-gray-300">Analisis AI:</p>
                            <p class="text-sm text-gray-400">${apiResponse.analysis}</p>
                        </div>
                        <div>
                            <p class="font-semibold text-gray-300">Rekomendasi Hashtag:</p>
                            <div class="flex flex-wrap gap-2 mt-2">
                                ${apiResponse.hashtags.map(tag => `<span class="bg-gray-700 text-gray-300 text-xs font-medium px-2.5 py-1 rounded-full">${tag}</span>`).join('')}
                            </div>
                        </div>
                    </div>
                `;
                trendingOutput.innerHTML = trendingHtml;
                finalAnalysisResults.innerHTML = trendingHtml;

            } catch (error) {
                console.error("Error analyzing trending potential:", error);
                const errorHtml = `<div class="bg-red-900/50 p-3 rounded-lg text-sm text-red-300">Gagal menganalisis potensi. Silakan coba lagi.</div>`;
                trendingOutput.innerHTML = errorHtml;
                finalAnalysisResults.innerHTML = "Gagal memuat.";
            }
        }

        async function generateViralTitles() {
            titlesOutput.innerHTML = '<div class="flex justify-center items-center p-4"><div class="loader"></div></div>';
            titlesOutput.classList.remove('hidden');

            const prompt = `Anda adalah seorang ahli branding YouTube yang kreatif. Berdasarkan judul asli dan transkrip video ini, buatlah 5 judul alternatif yang menarik, viral, dan cocok untuk format YouTube Shorts. Judul Asli: "${videoData.title}". Transkrip: "${videoData.transcript}". Berikan respons dalam format JSON berupa array berisi 5 string judul.`;

            const schema = {
                type: "ARRAY",
                items: { type: "STRING" }
            };

            try {
                const apiResponse = await callGeminiAPI(prompt, schema);
                
                let titlesHtml = '<ul class="list-disc list-inside bg-gray-800/50 p-4 rounded-lg text-sm space-y-2">';
                apiResponse.forEach(title => {
                    titlesHtml += `<li class="text-gray-300">${title}</li>`;
                });
                titlesHtml += '</ul>';

                titlesOutput.innerHTML = titlesHtml;
                finalTitlesResults.innerHTML = titlesHtml;
            } catch (error) {
                console.error("Error generating titles:", error);
                 const errorHtml = `<div class="bg-red-900/50 p-3 rounded-lg text-sm text-red-300">Gagal membuat judul. Silakan coba lagi.</div>`;
                titlesOutput.innerHTML = errorHtml;
                finalTitlesResults.innerHTML = "Gagal memuat.";
            }
        }
        
        // --- Event Listeners ---
        processVideoBtn.addEventListener('click', processVideo);
        generateSubtitlesBtn.addEventListener('click', generateSubtitles);
        analyzeTrendingBtn.addEventListener('click', analyzeTrendingPotential);
        generateTitlesBtn.addEventListener('click', generateViralTitles);
        
    </script>
</body>
</html>

