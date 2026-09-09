<!DOCTYPE html>
<html lang="sl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Spremljanje borznih cen & Kalkulator</title>
    
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #121212;
            color: #ffffff;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }

        main {
            flex: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 20px;
            max-width: 500px;
            margin: 0 auto;
            width: 100%;
        }

        .info-text {
            text-align: center;
            color: #b3b3b3;
            font-size: 0.95rem;
            line-height: 1.4;
        }

        .status-box {
            font-size: 0.85rem;
            color: #f1c40f;
            margin-bottom: 10px;
        }

        .card {
            background-color: #1e1e1e;
            border: 1px solid #333;
            border-radius: 12px;
            padding: 20px;
            width: 100%;
            box-sizing: border-box;
            box-shadow: 0 4px 15px rgba(0,0,0,0.5);
        }

        h2 {
            margin-top: 0;
            font-size: 1.3rem;
            display: flex;
            align-items: center;
            gap: 8px;
            border-bottom: 1px solid #333;
            padding-bottom: 10px;
        }

        .gold-title { color: #f1c40f; }
        .silver-title { color: #bdc3c7; }

        .price-row {
            display: flex;
            justify-content: space-between;
            padding: 10px 0;
            border-bottom: 1px dashed #2c2c2c;
        }
        .price-row:last-child { border-bottom: none; }

        .price-value {
            font-weight: bold;
            color: #2ecc71;
        }

        /* Stil za kalkulator spodaj */
        .form-group { margin-bottom: 15px; }
        label { display: block; margin-bottom: 5px; font-weight: bold; font-size: 0.9rem; color: #ccc;}
        select, input {
            width: 100%; padding: 10px; background-color: #2c2c2c; border: 1px solid #444;
            border-radius: 6px; box-sizing: border-box; color: #fff; font-size: 1rem;
        }
        button {
            width: 100%; padding: 12px; background-color: #f1c40f; color: #121212;
            border: none; border-radius: 6px; font-size: 1rem; cursor: pointer; font-weight: bold;
        }
        button:hover { background-color: #f39c12; }
        .result-box {
            margin-top: 15px; padding: 15px; background-color: #1a252f;
            border-left: 4px solid #f1c40f; border-radius: 4px; display: none;
        }
    </style>
</head>
<body>

<main>
    <p class="info-text">
        Spremljajte svetovne borzne cene za Zlato in Srebro. 
        Podatki se osvežujejo glede na svetovne borze.
    </p>
    
    <div class="status-box" id="status-update">Zadnja posodobitev: Osveževanje...</div>

    <!-- KARTICA ZA ZLATO -->
    <div class="card">
        <h2 class="gold-title">✨ Zlato (Gold)</h2>
        <div class="price-row"><span>1 Gram</span><span class="price-value" id="gold-g">- €</span></div>
        <div class="price-row"><span>1 Trojanska unča (oz)</span><span class="price-value" id="gold-oz">- €</span></div>
        <div class="price-row"><span>100 Gramov</span><span class="price-value" id="gold-100g">- €</span></div>
        <div class="price-row"><span>1 Kilogram (kg)</span><span class="price-value" id="gold-kg">- €</span></div>
    </div>

    <!-- KARTICA ZA SREBRO -->
    <div class="card">
        <h2 class="silver-title">🪙 Srebro (Silver)</h2>
        <div class="price-row"><span>1 Gram</span><span class="price-value" id="silver-g">- €</span></div>
        <div class="price-row"><span>1 Trojanska unča (oz)</span><span class="price-value" id="silver-oz">- €</span></div>
        <div class="price-row"><span>100 Gramov</span><span class="price-value" id="silver-100g">- €</span></div>
    </div>

    <!-- KALKULATOR ODKUPA -->
    <div class="card">
        <h2 style="color: #3498db;">📊 Pametni kalkulator</h2>
        <div class="form-group">
            <label>Izberi kovino:</label>
            <select id="calc-kovina">
                <option value="gold">Zlato</option>
                <option value="silver">Srebro</option>
            </select>
        </div>
        <div class="form-group">
            <label>Količina:</label>
            <input type="number" id="calc-kolicina" value="1" min="0" step="any">
        </div>
        <div class="form-group">
            <label>Enota:</label>
            <select id="calc-enota">
                <option value="oz">Trojanska unča (oz)</option>
                <option value="g">Gram (g)</option>
            </select>
        </div>
        <div class="form-group">
            <label>Vaša marža odkupa (%):</label>
            <input type="number" id="calc-marza" value="0" min="0" max="100" step="0.1">
        </div>
        <button id="calc-gumb">Izračunaj vrednost</button>
        <div id="calc-rezultat" class="result-box"></div>
    </div>
</main>

<script>
    // Globalni spremenljivki za shranjevanje pridobljenih cen (za unčo v EUR)
    let trenutnaCenaZlatoOz = 2320.50; // Privzeta varnostna vrednost
    let trenutnaCenaSrebroOz = 28.40;   // Privzeta varnostna vrednost

    async function osveziBorzneCene() {
        const statusDiv = document.getElementById("status-update");
        
        try {
            // Uporabimo zanesljiv javni API za osveževanje valut in kovin
            const response = await fetch("https://er-api.com");
            if (!response.ok) throw new Error("Napaka pri prenosu podatkov");
            
            const data = await response.json();
            
            // API vrne vrednost EUR glede na 1 unčo zlata (XAU) in srebra (XAG) iz obratnega razmerja
            if (data.rates && data.rates.XAU && data.rates.XAG) {
                trenutnaCenaZlatoOz = 1 / data.rates.XAU;
                trenutnaCenaSrebroOz = 1 / data.rates.XAG;
                
                const zdaj = new Date();
                statusDiv.innerText = `Zadnja posodobitev: ${zdaj.toLocaleTimeString('sl-SI')}`;
            } else {
                statusDiv.innerText = "Zadnja posodobitev: Uporabljeni offline podatki (osveževanje ni uspelo).";
            }
        } catch (error) {
            console.error("API Error:", error);
            statusDiv.innerText = "Zadnja posodobitev: Način brez povezave (prikazane privzete cene).";
        }

        PrikaziCeneNaStrani();
    }

    function PrikaziCeneNaStrani() {
        // Izračuni za Zlato
        const zlatoOz = trenutnaCenaZlatoOz;
        const zlatoG = zlatoOz / 31.1035;

        document.getElementById("gold-oz").innerText = `${zlatoOz.toFixed(2)} €`;
        document.getElementById("gold-g").innerText = `${zlatoG.toFixed(2)} €`;
        document.getElementById("gold-100g").innerText = `${(zlatoG * 100).toFixed(2)} €`;
        document.getElementById("gold-kg").innerText = `${(zlatoG * 1000).toFixed(2)} €`;

        // Izračuni za Srebro
        const srebroOz = trenutnaCenaSrebroOz;
        const srebroG = srebroOz / 31.1035;

        document.getElementById("silver-oz").innerText = `${srebroOz.toFixed(2)} €`;
        document.getElementById("silver-g").innerText = `${srebroG.toFixed(2)} €`;
        document.getElementById("silver-100g").innerText = `${(srebroG * 100).toFixed(2)} €`;
    }

    // Logika kalkulatorja
    document.getElementById("calc-gumb").addEventListener("click", function() {
        const kovina = document.getElementById("calc-kovina").value;
        const kolicina = parseFloat(document.getElementById("calc-kolicina").value) || 0;
        const enota = document.getElementById("calc-enota").value;
        const marza = parseFloat(document.getElementById("calc-marza").value) || 0;
        const rezultatDiv = document.getElementById("calc-rezultat");

        let izbranaCenaOz = (kovina === "gold") ? trenutnaCenaZlatoOz : trenutnaCenaSrebroOz;
        let cenaZaEnoto = (enota === "g") ? (izbranaCenaOz / 31.1035) : izbranaCenaOz;

        let borznaVrednost = cenaZaEnoto * kolicina;
        let končnaVrednost = borznaVrednost * (1 - (marza / 100));

        rezultatDiv.style.display = "block";
        rezultatDiv.innerHTML = `
            <h3 style="margin-top:0; color:#f1c40f;">Izračun:</h3>
            <p>Skupna borzna vrednost: <strong>${borznaVrednost.toFixed(2)} EUR</strong></p>
            <p>Odkupna cena (z odšteto maržo): <strong style="color:#2ecc71; font-size:1.15em;">${končnaVrednost.toFixed(2)} EUR</strong></p>
        `;
    });

    // Zagon ob nalaganju strani
    document.addEventListener("DOMContentLoaded", osveziBorzneCene);
</script>

</body>
</html>
