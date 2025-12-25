---
title: Calculateur de dégâts
subtitle: Adapté pour Dofus Unity (Dofus 3).
layout: page
permalink: /dofus/calculateur-de-degats
hidden: true
pagination: 
  enabled: true
---

<style>
/* =======================
   CONTENEUR
======================= */
#dofusCalc__container {
    background: #f0f0f0;
    padding: 10px;
    border-radius: 12px;
    max-width: 600px;
    font-family: Arial, sans-serif;
    box-shadow: 0 4px 10px rgba(0,0,0,0.08);
    margin-left: auto;
    margin-right: auto;
}

/* =======================
   TITRES
======================= */
#dofusCalc__container h3 {
    text-align: center;
    margin: 25px 0 15px;
}

/* =======================
   GRILLES
======================= */
.dofusCalc__twoCols {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 40px;
}

/* =======================
   STATS & BONUS
======================= */
.dofusCalc__col {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.dofusCalc__row {
    display: flex;
    align-items: center;
    gap: 6px;
    margin-bottom: 6px;
}

.dofusCalc__row input {
    width: 60px;
    text-align: center;
}

/* =======================
   LIGNES DE DÉGÂTS
======================= */
.dofusCalc__line {
    display: grid;
    grid-template-columns: auto 1fr auto;
    gap: 10px;
    align-items: center;
    margin-bottom: 8px;
}

.dofusCalc__line select,
.dofusCalc__line input {
    width: 60px;
    text-align: center;
}

.dofusCalc__remove {
    cursor: pointer;
}

/* Conteneur des lignes */
#dofusCalc__lines {
    display: flex;
    flex-direction: column;
    align-items: center;
}

/* Ligne de dégâts */
.dofusCalc__line {
    justify-content: center;
}

/* Grille dégâts avec titres */
.dofusCalc__damageGrid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 6px 8px;
    text-align: center;
}

/* Titres des blocs */
.dofusCalc__damageLabel {
    grid-column: span 2;
    font-size: 12px;
    font-weight: bold;
}



.dofusCalc__damageGrid input {
    width: 88px;
    text-align: center;
}

/* =======================
   BOUTONS
======================= */
#dofusCalc__addLine,
#dofusCalc__button {
    margin-top: 15px;
    padding: 8px 14px;
    cursor: pointer;
    border-radius: 8px;
    border: none;
}

#dofusCalc__addLine {
    display: block;
    margin: 5px auto;
    background: #e0e0e0;
    transition: background 0.2s ease, transform 0.1s ease;
}

#dofusCalc__addLine:hover {
    background: #d0d0d0;
    transform: scale(1.03);
}

#dofusCalc__button {
    margin-top: 15px;
    padding: 10px 18px;
    background: #3bb54a;          /* vert */
    color: white;
    font-weight: bold;
    border-radius: 10px;
    border: none;
    cursor: pointer;
    display: block;
    margin-left: auto;
    margin-right: auto;
}

#dofusCalc__button:hover {
    background: #33a041;
}

/* Sélecteur d'élément (emoji) */
.dofusCalc__line select {
    font-size: 22px;      /* emoji plus grand */
    padding: 1px 2px;
    height: 54px;
    width: 54px;
    border-radius: 8px;
    cursor: pointer;
}

/* Bouton supprimer taille fixe */
.dofusCalc__remove {
    width: 54px;
    height: 54px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 20px;
    cursor: pointer;
}

/* =======================
   RÉSULTAT
======================= */
#dofusCalc__result {
    margin-top: 20px;
    font-weight: bold;
    white-space: pre-line;
    text-align: center;
}

/* Encadré de la grille de dégâts */
.dofusCalc__damageGrid {
    background: #f7f7f7;
    padding: 6px 8px;
    border-radius: 8px;
    border: 1px solid #d0d0d0;
}
</style>

<div id="dofusCalc__container">

<div class="dofusCalc__twoCols">
    <div class="dofusCalc__col">
        <p><strong>Caractéristiques</strong></p>
        <div class="dofusCalc__row">⚡ <input id="dofusCalc__puissance" type="number" value="0"></div>
        <div class="dofusCalc__row">🌳 <input id="dofusCalc__force" type="number" value="0"></div>
        <div class="dofusCalc__row">🔥 <input id="dofusCalc__intel" type="number" value="0"></div>
        <div class="dofusCalc__row">💧 <input id="dofusCalc__chance" type="number" value="0"></div>
        <div class="dofusCalc__row">🌪️ <input id="dofusCalc__agi" type="number" value="0"></div>
    </div>
    <div class="dofusCalc__col">
        <p><strong>Dommages Bonus</strong></p>
        <div class="dofusCalc__row">☯️ <input id="dofusCalc__bNeutre" type="number" value="0"></div>
        <div class="dofusCalc__row">🌳 <input id="dofusCalc__bTerre" type="number" value="0"></div>
        <div class="dofusCalc__row">🔥 <input id="dofusCalc__bFeu" type="number" value="0"></div>
        <div class="dofusCalc__row">💧 <input id="dofusCalc__bEau" type="number" value="0"></div>
        <div class="dofusCalc__row">🌪️ <input id="dofusCalc__bAir" type="number" value="0"></div>
    </div>
</div>

<p style="text-align:center;padding-top:15px;"><strong>Dégâts du sort ou de l'arme</strong></p>

<div id="dofusCalc__lines"></div>
<button id="dofusCalc__addLine">➕ Ajouter une ligne de dégâts</button>

<button id="dofusCalc__button">Calculer les dégâts</button>

<div id="dofusCalc__result"></div>

</div>

<script>
(function () {

const el = id => document.getElementById(id);

/* =======================
   MAPPINGS
======================= */
const elementMap = {
    neutre: { stat: "force", bonus: "bNeutre", emoji: "☯️" },
    terre:  { stat: "force", bonus: "bTerre",  emoji: "🌳" },
    feu:    { stat: "intel", bonus: "bFeu",    emoji: "🔥" },
    eau:    { stat: "chance",bonus: "bEau",    emoji: "💧" },
    air:    { stat: "agi",   bonus: "bAir",    emoji: "🌪️" }
};

/* =======================
   GETTERS
======================= */
const getStat = name => +el("dofusCalc__" + name).value || 0;
const getBonus = name => +el("dofusCalc__" + name).value || 0;

/* =======================
   CRÉATION LIGNE
======================= */
const createLine = () => {
    const line = document.createElement("div");
    line.className = "dofusCalc__line";

    line.innerHTML = `
        <select class="element">
            <option value="neutre">☯️</option>
            <option value="terre">🌳</option>
            <option value="feu">🔥</option>
            <option value="eau">💧</option>
            <option value="air">🌪️</option>
        </select>

        <div class="dofusCalc__damageGrid">

            <div class="dofusCalc__damageLabel">Normaux</div>
            <input type="number" class="nMin" placeholder="Min">
            <input type="number" class="nMax" placeholder="Max">

            <div class="dofusCalc__damageLabel">Coup critique</div>
            <input type="number" class="cMin" placeholder="Min">
            <input type="number" class="cMax" placeholder="Max">

        </div>

        <span class="dofusCalc__remove">❌</span>
    `;

    line.querySelector(".dofusCalc__remove").onclick = () => line.remove();
    el("dofusCalc__lines").appendChild(line);
};

/* =======================
   CALCUL
======================= */
const calculate = () => {
    let out = "Dommages finaux :\n";

    let totalNMin = 0;
    let totalNMax = 0;
    let totalCMin = 0;
    let totalCMax = 0;

    document.querySelectorAll(".dofusCalc__line").forEach(line => {
        const element = line.querySelector(".element").value;
        const map = elementMap[element];

        const multi = (getStat(map.stat) + getStat("puissance")) / 100;
        const bonus = getBonus(map.bonus);

        const nMin = +line.querySelector(".nMin").value || 0;
        const nMax = +line.querySelector(".nMax").value || 0;
        const cMin = +line.querySelector(".cMin").value || 0;
        const cMax = +line.querySelector(".cMax").value || 0;

        const calc = v => Math.floor(v + v * multi + bonus);

        const rNMin = calc(nMin);
        const rNMax = calc(nMax);
        const rCMin = calc(cMin);
        const rCMax = calc(cMax);

        // affichage ligne
        out += `${map.emoji} ${rNMin} à ${rNMax}  -  ❗ ${rCMin} à ${rCMax}\n`;

        // cumul
        totalNMin += rNMin;
        totalNMax += rNMax;
        totalCMin += rCMin;
        totalCMax += rCMax;
    });

    out += `\nDommages totaux :\n`;
    out += `🗡️ ${totalNMin} à ${totalNMax}  -  ❗ ${totalCMin} à ${totalCMax}`;

    el("dofusCalc__result").textContent = out;
};

/* =======================
   EVENTS
======================= */
el("dofusCalc__addLine").onclick = createLine;
el("dofusCalc__button").onclick = calculate;

/* INIT */
createLine();

})();
</script>