<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Schichtplanung Maschinen</title>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Barlow:wght@400;600;700&family=Barlow+Semi+Condensed:wght@600;700&display=swap">
<style>
:root{box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px);color-scheme:light;
--bg:#e7ebf0;--card:#fff;--ink:#14202b;--mut:#5d6b79;--line:#cfd7df;--acc:#0b5fb3;--accbg:#dcebfa;--ok:#188a52;--warn:#c98400;--bad:#d3322a}
:root[data-theme="dark"]{color-scheme:dark;--bg:#10171e;--card:#18222c;--ink:#eaf0f5;--mut:#92a1b0;--line:#2a3846;--acc:#5aa7f0;--accbg:#1c3550;--ok:#43c486;--warn:#f0b429;--bad:#ff6b61}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){color-scheme:dark;--bg:#10171e;--card:#18222c;--ink:#eaf0f5;--mut:#92a1b0;--line:#2a3846;--acc:#5aa7f0;--accbg:#1c3550;--ok:#43c486;--warn:#f0b429;--bad:#ff6b61}}
html{scroll-padding-top:env(safe-area-inset-top,0px);height:100%}
*,*::before,*::after{box-sizing:inherit}
body{margin:0;background:var(--bg);color:var(--ink);font:16px/1.4 Barlow,system-ui,sans-serif;min-height:100%}
body::before{content:"";position:fixed;inset:0 0 auto;height:env(safe-area-inset-top,0px);background:var(--bg);z-index:10}
.wrap{max-width:1100px;margin:0 auto;padding:12px 14px 40px}
h1{font:700 24px/1.1 "Barlow Semi Condensed",Barlow,sans-serif;margin:6px 0 12px}
h2{font:700 18px "Barlow Semi Condensed",Barlow,sans-serif;margin:22px 0 8px}
.tabs,.row{display:flex;gap:6px;flex-wrap:wrap}
button,select,input,textarea{font:inherit;color:inherit}
.tab,.chip{min-height:44px;padding:8px 14px;border:1.5px solid var(--line);background:var(--card);border-radius:8px;cursor:pointer;font-weight:600}
.tab[aria-pressed="true"],.chip[aria-pressed="true"]{background:var(--acc);border-color:var(--acc);color:#fff}
.days{display:flex;gap:6px;overflow-x:auto;padding:2px 0 8px;margin:6px 0 4px}
.chip{flex:1 0 auto;text-align:center;line-height:1.15;padding:6px 10px}
.chip.we{border-style:dashed}
.chip small{display:block;font-weight:400;opacity:.85}
.btn{min-height:44px;padding:8px 14px;border-radius:8px;border:1.5px solid var(--acc);background:var(--accbg);color:var(--acc);font-weight:700;cursor:pointer}
.btn.s{min-height:40px;padding:4px 10px;font-size:14px}
.wnv{display:flex;gap:8px;align-items:center;margin:10px 0 2px}
.wnv .btn{min-width:44px}
.wnv .wl{flex:1;text-align:center;line-height:1.15}
.wnv .wl small{display:block;color:var(--mut)}
.tools{display:flex;gap:8px;flex-wrap:wrap;align-items:center;margin:8px 0}
.ok{color:var(--ok)}.wn{color:var(--warn)}.bd{color:var(--bad)}
.card,.m{background:var(--card);border:1px solid var(--line);border-radius:10px;padding:10px 12px}
.lrow{display:grid;grid-template-columns:110px 1fr 150px;gap:10px;align-items:center;padding:6px 0}
.lrow+.lrow{border-top:1px solid var(--line)}
.lname{font-weight:700;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.rl{display:block;font-weight:400;font-size:11px;line-height:1.1;color:var(--mut);overflow:hidden;text-overflow:ellipsis}
.bar{height:16px;background:var(--bg);border-radius:6px;overflow:hidden}
.bar span{display:block;height:100%;background:currentColor}
.lsum{text-align:right;font-weight:700;font-size:14px}
.m{border-left:8px solid var(--line);margin:8px 0}
.m.u{outline:2px solid var(--bad);outline-offset:-1px}
.mh{display:grid;grid-template-columns:1fr 90px;gap:8px;align-items:end}
.mn{font:700 18px "Barlow Semi Condensed",Barlow,sans-serif}
.mn small{font:400 14px Barlow;color:var(--mut)}
select,input[type=time],input[type=number],input[type=text]{min-height:44px;width:100%;padding:6px 8px;border:1.5px solid var(--line);border-radius:8px;background:var(--bg)}
.md{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:8px;margin:8px 0;align-items:end}
label{font-size:13px;color:var(--mut);display:block}
.rue{display:flex;align-items:center;gap:8px;min-height:44px;font-size:15px;color:var(--ink)}
.rue input{width:22px;height:22px}
.wt{font-weight:700;color:var(--mut);text-align:right}
.sr{display:grid;grid-template-columns:1fr 100px 28px 100px 44px;gap:6px;align-items:center;margin:4px 0}
.x{min-height:44px;border:1.5px solid var(--line);border-radius:8px;background:var(--card);cursor:pointer;color:var(--bad)}
.add{display:flex;gap:6px;flex-wrap:wrap;margin-top:6px}
.gs{overflow-x:auto}
.gt{min-width:780px}
.gr{display:grid;grid-template-columns:120px 1fr;gap:8px;align-items:center;margin:3px 0}
.gn{font-weight:600;font-size:14px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.gl{position:relative;height:34px;border-radius:6px;background:var(--card) repeating-linear-gradient(90deg,var(--line) 0 1px,transparent 1px calc(100% / 6))}
.gb{position:absolute;top:3px;bottom:3px;border-radius:5px;color:#fff;font-size:12px;font-weight:600;padding:0 5px;display:flex;align-items:center;overflow:hidden;white-space:nowrap}
.gh{position:relative;height:18px;margin-left:128px;font-size:12px;color:var(--mut)}
.gh span{position:absolute;transform:translateX(-50%)}
.now{position:absolute;top:0;bottom:0;width:2px;background:var(--bad);z-index:2}
.leg{display:flex;flex-wrap:wrap;gap:8px;margin:10px 0;font-size:14px}
.leg i{display:inline-block;width:12px;height:12px;border-radius:3px;margin-right:5px;vertical-align:-1px}
.wr{display:grid;grid-template-columns:150px 90px 80px 110px 1fr;gap:10px;align-items:center;padding:6px 0}
.wr+.wr{border-top:1px solid var(--line)}
.pr{display:inline-flex;align-items:center;gap:8px;margin:6px 8px 0 0;padding:6px 10px;background:var(--accbg);border-radius:8px;font-weight:600}
.pr i{font-style:normal;background:var(--acc);color:#fff;border-radius:6px;padding:1px 8px}
.ov{border-collapse:collapse;width:100%;min-width:520px;font-size:14px}
.ov th,.ov td{padding:4px 6px;text-align:center;border-top:1px solid var(--line)}
.ov tr:first-child th,.ov tr:first-child td{border-top:0}
.ov td:first-child,.ov th:first-child{text-align:left;font-weight:700}
.ovb{min-height:36px;min-width:40px;border:1.5px solid var(--line);border-radius:8px;background:var(--card);font-weight:700;cursor:pointer}
.ovb.on{background:var(--acc);border-color:var(--acc);color:#fff}
.oc{display:block;width:100%;text-align:left;margin:8px 0;cursor:pointer;background:var(--card);color:var(--ink);font:inherit;border-left:8px solid var(--line)}
.st-ok{border-left-color:var(--ok)}.st-warn{border-left-color:var(--warn)}.st-bad{border-left-color:var(--bad)}.st-blue{border-left-color:var(--acc)}.st-none{border-left-color:var(--line)}
.oc .bar{margin:6px 0}.oc .bar span{color:var(--acc)}
.ol{margin:6px 0;padding:6px 8px;background:var(--bg);border-radius:8px;font-size:14px}
.fr{display:grid;grid-template-columns:160px 1fr;gap:8px;align-items:center;margin:8px 0}
.fr label{text-align:right}
.busy{position:absolute;top:0;bottom:0;background:var(--accbg);border-radius:6px}
.gn small{display:block;font-weight:400;font-size:11px;line-height:1;color:var(--mut)}
.er{display:grid;grid-template-columns:1fr 1fr 44px;gap:6px;align-items:center;margin:6px 0}
.ea{display:grid;grid-template-columns:1fr 1fr auto;gap:6px;align-items:center;margin:10px 0}
@media(max-width:620px){.fr{grid-template-columns:1fr}.fr label{text-align:left}}
details{margin-top:20px}summary{cursor:pointer;font-weight:700;min-height:44px;display:flex;align-items:center}
textarea{width:100%;min-height:120px;padding:8px;border:1.5px solid var(--line);border-radius:8px;background:var(--bg)}
.hint{color:var(--mut);font-size:14px}
@media(max-width:620px){.lrow{grid-template-columns:80px 1fr}.lsum{grid-column:1/-1;text-align:left}.sr{grid-template-columns:1fr 1fr 1fr 44px}.sr span{display:none}.sr select{grid-column:1/-1}.wr{grid-template-columns:1fr 1fr}.wr .bar{grid-column:1/-1}.er{grid-template-columns:1fr 44px}.er input{order:1}.er button{order:2}.er select{order:3;grid-column:1/-1}.ea{grid-template-columns:1fr}}
</style>
</head>
<body>
<div class="wrap">
<h1>Schichtplanung Maschinen</h1>
<div class="tabs"><button class="tab" data-tab="plan">Planung</button><button class="tab" data-tab="day">Tagesansicht</button><button class="tab" data-tab="week">Woche und Soll</button><button class="tab" data-tab="orders">Aufträge</button></div>
<div id="app"></div>
</div>
<script>
/* Planungstag = 20:20 am Vorabend bis 20:20. Zeiten werden in Minuten ab 0:00 des Planungstags gespeichert,
   die Nachtschicht liegt daher bei -220 (20:20 Vorabend) bis 260 (4:20). Die Nachtschicht von Sonntag auf Montag zählt zum Montag. */
const M=["CTX beta 800 - 1","CTX beta 800 - 2","HQR - 1","HQR - 2","HQR - 3","Multiplex 6200","NEXUS 200 M","NEXUS 350 M","NEXUS 900 M","INTEGREX - 1","INTEGREX - 2","CLX450 TC - 1","CLX450 TC - 2"];
const SH=[["Nacht",-220,260],["Früh",260,740],["Normal 6–18",360,1080],["Spät",740,1220]];
const WS=-220,WE=1220,WL=WE-WS;
const DN=["Mo","Di","Mi","Do","Fr","Sa","So"];
const ROB=["Manuell gespannt","Roboter"],KOM=["Einfach","Mittel","Komplex"],MES=["Jedes 50. Teil","Jedes 10. Teil","100 % Kontrolle"],LAU=["Kurze Laufzeit","Mittlere Laufzeit","Lange Laufzeit"];
const ROLES=["Bediener","Bediener Nachtschicht","Einrichter","Lehrling"];
let st={emp:["Mitarbeiter 1","Mitarbeiter 2","Mitarbeiter 3","Mitarbeiter 4","Mitarbeiter 5","Mitarbeiter 6"],roles:{},cap:8,vz:10,sollDef:{},soll:{},days:{},v:0};
try{const r=localStorage.getItem("schicht2");if(r)st=Object.assign(st,JSON.parse(r))}catch(e){}
if(!st.roles||typeof st.roles!=="object")st.roles={};
const save=()=>{try{localStorage.setItem("schicht2",JSON.stringify(st))}catch(e){}};
const $=s=>document.querySelector(s);
const esc=s=>String(s).replace(/[&<>"]/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;"}[c]));
const opt=(a,v)=>a.map((x,i)=>`<option value="${i}"${i==v?" selected":""}>${esc(x)}</option>`).join("");
const roleOf=n=>ROLES.includes(st.roles[n])?st.roles[n]:ROLES[0];
const dt=o=>{const d=new Date();d.setHours(12,0,0,0);d.setDate(d.getDate()+o);return d};
const kd=d=>d.getFullYear()+"-"+String(d.getMonth()+1).padStart(2,"0")+"-"+String(d.getDate()).padStart(2,"0");
const pd=k=>new Date(k+"T12:00:00");
const add=(k,n)=>{const d=pd(k);d.setDate(d.getDate()+n);return kd(d)};
const wi=k=>(pd(k).getDay()+6)%7;
const isW=k=>wi(k)<5;
const mon=o=>{const d=dt(0);d.setDate(d.getDate()-((d.getDay()+6)%7)+7*o);return d};
const wdays=o=>[...Array(7)].map((_,i)=>{const d=mon(o);d.setDate(d.getDate()+i);return kd(d)});
const kw=k=>{const d=pd(k);d.setDate(d.getDate()+3-((d.getDay()+6)%7));const y=new Date(d.getFullYear(),0,4);return 1+Math.round(((d-y)/864e5-3+((y.getDay()+6)%7))/7)};
const tm=x=>{x=((x%1440)+1440)%1440;return String(Math.floor(x/60)).padStart(2,"0")+":"+String(x%60).padStart(2,"0")};
const pt=v=>{const [h,m]=v.split(":").map(Number);return h*60+m};
const nz=v=>v>=WE?v-1440:v;
const clone=x=>JSON.parse(JSON.stringify(x));
const defJ=m=>({prio:m+1,robot:1,kompl:1,mess:0,lauf:1,rue:0});
const G=k=>st.days[k]||{job:{},seg:[]};
const Jg=(k,m)=>G(k).job[m]||defJ(m);
const D=k=>st.days[k]||(st.days[k]={job:{},seg:[],e:0});
const J=(k,m)=>{const d=D(k);return d.job[m]||(d.job[m]=defJ(m))};
const w=e=>e.rue?4.5:1+(e.robot?0:1.5)+[0,.5,1][e.kompl]+[0,.5,1.5][e.mess]+[1,.5,0][e.lauf];
const hrs=s=>(s.t-s.f)/60;
const fm=n=>n.toLocaleString("de-DE",{maximumFractionDigits:1});
const col=n=>{const i=st.emp.indexOf(n);return i<0?"#7a8794":`hsl(${(i*67+210)%360} 52% 38%)`};
const lab=d=>d.toLocaleDateString("de-DE",{weekday:"long",day:"numeric",month:"long"});
const wd=k=>pd(k).toLocaleDateString("de-DE",{weekday:"long"});
const sd=k=>pd(k).getDate()+"."+(pd(k).getMonth()+1)+".";

/* Aufträge (aus dem Maschinenstatus-Rechner): gespeichert je Maschine unter dem Maschinennamen des Status-Rechners */
const KEY=["CTX beta 800 -1","CTX beta 800 -2","HQR 1","HQR 2","HQR 3","Multiplex 6200","NEXUS 200M","NEXUS 350 M","NEXUS 900 M","INTEGREX 400 S-1","INTEGREX 400 S-2","CLX450 TC 1","CLX450 TC 2"];
const STA=["Läuft","Rüsten","Störung"];
const ordGet=m=>{try{return JSON.parse(localStorage.getItem(KEY[m])||"null")}catch(e){return null}};
const ordSet=(m,o)=>{try{if(o===null)localStorage.removeItem(KEY[m]);else localStorage.setItem(KEY[m],JSON.stringify(o))}catch(e){}};
const num=v=>{const n=parseFloat(String(v==null?"":v).replace(",","."));return isNaN(n)?0:n};
const vzOf=d=>d&&d.vz!==undefined&&d.vz!==null&&d.vz!==""?num(d.vz):st.vz;
const runMin=(d,status)=>Math.max(0,num(d.total)-num(d.good)-num(d.scrap))*num(d.mpp)*(1+vzOf(d)/100)+(status===STA[1]?num(d.setup)*60:0);
const finOf=d=>d?(d.finishAt||Date.now()+runMin(d,d.status)*60000):0;
const at=(k,min)=>{const [y,mo,dd]=k.split("-").map(Number);return new Date(y,mo-1,dd,0,min).getTime()};
const overlap=(m,a,b)=>{const d=ordGet(m);if(!d)return 0;const s=Math.max(Date.now(),a),e=Math.min(finOf(d),b);return Math.max(0,e-s)/36e5};
const need=(k,m)=>overlap(m,at(k,WS),at(k,WE));
const hm=x=>{x=Math.round(x);return Math.floor(x/60)+" h "+String(x%60).padStart(2,"0")+" min"};
const fdt=ms=>{const d=new Date(ms);return d.toLocaleDateString("de-DE",{weekday:"short",day:"numeric",month:"numeric"})+" "+d.toLocaleTimeString("de-DE",{hour:"2-digit",minute:"2-digit"})};
const rd=id=>document.getElementById("o_"+id);
/* Statusfarbe je Maschine (gleiche Logik wie im Maschinenrechner): Störung rot, Rüsten blau, Läuft unter 24 h Rest gelb, sonst grün, ohne Auftrag neutral */
const stCls=m=>{const d=ordGet(m);if(!d)return "st-none";const remain=Math.max(0,Math.round((finOf(d)-Date.now())/60000));return d.status===STA[2]?"st-bad":d.status===STA[1]?"st-blue":remain<1440?"st-warn":"st-ok"};
const stLeg=()=>`<div class="leg"><span><i style="background:var(--ok)"></i>Läuft, über 24 h Rest</span><span><i style="background:var(--warn)"></i>Läuft, unter 24 h Rest</span><span><i style="background:var(--acc)"></i>Rüsten</span><span><i style="background:var(--bad)"></i>Störung</span><span><i style="background:var(--line)"></i>Kein Auftrag</span></div>`;
const ordLine=(k,m,h)=>{
  const d=ordGet(m);if(!d)return "";
  const fin=finOf(d),remain=Math.max(0,Math.round((fin-Date.now())/60000)),nd=need(k,m),gap=nd-h,c=nd<=0?"":gap>.05?"bd":"ok";
  return `<div class="ol"><b>${esc(d.order?"Auftrag "+d.order:"Auftrag")}</b>${d.artNr?" · "+esc(d.artNr):""}${d.desc?" · "+esc(d.desc):""}<br><span class="hint">Rest ${hm(remain)} (inkl. ${fm(vzOf(d))} % Verteilzeit) · fertig ${fdt(fin)} · ${esc(d.status||STA[0])}</span><br><span class="${c}"><b>Bedarf an diesem Tag ${fm(nd)} h · geplant ${fm(h)} h${gap>.05?" · es fehlen "+fm(gap)+" h":""}</b></span></div>`;
};

function editView(m){
  const d=ordGet(m)||{};
  const n=(id,l,ph)=>`<div class="fr"><label for="o_${id}">${l}</label><input id="o_${id}" type="number" step="any" inputmode="decimal" value="${esc(d[id]==null?"":d[id])}" placeholder="${esc(ph||"")}"></div>`;
  const t=(id,l)=>`<div class="fr"><label for="o_${id}">${l}</label><input id="o_${id}" type="text" value="${esc(d[id]==null?"":d[id])}"></div>`;
  return `<h2>${esc(M[m])}</h2><div class="card" id="oe">
  <div class="fr"><label for="o_status">Status</label><select id="o_status">${STA.map(s=>`<option${(d.status||STA[0])===s?" selected":""}>${s}</option>`).join("")}</select></div>
  ${n("total","Gesamtstück")}${n("good","Gutteile")}${n("mpp","Minuten pro Stück")}${n("scrap","Ausschuss")}${n("setup","Rüstzeit (Stunden)")}${n("vz","Verteilzeit (%)","Standard "+st.vz)}
  <p class="hint">Verteilzeit: Zuschlag für Plattenwechsel, Späne entfernen und Ähnliches. Die Maschine läuft nicht durchgehend, die Laufzeit verlängert sich um diesen Prozentsatz. Leer lassen = Standardwert.</p>
  <div class="fr"><label for="o_note">Bemerkung</label><textarea id="o_note">${esc(d.note||"")}</textarea></div>
  <details><summary>Weitere Angaben (optional)</summary>${t("artNr","Artikelnummer")}${t("desc","Bezeichnung")}${t("order","Auftragsnummer")}</details>
  <div class="card" id="oinfo" style="margin:10px 0"></div>
  <div class="tools"><button class="btn" data-a="osave">Speichern</button><button class="btn" data-a="oreset" style="color:var(--bad);border-color:var(--bad)">Zurücksetzen</button><button class="btn" data-a="ocancel">Abbrechen</button></div></div>`;
}
function ordPreview(){
  const el=document.getElementById("oinfo");if(!el||!rd("total"))return;
  const d={total:rd("total").value,good:rd("good").value,scrap:rd("scrap").value,mpp:rd("mpp").value,setup:rd("setup").value,vz:rd("vz").value},status=rd("status").value;
  const rest=Math.max(0,num(d.total)-num(d.good)-num(d.scrap)),pure=rest*num(d.mpp),vzm=pure*vzOf(d)/100,su=status===STA[1]?num(d.setup)*60:0,tot=pure+vzm+su;
  el.innerHTML=`<b>Reststücke:</b> ${rest}<br><b>Reine Laufzeit:</b> ${hm(pure)}<br><b>Verteilzeit (${fm(vzOf(d))} %):</b> + ${hm(vzm)}<br>${su?`<b>Rüstzeit:</b> + ${hm(su)}<br>`:""}<b>Restlaufzeit gesamt (ab jetzt):</b> ${hm(tot)}<br><b>Fertig (Vorschau):</b> ${fdt(Date.now()+tot*6e4)}`;
}
function ordSave(m){
  const now=Date.now(),status=rd("status").value;
  const o={artNr:rd("artNr").value,desc:rd("desc").value,order:rd("order").value,total:num(rd("total").value),good:num(rd("good").value),scrap:num(rd("scrap").value),mpp:num(rd("mpp").value),setup:num(rd("setup").value),vz:String(rd("vz").value).trim()===""?"":num(rd("vz").value),status,note:rd("note").value,updatedAt:now};
  o.finishAt=now+runMin(o,status)*60000;ordSet(m,o);
}
function ordView(){
  if(cur.edit!==null&&cur.edit!==undefined)return editView(cur.edit);
  const cards=M.map((n,m)=>{
    const d=ordGet(m);
    if(!d)return `<button class="card oc" data-o="${m}"><b>${esc(n)}</b><br><span class="hint">Kein Auftrag</span></button>`;
    const fin=finOf(d),remain=Math.max(0,Math.round((fin-Date.now())/60000)),p=d.total?Math.min(100,Math.round(num(d.good)/d.total*100)):0,sp=d.total?Math.round(num(d.scrap)/d.total*100):0;
    const c=stCls(m);
    const upd=d.updatedAt?new Date(d.updatedAt):null,today=upd&&upd.toDateString()===new Date().toDateString();
    return `<button class="card oc ${c}" data-o="${m}"><b>${esc(n)}</b>${d.artNr?` <span class="hint">[${esc(d.artNr)}]</span>`:""}${upd?` <span class="hint ${today?"ok":""}">${today?"● heute "+upd.toLocaleTimeString("de-DE",{hour:"2-digit",minute:"2-digit"}):"Aktualisiert "+upd.toLocaleDateString("de-DE")}</span>`:""}<br>${esc(d.desc||"")}${d.order?`<br><span class="hint">Auftrag: ${esc(d.order)}</span>`:""}<br><b>${fm(num(d.good))} / ${fm(num(d.total))} Stück</b><div class="bar"><span style="width:${p}%"></span></div>${d.scrap?`<span class="hint ${sp>2?"bd":""}">Ausschuss: ${fm(num(d.scrap))} (${sp} %)</span><br>`:""}<span class="hint">${esc(d.status||STA[0])} · Rest ${hm(remain)} · Verteilzeit ${fm(vzOf(d))} %<br>Fertig: ${fdt(fin)}</span>${d.note?`<br><span class="hint">Notiz: ${esc(d.note)}</span>`:""}</button>`;
  }).join("");
  return `<h2>Aufträge je Maschine</h2><p class="hint">Hier trägst du die aktuellen Aufträge ein. Daraus berechnet die Planung den Bedarf pro Maschine, Tag und Woche. Standard-Verteilzeit: ${fm(st.vz)} % (änderbar unter Planung, ganz unten).</p>${cards}`;
}

/* Einmalige Umstellung alter Daten: Nachtschichten, die am Abend des Tages begannen, gehören jetzt zum Folgetag */
if(!st.v||st.v<3){
  const nd={};
  Object.keys(st.days).forEach(k=>{const d=st.days[k];nd[k]={job:clone(d.job||{}),seg:clone(d.seg||[]),e:1}});
  Object.keys(st.days).sort().forEach(k=>{
    const d=nd[k],stay=[];
    d.seg.forEach(s=>{
      if(s.f>=WE){
        const n=add(k,1),x=nd[n]||(nd[n]={job:{},seg:[],e:1});
        if(!x.job[s.m]&&d.job[s.m])x.job[s.m]=clone(d.job[s.m]);
        x.seg.push({m:s.m,emp:s.emp,f:s.f-1440,t:s.t-1440});
      }else stay.push(s);
    });
    d.seg=stay;
  });
  st.days=nd;st.v=3;save();
}
/* Korrektur: Nachtschicht endet wieder um 4:20 */
if(st.v<4){Object.values(st.days).forEach(d=>d.seg.forEach(s=>{if(s.f===-220&&s.t===240)s.t=260}));st.v=4;save();}

let cur={tab:"plan",w:0,i:0,msg:"",edit:null,emp:false};
(()=>{const n=new Date(),nm=n.getHours()*60+n.getMinutes(),pk=kd(nm>=WE?dt(1):dt(0)),diff=Math.round((pd(pk)-pd(wdays(0)[0]))/864e5);cur.w=Math.floor(diff/7);cur.i=((diff%7)+7)%7})();
const sel=()=>wdays(cur.w)[cur.i];

/* Letzter Arbeitstag (Mo-Fr) mit Einteilung vor Tag k */
const srcOf=k=>{let p=k;for(let i=0;i<7;i++){p=add(p,-1);if(isW(p)&&st.days[p]&&st.days[p].seg.length)return p}return null};
/* Mo-Fr ab heute bis Ende der angezeigten Woche automatisch vorbefüllen, solange der Tag nicht selbst bearbeitet wurde */
function auto(){
  const end=wdays(cur.w)[6];let ch=false;
  for(let k=kd(dt(0));k<=end;k=add(k,1)){
    if(!isW(k))continue;
    const d=st.days[k];if(d&&d.e)continue;
    const s=srcOf(k);if(!s)continue;
    const S=st.days[s];
    if(d&&d.src===s&&JSON.stringify([d.job,d.seg])===JSON.stringify([S.job,S.seg]))continue;
    st.days[k]={job:clone(S.job),seg:clone(S.seg),e:0,src:s};ch=true;
  }
  if(ch)save();
}

/* Mitarbeiter verwalten: Namen sind die Schlüssel in den Einsätzen, daher beim Umbenennen und Löschen überall nachziehen */
function renameEmp(i,nn){
  const old=st.emp[i];if(old===nn)return;
  st.emp[i]=nn;st.roles[nn]=roleOf(old);delete st.roles[old];
  Object.values(st.days).forEach(d=>(d.seg||[]).forEach(s=>{if(s.emp===old)s.emp=nn}));
}
function delEmp(i){
  const n=st.emp[i];
  Object.values(st.days).forEach(d=>(d.seg||[]).forEach(s=>{if(s.emp===n)s.emp=""}));
  st.emp.splice(i,1);delete st.roles[n];
}

const weekNav=()=>{const ds=wdays(cur.w);return `<div class="wnv"><button class="btn" data-wn="-1" aria-label="Vorherige Woche">‹</button><div class="wl"><b>Woche ${kw(ds[0])}</b><small>${sd(ds[0])} – ${sd(ds[6])}</small></div><button class="btn" data-wn="1" aria-label="Nächste Woche">›</button><button class="btn" data-wn="0">Heute</button></div>`};
const strip=()=>`<div class="days">${wdays(cur.w).map((k,i)=>`<button class="chip${i>4?" we":""}" data-i="${i}" aria-pressed="${i==cur.i}">${DN[i]}<small>${sd(k)}</small></button>`).join("")}</div>`;
const dayHint=k=>`<p class="hint">Dieser Planungstag beginnt am Vorabend (${esc(wd(add(k,-1)))}) um 20:20 mit der Nachtschicht und endet um 20:20.</p>`;

function overview(){
  const ds=wdays(cur.w);
  const hr=(k,f)=>G(k).seg.filter(f).reduce((a,s)=>a+hrs(s),0);
  const rows=st.emp.map(e=>`<tr><td class="lname">${esc(e)}<small class="rl">${esc(roleOf(e))}</small></td>${ds.map(k=>{const h=hr(k,s=>s.emp===e);return `<td>${h?fm(h):"–"}</td>`}).join("")}</tr>`).join("");
  const open=`<tr><td>Nicht zugeteilt</td>${ds.map(k=>{const h=hr(k,s=>!s.emp);return `<td class="${h?"bd":""}">${h?fm(h):"–"}</td>`}).join("")}</tr>`;
  return `<h2>Woche im Überblick (Stunden)</h2><div class="card gs"><table class="ov"><tr><th></th>${ds.map((k,i)=>`<th><button class="ovb${i==cur.i?" on":""}" data-i="${i}">${DN[i]}</button></th>`).join("")}</tr>${rows}${open}</table></div>`;
}

function planView(){
  const k=sel(),d=G(k),ds=d.seg;
  const load=st.emp.map(n=>{
    const sg=ds.filter(s=>s.emp===n),h=sg.reduce((a,s)=>a+hrs(s),0);
    const pts=sg.reduce((a,s)=>a+w(Jg(k,s.m))*hrs(s)/8,0),ms=new Set(sg.map(s=>s.m)).size,r=pts/st.cap,c=r>1?"bd":r>.75?"wn":"ok";
    return `<div class="lrow"><div class="lname">${esc(n)}<small class="rl">${esc(roleOf(n))}</small></div><div class="bar ${c}"><span style="width:${Math.min(100,r*100)}%"></span></div><div class="lsum ${c}">${ms} Masch. · ${fm(h)} h · Last ${fm(pts)}</div></div>`}).join("");
  const segRow=(s,i)=>`<div class="sr" data-si="${i}"><select data-sf="emp"><option value="">Nicht zugeteilt</option>${st.emp.map(x=>`<option value="${esc(x)}"${x===s.emp?" selected":""}>${esc(x)} · ${esc(roleOf(x))}</option>`).join("")}</select><input type="time" data-sf="f" value="${tm(s.f)}"><span>bis</span><input type="time" data-sf="t" value="${tm(s.t)}"><button class="x" data-a="del" aria-label="Einsatz löschen">✕</button></div>`;
  const cards=M.map((n,m)=>{
    const j=Jg(k,m),sg=ds.map((s,i)=>[s,i]).filter(([s])=>s.m===m),h=sg.reduce((a,[s])=>a+hrs(s),0),un=sg.some(([s])=>!s.emp);
    return `<div class="m ${stCls(m)}${un?" u":""}" data-m="${m}"><div class="mh"><div class="mn">${esc(n)} <small>${fm(h)} h geplant${un?" · ohne Mitarbeiter":""}</small></div><div><label>Prio</label><select data-j="prio">${opt(Array.from({length:13},(_,x)=>x+1),j.prio-1)}</select></div></div>
    ${ordLine(k,m,h)}
    <div class="md"><div><label>Spannen</label><select data-j="robot">${opt(ROB,j.robot)}</select></div><div><label>Komplexität</label><select data-j="kompl">${opt(KOM,j.kompl)}</select></div><div><label>Messen</label><select data-j="mess">${opt(MES,j.mess)}</select></div><div><label>Laufzeit</label><select data-j="lauf">${opt(LAU,j.lauf)}</select></div><label class="rue"><input type="checkbox" data-j="rue"${j.rue?" checked":""}>Rüsten</label><div class="wt">Aufwand ${fm(w(j))}</div></div>
    ${sg.map(([s,i])=>segRow(s,i)).join("")}
    <div class="add">${SH.map((p,x)=>`<button class="btn s" data-a="add" data-p="${x}">+ ${p[0]}</button>`).join("")}<button class="btn s" data-a="add" data-p="-1">+ Eigene Zeit</button></div></div>`}).join("");
  const note=d.src&&!d.e?`<p class="hint">Automatisch übernommen von ${esc(lab(pd(d.src)))}. Sobald du etwas änderst, gilt der Tag als deine eigene Planung.</p>`:(!isW(k)&&!ds.length?`<p class="hint">Wochenende: wird nicht vorausgefüllt, Arbeiten ist optional.</p>`:"");
  const empMgr=`<details id="empd"${cur.emp?" open":""}><summary>Mitarbeiter, Kapazität und Verteilzeit bearbeiten</summary>
  <h2>Mitarbeiter und Rollen</h2>
  ${st.emp.map((e,i)=>`<div class="er" data-ei="${i}"><input type="text" data-en value="${esc(e)}" aria-label="Name"><select data-er aria-label="Rolle">${ROLES.map(r=>`<option${r===roleOf(e)?" selected":""}>${esc(r)}</option>`).join("")}</select><button class="x" data-a="delEmp" aria-label="Mitarbeiter löschen">✕</button></div>`).join("")}
  <div class="ea"><input type="text" id="newName" placeholder="Neuer Mitarbeiter" aria-label="Name neuer Mitarbeiter"><select id="newRole" aria-label="Rolle neuer Mitarbeiter">${ROLES.map(r=>`<option>${esc(r)}</option>`).join("")}</select><button class="btn" data-a="addEmp">Hinzufügen</button></div>
  <p class="hint">Namen und Rollen werden direkt beim Ändern gespeichert. Beim Umbenennen bleiben alle Einsätze erhalten. Beim Löschen werden die Einsätze der Person auf „Nicht zugeteilt“ gesetzt.</p>
  <h2>Kapazität und Verteilzeit</h2>
  <label>Kapazität pro Tag (Lastpunkte)</label><input id="cap" type="number" min="1" step="0.5" value="${st.cap}"><label style="margin-top:8px">Standard-Verteilzeit in % (Plattenwechsel, Späne entfernen)</label><input id="vz" type="number" min="0" step="any" value="${st.vz}"><div class="tools"><button class="btn" data-a="saveEmp">Speichern</button></div></details>`;
  return `${weekNav()}${strip()}${overview()}<h2>${lab(pd(k))}</h2>${dayHint(k)}${note}
  <div class="tools"><button class="btn" data-a="copy">Vom letzten Arbeitstag übernehmen</button><button class="btn" data-a="clear">Tag leeren</button><span class="hint">${esc(cur.msg)}</span></div>
  <div class="card">${load}</div><p class="hint">Je Mitarbeiter: Anzahl Maschinen · Stunden · Last (Aufwand mal Stunden geteilt durch 8). Kapazität: ${fm(st.cap)}.</p>
  <h2>Maschinen</h2>${stLeg()}<p class="hint">Der farbige Streifen links zeigt den Status des Auftrags (wie im Maschinenrechner). Rot umrandet = Einsatz ohne Mitarbeiter.</p>${cards}
  ${empMgr}`;
}

function dayView(){
  const k=sel(),n=new Date(),nm=n.getHours()*60+n.getMinutes();
  const cpk=kd(nm>=WE?dt(1):dt(0)),cpos=nm>=WE?nm-1440:nm;
  const own=m=>G(k).seg.filter(s=>s.m===m&&Math.min(s.t,WE)>s.f).map(s=>({...s,c:Math.min(s.t,WE)}));
  const pc=x=>(x-WS)/WL*100;
  const blk=s=>`<div class="gb" style="left:${pc(s.f)}%;width:${pc(s.c)-pc(s.f)}%;background:${col(s.emp)}" title="${esc(s.emp||"Nicht zugeteilt")} ${tm(s.f)}–${tm(s.t)}">${esc(s.emp||"?")} ${tm(s.f)}–${tm(s.t)}</div>`;
  const hh=[0,1,2,3,4,5,6].map(i=>`<span style="left:${i/6*100}%">${tm(WS+i*240)}</span>`).join("");
  const band=m=>{const d=ordGet(m);if(!d)return "";const s=Math.max(Date.now(),at(k,WS)),e=Math.min(finOf(d),at(k,WE));if(e<=s)return "";const a=(s-at(k,0))/6e4,b=(e-at(k,0))/6e4;return `<div class="busy" style="left:${pc(a)}%;width:${pc(b)-pc(a)}%" title="Auftrag läuft bis ${fdt(finOf(d))}"></div>`};
  const rows=M.map((nme,m)=>{const d=ordGet(m);return `<div class="gr"><div class="gn" title="${esc(nme+(d&&d.order?" · Auftrag "+d.order:""))}">${esc(nme)}${d&&d.order?`<small>${esc(d.order)}</small>`:""}</div><div class="gl">${band(m)}${k===cpk?`<span class="now" style="left:${pc(cpos)}%"></span>`:""}${own(m).map(blk).join("")}</div></div>`}).join("");
  return `${weekNav()}${strip()}<h2>${lab(pd(k))}</h2>${dayHint(k)}<div class="gs"><div class="gt"><div class="gh">${hh}</div>${rows}</div></div>
  <div class="leg">${st.emp.map(e=>`<span><i style="background:${col(e)}"></i>${esc(e)} (${esc(roleOf(e))})</span>`).join("")}</div>
  <p class="hint">Balken zeigen, wer wann an welcher Maschine steht. Die Zeitachse läuft von 20:20 am Vorabend bis 20:20. Die hellblaue Fläche zeigt, wann ein Auftrag auf der Maschine läuft. Die rote Linie ist die aktuelle Uhrzeit.</p>`;
}

function weekView(){
  const ds=wdays(cur.w),wk=ds[0],sg=ds.flatMap(k=>G(k).seg);
  let tS=0,tP=0;
  const rows=M.map((n,m)=>{
    const p=sg.filter(s=>s.m===m).reduce((a,s)=>a+hrs(s),0),ex=st.soll[wk]?.[m],au=ordGet(m)?Math.round(overlap(m,at(ds[0],WS),at(ds[6],WE))*10)/10:undefined,v=ex??(au!==undefined?au:st.sollDef[m]),fo=ex===undefined&&au!==undefined;
    const has=v!==undefined&&v!==null,diff=has?p-v:0,c=!has?"":diff<0?"bd":"ok";
    if(has)tS+=v;tP+=p;
    return `<div class="wr"><div class="lname" title="${esc(n)}">${esc(n)}</div><div><label>Soll h${fo?" (Auftrag)":""}</label><input type="number" min="0" step="1" data-soll="${m}" value="${has?v:""}"></div><div><label>Geplant h</label><b>${fm(p)}</b></div><div class="${c}"><label>Differenz</label><b>${has?(diff>=0?"+":"")+fm(diff)+" h":"Soll eintragen"}</b></div><div class="bar ${c||"wn"}"><span style="width:${has&&v>0?Math.min(100,p/v*100):0}%"></span></div></div>`}).join("");
  const er=st.emp.map(e=>{const h=sg.filter(s=>s.emp===e).reduce((a,s)=>a+hrs(s),0);return `<div class="lrow"><div class="lname">${esc(e)}<small class="rl">${esc(roleOf(e))}</small></div><div class="bar"><span style="width:${Math.min(100,h/60*100)}%;color:${col(e)}"></span></div><div class="lsum">${fm(h)} h</div></div>`}).join("");
  return `${weekNav()}<h2>Soll und geplant pro Maschine</h2><div class="card">${rows}<div class="wr"><b>Gesamt</b><b>${fm(tS)} h</b><b>${fm(tP)} h</b><b class="${tP<tS?"bd":"ok"}">${(tP-tS>=0?"+":"")+fm(tP-tS)} h</b><span></span></div></div>
  <p class="hint">Soll kommt automatisch aus dem Auftrag der Maschine (Laufzeit inklusive Verteilzeit), solange du nichts Eigenes einträgst. Ohne Auftrag gilt dein zuletzt eingetragenes Soll weiter. Geplant ist die Summe aller Einsätze der Woche Montag bis Sonntag. Die Nachtschicht von Sonntag auf Montag zählt zum Montag. Es wird nichts gesperrt.</p>
  <h2>Stunden pro Mitarbeiter</h2><div class="card">${er}</div><p class="hint">Balken: 60 Stunden entsprechen voll.</p>`;
}

function render(){
  auto();
  document.querySelectorAll(".tab").forEach(b=>b.setAttribute("aria-pressed",b.dataset.tab===cur.tab));
  $("#app").innerHTML={plan:planView,day:dayView,week:weekView,orders:ordView}[cur.tab]();
  if(cur.tab==="orders"&&cur.edit!=null)ordPreview();
}
/* Minütlich aktualisieren (Statusfarben, Restzeiten), aber nie während man gerade etwas eingibt */
setInterval(()=>{
  const a=document.activeElement,typing=a&&a.matches&&a.matches("input,select,textarea");
  if(typing)return;
  if((cur.tab==="orders"&&cur.edit==null)||cur.tab==="plan")render();
},60000);
document.addEventListener("toggle",ev=>{if(ev.target&&ev.target.id==="empd")cur.emp=ev.target.open},true);
document.addEventListener("input",ev=>{if(ev.target.id&&ev.target.id.startsWith("o_"))ordPreview()});
document.addEventListener("click",ev=>{
  const t=ev.target.closest("button");if(!t)return;const a=t.dataset,k=sel();cur.msg="";
  if(a.tab){cur.tab=a.tab;cur.edit=null}
  else if(a.o!==undefined)cur.edit=+a.o;
  else if(a.a==="ocancel")cur.edit=null;
  else if(a.a==="osave"){ordSave(cur.edit);cur.edit=null}
  else if(a.a==="oreset"){if(!confirm(M[cur.edit]+" wirklich zurücksetzen? Alle Felder werden geleert."))return;ordSet(cur.edit,null);cur.edit=null}
  else if(a.i!==undefined)cur.i=+a.i;
  else if(a.wn!==undefined){cur.w=a.wn==="0"?0:cur.w+ +a.wn;if(a.wn==="0"){const n=new Date(),nm=n.getHours()*60+n.getMinutes(),df=Math.round((pd(kd(nm>=WE?dt(1):dt(0)))-pd(wdays(0)[0]))/864e5);cur.w=Math.floor(df/7);cur.i=((df%7)+7)%7}}
  else if(a.a==="add"){const p=SH[+a.p]||["",480,960],d=D(k);d.e=1;d.seg.push({m:+t.closest("[data-m]").dataset.m,emp:"",f:p[1],t:p[2]});save()}
  else if(a.a==="del"){const d=D(k);d.e=1;d.seg.splice(+t.closest("[data-si]").dataset.si,1);save()}
  else if(a.a==="copy"){const s=srcOf(k);if(s){st.days[k]={job:clone(st.days[s].job),seg:clone(st.days[s].seg),e:1};save()}else cur.msg="Kein vorheriger Arbeitstag mit Planung gefunden."}
  else if(a.a==="clear"){st.days[k]={job:{},seg:[],e:1};save()}
  else if(a.a==="addEmp"){
    const nn=$("#newName").value.trim(),rl=$("#newRole").value;
    if(!nn){alert("Bitte einen Namen eingeben.");return}
    if(st.emp.includes(nn)){alert("Diesen Namen gibt es schon. Bitte einen eindeutigen Namen verwenden, z. B. mit Nachnamen-Initial.");return}
    st.emp.push(nn);st.roles[nn]=ROLES.includes(rl)?rl:ROLES[0];cur.emp=true;save()}
  else if(a.a==="delEmp"){
    const i=+t.closest("[data-ei]").dataset.ei,n=st.emp[i];
    if(!confirm(n+" wirklich löschen? Bestehende Einsätze der Person werden auf „Nicht zugeteilt“ gesetzt."))return;
    delEmp(i);cur.emp=true;save()}
  else if(a.a==="saveEmp"){st.cap=Math.max(1,+$("#cap").value||8);{const v=parseFloat(String($("#vz").value).replace(",","."));st.vz=isNaN(v)?10:Math.max(0,v)}save()}
  else return;
  render();
});
document.addEventListener("change",ev=>{
  const t=ev.target,k=sel();
  if(t.id==="cap"||t.id==="vz"||t.id==="newName"||t.id==="newRole"||(t.id&&t.id.startsWith("o_")))return;
  const er=t.closest("[data-ei]");
  if(er){
    const i=+er.dataset.ei,old=st.emp[i];
    if(t.dataset.en!==undefined){
      const nn=t.value.trim();
      if(!nn||(nn!==old&&st.emp.includes(nn))){alert(!nn?"Der Name darf nicht leer sein.":"Diesen Namen gibt es schon.");return render()}
      renameEmp(i,nn);
    }else if(t.dataset.er!==undefined){st.roles[old]=ROLES.includes(t.value)?t.value:ROLES[0]}
    cur.emp=true;save();return render();
  }
  if(t.dataset.soll!==undefined){const wk=wdays(cur.w)[0],v=Math.max(0,+t.value||0);(st.soll[wk]=st.soll[wk]||{})[t.dataset.soll]=v;st.sollDef[t.dataset.soll]=v;save();return render()}
  const sr=t.closest("[data-si]"),mc=t.closest("[data-m]");
  if(sr&&t.dataset.sf){const d=D(k),s=d.seg[+sr.dataset.si],f=t.dataset.sf;d.e=1;
    if(f==="emp")s.emp=t.value;
    else if(f==="f"){s.f=nz(pt(t.value));if(s.t<=s.f)s.t+=1440}
    else{let v=nz(pt(t.value));if(v<=s.f)v+=1440;s.t=v}}
  if(mc&&t.dataset.j){const f=t.dataset.j,j=J(k,+mc.dataset.m);D(k).e=1;j[f]=f==="rue"?(t.checked?1:0):f==="prio"?+t.value+1:+t.value}
  save();render();
});
render();
</script>
</body>
</html>
