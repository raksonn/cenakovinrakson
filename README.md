# cenakovinrakson
Cene kovin
<!DOCTYPE html>
<html lang="sl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trenutna Cena Plemenitih Kovin | Zlato, Srebro, Platina</title>
    <meta name="description" content="Preverite aktualne cene plemenitih kovin na gram, unčo, 100g in kilogram. Vgrajen kalkulator za odkup zlata in grafi gibanja cen.">
    <!-- Tailwind CSS za sodoben dizajn -->
    <script src="https://jsdelivr.net"></script>
    <!-- Chart.js za napredne grafe -->
    <script src="https://jsdelivr.net"></script>
    <style>
        .modal { transition: opacity 0.25s ease; }
        body.modal-active { overflow: hidden; }
    </style>
</head>
<body class="bg-gray-50 text-gray-800 font-sans flex flex-col min-h-screen justify-between">

    <!-- NAVIGACIJA -->
    <header class="bg-white shadow-sm sticky top-0 z-50">
        <div class="max-w-6xl mx-auto px-4 py-4 flex flex-col sm:flex-row justify-between items-center gap-4">
            <a href="#" class="text-2xl font-bold text-amber-600 flex items-center gap-2">
                🪙 KovineUra.si
            </a>
            <nav class="flex flex-wrap gap-4 sm:gap-6 text-sm font-medium text-gray-600 justify-center">
                <a href="#tecaji" class="hover:text-amber-600 transition">Trenutni Tečaji</a>
                <a href="#kalkulator" class="hover:text-amber-600 transition">Odkupni Kalkulator</a>
                <a href="#grafi" class="hover:text-amber-600 transition">Zgodovinski Graf</a>
                <a href="#o-kovinah" class="hover:text-amber-600 transition">O kovinah</a>
                <a href="#kontakt" class="hover:text-amber-600 transition">Kontakt</a>
            </nav>
        </div>
    </header>

    <!-- ADSENSE REKLAMA VRH -->
    <div class="max-w-6xl mx-auto w-full px-4 mt-6 text-center">
        <div class="bg-gray-200 py-4 text-xs text-gray-500 rounded border border-dashed border-gray-400">
            [PROSTOR ZA ADSENSE OGLAS - Vrh strani]
            <!-- <ins class="adsbygoogle" style="display:block" data-ad-client="ca-pub-XXXXX" data-ad-slot="XXXXX" data-ad-format="auto"></ins> -->
        </div>
    </div>

    <!-- GLAVNA VSEBINA -->
    <main class="max-w-6xl mx-auto w-full px-4 py-8 flex-grow">
        
        <!-- UVOD IN CAS -->
        <div class="text-center mb-10">
            <h1 class="text-3xl md:text-4xl font-extrabold text-gray-900 mb-2">Aktualne Cene Plemenitih Kovin v EUR</h1>
            <p class="text-gray-600 max-w-2xl mx-auto">Spremljajte svetovne borzne cene za Zlato, Srebro in Platino. Podatki se osvežujejo glede na svetovne borze.</p>
            <div class="mt-4 inline-flex items-center gap-2 text-xs bg-amber-50 text-amber-800 px-3 py-1.5 rounded-full font-medium">
                <span class="w-2 h-2 rounded-full bg-green-500 animate-pulse"></span>
                Zadnja posodobitev: <span id="update-time">Osveževanje...</span>
            </div>
        </div>

        <!-- PRIKAZ CEN (KARTICE) -->
        <section id="tecaji" class="grid md:grid-cols-3 gap-6 mb-12">
            <!-- ZLATO -->
            <div class="bg-white rounded-2xl shadow-md border border-amber-100 overflow-hidden">
                <div class="bg-amber-500 text-white px-6 py-4 font-bold text-xl flex justify-between items-center">
                    <span>Zlato (Gold)</span>
                    <span class="text-2xl">✨</span>
                </div>
                <div class="p-6 divide-y divide-gray-100">
                    <div class="py-3 flex justify-between">
                        <span class="text-gray-500">1 Gram</span>
                        <span class="font-bold text-gray-900" id="gold-gram">- €</span>
                    </div>
                    <div class="py-3 flex justify-between">
                        <span class="text-gray-500">1 Trojanska unča (oz)</span>
                        <span class="font-bold text-gray-900" id="gold-ounce">- €</span>
                    </div>
                    <div class="py-3 flex justify-between">
                        <span class="text-gray-500">100 Gramov</span>
                        <span class="font-bold text-gray-900" id="gold-100g">- €</span>
                    </div>
                    <div class="py-3 flex justify-between">
                        <span class="text-gray-500">1 Kilogram (kg)</span>
                        <span class="font-bold text-gray-900" id="gold-kg">- €</span>
                    </div>
                </div>
            </div>

            <!-- SREBRO -->
            <div class="bg-white rounded-2xl shadow-md border border-slate-100 overflow-hidden">
                <div class="bg-slate-400 text-white px-6 py-4 font-bold text-xl flex justify-between items-center">
                    <span>Srebro (Silver)</span>
                    <span class="text-2xl">🪙</span>
                </div>
                <div class="p-6 divide-y divide-gray-100">
                    <div class="py-3 flex justify-between">
                        <span class="text-gray-500">1 Gram</span>
                        <span class="font-bold text-gray-900" id="silver-gram">- €</span>
                    </div>
                    <div class="py-3 flex justify-between">
                        <span class="text-gray-500">1 Trojanska unča (oz)</span>
                        <span class="font-bold text-gray-900" id="silver-ounce">- €</span>
                    </div>
                    <div class="py-3 flex justify-between">
                        <span class="text-gray-500">100 Gramov</span>
                        <span class="font-bold text-gray-900" id="silver-100g">- €</span>
                    </div>
                    <div class="py-3 flex justify-between">
                        <span class="text-gray-500">1 Kilogram (kg)</span>
                        <span class="font-bold text-gray-900" id="silver-kg">- €</span>
                    </div>
                </div>
            </div>

            <!-- PLATINA -->
            <div class="bg-white rounded-2xl shadow-md border border-teal-100 overflow-hidden">
                <div class="bg-teal-600 text-white px-6 py-4 font-bold text-xl flex justify-between items-center">
                    <span>Platina (Platinum)</span>
                    <span class="text-2xl">💿</span>
                </div>
                <div class="p-6 divide-y divide-gray-100">
                    <div class="py-3 flex justify-between">
                        <span class="text-gray-500">1 Gram</span>
                        <span class="font-bold text-gray-900" id="plat-gram">- €</span>
                    </div>
                    <div class="py-3 flex justify-between">
                        <span class="text-gray-500">1 Trojanska unča (oz)</span>
                        <span class="font-bold text-gray-900" id="plat-ounce">- €</span>
                    </div>
                    <div class="py-3 flex justify-between">
                        <span class="text-gray-500">100 Gramov</span>
                        <span class="font-bold text-gray-900" id="plat-100g">- €</span>
                    </div>
                    <div class="py-3 flex justify-between">
                        <span class="text-gray-500">1 Kilogram (kg)</span>
                        <span class="font-bold text-gray-900" id="plat-kg">- €</span>
                    </div>
                </div>
            </div>
        </section>

        <!-- ADSENSE REKLAMA SREDA -->
        <div class="w-full text-center mb-12">
            <div class="bg-gray-200 py-4 text-xs text-gray-500 rounded border border-dashed border-gray-400">
                [PROSTOR ZA ADSENSE OGLAS - Sredina strani]
            </div>
        </div>

        <!-- KALKULATOR ZA OTKUP Z MARŽO -->
        <section id="kalkulator" class="bg-white p-6 md:p-8 rounded-2xl shadow-md border border-gray-100 mb-12">
            <h2 class="text-2xl font-bold text-gray-950 mb-2">🧮 Pametni kalkulator odkupne vrednosti</h2>
            <p class="text-sm text-gray-500 mb-6">Izračunajte informativno odkupno vrednost. Vključena je vaša prilagodljiva marža portala.</p>
            <div class="grid md:grid-cols-4 gap-4 items-end">
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Izberi kovino</label>
                    <select id="calc-metal" class="w-full border border-gray-300 rounded-lg p-2.5 bg-gray-50 focus:ring-2 focus:ring-amber-500">
                        <option value="gold">Zlato</option>
                        <option value="silver">Srebro</option>
                        <option value="platinum">Platina</option>
                    </select>
                </div>
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Količina</label>
                    <input type="number" id="calc-amount" value="1" min="0.01" step="any" class="w-full border border-gray-300 rounded-lg p-2.5 bg-gray-50 focus:ring-2 focus:ring-amber-500">
                </div>
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Enota</label>
                    <select id="calc-unit" class="w-full border border-gray-300 rounded-lg p-2.5 bg-gray-50 focus:ring-2 focus:ring-amber-500">
                        <option value="gram">Gram (g)</option>
                        <option value="ounce">Trojanska unča (oz)</option>
                        <option value="100g">100 Gramov</option>
                        <option value="kg">Kilogram (kg)</option>
                    </select>
                </div>
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Vaša marža odkupa (%)</label>
                    
            </div>
        </section>

    </main>

    <!-- NOGA STRANI -->
    <footer class="bg-white border-t border-gray-200 mt-12 py-6">
        <div class="max-w-6xl mx-auto px-4 flex flex-col md:flex-row justify-between items-center gap-4 text-xs text-gray-500">
            <div>
                &copy; 2026 KovineUra. Vse pravice pridržane. Podatki so informativne narave.
            </div>
            <div class="flex gap-4 font-medium">
                <button onclick="toggleModal('privacy-modal')" class="hover:underline cursor-pointer">Politika zasebnosti</button>
                <button onclick="toggleModal('terms-modal')" class="hover:underline cursor-pointer">Pogoji poslovanja</button>
                <button onclick="toggleModal('disclaimer-modal')" class="hover:underline cursor-pointer">Pravno obvestilo</button>
            </div>
        </div>
    </footer>

    <!-- MODALNA OKNA -->
    <div id="privacy-modal" class="modal opacity-0 pointer-events-none fixed w-full h-full top-0 left-0 flex items-center justify-center z-50">
        <div class="modal-overlay absolute w-full h-full bg-gray-900/50 backdrop-blur-xs"></div>
        <div class="modal-container bg-white w-11/12 md:max-w-xl mx-auto rounded-xl shadow-lg z-50 overflow-y-auto max-h-[80vh] p-6">
            <h3 class="text-xl font-bold mb-4">Politika zasebnosti in piškotki</h3>
            <div class="text-sm text-gray-600 space-y-3">
                <p>Na tej spletni strani spoštujemo vašo zasebnost. Stran uporablja Google AdSense za prikazovanje oglasov.</p>
            </div>
            <button onclick="toggleModal('privacy-modal')" class="mt-6 bg-gray-900 text-white px-4 py-2 rounded-lg text-sm font-semibold hover:bg-gray-800 cursor-pointer">Zapri</button>
        </div>
    </div>

    <!-- JAVASCRIPT IN LOGIKA -->
    <script>
        const API_KEY = 'goldapi-30f777ec0212ee9a251d9fe7f67af070-io'; 
        
        let pricesInOunce = { gold: 2380.45, silver: 28.90, platinum: 945.20 };

        function calculateUnits(ouncePrice) {
            const gram = ouncePrice / 31.1034768;
            return { ounce: ouncePrice, gram: gram, g100: gram * 100, kg: gram * 1000 };
        }

        function updateUI() {
            const gold = calculateUnits(pricesInOunce.gold);
            const silver = calculateUnits(pricesInOunce.silver);
            const platinum = calculateUnits(pricesInOunce.platinum);

            document.getElementById('gold-gram').innerText = gold.gram.toFixed(2) + ' €';
            document.getElementById('gold-ounce').innerText = gold.ounce.toFixed(2) + ' €';
            document.getElementById('gold-100g').innerText = gold.g100.toFixed(2) + ' €';
            document.getElementById('gold-kg').innerText = gold.kg.toLocaleString('sl-SI') + ' €';

            document.getElementById('silver-gram').innerText = silver.gram.toFixed(2) + ' €';
            document.getElementById('silver-ounce').innerText = silver.ounce.toFixed(2) + ' €';
            document.getElementById('silver-100g').innerText = silver.g100.toFixed(2) + ' €';
            document.getElementById('silver-kg').innerText = silver.kg.toLocaleString('sl-SI') + ' €';

            document.getElementById('plat-gram').innerText = platinum.gram.toFixed(2) + ' €';
            document.getElementById('plat-ounce').innerText = platinum.ounce.toFixed(2) + ' €';
            document.getElementById('plat-100g').innerText = platinum.g100.toFixed(2) + ' €';
            document.getElementById('plat-kg').innerText = platinum.kg.toLocaleString('sl-SI') + ' €';

            const sedaj = new Date();
            document.getElementById('update-time').innerText = sedaj.toLocaleDateString('sl-SI') + ' ob ' + sedaj.toLocaleTimeString('sl-SI');
            runCalculator();
        }

        async function fetchLivePrices() {
            if(!API_KEY || API_KEY === 'goldapi-30f777ec0212ee9a251d9fe7f67af070-io') {
                updateUI();
                return;
            }
            try {
                const responseGold = await fetch('https://goldapi.io', { headers: { 'x-access-token': API_KEY } });
                const dataGold = await responseGold.json();
                if(dataGold.price) pricesInOunce.gold = dataGold.price;
                updateUI();
            } catch (error) {
                console.error(error);
                updateUI();
            }
        }

        function runCalculator() {
            const metal = document.getElementById('calc-metal').value;
            const amount = parseFloat(document.getElementById('calc-amount').value) || 0;
            const unit = document.getElementById('calc-unit').value;
            const marginPercent = parseFloat(document.getElementById('calc-margin').value) || 0;

            const units = calculateUnits(pricesInOunce[metal]);
            let marketPrice = 0;
            if(unit === 'gram') marketPrice = units.gram * amount;
            if(unit === 'ounce') marketPrice = units.ounce * amount;
            if(unit === '100g') marketPrice = units.g100 * amount;
            if(unit === 'kg') marketPrice = units.kg * amount;

            let finalPayout = marketPrice * (1 + (marginPercent / 100));
            document.getElementById('calc-market-result').innerText = marketPrice.toLocaleString('sl-SI') + ' €';
            document.getElementById('calc-result').innerText = finalPayout.toLocaleString('sl-SI') + ' €';
        }

        document.getElementById('calc-metal').addEventListener('change', runCalculator);
        document.getElementById('calc-amount').addEventListener('input', runCalculator);
        document.getElementById('calc-unit').addEventListener('change', runCalculator);
        document.getElementById('calc-margin').addEventListener('input', runCalculator);

        function toggleModal(modalId) {
            document.getElementById(modalId).classList.toggle('opacity-0');
            document.getElementById(modalId).classList.toggle('pointer-events-none');
        }

        window.onload = function() { fetchLivePrices(); };
    </script>
</body>
</html>
