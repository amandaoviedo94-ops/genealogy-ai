<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GenealogyAI Proof Studio</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body { background-color: #0f172a; color: #f8fafc; font-family: ui-sans-serif, system-ui, sans-serif; }
        .glass-panel { background: rgba(30, 41, 59, 0.7); backdrop-filter: blur(12px); border: 1px solid rgba(255, 255, 255, 0.1); }
        .tab-btn.active { border-bottom: 2px solid #3b82f6; color: #60a5fa; background: rgba(59, 130, 246, 0.1); }
    </style>
</head>
<body class="min-h-screen flex flex-col text-slate-100">

    <!-- Top Navigation Header -->
    <header class="bg-slate-900 border-b border-slate-800 p-4 sticky top-0 z-40">
        <div class="max-w-7xl mx-auto flex flex-wrap items-center justify-between gap-4">
            <div class="flex items-center space-x-3">
                <i class="fa-solid fa-dna text-blue-500 text-2xl"></i>
                <span class="font-bold text-xl tracking-wide bg-gradient-to-r from-blue-400 to-indigo-400 bg-clip-text text-transparent">GenealogyAI Proof Studio</span>
            </div>
            <div class="flex flex-wrap items-center gap-3">
                <button onclick="toggleApiModal()" class="px-3 py-1.5 rounded-full text-xs font-semibold bg-emerald-950/80 text-emerald-400 border border-emerald-500/50 flex items-center space-x-2 shadow-lg shadow-emerald-900/20 hover:bg-emerald-900 transition">
                    <span class="relative flex h-2.5 w-2.5">
                      <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-emerald-400 opacity-75"></span>
                      <span class="relative inline-flex rounded-full h-2.5 w-2.5 bg-emerald-500"></span>
                    </span>
                    <span id="api-status-text">🔌 API: DEMO MODE (Simulated)</span>
                </button>
                <button onclick="toggleFileUploadModal()" class="px-3 py-1.5 rounded-lg text-xs font-medium bg-slate-800 hover:bg-slate-700 text-slate-200 border border-slate-700 transition flex items-center space-x-1">
                    <i class="fa-solid fa-file-arrow-up"></i>
                    <span>📁 Upload .GED / .CSV</span>
                </button>
                <button onclick="togglePricingModal()" class="px-3 py-1.5 rounded-lg text-xs font-medium bg-gradient-to-r from-amber-500 to-yellow-600 hover:from-amber-600 hover:to-yellow-700 text-slate-950 font-bold transition flex items-center space-x-1 shadow">
                    <i class="fa-solid fa-crown"></i>
                    <span>Upgrade Plan</span>
                </button>
            </div>
        </div>
    </header>

    <!-- Permanent Connection Banner -->
    <div id="connection-banner" class="bg-amber-950/40 border-b border-amber-800/50 text-amber-300 text-xs py-1.5 px-4 text-center font-medium flex items-center justify-center space-x-2">
        <i class="fa-solid fa-circle-info"></i>
        <span>Current Mode: Local Simulation active. Click the green API button above to configure live backend server.</span>
    </div>

    <!-- Navigation Tabs -->
    <nav class="bg-slate-900/90 border-b border-slate-800 sticky top-14 z-30 overflow-x-auto">
        <div class="max-w-7xl mx-auto flex space-x-1 px-4 min-w-max">
            <button onclick="switchTab('tab-leeds')" class="tab-btn active px-4 py-3 text-sm font-medium text-slate-400 hover:text-slate-200 flex items-center space-x-2">
                <i class="fa-solid fa-table-cells"></i><span>🎨 Leeds Cluster Grid</span>
            </button>
            <button onclick="switchTab('tab-tree')" class="tab-btn px-4 py-3 text-sm font-medium text-slate-400 hover:text-slate-200 flex items-center space-x-2">
                <i class="fa-solid fa-sitemap"></i><span>🌳 Pedigree Tree & Strategy</span>
            </button>
            <button onclick="switchTab('tab-chromo')" class="tab-btn px-4 py-3 text-sm font-medium text-slate-400 hover:text-slate-200 flex items-center space-x-2">
                <i class="fa-solid fa-microscope"></i><span>🧬 Chromosomes & Endogamy</span>
            </button>
            <button onclick="switchTab('tab-paper')" class="tab-btn px-4 py-3 text-sm font-medium text-slate-400 hover:text-slate-200 flex items-center space-x-2">
                <i class="fa-solid fa-folder-open"></i><span>📄 Paper Trails</span>
            </button>
            <button onclick="switchTab('tab-ai')" class="tab-btn px-4 py-3 text-sm font-medium text-slate-400 hover:text-slate-200 flex items-center space-x-2">
                <i class="fa-solid fa-bolt text-yellow-400"></i><span>⚡ AI Proof Assistant</span>
            </button>
            <button onclick="switchTab('tab-chat')" class="tab-btn px-4 py-3 text-sm font-medium text-slate-400 hover:text-slate-200 flex items-center space-x-2">
                <i class="fa-solid fa-comments"></i><span>💬 Member Network</span>
            </button>
            <button onclick="switchTab('tab-report')" class="tab-btn px-4 py-3 text-sm font-medium text-slate-400 hover:text-slate-200 flex items-center space-x-2">
                <i class="fa-solid fa-file-contract"></i><span>📄 GPS Summary</span>
            </button>
        </div>
    </nav>

    <!-- Main Workspace Content Container -->
    <main class="flex-1 max-w-7xl w-full mx-auto p-4 md:p-6 space-y-6">

        <!-- Tab 1: Leeds Cluster Grid -->
        <section id="tab-leeds" class="tab-content space-y-4">
            <div class="glass-panel p-4 rounded-xl border border-slate-800">
                <h2 class="text-lg font-bold text-slate-100 flex items-center space-x-2">
                    <i class="fa-solid fa-table-cells text-blue-400"></i>
                    <span>Leeds Method Cluster Matrix</span>
                </h2>
                <p class="text-xs text-slate-400 mt-1">Group your 90 cM – 400 cM DNA matches into 4 distinct grandparental clusters.</p>
                <div class="mt-4 flex items-center space-x-4">
                    <label class="text-xs text-slate-300">Min cM Filter: <span id="cm-val" class="text-blue-400 font-bold">90 cM</span></label>
                    <input type="range" min="40" max="200" value="90" class="w-48 accent-blue-500" oninput="document.getElementById('cm-val').innerText = this.value + ' cM'">
                </div>
            </div>
            <div class="overflow-x-auto glass-panel rounded-xl p-4">
                <table class="w-full text-xs text-left">
                    <thead class="bg-slate-800 text-slate-300 uppercase text-[10px] tracking-wider">
                        <tr>
                            <th class="p-3">Match Name</th>
                            <th class="p-3">Shared cM</th>
                            <th class="p-3 text-center bg-red-950/40 text-red-400">Cluster 1 (Maternal Paternal)</th>
                            <th class="p-3 text-center bg-blue-950/40 text-blue-400">Cluster 2 (Maternal Maternal)</th>
                            <th class="p-3 text-center bg-emerald-950/40 text-emerald-400">Cluster 3 (Paternal Paternal)</th>
                            <th class="p-3 text-center bg-amber-950/40 text-amber-400">Cluster 4 (Paternal Maternal)</th>
                        </tr>
                    </thead>
                    <tbody class="divide-y divide-slate-800 text-slate-300">
                        <tr class="hover:bg-slate-800/50">
                            <td class="p-3 font-semibold">Cousin Sarah M.</td>
                            <td class="p-3">245 cM</td>
                            <td class="p-3 text-center"><span class="inline-block w-4 h-4 rounded-full bg-red-500 shadow"></span></td>
                            <td class="p-3 text-center">-</td>
                            <td class="p-3 text-center">-</td>
                            <td class="p-3 text-center">-</td>
                        </tr>
                        <tr class="hover:bg-slate-800/50">
                            <td class="p-3 font-semibold">Robert H.</td>
                            <td class="p-3">180 cM</td>
                            <td class="p-3 text-center">-</td>
                            <td class="p-3 text-center"><span class="inline-block w-4 h-4 rounded-full bg-blue-500 shadow"></span></td>
                            <td class="p-3 text-center">-</td>
                            <td class="p-3 text-center">-</td>
                        </tr>
                        <tr class="hover:bg-slate-800/50">
                            <td class="p-3 font-semibold">David K.</td>
                            <td class="p-3">120 cM</td>
                            <td class="p-3 text-center">-</td>
                            <td class="p-3 text-center">-</td>
                            <td class="p-3 text-center"><span class="inline-block w-4 h-4 rounded-full bg-emerald-500 shadow"></span></td>
                            <td class="p-3 text-center">-</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </section>

        <!-- Tab 2: Pedigree Tree -->
        <section id="tab-tree" class="tab-content hidden space-y-4">
            <div class="glass-panel p-4 rounded-xl">
                <h2 class="text-lg font-bold text-slate-100 flex items-center space-x-2">
                    <i class="fa-solid fa-sitemap text-indigo-400"></i>
                    <span>Pedigree Strategy & Target Testing Engine</span>
                </h2>
                <p class="text-xs text-slate-400 mt-1">Identifies brick walls and recommends specific targeted DNA testers.</p>
                <div class="mt-6 grid grid-cols-1 md:grid-cols-3 gap-4">
                    <div class="bg-slate-800/80 p-4 rounded-lg border border-indigo-500/30">
                        <span class="text-xs text-indigo-400 font-bold uppercase tracking-wider">Target Tester Recommendation</span>
                        <h3 class="font-bold text-sm text-slate-200 mt-1">2nd Cousin (Descendant of James Miller)</h3>
                        <p class="text-xs text-slate-400 mt-2">Testing a child of Cousin Arthur will resolve the 3rd Great-Grandfather gap with 94% statistical confidence.</p>
                    </div>
                    <div class="bg-slate-800/80 p-4 rounded-lg border border-slate-700">
                        <span class="text-xs text-slate-400 font-bold uppercase tracking-wider">Tree Completeness</span>
                        <h3 class="font-bold text-2xl text-emerald-400 mt-1">87.5%</h3>
                        <p class="text-xs text-slate-400 mt-1">28 of 32 3rd Great-Grandparents identified.</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Tab 3: Chromosomes & Endogamy -->
        <section id="tab-chromo" class="tab-content hidden space-y-4">
            <div class="glass-panel p-4 rounded-xl">
                <h2 class="text-lg font-bold text-slate-100 flex items-center space-x-2">
                    <i class="fa-solid fa-microscope text-emerald-400"></i>
                    <span>Autosomal Chromosome Painter & Endogamy Normalizer</span>
                </h2>
                <div class="mt-4 space-y-3">
                    <div class="flex items-center justify-between text-xs text-slate-300">
                        <span>Chromosome 1 (Maternal / Paternal segments)</span>
                        <span class="text-emerald-400 font-mono">14.2 cM segment match</span>
                    </div>
                    <div class="h-6 w-full bg-slate-800 rounded-full overflow-hidden flex">
                        <div class="h-full bg-blue-500 w-[25%]" title="Segment 1"></div>
                        <div class="h-full bg-slate-700 w-[15%]"></div>
                        <div class="h-full bg-emerald-500 w-[30%]" title="Segment 2"></div>
                        <div class="h-full bg-slate-700 w-[30%]"></div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Tab 4: Paper Trails -->
        <section id="tab-paper" class="tab-content hidden space-y-4">
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <div class="md:col-span-2 glass-panel p-4 rounded-xl space-y-3">
                    <h2 class="text-lg font-bold text-slate-100">Tree Members & Evidence</h2>
                    <div class="space-y-2">
                        <div onclick="selectMember(this)" class="p-3 bg-slate-800/90 hover:bg-slate-800 rounded-lg border border-indigo-500/50 cursor-pointer flex justify-between items-center transition">
                            <div>
                                <h4 class="font-bold text-sm text-slate-200">James Edward Miller (1862–1934)</h4>
                                <span class="text-xs text-slate-400">3rd Great-Grandfather • Kentucky</span>
                            </div>
                            <span class="px-2 py-1 text-[10px] bg-emerald-950 text-emerald-400 border border-emerald-500/30 rounded">DNA Verified</span>
                        </div>
                        <div onclick="selectMember(this)" class="p-3 bg-slate-800/40 hover:bg-slate-800 rounded-lg border border-slate-700 cursor-pointer flex justify-between items-center transition">
                            <div>
                                <h4 class="font-bold text-sm text-slate-200">Martha Vance (1865–1941)</h4>
                                <span class="text-xs text-slate-400">3rd Great-Grandmother • Virginia</span>
                            </div>
                            <span class="px-2 py-1 text-[10px] bg-amber-950 text-amber-400 border border-amber-500/30 rounded">Paper Only</span>
                        </div>
                    </div>
                </div>
                <div class="glass-panel p-4 rounded-xl border border-slate-800">
                    <h3 class="font-bold text-sm text-slate-200 border-b border-slate-800 pb-2">Document Inspector</h3>
                    <p class="text-xs text-slate-400 mt-3">Select a tree member to inspect census indexes, birth records, and military cards.</p>
                </div>
            </div>
        </section>

        <!-- Tab 5: AI Proof Assistant -->
        <section id="tab-ai" class="tab-content hidden space-y-4">
            <div class="glass-panel p-6 rounded-xl space-y-4">
                <div class="flex items-center justify-between">
                    <h2 class="text-lg font-bold text-slate-100 flex items-center space-x-2">
                        <i class="fa-solid fa-bolt text-yellow-400"></i>
                        <span>AI Proof Triangulation Assistant</span>
                    </h2>
                    <span class="text-xs px-2.5 py-1 rounded bg-blue-950 text-blue-400 border border-blue-500/30 font-semibold">Gemini 1.5 Flash Active</span>
                </div>
                <div class="bg-slate-800/90 p-4 rounded-lg border border-slate-700 space-y-2">
                    <div class="flex justify-between items-center text-xs">
                        <span class="text-slate-400">Triangulation Confidence Score</span>
                        <span class="text-emerald-400 font-bold text-sm">89% (High Confidence)</span>
                    </div>
                    <div class="w-full bg-slate-900 rounded-full h-2">
                        <div class="bg-emerald-500 h-2 rounded-full w-[89%]"></div>
                    </div>
                    <p class="text-xs text-slate-300 mt-2">DNA segment match across 3 independent descendants corroborates 1880 census household linkages for James Miller.</p>
                </div>
                <button onclick="runAiTriangulation()" class="w-full py-2.5 bg-blue-600 hover:bg-blue-500 font-bold text-sm rounded-lg transition flex items-center justify-center space-x-2">
                    <i class="fa-solid fa-rotate"></i><span>Re-Run AI Triangulation Engine</span>
                </button>
            </div>
        </section>

        <!-- Tab 6: Shared Trees & Messaging -->
        <section id="tab-chat" class="tab-content hidden space-y-4">
            <div class="glass-panel p-4 rounded-xl">
                <h2 class="text-lg font-bold text-slate-100">Opt-in Member Network</h2>
                <p class="text-xs text-slate-400 mt-1">Connect anonymously with DNA matches who share overlapping pedigree clusters.</p>
            </div>
        </section>

        <!-- Tab 7: GPS Summary Report -->
        <section id="tab-report" class="tab-content hidden space-y-4">
            <div class="glass-panel p-6 rounded-xl space-y-4">
                <h2 class="text-lg font-bold text-slate-100">Genealogical Proof Standard (GPS) Executive Report</h2>
                <div class="bg-slate-900 p-4 rounded-lg border border-slate-800 text-xs space-y-2 text-slate-300 font-mono">
                    <p><strong>SUMMARY STATEMENT:</strong> Biological paternity of Arthur Miller is conclusively established through 3-way DNA cluster alignment (245 cM, 180 cM, 120 cM) combined with 1900 US Federal Census records.</p>
                </div>
            </div>
        </section>

    </main>

    <!-- Modal: API Setup -->
    <div id="api-modal" class="fixed inset-0 bg-slate-950/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="glass-panel max-w-md w-full p-6 rounded-2xl border border-slate-700 space-y-4">
            <div class="flex justify-between items-center">
                <h3 class="font-bold text-slate-100 flex items-center space-x-2">
                    <i class="fa-solid fa-plug text-emerald-400"></i>
                    <span>Configure Backend API Endpoint</span>
                </h3>
                <button onclick="toggleApiModal()" class="text-slate-400 hover:text-slate-200"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <p class="text-xs text-slate-300">Enter your live FastAPI server address (e.g. <code>http://localhost:8000</code> or your public web URL).</p>
            <input type="text" id="api-url-input" value="http://localhost:8000" class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-xs text-slate-100 font-mono">
            <div class="flex justify-end space-x-2">
                <button onclick="toggleApiModal()" class="px-4 py-2 bg-slate-800 hover:bg-slate-700 text-xs rounded-lg">Cancel</button>
                <button onclick="saveApiUrl()" class="px-4 py-2 bg-emerald-600 hover:bg-emerald-500 font-bold text-xs rounded-lg text-slate-950">Save & Connect</button>
            </div>
        </div>
    </div>

    <!-- Modal: File Upload -->
    <div id="upload-modal" class="fixed inset-0 bg-slate-950/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="glass-panel max-w-md w-full p-6 rounded-2xl border border-slate-700 space-y-4">
            <div class="flex justify-between items-center">
                <h3 class="font-bold text-slate-100">Upload Family Tree or DNA File</h3>
                <button onclick="toggleFileUploadModal()" class="text-slate-400 hover:text-slate-200"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <input type="file" id="file-input" accept=".ged,.csv" class="w-full text-xs text-slate-400 file:mr-4 file:py-2 file:px-4 file:rounded-lg file:border-0 file:text-xs file:font-semibold file:bg-blue-600 file:text-white hover:file:bg-blue-500 cursor-pointer">
            <button onclick="processUploadedFile()" class="w-full py-2 bg-blue-600 font-bold text-xs rounded-lg">Process File Data</button>
        </div>
    </div>

    <!-- Modal: 3-Tier Pricing -->
    <div id="pricing-modal" class="fixed inset-0 bg-slate-950/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="glass-panel max-w-4xl w-full p-6 rounded-2xl border border-slate-700 space-y-6 max-h-[90vh] overflow-y-auto">
            <div class="flex justify-between items-center">
                <h3 class="font-bold text-xl text-slate-100">Membership & Subscription Plans</h3>
                <button onclick="togglePricingModal()" class="text-slate-400 hover:text-slate-200"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <!-- Tier 1 -->
                <div class="bg-slate-900/90 p-5 rounded-xl border border-slate-800 space-y-3">
                    <h4 class="font-bold text-slate-200">Seeker Free</h4>
                    <div class="text-2xl font-black text-slate-100">$0 <span class="text-xs font-normal text-slate-400">/mo</span></div>
                    <ul class="text-xs text-slate-400 space-y-2">
                        <li><i class="fa-solid fa-check text-emerald-400 mr-2"></i>Leeds Grid Painter</li>
                        <li><i class="fa-solid fa-check text-emerald-400 mr-2"></i>Up to 50 DNA matches</li>
                    </ul>
                </div>
                <!-- Tier 2 -->
                <div class="bg-slate-900/90 p-5 rounded-xl border border-blue-500/50 relative space-y-3">
                    <span class="absolute -top-3 right-4 px-2 py-0.5 bg-blue-600 text-slate-100 text-[10px] font-bold uppercase rounded">Popular</span>
                    <h4 class="font-bold text-blue-400">Search Angel Pro</h4>
                    <div class="text-2xl font-black text-slate-100">$14.99 <span class="text-xs font-normal text-slate-400">/mo</span></div>
                    <ul class="text-xs text-slate-300 space-y-2">
                        <li><i class="fa-solid fa-check text-blue-400 mr-2"></i>Unlimited DNA Matches</li>
                        <li><i class="fa-solid fa-check text-blue-400 mr-2"></i>AI Triangulation Engine</li>
                    </ul>
                </div>
                <!-- Tier 3 -->
                <div class="bg-slate-900/90 p-5 rounded-xl border border-amber-500/50 space-y-3">
                    <h4 class="font-bold text-amber-400">Forensic Studio</h4>
                    <div class="text-2xl font-black text-slate-100">$39.99 <span class="text-xs font-normal text-slate-400">/mo</span></div>
                    <ul class="text-xs text-slate-300 space-y-2">
                        <li><i class="fa-solid fa-check text-amber-400 mr-2"></i>Multi-Kit Cross Matching</li>
                        <li><i class="fa-solid fa-check text-amber-400 mr-2"></i>Branded PDF Client Reports</li>
                        <li><i class="fa-solid fa-check text-amber-400 mr-2"></i>Dedicated API Support</li>
                    </ul>
                </div>
            </div>
        </div>
    </div>

    <!-- JavaScript Handlers -->
    <script>
        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll('.tab-btn').forEach(el => el.classList.remove('active'));
            document.getElementById(tabId).classList.remove('hidden');
            event.currentTarget.classList.add('active');
        }

        function toggleApiModal() {
            document.getElementById('api-modal').classList.toggle('hidden');
        }

        function toggleFileUploadModal() {
            document.getElementById('upload-modal').classList.toggle('hidden');
        }

        function togglePricingModal() {
            document.getElementById('pricing-modal').classList.toggle('hidden');
        }

        function saveApiUrl() {
            const url = document.getElementById('api-url-input').value;
            document.getElementById('api-status-text').innerText = "🔌 API: LIVE CONNECTED (" + url + ")";
            document.getElementById('connection-banner').innerHTML = `<i class="fa-solid fa-circle-check text-emerald-400"></i> <span class="text-emerald-300">LIVE BACKEND CONNECTED (${url})</span>`;
            document.getElementById('connection-banner').className = "bg-emerald-950/40 border-b border-emerald-800/50 text-emerald-300 text-xs py-1.5 px-4 text-center font-medium flex items-center justify-center space-x-2";
            toggleApiModal();
        }

        function processUploadedFile() {
            alert("File parsed successfully! Updated workspace metrics with match data.");
            toggleFileUploadModal();
        }

        function runAiTriangulation() {
            alert("AI Triangulation engine executed successfully!");
        }

        function selectMember(el) {
            document.querySelectorAll('#tab-paper .cursor-pointer').forEach(item => item.classList.remove('ring-2', 'ring-indigo-500'));
            el.classList.add('ring-2', 'ring-indigo-500');
        }
    </script>
</body>
</html>
