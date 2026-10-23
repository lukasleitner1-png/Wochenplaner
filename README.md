<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Schichtplanung Maschinen</title>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Barlow:wght@400;600;700&family=Barlow+Semi+Condensed:wght@600;700&display=swap">
<style>
:root {
  box-sizing: border-box;
  padding-top: env(safe-area-inset-top, 0px);
  padding-bottom: env(safe-area-inset-bottom, 0px);
  color-scheme: light;
  --bg: #e7ebf0; --card: #fff; --ink: #14202b; --mut: #5d6b79; --line: #cfd7df;
  --acc: #0b5fb3; --accbg: #dcebfa; --ok: #188a52; --okbg: #d1e7dd; --warn: #c98400; --bad: #d3322a;
}
:root[data-theme="dark"] {
  color-scheme: dark;
  --bg: #10171e; --card: #18222c; --ink: #eaf0f5; --mut: #92a1b0; --line: #2a3846;
  --acc: #5aa7f0; --accbg: #1c3550; --ok: #43c486; --okbg: #0f3d2a; --warn: #f0b429; --bad: #ff6b61;
}
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    color-scheme: dark;
    --bg: #10171e; --card: #18222c; --ink: #eaf0f5; --mut: #92a1b0;
    --line: #2a3846; --acc: #5aa7f0; --accbg: #1c3550; --ok: #43c486; --okbg: #0f3d2a; --warn: #f0b429; --bad: #ff6b61;
  }
}
html { scroll-padding-top: env(safe-area-inset-top, 0px); height: 100%; }
*, *::before, *::after { box-sizing: inherit; }
body { margin: 0; background: var(--bg); color: var(--ink); font: 16px/1.4 Barlow, system-ui, sans-serif; min-height: 100%; }
.wrap { max-width: 1200px; margin: 0 auto; padding: 12px 14px 40px; }
h1 { font: 700 24px/1.1 "Barlow Semi Condensed", Barlow, sans-serif; margin: 6px 0 12px; }
h2 { font: 700 18px "Barlow Semi Condensed", Barlow, sans-serif; margin: 22px 0 8px; }
.tabs, .row { display: flex; gap: 6px; flex-wrap: wrap; }
button, select, input, textarea { font: inherit; color: inherit; }
.tab, .chip { min-height: 44px; padding: 8px 14px; border: 1.5px solid var(--line); background: var(--card); border-radius: 8px; cursor: pointer; font-weight: 600; }
.tab[aria-pressed="true"], .chip[aria-pressed="true"] { background: var(--acc); border-color: var(--acc); color: #fff; }
.days { display: flex; gap: 6px; overflow-x: auto; padding: 2px 0 8px; margin: 6px 0 4px; }
.chip { flex: 1 0 auto; text-align: center; line-height: 1.15; padding: 6px 10px; }
.chip.we { border-style: dashed; }
.chip small { display: block; font-weight: 400; opacity: .85; }
.btn { min-height: 44px; padding: 8px 14px; border-radius: 8px; border: 1.5px solid var(--acc); background: var(--accbg); color: var(--acc); font-weight: 700; cursor: pointer; }
.btn.s { min-height: 40px; padding: 4px 10px; font-size: 14px; }
.wnv { display: flex; gap: 8px; align-items: center; margin: 10px 0 2px; }
.wnv .wl { flex: 1; text-align: center; line-height: 1.15; }
.wnv .wl small { display: block; color: var(--mut); }
.tools { display: flex; gap: 8px; flex-wrap: wrap; align-items: center; margin: 8px 0; }
.card, .m { background: var(--card); border: 1px solid var(--line); border-radius: 10px; padding: 10px 12px; }
.m { border-left: 8px solid var(--line); margin: 8px 0; }
.m.u { outline: 2px solid var(--bad); outline-offset: -1px; }
.mh { display: grid; grid-template-columns: 1fr 90px; gap: 8px; align-items: end; }
.mn { font: 700 18px "Barlow Semi Condensed", Barlow, sans-serif; }
.mn small { font: 400 14px Barlow; color: var(--mut); }
select, input[type=time], input[type=number], input[type=text] { min-height: 44px; width: 100%; padding: 6px 8px; border: 1.5px solid var(--line); border-radius: 8px; background: var(--bg); }
.md { display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 8px; margin: 8px 0; align-items: end; }
label { font-size: 13px; color: var(--mut); display: block; }
.rue { display: flex; align-items: center; gap: 8px; min-height: 44px; font-size: 15px; color: var(--ink); }
.sr { display: grid; grid-template-columns: 1fr 100px 28px 100px 44px; gap: 6px; align-items: center; margin: 4px 0; }
.x { min-height: 44px; border: 1.5px solid var(--line); border-radius: 8px; background: var(--card); cursor: pointer; color: var(--bad); }
.add { display: flex; gap: 6px; flex-wrap: wrap; margin-top: 6px; }
.gs { overflow-x: auto; }
.gt { min-width: 780px; }
.gr { display: grid; grid-template-columns: 120px 1fr; gap: 8px; align-items: center; margin: 3px 0; }
.gn { font-weight: 600; font-size: 14px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
.gl { position: relative; height: 34px; border-radius: 6px; background: var(--card); repeating-linear-gradient(90deg, var(--line) 0 1px, transparent 1px calc(100%/6)); }
.gb { position: absolute; top: 3px; bottom: 3px; border-radius: 5px; color: #fff; font-size: 12px; font-weight: 600; padding: 0 5px; display: flex; align-items: center; overflow: hidden; white-space: nowrap; }
.gh { position: relative; height: 18px; margin-left: 128px; font-size: 12px; color: var(--mut); }
.gh span { position: absolute; transform: translateX(-50%); }
.now { position: absolute; top: 0; bottom: 0; width: 2px; background: var(--bad); z-index: 2; }
.leg { display: flex; flex-wrap: wrap; gap: 8px; margin: 10px 0; font-size: 14px; }
.leg i { display: inline-block; width: 12px; height: 12px; border-radius: 3px; margin-right: 5px; vertical-align: -1px; }

/* Status-Markierungen für Aufträge */
.oc { display: block; width: 100%; text-align: left; margin: 8px 0; cursor: pointer; background: var(--card); color: var(--ink); font: inherit; border-left: 8px solid var(--line); transition: all 0.2s; }
.st-ok { border-left-color: var(--ok); }
.st-warn { border-left-color: var(--warn); }
.st-bad { border-left-color: var(--bad); }
.st-blue { border-left-color: var(--acc); }
.st-none { border-left-color: var(--line); }

/* Besondere Hervorhebung wenn heute aktualisiert */
.is-updated-today {
  background: var(--okbg) !important;
  border-color: var(--ok) !important;
}
.badge-updated {
  display: inline-block;
  background: var(--ok);
  color: #fff;
  font-weight: 700;
  font-size: 11px;
  padding: 2px 6px;
  border-radius: 4px;
  margin-left: 6px;
}

/* Neue Maschinen-Wochen-Tabelle */
.m-table { width: 100%; border-collapse: collapse; min-width: 900px; font-size: 13px; }
.m-table th, .m-table td { border: 1px solid var(--line); padding: 8px 6px; vertical-align: top; }
.m-table th { background: var(--accbg); color: var(--acc); font-weight: 700; }
.m-table .m-name { font-weight: 700; font-size: 14px; background: var(--card); position: sticky; left: 0; }
.m-cell-emp { font-weight: 600; color: var(--ink); }
.m-cell-ord { font-size: 11px; color: var(--mut); margin-top: 4px; border-top: 1px dashed var(--line); padding-top: 2px; }

.ol { margin: 6px 0; padding: 6px 8px; background: var(--bg); border-radius: 8px; font-size: 14px; }
.fr { display: grid; grid-template-columns: 160px 1fr; gap: 8px; align-items: center; margin: 8px 0; }
.fr label { text-align: right; }
.hint { color: var(--mut); font-size: 14px; }
.next-order-box { border: 1.5px dashed var(--acc); padding: 10px; border-radius: 8px; margin-top: 10px; background: var(--accbg); }
@media (max-width: 620px) { .fr { grid-template-columns: 1fr; } .fr label { text-align: left; } }
</style>
</head>
<body>
<div class="wrap">
<h1>Schichtplanung Maschinen</h1>
<div class="tabs">
  <button class="tab" data-tab="plan">Planung</button>
  <button class="tab" data-tab="day">Tagesansicht</button>
  <button class="tab" data-tab="week">Wochenübersicht Maschinen</button> 
  <button class="tab" data-tab="orders">Aufträge & Status</button>
</div>
<div id="app"></div>
</div>

<script>
const M = ["CTX beta 800 1", "CTX beta 800 2", "HQR-1", "HQR 2", "HQR 3", "Multiplex 6200", "NEXUS 200 M", "NEXUS 350 M", "NEXUS 900 M", "INTEGREX 1", "INTEGREX 2", "CLX450 TC 1", "CLX450 TC 2"];
const SH = [["Nacht", -220, 260], ["Früh", 260, 740], ["Normal 6-18", 360, 1080], ["Spät", 740, 1220]];
const WS = -220, WE = 1220, WL = WE - WS;
const DN = ["Mo", "Di", "Mi", "Do", "Fr", "Sa", "So"];
const ROB = ["Manuell gespannt", "Roboter"], KOM = ["Einfach", "Mittel", "Komplex"], MES = ["Jedes 50. Teil", "Jedes 10. Teil", "100% Kontrolle"], LAU = ["Kurze Laufzeit", "Mittlere Laufzeit", "Lange Laufzeit"];
const ROLES = ["Bediener", "Bediener Nachtschicht", "Einrichter", "Lehrling"];

let st = { emp: ["Mitarbeiter 1", "Mitarbeiter 2", "Mitarbeiter 3", "Mitarbeiter 4", "Mitarbeiter 5", "Mitarbeiter 6"], roles: {}, cap: 8, vz: 10, sollDef: {}, soll: {}, days: {}, v: 0 };

try { const r = localStorage.getItem("schicht2"); if (r) st = Object.assign(st, JSON.parse(r)); } catch (e) {}
if (!st.roles || typeof st.roles !== "object") st.roles = {};

const save = () => { try { localStorage.setItem("schicht2", JSON.stringify(st)); } catch (e) {} };
const $ = s => document.querySelector(s);
const esc = s => String(s).replace(/[&<>"']/g, c => ({ "&": "&amp;", "<": "&lt;", ">": "&gt;", '"': "&quot;", "'": "&#39;" }[c]));
const opt = (a, v) => a.map((x, i) => `<option value="${i}"${i == v ? " selected" : ""}>${esc(x)}</option>`).join("");
const roleOf = n => ROLES.includes(st.roles[n]) ? st.roles[n] : ROLES[0];
const dt = o => { const d = new Date(); d.setHours(12, 0, 0, 0); d.setDate(d.getDate() + o); return d; };
const kd = d => d.getFullYear() + "-" + String(d.getMonth() + 1).padStart(2, "0") + "-" + String(d.getDate()).padStart(2, "0");
const pd = k => new Date(k + "T12:00:00");
const add = (k, n) => { const d = pd(k); d.setDate(d.getDate() + n); return kd(d); };
const wi = k => (pd(k).getDay() + 6) % 7;
const isW = k => wi(k) < 5;
const mon = () => { const d = dt(0); d.setDate(d.getDate() - ((d.getDay() + 6) % 7)); return d; };
const wdays = wOffset => [...Array(7)].map((_, i) => { const d = mon(); d.setDate(d.getDate() + i + (wOffset * 7)); return kd(d); });
const kw = k => { const d = pd(k); d.setDate(d.getDate() + 3 - ((d.getDay() + 6) % 7)); const y = new Date(d.getFullYear(), 0, 4); return 1 + Math.round(((d - y) / 864e5 - 3 + ((y.getDay() + 6) % 7)) / 7); };
const tm = x => { x = ((x % 1440) + 1440) % 1440; return String(Math.floor(x / 60)).padStart(2, "0") + ":" + String(x % 60).padStart(2, "0"); };
const pt = v => { const [h, m] = v.split(":").map(Number); return h * 60 + m; };
const nz = v => v >= WE ? v - 1440 : v;
const clone = x => JSON.parse(JSON.stringify(x));
const defJ = m => ({ prio: m + 1, robot: 1, kompl: 1, mess: 0, lauf: 1, rue: 0 });
const G = k => st.days[k] || { job: {}, seg: [] };
const Jg = (k, m) => G(k).job[m] || defJ(m);
const D = k => st.days[k] || (st.days[k] = { job: {}, seg: [], e: 0 });
const J = (k, m) => { const d = D(k); return d.job[m] || (d.job[m] = defJ(m)); };
const w = e => e.rue ? 4.5 : 1 + (e.robot ? 0 : 1.5) + [0, .5, 1][e.kompl] + [0, .5, 1.5][e.mess] + [1, .5, 0][e.lauf];
const hrs = s => (s.t - s.f) / 60;
const fm = n => n.toLocaleString("de-DE", { maximumFractionDigits: 1 });
const col = n => { const i = st.emp.indexOf(n); return i < 0 ? "#7a8794" : `hsl(${(i * 67 + 210) % 360} 52% 38%)`; };
const lab = d => d.toLocaleDateString("de-DE", { weekday: "long", day: "numeric", month: "long" });
const wd = k => pd(k).toLocaleDateString("de-DE", { weekday: "long" });
const sd = k => pd(k).getDate() + "." + (pd(k).getMonth() + 1) + ".";

const KEY = M;
const STA = ["Läuft", "Rüsten", "Störung"];
const ordGet = m => { try { return JSON.parse(localStorage.getItem(KEY[m]) || "null"); } catch (e) { return null; } };
const ordSet = (m, o) => { try { if (o === null) localStorage.removeItem(KEY[m]); else localStorage.setItem(KEY[m], JSON.stringify(o)); } catch (e) {} };
const num = v => { const n = parseFloat(String(v == null ? "" : v).replace(",", ".")); return isNaN(n) ? 0 : n; };
const vzOf = d => d && d.vz !== undefined && d.vz !== null && d.vz !== "" ? num(d.vz) : st.vz;

/* Berechnung Laufzeiten unter Berücksichtigung von Folgeauftrag & Rüstzeit */
function calcRunMin(d, status) {
  if (!d) return 0;
  const restPieces = Math.max(0, num(d.total) - num(d.good) - num(d.scrap));
  let mins = restPieces * num(d.mpp) * (1 + vzOf(d) / 100);
  
  // Aktuelle Rüstzeit wenn gerade "Rüsten" aktiv
  if (status === STA[1]) mins += num(d.setup) * 60;
  
  // Folgeauftrag einrechnen falls vorhanden
  if (d.nextOrder) {
    const nextRest = Math.max(0, num(d.nextTotal) - num(d.nextGood));
    let nextMins = nextRest * num(d.nextMpp) * (1 + vzOf(d) / 100);
    // Rüstzeit für Folgeauftrag nur dazurechnen, wenn KEIN direkter Folgeauftrag (isFollow == false)
    if (!d.nextIsFollow) {
      nextMins += num(d.nextSetup) * 60;
    }
    mins += nextMins;
  }
  return mins;
}

const finOf = d => d ? (d.finishAt || Date.now() + calcRunMin(d, d.status) * 60000) : 0;
const setupNeededAt = d => {
  if (!d) return 0;
  const restPieces = Math.max(0, num(d.total) - num(d.good) - num(d.scrap));
  const currentRunMins = restPieces * num(d.mpp) * (1 + vzOf(d) / 100) + (d.status === STA[1] ? num(d.setup) * 60 : 0);
  return Date.now() + (currentRunMins * 60000);
};

const at = (k, min) => { const [y, mo, dd] = k.split("-").map(Number); return new Date(y, mo - 1, dd, 0, min).getTime(); };
const hm = x => { x = Math.round(x); return Math.floor(x / 60) + " h " + String(x % 60).padStart(2, "0") + " min"; };
const fdt = ms => { if (!ms) return "-"; const d = new Date(ms); return d.toLocaleDateString("de-DE", { weekday: "short", day: "numeric", month: "numeric" }) + " " + d.toLocaleTimeString("de-DE", { hour: "2-digit", minute: "2-digit" }); };
const rd = id => document.getElementById("o_" + id);

const stCls = m => {
  const d = ordGet(m); if (!d) return "st-none";
  const remain = Math.max(0, Math.round((finOf(d) - Date.now()) / 60000));
  return d.status === STA[2] ? "st-bad" : d.status === STA[1] ? "st-blue" : remain < 1440 ? "st-warn" : "st-ok";
};

/* Prüfen ob HEUTE aktualisiert */
const isUpdatedToday = d => {
  if (!d || !d.updatedAt) return false;
  return new Date(d.updatedAt).toDateString() === new Date().toDateString();
};

function editView(m) {
  const d = ordGet(m) || {};
  const n = (id, l, ph) => `<div class="fr"><label for="o_${id}">${l}</label><input id="o_${id}" type="number" step="any" inputmode="decimal" value="${esc(d[id] == null ? "" : d[id])}" placeholder="${esc(ph || "")}"></div>`;
  const t = (id, l) => `<div class="fr"><label for="o_${id}">${l}</label><input id="o_${id}" type="text" value="${esc(d[id] == null ? "" : d[id])}"></div>`;
  
  return `<h2>Bearbeite ${esc(M[m])}</h2>
  <div class="card" id="oe">
    <div class="fr"><label for="o_status">Status</label>
      <select id="o_status">${STA.map(s => `<option${(d.status || STA[0]) === s ? " selected" : ""}>${s}</option>`).join("")}</select>
    </div>
    ${t("order", "Auftragsnummer")}
    ${t("artNr", "Artikelnummer")}
    ${n("total", "Gesamtstück")}
    ${n("good", "Gutteile")}
    ${n("scrap", "Ausschuss")}
    ${n("mpp", "Minuten pro Stück")}
    ${n("setup", "Rüstzeit (Stunden)")}
    ${n("vz", "Verteilzeit (%)", "Standard " + st.vz)}
    
    <div class="next-order-box">
      <h3>Folgeauftrag einplanen</h3>
      <div class="fr">
        <label for="o_nextIsFollow">Auftragstyp</label>
        <select id="o_nextIsFollow">
          <option value="1" ${d.nextIsFollow ? "selected" : ""}>Direkter Folgeauftrag (Gleicher Typ / KEINE Rüstzeit)</option>
          <option value="0" ${!d.nextIsFollow ? "selected" : ""}>Neuer Auftrag (Umrüsten nötig / Zzgl. Rüstzeit)</option>
        </select>
      </div>
      ${t("nextOrder", "Folge-Auftrags-Nr.")}
      ${n("nextTotal", "Folge-Gesamtstück")}
      ${n("nextGood", "Folge-Gutteile (bisher)")}
      ${n("nextMpp", "Folge-Min. pro Stück")}
      ${n("nextSetup", "Folge-Rüstzeit (Std.)")}
    </div>

    <div class="fr"><label for="o_note">Bemerkung</label><textarea id="o_note">${esc(d.note || "")}</textarea></div>
    <div class="card" id="oinfo" style="margin:10px 0"></div>
    <div class="tools">
      <button class="btn" data-a="osave">Speichern & Aktualisieren</button>
      <button class="btn" data-a="oreset" style="color:var(--bad); border-color:var(--bad)">Zurücksetzen</button>
      <button class="btn" data-a="ocancel">Abbrechen</button>
    </div>
  </div>`;
}

function ordPreview() {
  const el = document.getElementById("oinfo"); if (!el || !rd("total")) return;
  const status = rd("status").value;
  const d = {
    total: rd("total").value, good: rd("good").value, scrap: rd("scrap").value, mpp: rd("mpp").value, setup: rd("setup").value, vz: rd("vz").value,
    nextOrder: rd("nextOrder").value, nextTotal: rd("nextTotal").value, nextGood: rd("nextGood").value, nextMpp: rd("nextMpp").value, nextSetup: rd("nextSetup").value,
    nextIsFollow: rd("nextIsFollow").value === "1"
  };
  
  const rest = Math.max(0, num(d.total) - num(d.good) - num(d.scrap));
  const pure = rest * num(d.mpp);
  const vzm = pure * vzOf(d) / 100;
  const su = status === STA[1] ? num(d.setup) * 60 : 0;
  const curTot = pure + vzm + su;
  
  let nextInfo = "";
  let totalTot = curTot;
  
  if (d.nextOrder && num(d.nextTotal) > 0) {
    const nextRest = Math.max(0, num(d.nextTotal) - num(d.nextGood));
    const nextPure = nextRest * num(d.nextMpp);
    const nextVz = nextPure * vzOf(d) / 100;
    const nextSu = d.nextIsFollow ? 0 : num(d.nextSetup) * 60;
    const nextTot = nextPure + nextVz + nextSu;
    totalTot += nextTot;
    
    nextInfo = `<br><hr><b>Einrichter benötigt ab (Maschine frei zum Umbau):</b> ${fdt(Date.now() + curTot * 6e4)}<br>
    <b>Folgeauftrag (${esc(d.nextOrder)}):</b> ${d.nextIsFollow ? "Keine Rüstzeit" : "+" + hm(nextSu) + " Rüstzeit"} | Dauer: ${hm(nextTot)}`;
  }

  el.innerHTML = `<b>Aktueller Auftrag Restlaufzeit:</b> ${hm(curTot)}<br>
  <b>Fertig/Auslauf aktuell:</b> ${fdt(Date.now() + curTot * 6e4)}
  ${nextInfo}
  <br><br><b>Gesamtlaufzeit inkl. Folgeauftrag:</b> ${hm(totalTot)}<br>
  <b>Endgültig fertig:</b> ${fdt(Date.now() + totalTot * 6e4)}`;
}

function ordSave(m) {
  const status = rd("status").value;
  const o = {
    artNr: rd("artNr").value, order: rd("order").value, total: num(rd("total").value),
    good: num(rd("good").value), scrap: num(rd("scrap").value), mpp: num(rd("mpp").value),
    setup: num(rd("setup").value), vz: rd("vz").value, status: status, note: rd("note").value,
    nextOrder: rd("nextOrder").value, nextTotal: num(rd("nextTotal").value), nextGood: num(rd("nextGood").value),
    nextMpp: num(rd("nextMpp").value), nextSetup: num(rd("nextSetup").value), nextIsFollow: rd("nextIsFollow").value === "1",
    updatedAt: new Date().toISOString()
  };
  o.finishAt = Date.now() + calcRunMin(o, status) * 60000;
  ordSet(m, o);
}

function ordView() {
  if (cur.edit !== null && cur.edit !== undefined) return editView(cur.edit);
  const cards = M.map((n, m) => {
    const d = ordGet(m);
    if (!d) return `<button class="card oc" data-o="${m}"><b>${esc(n)}</b><br><span class="hint">Kein Auftrag erfasst</span></button>`;
    
    const fin = finOf(d);
    const remain = Math.max(0, Math.round((fin - Date.now()) / 60000));
    const p = d.total ? Math.min(100, Math.round(num(d.good) / d.total * 100)) : 0;
    const c = stCls(m);
    const updatedToday = isUpdatedToday(d);
    const updDate = d.updatedAt ? new Date(d.updatedAt) : null;
    
    const setupTime = setupNeededAt(d);

    return `<button class="card oc ${c} ${updatedToday ? "is-updated-today" : ""}" data-o="${m}">
      <b>${esc(n)}</b> 
      ${updatedToday ? `<span class="badge-updated">✓ HEUTE AKTUALISIERT (${updDate.toLocaleTimeString("de-DE", {hour:'2-digit', minute:'2-digit'})})</span>` : (updDate ? `<span class="hint">Alt: ${updDate.toLocaleDateString("de-DE")}</span>` : "")}
      <br>
      ${d.order ? `<b>Auftrag: ${esc(d.order)}</b>` : "Keine Auftrags-Nr."} ${d.artNr ? `[${esc(d.artNr)}]` : ""}
      <br>
      <b>${fm(num(d.good))} / ${fm(num(d.total))} Stück (${p}%)</b>
      <br>
      <span class="hint">Status: ${esc(d.status || STA[0])} | Auslauf / Einrichter nötig: <b>${fdt(setupTime)}</b></span>
      ${d.nextOrder ? `<br><span class="hint"><b>Folgeauftrag:</b> ${esc(d.nextOrder)} (${d.nextIsFollow ? "Gleicher Typ / Ohne Rüstzeit" : "Neuer Typ / Inkl. Rüstzeit"})</span>` : ""}
      <br>
      <span class="hint">Gesamtlaufzeit Rest: ${hm(remain)} | Fertig komplett: ${fdt(fin)}</span>
    </button>`;
  }).join("");

  return `<h2>Aufträge & Maschinenstatus</h2>
  <p class="hint">Klicke auf eine Maschine, um Zeiten, Stückzahlen oder Folgeaufträge zu aktualisieren. Grün markierte Karten wurden HEUTE aktualisiert.</p>
  ${cards}`;
}

let cur = { tab: "plan", w: 0, i: 0, msg: "", edit: null, emp: false };

(() => {
  const n = new Date(), nm = n.getHours() * 60 + n.getMinutes(), pk = kd(nm >= WE ? dt(1) : dt(0)), diff = Math.round((pd(pk) - pd(wdays(0)[0])) / 864e5);
  cur.w = Math.floor(diff / 7); cur.i = ((diff % 7) + 7) % 7;
})();

const sel = () => wdays(cur.w)[cur.i];
const srcOf = k => { let p = k; for (let i = 0; i < 7; i++) { p = add(p, -1); if (isW(p) && st.days[p] && st.days[p].seg.length) return p; } return null; };

function auto() {
  const end = wdays(cur.w)[6]; let ch = false;
  for (let k = kd(dt(0)); k <= end; k = add(k, 1)) {
    if (!isW(k)) continue;
    const d = st.days[k]; if (d && d.e) continue;
    const s = srcOf(k); if (!s) continue;
    const S = st.days[s];
    if (d && d.src === s && JSON.stringify([d.job, d.seg]) === JSON.stringify([S.job, S.seg])) continue;
    st.days[k] = { job: clone(S.job), seg: clone(S.seg), e: 0, src: s }; ch = true;
  }
  if (ch) save();
}

const weekNav = () => {
  const ds = wdays(cur.w);
  return `<div class="wnv">
    <button class="btn" data-wn="-1"><</button>
    <div class="wl"><b>Woche ${kw(ds[0])}</b><small>${sd(ds[0])} - ${sd(ds[6])}</small></div>
    <button class="btn" data-wn="1">></button>
    <button class="btn" data-wn="0">Heute</button>
  </div>`;
};

const strip = () => `<div class="days">${wdays(cur.w).map((k, i) => `<button class="chip${i > 4 ? " we" : ""}" data-i="${i}" aria-pressed="${i == cur.i}">${DN[i]}<small>${sd(k)}</small></button>`).join("")}</div>`;

/* NEUE WOCHENÜBERSICHT FÜR MASCHINEN */
function overviewMachineWeek() {
  const ds = wdays(cur.w);
  
  const tableRows = M.map((mName, mIdx) => {
    const ord = ordGet(mIdx);
    const isUpd = isUpdatedToday(ord);
    
    const dayCells = ds.map(k => {
      const daySegs = G(k).seg.filter(s => s.m === mIdx);
      const emps = [...new Set(daySegs.map(s => s.emp).filter(Boolean))].join(", ") || (daySegs.length ? "<i style='color:var(--bad)'>Offen</i>" : "-");
      
      let ordText = "";
      if (ord) {
        const setupTime = setupNeededAt(ord);
        const setupDateStr = kd(new Date(setupTime));
        const isExpiringDay = setupDateStr === k;
        ordText = `<div class="m-cell-ord" style="${isExpiringDay ? 'color:var(--bad);font-weight:700;' : ''}">
          ${esc(ord.order || 'Auftrag')}<br>
          ${isExpiringDay ? '⚠️ Läuft ab: ' + new Date(setupTime).toLocaleTimeString([], {hour:'2-digit', minute:'2-digit'}) : 'Auslauf: ' + sd(setupDateStr)}
        </div>`;
      }

      return `<td>
        <div class="m-cell-emp">${emps}</div>
        ${ordText}
      </td>`;
    }).join("");

    return `<tr>
      <td class="m-name ${isUpd ? 'is-updated-today' : ''}">
        ${esc(mName)}
        ${isUpd ? '<br><span class="badge-updated">Aktualisiert</span>' : ''}
      </td>
      ${dayCells}
    </tr>`;
  }).join("");

  return `<h2>Wochenübersicht Maschinen & Ablaufzeiten</h2>
  <p class="hint">Übersicht: Wer arbeitet auf welcher Maschine und wann läuft der aktuelle Auftrag aus (Einrichter-Einsatz nötig).</p>
  <div class="card gs">
    <table class="m-table">
      <thead>
        <tr>
          <th>Maschine</th>
          ${ds.map((k, i) => `<th>${DN[i]} ${sd(k)}</th>`).join("")}
        </tr>
      </thead>
      <tbody>
        ${tableRows}
      </tbody>
    </table>
  </div>`;
}

function planView() {
  const k = sel(), d = G(k), ds = d.seg;
  const cards = M.map((n, m) => {
    const j = Jg(k, m), sg = ds.map((s, i) => [s, i]).filter(([s]) => s.m === m), h = sg.reduce((a, [s]) => a + hrs(s), 0), un = sg.some(([s]) => !s.emp);
    const ord = ordGet(m);
    const updatedToday = isUpdatedToday(ord);

    return `<div class="m ${stCls(m)} ${un ? " u" : ""} ${updatedToday ? "is-updated-today" : ""}" data-m="${m}">
      <div class="mh">
        <div class="mn">${esc(n)} ${updatedToday ? '<span class="badge-updated">✓ HEUTE AKTUALISIERT</span>' : ''} <small>${fm(h)} h geplant</small></div>
      </div>
      ${ord ? `<div class="ol"><b>Auftrag: ${esc(ord.order || "Ohne Nr.")}</b> | Restlaufzeit: ${hm(Math.max(0, Math.round((finOf(ord) - Date.now()) / 60000)))}<br>Einrichter nötig ab: <b>${fdt(setupNeededAt(ord))}</b></div>` : '<div class="ol hint">Kein aktiver Auftrag</div>'}
    </div>`;
  }).join("");

  return `${weekNav()}${strip()}
  ${overviewMachineWeek()}
  <h2>Tages-Einteilung: ${lab(pd(k))}</h2>
  <div class="card">${cards}</div>`;
}

function dayView() {
  const k = sel();
  return `${weekNav()}${strip()}<h2>Einteilung ${lab(pd(k))}</h2><p class="hint">Nutze die Registerkarte "Wochenübersicht Maschinen" für die komplette Auftrags- und Mitarbeiter-Matrix.</p>`;
}

function render() {
  auto();
  document.querySelectorAll(".tab").forEach(b => b.setAttribute("aria-pressed", b.dataset.tab === cur.tab));
  const views = { plan: planView, day: dayView, week: overviewMachineWeek, orders: ordView };
  $("#app").innerHTML = (views[cur.tab] || planView)();
}

if (cur.tab === "orders" && cur.edit != null) ordPreview();

setInterval(() => {
  const a = document.activeElement, typing = a && a.matches && a.matches("input, select, textarea");
  if (typing) return;
  if ((cur.tab === "orders" && cur.edit == null) || cur.tab === "plan") render();
}, 60000);

document.addEventListener("input", ev => {
  if (ev.target.id && ev.target.id.startsWith("o_")) ordPreview();
});

document.addEventListener("click", ev => {
  const t = ev.target.closest("button"); if (!t) return;
  const a = t.dataset, k = sel();
  if (a.tab) { cur.tab = a.tab; cur.edit = null; }
  else if (a.o !== undefined) cur.edit = +a.o;
  else if (a.a === "ocancel") cur.edit = null;
  else if (a.a === "osave") { ordSave(cur.edit); cur.edit = null; }
  else if (a.a === "oreset") { if (confirm("Wirklich zurücksetzen?")) { ordSet(cur.edit, null); cur.edit = null; } }
  else if (a.i !== undefined) cur.i = +a.i;
  else if (a.wn !== undefined) { cur.w = a.wn === "0" ? 0 : cur.w + (+a.wn); }
  render();
});

document.addEventListener("change", ev => {
  if (ev.target.id && ev.target.id.startsWith("o_")) ordPreview();
});

render();
</script>
</body>
</html>
