<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="theme-color" content="#1a3a6b">
<title>Wildcard — Helsinki Tennis</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,600;1,600&family=Lora:ital,wght@0,400;0,500;0,600;1,400&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0}
html,body{height:100%;-webkit-text-size-adjust:100%}
body{font-family:'Lora',Georgia,serif;background:#edf1fb;color:#1a1a2e;max-width:430px;margin:0 auto;overflow-x:hidden;-webkit-font-smoothing:antialiased}
button,a{cursor:pointer;border:none;background:none;font-family:inherit;-webkit-tap-highlight-color:transparent;text-decoration:none;color:inherit}
input,textarea,select{font-family:'Lora',Georgia,serif;font-size:16px;-webkit-appearance:none;outline:none}
svg{display:block;flex-shrink:0}

:root{
  --b:#1a3a6b;--bm:#2756a8;--bl:#dde8f8;--bp:#edf1fb;
  --g:#156b38;--gm:#1a9e4f;--gl:#dff0eb;
  --p:#4a1a7b;--pm:#7c3aed;--pl:#ede6ff;
  --sur:#fff;--bdr:#ccd4ec;--bdr2:#a8b4d8;
  --t1:#1a1a2e;--t2:#3a3a5c;--t3:#7880a8;
  --r:14px;--rs:10px;--nh:66px;
}

/* ── SCREENS ── */
.screen{display:none;flex-direction:column;min-height:100dvh}
.screen.active{display:flex}
.scr-content{flex:1;overflow-y:auto;padding-bottom:calc(var(--nh)+16px);-webkit-overflow-scrolling:touch}

/* ── TOP BAR ── */
.bar{background:var(--sur);border-bottom:1px solid var(--bdr2);padding:12px 16px;display:flex;align-items:center;gap:10px;position:sticky;top:0;z-index:50}
.bar-title{font-family:'Playfair Display',serif;font-size:17px;font-style:italic;font-weight:600;flex:1;color:var(--t1)}
.bar-back{color:var(--bm);display:flex;align-items:center;gap:4px;font-size:14px;font-weight:500}
.bar-icon{position:relative;padding:5px;color:var(--t3);display:flex}
.ndot{position:absolute;top:4px;right:3px;width:8px;height:8px;background:#e83050;border-radius:50%;border:2px solid var(--sur);pointer-events:none}

/* ── BOTTOM NAV ── */
.bnav{position:fixed;bottom:0;left:50%;transform:translateX(-50%);width:100%;max-width:430px;height:var(--nh);background:var(--sur);border-top:1px solid var(--bdr2);display:flex;z-index:100;padding-bottom:env(safe-area-inset-bottom,0px)}
.ni{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:3px;color:var(--t3);font-size:9px;font-weight:500;letter-spacing:.3px;padding:4px 2px 6px;transition:color .15s}
.ni.on{color:var(--bm)}
.ni svg{width:22px;height:22px;stroke:currentColor;fill:none;stroke-width:1.7;stroke-linecap:round;stroke-linejoin:round}
.ni.on svg{stroke-width:2.1}

/* ── RANK RIBBON ── */
.rrbn{display:flex;align-items:center;gap:8px;background:var(--pl);border-bottom:1px solid #c4aef0;padding:7px 16px;font-size:13px;color:var(--p);font-style:italic}
.rrbn svg{stroke:var(--pm);fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round;flex-shrink:0}

/* ── AFFIRMATION ── */
.affirm{background:linear-gradient(130deg,var(--b),var(--p));padding:12px 18px;color:#fff;position:relative;overflow:hidden}
.affirm::after{content:'';position:absolute;inset:0;background:radial-gradient(ellipse at 75% 50%,rgba(255,255,255,.07),transparent 65%);pointer-events:none}
.affirm-em{font-size:18px;margin-bottom:4px;display:block;position:relative;z-index:1}
.affirm-tx{font-size:13px;line-height:1.55;font-style:italic;position:relative;z-index:1;opacity:.95}

/* ── AUTH ── */
.auth{display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:100dvh;padding:48px 28px 36px;background:linear-gradient(155deg,var(--bl) 0%,var(--pl) 50%,var(--gl) 100%)}
.auth-ball{width:96px;height:96px;margin-bottom:14px;filter:drop-shadow(0 4px 14px rgba(39,86,168,.3))}
.auth h1{font-family:'Playfair Display',serif;font-size:30px;font-weight:600;letter-spacing:.3px;margin-bottom:4px;background:linear-gradient(125deg,var(--b),var(--p));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.auth-sub{font-size:13px;color:var(--t3);margin-bottom:28px;font-style:italic}
.fld{width:100%;margin-bottom:13px}
.fld label{display:block;font-size:10px;letter-spacing:1px;color:var(--t2);margin-bottom:5px;text-transform:uppercase;font-weight:600;font-family:'Lora',serif}
.fld input,.fld select,.fld textarea{width:100%;padding:12px 14px;border:1.5px solid var(--bdr2);border-radius:var(--rs);background:var(--sur);color:var(--t1);font-size:15px;transition:border-color .2s}
.fld input:focus,.fld textarea:focus{border-color:var(--bm)}
.fld textarea{resize:none;height:78px}

/* ── BUTTONS ── */
.btn{width:100%;padding:13px;border-radius:var(--rs);font-size:15px;font-weight:600;margin-bottom:10px;font-family:'Lora',serif;transition:transform .1s,opacity .2s}
.btn:active{transform:scale(.98)}
.btn-p{background:linear-gradient(130deg,var(--bm),var(--pm));color:#fff}
.btn-o{background:none;border:2px solid var(--bm);color:var(--bm)}
.btn-sm{padding:7px 14px;border-radius:var(--rs);font-size:12px;width:auto;font-weight:600;font-family:'Lora',serif}
.btn-bsm{background:var(--bm);color:#fff}
.btn-osm{background:none;border:1.5px solid var(--bm);color:var(--bm)}

/* ── HERO ── */
.hero{background:linear-gradient(130deg,var(--b) 0%,var(--bm) 55%,var(--p) 100%);padding:18px 18px 16px;color:#fff;display:flex;align-items:center;gap:14px}
.hero-ball{width:54px;height:54px;filter:drop-shadow(0 2px 6px rgba(0,0,0,.3))}
.hero-ey{font-size:9px;letter-spacing:1.5px;opacity:.65;text-transform:uppercase;font-weight:600;font-family:'Lora',serif;margin-bottom:3px}
.hero-nm{font-family:'Playfair Display',serif;font-size:18px;font-style:italic;font-weight:600;line-height:1.2}
.hero-sub{font-size:11px;opacity:.7;margin-top:2px}
.hero-rank{display:inline-flex;align-items:center;gap:5px;background:rgba(255,255,255,.16);border:1px solid rgba(255,255,255,.28);border-radius:20px;padding:3px 10px;margin-top:8px;font-size:11px;color:#fff;font-weight:500}

/* ── GRID ── */
.qgrid{display:grid;grid-template-columns:1fr 1fr;gap:10px;padding:14px}
.qcard{background:var(--sur);border-radius:var(--r);border:1px solid var(--bdr);padding:16px 12px;text-align:center;cursor:pointer;transition:transform .1s}
.qcard:active{transform:scale(.96)}
.qcard svg{width:26px;height:26px;stroke:var(--bm);fill:none;stroke-width:1.7;stroke-linecap:round;stroke-linejoin:round;display:block;margin:0 auto 8px}
.qcard span{font-size:13px;font-weight:600;color:var(--t1)}

/* ── SECTION LABEL ── */
.slbl{font-size:10px;letter-spacing:1.2px;color:var(--t3);text-transform:uppercase;padding:14px 16px 7px;font-weight:700;font-family:'Lora',serif}

/* ── CARD ── */
.card{background:var(--sur);border-radius:var(--r);border:1px solid var(--bdr);margin:8px 16px;overflow:hidden}
.ci{padding:13px 15px}

/* ── TOURNAMENT CARD ── */
.tc{background:var(--sur);border-radius:var(--r);border:1px solid var(--bdr);margin:8px 16px;overflow:hidden}
.tc-hd{background:linear-gradient(130deg,var(--b),var(--bm));padding:13px 15px}
.tc-hd h3{color:#fff;font-family:'Playfair Display',serif;font-size:15px;font-style:italic;font-weight:600;line-height:1.3}
.tc-hd p{color:rgba(255,255,255,.72);font-size:11px;margin-top:3px;font-weight:500}
.tc-body{padding:13px 15px}
.t-meta{display:flex;gap:12px;margin-bottom:10px;flex-wrap:wrap}
.t-mi{display:flex;align-items:center;gap:5px;font-size:12px;color:var(--t3);font-weight:500}
.t-mi svg{stroke:var(--bm);fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round;flex-shrink:0}

/* ── BADGES ── */
.badge{display:inline-flex;align-items:center;padding:2px 9px;border-radius:20px;font-size:10px;font-weight:700;letter-spacing:.2px}
.bb{background:var(--bl);color:var(--b)}
.bg{background:var(--gl);color:var(--g)}
.bp{background:var(--pl);color:var(--p)}
.bs{background:#edf0f7;color:#3a4a70}

/* ── GROUPS / BRACKET ── */
.gbox{background:var(--sur);border-radius:var(--r);border:1px solid var(--bdr);margin:7px 16px;overflow:hidden}
.ghd{background:var(--bl);padding:9px 13px;display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid var(--bdr)}
.ghd h4{font-size:13px;color:var(--b);font-weight:600}
.mrow{display:flex;align-items:center;padding:9px 13px;border-bottom:1px solid var(--bdr)}
.mrow:last-child{border-bottom:none}
.mpl{font-size:13px;flex:1;font-weight:500}
.mvs{font-size:10px;color:var(--t3);padding:0 6px;font-weight:700}
.mtime{font-size:11px;color:var(--bm);font-weight:700;white-space:nowrap}
.bwrap{overflow-x:auto;padding:0 16px 14px;-webkit-overflow-scrolling:touch}
.bracket{display:flex;gap:10px;min-width:440px}
.bcol{display:flex;flex-direction:column;gap:7px;flex:1}
.blbl{font-size:9px;letter-spacing:.7px;color:var(--t3);text-transform:uppercase;margin-bottom:3px;text-align:center;font-weight:700}
.mbox{background:var(--sur);border:1px solid var(--bdr);border-radius:var(--rs);overflow:hidden}
.mbox .bp2{padding:6px 9px;font-size:12px;border-bottom:1px solid var(--bdr);display:flex;justify-content:space-between;font-weight:500}
.mbox .bp2:last-child{border-bottom:none}
.mbox .bw2{color:var(--bm);font-weight:700}
.bsc{color:var(--t3);font-size:10px;font-weight:700}

/* ── COURTS ── */
.crt{background:var(--sur);border-radius:var(--r);border:1px solid var(--bdr);margin:8px 16px;overflow:hidden}
.crt-banner{height:82px;display:flex;align-items:flex-end;padding:0 13px 10px;position:relative}
.crt-nm{color:#fff;font-family:'Playfair Display',serif;font-size:15px;font-style:italic;font-weight:600;text-shadow:0 1px 4px rgba(0,0,0,.5)}
.crt-info{padding:10px 13px}
.crt-meta{font-size:12px;color:var(--t3);display:flex;gap:12px;flex-wrap:wrap;margin-top:3px;align-items:center;font-weight:500}
.crt-meta svg{stroke:var(--t3);fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round;flex-shrink:0}
.crt-price{font-size:12px;color:var(--g);font-weight:700;margin-top:3px}
.crt-note{font-size:11px;color:var(--t3);margin-top:3px;font-style:italic}
.slots{display:flex;flex-wrap:wrap;gap:4px;margin-top:7px}
.slots-hd{font-size:10px;font-weight:700;color:var(--t3);margin-top:7px;text-transform:uppercase;letter-spacing:.8px}
.ts{padding:3px 9px;border-radius:20px;font-size:11px;font-weight:700}
.ts-f{background:var(--gl);color:var(--g)}
.ts-t{background:#fde8ee;color:#8b1a3a;text-decoration:line-through}
.ts-m{background:#fff3cd;color:#7a5a00}
.crt-btn{margin-top:9px;width:100%;padding:9px;border-radius:var(--rs);font-size:12px;font-weight:600;background:var(--bl);color:var(--bm);border:1px solid var(--bdr);cursor:pointer;font-family:'Lora',serif;transition:background .15s,color .15s}
.crt-btn:active{background:var(--bm);color:#fff}

/* ── FEED ── */
.pcard{background:var(--sur);border-radius:var(--r);border:1px solid var(--bdr);margin:8px 16px;overflow:hidden}
.phdr{display:flex;align-items:center;gap:10px;padding:11px 13px;border-bottom:1px solid var(--bdr)}
.pimg{background:var(--bl);height:190px;display:flex;align-items:center;justify-content:center;flex-direction:column;gap:6px;font-size:42px}
.pbody{padding:11px 13px;font-size:14px;line-height:1.55;color:var(--t2);font-style:italic}
.pacts{display:flex;gap:14px;padding:9px 13px;border-top:1px solid var(--bdr)}
.pact{display:flex;align-items:center;gap:5px;font-size:12px;color:var(--t3);font-weight:600;cursor:pointer}
.pact svg{stroke:currentColor;fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round}
.pact.liked{color:#e83050}
.pact.liked svg{fill:#e83050;stroke:#e83050}

/* ── MESSAGES ── */
.cshd{padding:8px 16px 5px;font-size:10px;letter-spacing:1.2px;color:var(--t3);text-transform:uppercase;font-weight:700;background:var(--bp);border-bottom:1px solid var(--bdr)}
.crow{display:flex;align-items:center;gap:11px;padding:12px 16px;border-bottom:1px solid var(--bdr);background:var(--sur);cursor:pointer;transition:background .12s}
.crow:active{background:var(--bp)}
.cinfo{flex:1;min-width:0}
.cnm{font-size:14px;font-weight:600}
.cprev{font-size:12px;color:var(--t3);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;margin-top:2px}
.ctm{font-size:11px;color:var(--t3);font-weight:600;white-space:nowrap}
.udot{width:8px;height:8px;background:var(--bm);border-radius:50%;flex-shrink:0}

/* ── AVATAR ── */
.av{width:36px;height:36px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:700;flex-shrink:0;border:1px solid var(--bdr)}
.av-b{background:var(--bl);color:var(--b)}
.av-g{background:var(--gl);color:var(--g)}
.av-p{background:var(--pl);color:var(--p)}
.av-s{background:#edf0f7;color:#3a4070}

/* ── CHAT WINDOW ── */
.chat-scr{display:none;flex-direction:column;min-height:100dvh}
.chat-scr.active{display:flex}
.msgs{flex:1;padding:14px;display:flex;flex-direction:column;gap:10px;padding-bottom:76px;overflow-y:auto;-webkit-overflow-scrolling:touch}
.bbl{max-width:78%;padding:9px 13px;border-radius:18px;font-size:14px;line-height:1.45}
.bbl-in{background:var(--sur);border:1px solid var(--bdr);align-self:flex-start;border-bottom-left-radius:4px}
.bbl-out{background:linear-gradient(130deg,var(--bm),var(--pm));color:#fff;align-self:flex-end;border-bottom-right-radius:4px}
.bbl-meta{font-size:10px;color:var(--t3);margin-top:2px;font-weight:500}
.bbl-r{text-align:right}
.msgbar{position:fixed;bottom:0;left:50%;transform:translateX(-50%);width:100%;max-width:430px;background:var(--sur);border-top:1px solid var(--bdr2);padding:9px 13px calc(9px + env(safe-area-inset-bottom,0px));display:flex;gap:8px;align-items:center;z-index:50}
.msgbar input{flex:1;padding:9px 14px;border:1.5px solid var(--bdr2);border-radius:22px;background:var(--bp);font-size:15px;font-family:'Lora',serif;color:var(--t1);transition:border-color .2s}
.msgbar input:focus{border-color:var(--bm)}
.sndbtn{width:38px;height:38px;border-radius:50%;background:linear-gradient(130deg,var(--bm),var(--pm));color:#fff;display:flex;align-items:center;justify-content:center;flex-shrink:0}
.sndbtn svg{stroke:#fff;fill:none;stroke-width:2;stroke-linecap:round;stroke-linejoin:round}

/* ── PROFILE ── */
.phero{background:linear-gradient(130deg,var(--b) 0%,var(--p) 100%);padding:22px 18px 18px;color:#fff;display:flex;align-items:center;gap:14px}
.pball{width:62px;height:62px;filter:drop-shadow(0 2px 8px rgba(0,0,0,.3))}
.p-nm{font-family:'Playfair Display',serif;font-size:18px;font-style:italic;font-weight:600}
.p-sub{font-size:12px;opacity:.7;margin-top:2px}
.stats{display:flex;border-bottom:1px solid var(--bdr)}
.stat{flex:1;text-align:center;padding:13px 4px;background:var(--sur);border-right:1px solid var(--bdr)}
.stat:last-child{border-right:none}
.stat-n{font-family:'Playfair Display',serif;font-size:19px;color:var(--bm)}
.stat-l{font-size:10px;color:var(--t3);margin-top:2px;font-weight:700;letter-spacing:.3px}

/* ── RANKING ── */
.rcard{background:linear-gradient(145deg,#edf1ff,#ede6ff);border:1px solid #c0caf0;border-radius:var(--r);margin:8px 16px;padding:14px}
.rtitle{font-size:10px;letter-spacing:1px;color:var(--b);text-transform:uppercase;font-weight:700;margin-bottom:9px}
.rdisplay{display:flex;align-items:flex-start;gap:13px;margin-bottom:12px}
.rbadge{width:54px;height:54px;border-radius:50%;border:2px solid var(--pm);display:flex;flex-direction:column;align-items:center;justify-content:center;background:#fff;flex-shrink:0}
.rbadge .rn{font-family:'Playfair Display',serif;font-size:20px;color:var(--p);line-height:1}
.rbadge .rl{font-size:8px;color:var(--pm);text-transform:uppercase;letter-spacing:.4px;font-weight:700}
.rinfo h4{font-size:14px;color:var(--b);font-weight:700;margin-bottom:4px;font-style:italic}
.rinfo p{font-size:12px;color:var(--t2);line-height:1.55}
.rinfo .rsk{font-size:11px;color:var(--bm);font-style:italic;margin-top:5px;font-weight:500}
.rbar-track{height:7px;background:rgba(74,26,123,.12);border-radius:4px;overflow:hidden;margin-bottom:3px}
.rbar-fill{height:100%;background:linear-gradient(90deg,var(--bm),var(--pm));border-radius:4px;transition:width .5s}
.rbar-lbls{display:flex;justify-content:space-between;font-size:10px;color:var(--t3);font-weight:700}
.rlvls{display:flex;flex-direction:column;gap:6px;padding:0 16px 6px}
.rlv{display:flex;align-items:flex-start;gap:10px;padding:10px 12px;border-radius:var(--rs);border:1px solid var(--bdr);background:var(--sur)}
.rlv-mine{border-color:var(--pm);background:var(--pl)}
.rlv-ico{width:32px;height:32px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0;background:var(--bl)}
.rlv-nm{font-size:13px;font-weight:700;color:var(--t1)}
.rlv-desc{font-size:12px;color:var(--t3);line-height:1.5;margin-top:2px}
.rlv-sk{font-size:11px;color:var(--bm);font-style:italic;margin-top:4px}

/* ── CONNECTIONS ── */
.con-item{display:flex;align-items:center;gap:11px;padding:11px 16px;border-bottom:1px solid var(--bdr);background:var(--sur)}
.con-item:last-child{border-bottom:none}

/* ── MENU ── */
.mnu{display:flex;align-items:center;gap:12px;padding:13px 16px;border-bottom:1px solid var(--bdr);background:var(--sur);cursor:pointer;transition:background .12s}
.mnu:last-child{border-bottom:none}
.mnu:active{background:var(--bp)}
.mnu-ico{width:20px;height:20px;stroke:var(--bm);fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round;flex-shrink:0}
.mnu-lbl{font-size:14px;flex:1;font-weight:600;color:var(--t1)}
.mnu-chev{stroke:var(--t3);fill:none;stroke-width:2;stroke-linecap:round}
.mnu-danger .mnu-ico{stroke:#c0392b}
.mnu-danger .mnu-lbl{color:#c0392b}

/* ── TAB BAR ── */
.tabs{display:flex;background:var(--sur);border-bottom:1.5px solid var(--bdr2);position:sticky;top:49px;z-index:40}
.tab{flex:1;padding:10px 3px;font-size:11px;color:var(--t3);background:none;border-bottom:2.5px solid transparent;text-align:center;font-weight:600;transition:color .15s;cursor:pointer;font-family:'Lora',serif}
.tab.on{color:var(--bm);border-bottom-color:var(--bm)}

/* ── SEGMENT ── */
.seg-wrap{display:flex;background:var(--bp);border:1px solid var(--bdr);border-radius:var(--rs);padding:3px;margin:12px 16px 0}
.seg{flex:1;padding:7px;border-radius:7px;font-size:12px;background:none;color:var(--t3);text-align:center;font-weight:600;transition:all .15s;cursor:pointer;font-family:'Lora',serif}
.seg.on{background:var(--sur);color:var(--bm);box-shadow:0 1px 3px rgba(39,86,168,.15)}

/* ── OVERLAY ── */
.ovl{position:fixed;inset:0;background:rgba(8,12,38,.58);z-index:200;display:flex;align-items:flex-end}
.ovl-panel{background:var(--sur);border-radius:22px 22px 0 0;padding:20px 20px calc(20px + env(safe-area-inset-bottom,0px));width:100%;max-height:90vh;overflow-y:auto;-webkit-overflow-scrolling:touch;animation:slideUp .24s ease}
@keyframes slideUp{from{transform:translateY(100%)}to{transform:translateY(0)}}
.ovl-handle{width:34px;height:4px;background:var(--bdr2);border-radius:2px;margin:0 auto 16px}
.ovl-panel h3{font-family:'Playfair Display',serif;font-size:17px;font-style:italic;font-weight:600;margin-bottom:14px;color:var(--t1)}

/* ── SETTINGS TOGGLE ── */
.strow{display:flex;align-items:center;gap:12px;padding:12px 14px;border-bottom:1px solid var(--bdr);background:var(--sur)}
.strow:last-child{border-bottom:none}
.strow-ico{width:19px;height:19px;stroke:var(--bm);fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round;flex-shrink:0}
.strow-nm{font-size:13px;font-weight:600;color:var(--t1)}
.strow-sub{font-size:11px;color:var(--t3);margin-top:1px}
.toggle{position:relative;width:44px;height:26px;flex-shrink:0}
.toggle input{position:absolute;opacity:0;width:0;height:0}
.tog-track{position:absolute;inset:0;border-radius:13px;background:#c8cce0;transition:background .2s;cursor:pointer}
.toggle input:checked+.tog-track{background:var(--bm)}
.tog-track::after{content:'';position:absolute;left:3px;top:3px;width:20px;height:20px;border-radius:50%;background:#fff;box-shadow:0 1px 3px rgba(0,0,0,.2);transition:transform .18s}
.toggle input:checked+.tog-track::after{transform:translateX(18px)}

/* ── NOTIF ── */
.ni-item{display:flex;align-items:flex-start;gap:11px;padding:11px 4px;border-bottom:1px solid var(--bdr)}
.ni-item:last-child{border-bottom:none}
.ni-ico{width:36px;height:36px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:17px;flex-shrink:0}
.ni-b{background:var(--bl)}.ni-g{background:var(--gl)}.ni-p{background:var(--pl)}
.ni-t{font-size:13px;font-weight:700;color:var(--t1);margin-bottom:2px}
.ni-b2{font-size:12px;color:var(--t3);line-height:1.45}
.ni-tm{font-size:11px;color:var(--t3);margin-top:3px;font-weight:600}
.ni-clr{width:100%;padding:11px;border-radius:var(--rs);font-size:13px;font-weight:600;background:var(--bl);color:var(--bm);margin-top:13px;cursor:pointer;font-family:'Lora',serif}

.hidden{display:none!important}
</style>
</head>
<body>

<!-- TENNIS BALL SVG SYMBOL -->
<svg style="display:none">
  <symbol id="ball" viewBox="0 0 100 100">
    <circle cx="50" cy="50" r="48" fill="#c8e648"/>
    <path d="M14,28 Q32,50 14,72" fill="none" stroke="#fff" stroke-width="5.5" stroke-linecap="round"/>
    <path d="M86,28 Q68,50 86,72" fill="none" stroke="#fff" stroke-width="5.5" stroke-linecap="round"/>
    <circle cx="50" cy="50" r="48" fill="none" stroke="rgba(0,0,0,0.07)" stroke-width="2"/>
  </symbol>
</svg>

<!-- SVG ICON HELPERS (defined once, used everywhere via JS) -->
<script>
const I={
  home:'<svg viewBox="0 0 24 24"><path d="M3 12L12 3l9 9M5 10v9a1 1 0 001 1h4v-5h4v5h4a1 1 0 001-1v-9"/></svg>',
  trophy:'<svg viewBox="0 0 24 24"><path d="M8 21h8M12 17v4M7 4h10l1 7a5 5 0 01-10 0z"/><path d="M5 7H3a2 2 0 000 4c.8 2 2 3 4 3M19 7h2a2 2 0 010 4c-.8 2-2 3-4 3"/></svg>',
  court:'<svg viewBox="0 0 24 24"><rect x="3" y="3" width="18" height="18" rx="1"/><line x1="12" y1="3" x2="12" y2="21"/><line x1="3" y1="12" x2="21" y2="12"/><line x1="7.5" y1="3" x2="7.5" y2="10.5" stroke-dasharray="2 1.5"/><line x1="16.5" y1="3" x2="16.5" y2="10.5" stroke-dasharray="2 1.5"/><line x1="7.5" y1="13.5" x2="7.5" y2="21" stroke-dasharray="2 1.5"/><line x1="16.5" y1="13.5" x2="16.5" y2="21" stroke-dasharray="2 1.5"/></svg>',
  feed:'<svg viewBox="0 0 24 24"><rect x="3" y="3" width="18" height="18" rx="2"/><circle cx="8.5" cy="8.5" r="1.5"/><path d="M21 15l-5-5L5 21"/></svg>',
  chat:'<svg viewBox="0 0 24 24"><path d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2z"/></svg>',
  user:'<svg viewBox="0 0 24 24"><circle cx="12" cy="8" r="4"/><path d="M4 20c0-4 3.6-7 8-7s8 3 8 7"/></svg>',
  bell:'<svg viewBox="0 0 24 24"><path d="M18 8A6 6 0 006 8c0 7-3 9-3 9h18s-3-2-3-9M13.73 21a2 2 0 01-3.46 0"/></svg>',
  pin:'<svg viewBox="0 0 24 24"><path d="M21 10c0 7-9 13-9 13S3 17 3 10a9 9 0 0118 0z"/><circle cx="12" cy="10" r="3"/></svg>',
  users:'<svg viewBox="0 0 24 24"><path d="M17 21v-2a4 4 0 00-4-4H5a4 4 0 00-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 00-3-3.87M16 3.13a4 4 0 010 7.75"/></svg>',
  clock:'<svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>',
  grid:'<svg viewBox="0 0 24 24"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/></svg>',
  sun:'<svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="5"/><line x1="12" y1="1" x2="12" y2="3"/><line x1="12" y1="21" x2="12" y2="23"/><line x1="4.22" y1="4.22" x2="5.64" y2="5.64"/><line x1="18.36" y1="18.36" x2="19.78" y2="19.78"/><line x1="1" y1="12" x2="3" y2="12"/><line x1="21" y1="12" x2="23" y2="12"/><line x1="4.22" y1="19.78" x2="5.64" y2="18.36"/><line x1="18.36" y1="5.64" x2="19.78" y2="4.22"/></svg>',
  heart:'<svg viewBox="0 0 24 24"><path d="M20.84 4.61a5.5 5.5 0 00-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 00-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 000-7.78z"/></svg>',
  reply:'<svg viewBox="0 0 24 24"><path d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2z"/></svg>',
  share:'<svg viewBox="0 0 24 24"><circle cx="18" cy="5" r="3"/><circle cx="6" cy="12" r="3"/><circle cx="18" cy="19" r="3"/><line x1="8.59" y1="13.51" x2="15.42" y2="17.49"/><line x1="15.41" y1="6.51" x2="8.59" y2="10.49"/></svg>',
  chev:'<svg viewBox="0 0 24 24"><path d="M9 18l6-6-6-6"/></svg>',
  back:'<svg viewBox="0 0 24 24"><path d="M19 12H5M12 5l-7 7 7 7"/></svg>',
  send:'<svg viewBox="0 0 24 24"><line x1="22" y1="2" x2="11" y2="13"/><polygon points="22 2 15 22 11 13 2 9 22 2"/></svg>',
  settings:'<svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 00.33 1.82l.06.06a2 2 0 010 2.83 2 2 0 01-2.83 0l-.06-.06a1.65 1.65 0 00-1.82-.33 1.65 1.65 0 00-1 1.51V21a2 2 0 01-4 0v-.09A1.65 1.65 0 009 19.4a1.65 1.65 0 00-1.82.33l-.06.06a2 2 0 01-2.83-2.83l.06-.06A1.65 1.65 0 004.68 15a1.65 1.65 0 00-1.51-1H3a2 2 0 010-4h.09A1.65 1.65 0 004.6 9a1.65 1.65 0 00-.33-1.82l-.06-.06a2 2 0 012.83-2.83l.06.06A1.65 1.65 0 009 4.68a1.65 1.65 0 001-1.51V3a2 2 0 014 0v.09a1.65 1.65 0 001 1.51 1.65 1.65 0 001.82-.33l.06-.06a2 2 0 012.83 2.83l-.06.06A1.65 1.65 0 0019.4 9a1.65 1.65 0 001.51 1H21a2 2 0 010 4h-.09a1.65 1.65 0 00-1.51 1z"/></svg>',
  smile:'<svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><path d="M8 13s1.5 2 4 2 4-2 4-2M9 9h.01M15 9h.01"/></svg>',
  bar:'<svg viewBox="0 0 24 24"><line x1="18" y1="20" x2="18" y2="10"/><line x1="12" y1="20" x2="12" y2="4"/><line x1="6" y1="20" x2="6" y2="14"/><line x1="2" y1="20" x2="22" y2="20"/></svg>',
  vol:'<svg viewBox="0 0 24 24"><polygon points="11 5 6 9 2 9 2 15 6 15 11 19 11 5"/><path d="M19.07 4.93a10 10 0 010 14.14M15.54 8.46a5 5 0 010 7.07"/></svg>',
  logout:'<svg viewBox="0 0 24 24"><path d="M9 21H5a2 2 0 01-2-2V5a2 2 0 012-2h4M16 17l5-5-5-5M21 12H9"/></svg>',
  award:'<svg viewBox="0 0 24 24"><circle cx="12" cy="8" r="6"/><path d="M15.477 12.89L17 22l-5-3-5 3 1.523-9.11"/></svg>',
  edit:'<svg viewBox="0 0 24 24"><path d="M11 4H4a2 2 0 00-2 2v14a2 2 0 002 2h14a2 2 0 002-2v-7M18.5 2.5a2.121 2.121 0 013 3L12 15l-4 1 1-4 9.5-9.5z"/></svg>',
  shield:'<svg viewBox="0 0 24 24"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>',
  info:'<svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><line x1="12" y1="8" x2="12" y2="12"/><line x1="12" y1="16" x2="12.01" y2="16"/></svg>',
  plus:'<svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><line x1="12" y1="8" x2="12" y2="16"/><line x1="8" y1="12" x2="16" y2="12"/></svg>',
};
function ico(name,w,h,extra){
  w=w||20;h=h||20;
  const s=I[name]||'';
  return s.replace('<svg ','<svg width="'+w+'" height="'+h+'" style="'+( extra||'')+'stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round;fill:none;stroke:currentColor;" ');
}
</script>

<!-- ══ AUTH ══ -->
<div id="s-auth" class="screen active">
  <div class="auth">
    <svg class="auth-ball" viewBox="0 0 100 100"><use href="#ball"/></svg>
    <h1>Wildcard</h1>
    <p class="auth-sub">Helsinki Tennis Community · 2026</p>
    <div class="fld"><label>First name</label><input id="fn" type="text" value="Mikael" autocomplete="given-name"></div>
    <div class="fld"><label>Last name</label><input id="ln" type="text" value="Järvinen" autocomplete="family-name"></div>
    <button class="btn btn-p" onclick="doLogin()">Enter the club</button>
    <p style="text-align:center;font-size:12px;color:var(--t3);font-style:italic;margin-top:2px">New members always welcome</p>
  </div>
</div>

<!-- ══ HOME ══ -->
<div id="s-home" class="screen">
  <div class="scr-content">
    <div class="hero">
      <svg class="hero-ball" viewBox="0 0 100 100"><use href="#ball"/></svg>
      <div>
        <div class="hero-ey">Welcome back</div>
        <div class="hero-nm" id="heroName">Mikael Järvinen</div>
        <div class="hero-sub">Helsinki Tennis Community</div>
        <div class="hero-rank"><span id="h-ri">🎾</span><span id="h-rt">Club Player · Lvl 3</span></div>
      </div>
    </div>
    <div class="affirm" id="affirmBox">
      <span class="affirm-em" id="affE">💪</span>
      <div class="affirm-tx" id="affT">"Your backhand has more in common with modern art than tennis — but hey, Picasso wasn't built in a day."</div>
    </div>
    <div class="qgrid" id="qgrid"></div>
    <div class="slbl">Next on court</div>
    <div class="tc" onclick="goTab('tournaments')" style="cursor:pointer">
      <div class="tc-hd"><h3>Tali Open — Sunday Tournament</h3><p>Sun 10 May 2026 · 12:00–15:00</p></div>
      <div class="tc-body">
        <div class="t-meta">
          <div class="t-mi" id="h-pin"></div>
          <div class="t-mi"><span id="h-cnt">8</span>/16 signed up</div>
        </div>
        <span class="badge bb">Open for sign-up</span>
      </div>
    </div>
    <div class="slbl">Today's conditions</div>
    <div class="card"><div class="ci" style="display:flex;align-items:center;gap:14px">
      <span style="font-size:34px" id="weatherIco">☀️</span>
      <div><div style="font-size:17px;font-weight:700">18°C · Sunny</div><div style="font-size:13px;color:var(--t3)">Excellent for outdoor courts</div></div>
    </div></div>
    <div class="slbl">Your ranking</div>
    <div class="rcard">
      <div class="rtitle">Club ranking — private</div>
      <div class="rdisplay">
        <div class="rbadge"><span class="rn" id="h-rn">3</span><span class="rl">Level</span></div>
        <div class="rinfo"><h4 id="h-rnm">Club Player</h4><p id="h-rd">Reliable serve, good rallying, growing tactical awareness.</p><div class="rsk" id="h-rsk"></div></div>
      </div>
      <div class="rbar-track"><div class="rbar-fill" id="h-rb" style="width:38%"></div></div>
      <div class="rbar-lbls"><span>🎾 Beginner</span><span id="h-rl">Level 3 of 7</span><span>Sinner 🏆</span></div>
    </div>
  </div>
  <nav class="bnav" id="nav-home"></nav>
</div>

<!-- ══ TOURNAMENTS ══ -->
<div id="s-tournaments" class="screen">
  <div class="rrbn hidden" id="rr-t"><span id="rr-t-ico"></span><span>Your ranking: <strong id="rr-t-tx"></strong></span></div>
  <div class="bar"><span class="bar-title">Tournaments</span><button class="btn-sm btn-bsm" onclick="showOvl('new-tourn')">+ New</button></div>
  <div class="scr-content">
    <div class="tabs">
      <button class="tab on" id="tt-list" onclick="tTab('list')">Tournaments</button>
      <button class="tab" id="tt-draw" onclick="tTab('draw')">Draw</button>
      <button class="tab" id="tt-sched" onclick="tTab('sched')">Schedule</button>
    </div>
    <div id="tc-list">
      <div class="tc">
        <div class="tc-hd"><h3>Tali Open — Sunday Tournament</h3><p>Sun 10 May 2026 · 12:00–15:00</p></div>
        <div class="tc-body">
          <div class="t-meta">
            <div class="t-mi" id="t-pin"></div>
            <div class="t-mi" id="t-users"></div>
          </div>
          <div style="display:flex;gap:6px;flex-wrap:wrap;margin-bottom:10px"><span class="badge bb">Open sign-up</span><span class="badge bs">Group + KO</span></div>
          <div id="signedList" style="font-size:12px;color:var(--t3);margin-bottom:10px;line-height:1.65">Signed up: Anna K, Mikko L, Sara H, Johan B, Pekka V, Emma R, Lauri N, Tiina M</div>
          <button class="btn btn-p" id="signupBtn" onclick="doSignup()" style="margin-bottom:8px">Sign up for this tournament</button>
          <button class="btn btn-o" onclick="showOvl('invite')">Invite a player</button>
        </div>
      </div>
      <div class="slbl">Format guide</div>
      <div class="card"><div class="ci" style="font-size:12px;color:var(--t3);line-height:1.85">
        12 players → 4×3 groups → 24 matches · ~9 h<br>
        13 players → 3×3 + 1×4 groups → 30 matches · ~11.5 h<br>
        14–15 players → mixed groups → 33 matches · ~12.5 h<br>
        16 players → 4×4 groups → 40 matches · ~15 h<br>
        <span style="color:var(--bm);font-weight:600;font-style:italic">Avg match: 20–25 min · 4–5 games per player</span>
      </div></div>
    </div>
    <div id="tc-draw" class="hidden">
      <div class="slbl">Group stage</div>
      <div class="gbox"><div class="ghd"><h4>Group A</h4><span class="badge bb">3 players</span></div>
        <div class="mrow"><span class="mpl">Anna Korhonen</span><span class="mvs">v</span><span class="mpl" style="text-align:right">Mikko Laine</span><span class="mtime">12:00</span></div>
        <div class="mrow"><span class="mpl">Anna Korhonen</span><span class="mvs">v</span><span class="mpl" style="text-align:right">Sara Häkinen</span><span class="mtime">12:25</span></div>
        <div class="mrow"><span class="mpl">Mikko Laine</span><span class="mvs">v</span><span class="mpl" style="text-align:right">Sara Häkinen</span><span class="mtime">12:50</span></div>
      </div>
      <div class="gbox"><div class="ghd"><h4>Group B</h4><span class="badge bb">3 players</span></div>
        <div class="mrow"><span class="mpl">Johan Berg</span><span class="mvs">v</span><span class="mpl" style="text-align:right">Pekka Virtanen</span><span class="mtime">12:00</span></div>
        <div class="mrow"><span class="mpl">Johan Berg</span><span class="mvs">v</span><span class="mpl" style="text-align:right">Emma Räsänen</span><span class="mtime">12:25</span></div>
        <div class="mrow"><span class="mpl">Pekka Virtanen</span><span class="mvs">v</span><span class="mpl" style="text-align:right">Emma Räsänen</span><span class="mtime">12:50</span></div>
      </div>
      <div class="slbl">Knockout</div>
      <div class="bwrap"><div class="bracket">
        <div class="bcol"><div class="blbl">QF</div>
          <div class="mbox"><div class="bp2 bw2">A1 <span class="bsc">6–3</span></div><div class="bp2">B2 <span class="bsc">3–6</span></div></div>
          <div class="mbox" style="margin-top:7px"><div class="bp2 bw2">B1 <span class="bsc">6–4</span></div><div class="bp2">A2 <span class="bsc">4–6</span></div></div>
        </div>
        <div class="bcol"><div class="blbl">SF</div><div class="mbox" style="margin-top:32px"><div class="bp2">A1</div><div class="bp2">B1</div></div></div>
        <div class="bcol"><div class="blbl">Final</div><div class="mbox" style="margin-top:56px"><div class="bp2">SF1</div><div class="bp2">SF2</div></div></div>
      </div></div>
    </div>
    <div id="tc-sched" class="hidden">
      <div class="slbl">Schedule · Tali · 10 May 2026</div>
      <div id="schedList"></div>
    </div>
  </div>
  <nav class="bnav" id="nav-tournaments"></nav>
</div>

<!-- ══ COURTS ══ -->
<div id="s-courts" class="screen">
  <div class="rrbn hidden" id="rr-c"><span id="rr-c-ico"></span><span>Your ranking: <strong id="rr-c-tx"></strong></span></div>
  <div class="bar"><span class="bar-title">Helsinki Courts</span></div>
  <div class="scr-content">
    <div class="seg-wrap">
      <button class="seg on" onclick="filterCourts('all',this)">All</button>
      <button class="seg" onclick="filterCourts('indoor',this)">Indoor</button>
      <button class="seg" onclick="filterCourts('outdoor',this)">Outdoor</button>
    </div>
    <p style="font-size:11px;color:var(--t3);padding:8px 16px 0;font-style:italic">Outdoor season open · City courts €8/h via varaamo.hel.fi · Free walk-on if empty</p>
    <div id="courtsList" style="margin-top:4px"></div>
  </div>
  <nav class="bnav" id="nav-courts"></nav>
</div>

<!-- ══ FEED ══ -->
<div id="s-feed" class="screen">
  <div class="rrbn hidden" id="rr-f"><span id="rr-f-ico"></span><span>Your ranking: <strong id="rr-f-tx"></strong></span></div>
  <div class="bar"><span class="bar-title">From the courts</span><button class="btn-sm btn-bsm" onclick="showOvl('add-photo')">+ Share</button></div>
  <div class="scr-content" id="feedContent"></div>
  <nav class="bnav" id="nav-feed"></nav>
</div>

<!-- ══ MESSAGES ══ -->
<div id="s-messages" class="screen">
  <div class="rrbn hidden" id="rr-m"><span id="rr-m-ico"></span><span>Your ranking: <strong id="rr-m-tx"></strong></span></div>
  <div class="bar">
    <span class="bar-title">Messages</span>
    <button class="bar-icon" id="bellBtn" onclick="showOvl('notifs')"></button>
    <button class="btn-sm btn-osm" onclick="showOvl('new-chat')">+ New</button>
  </div>
  <div class="scr-content"><div id="chatList"></div></div>
  <nav class="bnav" id="nav-messages"></nav>
</div>

<!-- ══ CHAT WINDOW ══ -->
<div id="s-chat" class="chat-scr">
  <div class="bar">
    <button class="bar-back" id="chatBack"></button>
    <span class="bar-title" id="chatTitle" style="font-size:15px">Chat</span>
    <span class="badge bb" id="chatBadge" style="font-size:10px"></span>
  </div>
  <div class="msgs" id="msgList"></div>
  <div class="msgbar">
    <input type="text" id="msgInput" placeholder="Write a message…" onkeydown="if(event.key==='Enter')sendMsg()">
    <button class="sndbtn" onclick="sendMsg()" id="sendBtn"></button>
  </div>
</div>

<!-- ══ PROFILE ══ -->
<div id="s-profile" class="screen">
  <div class="scr-content">
    <div class="phero">
      <svg class="pball" viewBox="0 0 100 100"><use href="#ball"/></svg>
      <div>
        <div class="p-nm" id="pName">Mikael Järvinen</div>
        <div class="p-sub">Member since May 2026</div>
        <div class="hero-rank" style="margin-top:7px"><span id="p-ri">🎾</span><span id="p-rt">Club Player · Lvl 3</span></div>
      </div>
    </div>
    <div class="stats">
      <div class="stat"><div class="stat-n">3</div><div class="stat-l">Tournaments</div></div>
      <div class="stat"><div class="stat-n">12</div><div class="stat-l">Matches</div></div>
      <div class="stat"><div class="stat-n">7–5</div><div class="stat-l">W–L</div></div>
      <div class="stat"><div class="stat-n" id="connCount">4</div><div class="stat-l">Connections</div></div>
    </div>
    <div class="slbl">My ranking</div>
    <div class="rcard">
      <div class="rtitle">Club ranking — private to you</div>
      <div class="rdisplay">
        <div class="rbadge"><span class="rn" id="p-rn">3</span><span class="rl">Level</span></div>
        <div class="rinfo"><h4 id="p-rnm">Club Player</h4><p id="p-rd">Consistent rallying, reliable serve, growing match experience.</p><div class="rsk" id="p-rsk"></div></div>
      </div>
      <div class="rbar-track"><div class="rbar-fill" id="p-rb" style="width:38%"></div></div>
      <div class="rbar-lbls"><span>🎾 Beginner</span><span id="p-rl">Level 3 of 7</span><span>Sinner 🏆</span></div>
    </div>
    <div class="slbl">All ranking levels</div>
    <div class="rlvls" id="rankLevels"></div>
    <div class="slbl">Connections</div>
    <div class="card" style="margin-top:0;padding:0;overflow:hidden" id="connList"></div>
    <div style="padding:10px 16px 4px"><button class="btn btn-o" onclick="showOvl('add-conn')">Add connection</button></div>
    <div class="slbl">Account</div>
    <div class="card" style="margin-top:0;padding:0;overflow:hidden" id="profileMenu"></div>
    <div style="height:20px"></div>
  </div>
  <nav class="bnav" id="nav-profile"></nav>
</div>

<!-- ══ OVERLAY ══ -->
<div id="ovlWrap" class="ovl hidden" onclick="closeOvlOutside(event)">
  <div class="ovl-panel"><div class="ovl-handle"></div><div id="ovlContent"></div></div>
</div>

<script>
// ── DATA ──────────────────────────────────────────────────────────────────
const RANKS=[
  {level:1,icon:'🎾',name:'Beginner',pct:7,
   desc:'Just picking up the game. Focus is on making contact consistently, learning the basic grip, and understanding scoring. Rallies are short and inconsistent. No competitive play yet — this level is about exploration and building confidence on court.',
   skills:'Basic grip · Short rallies · Court awareness · Serve introduction'},
  {level:2,icon:'🌱',name:'Improver',pct:21,
   desc:'Can sustain rallies of 5–10 shots and has a recognisable forehand and serve. Starting to understand court positioning and basic tactics. Plays socially and participates in beginner leagues. Unforced errors are frequent but footwork is developing.',
   skills:'Consistent forehand · Basic backhand · Serve in play · Social match play'},
  {level:3,icon:'⚡',name:'Club Player',pct:38,
   desc:'A reliable club-level competitor. Both forehand and backhand work under moderate pressure. Serves land consistently. Understands basic tactics — cross-court vs down-the-line, approaching the net. Competes in club tournaments and wins matches against similar players.',
   skills:'Topspin forehand · Slice backhand · Net play · Club tournament experience'},
  {level:4,icon:'🎯',name:'Competitive',pct:54,
   desc:'A serious club competitor who wins regularly at local level. Uses spin, pace and placement intentionally. Can construct points — setting up short balls, building with the backhand, finishing at the net. First serve percentage is solid. Reaches club finals and competes in open regional events.',
   skills:'Consistent topspin · Drop shots · Volley pressure · Physical endurance · Match tactics'},
  {level:5,icon:'🔥',name:'Advanced',pct:69,
   desc:'Plays at tournament level with a clear game style. Groundstrokes are powerful and directional under pressure. Serve is a genuine weapon — varying spin, placement and pace. Can execute the full tactical spectrum: aggressive baseline play, chip-and-charge, pattern construction. Competes at regional and national open events.',
   skills:'Heavy topspin · Kick serve · First-strike tennis · Point construction · Mental resilience'},
  {level:6,icon:'💎',name:'Elite Club',pct:84,
   desc:'District or national-level competitor with near-professional technique. Every shot is executed with consistent depth, spin and intent. Reads the game at a high level — anticipates opponents, exploits patterns and executes under pressure in match tiebreaks. Often coaches or leads club teams. Has competed at ITF or national league level.',
   skills:'Professional mechanics · All-court game · Tactical reading · Coaching ability · National competition'},
  {level:7,icon:'🏆',name:'Sinner',pct:98,
   desc:'The pinnacle. Plays at or near professional standard — national ranking, ATP/WTA/ITF points, or equivalent elite amateur status. Technique is textbook under full pressure. The serve is a multi-dimensional weapon. Groundstrokes are heavy, fast and consistently directional. Mental game is elite: resilient under pressure, adaptive in tactics, able to perform at the highest level. Jannik would nod.',
   skills:'Pro-level serve · Heavy ball · Elite fitness · Tactical IQ · National/international ranking'},
];

const AFFIRMS=[
  {e:'💪',t:'"Your backhand has more in common with modern art than tennis — but hey, Picasso wasn\'t built in a day either."'},
  {e:'🎾',t:'"The ball goes where you believe it goes. Unfortunately, you currently believe it goes into the net."'},
  {e:'😤',t:'"You\'re not double-faulting — you\'re giving the ball two chances to cooperate with your vision."'},
  {e:'🌟',t:'"Every great champion started exactly where you are. Nadal\'s first serve was also a miss. Probably."'},
  {e:'🤔',t:'"Your footwork is not slow — it\'s deliberate, artistic and completely its own aesthetic style."'},
  {e:'🏃',t:'"Running for that ball you clearly won\'t reach is called commitment. Or cardio. Either way, impressive."'},
  {e:'🎯',t:'"A missed return is just a forehand that peaked too early. Like a very enthusiastic firework."'},
  {e:'💡',t:'"Today you will discover that the net is 91.4 cm high. This will be a surprise every single time."'},
  {e:'🦁',t:'"You have the heart of a champion and the serve of someone who just discovered tennis last Thursday."'},
  {e:'😎',t:'"Bad day on court? Even Federer once had a bad day. He just had it in 1997 and never spoke of it again."'},
];

const AVC=['av-b','av-g','av-p','av-s'];
function av(i){return AVC[i%4]}
function ini(n){return n.split(' ').map(w=>w[0]||'').join('').toUpperCase().slice(0,2)}

let USER={first:'Mikael',last:'Järvinen',rankLevel:3};
let SIGNEDUP=false;
let SIGNUP_NAMES=['Anna K','Mikko L','Sara H','Johan B','Pekka V','Emma R','Lauri N','Tiina M'];
let LIKES={};
let CONNS=['Sara Häkinen','Johan Berg','Pekka Virtanen','Anna Korhonen'];
let POSTS=[
  {id:1,author:'Anna Korhonen',time:'2h ago',emoji:'🎾',caption:'Perfect morning at Tali. Indoor courts in great shape — booked next week already.',likes:7},
  {id:2,author:'Johan Berg',time:'5h ago',emoji:'🏆',caption:'Last week\'s final set was one for the ages. Brilliant afternoon at Taivallahti!',likes:14},
  {id:3,author:'Pekka Virtanen',time:'Yesterday',emoji:'☀️',caption:'Herttoniemi outdoor courts open for the 2026 season. Walked on free at 7pm — still daylight!',likes:5},
];
let NOTIFS=[
  {id:1,ico:'🏆',cls:'ni-b',title:'Tournament draw published',body:'Groups for Tali Open 10 May are live — check the Draw tab.',time:'Just now',unread:true},
  {id:2,ico:'🎾',cls:'ni-g',title:'Anna K sent you a message',body:'"Good luck on Sunday — may the best player win!"',time:'1h ago',unread:true},
  {id:3,ico:'📅',cls:'ni-p',title:'Court booking reminder',body:'Tali Court 3 starts in 2 hours — Mon 11 May 18:00.',time:'2h ago',unread:false},
  {id:4,ico:'👥',cls:'ni-b',title:'Pekka Virtanen joined',body:'Pekka signed up for Sunday. 9 players confirmed.',time:'3h ago',unread:false},
  {id:5,ico:'🌟',cls:'ni-p',title:'Ranking updated',body:'You\'re now Level 3 — Club Player. Keep going!',time:'Yesterday',unread:false},
];
let SETTINGS={matchN:true,tournN:true,msgN:true,affirm:true,weekly:false,sound:false};

const COURTS=[
  {name:'Tali Tennis Center',type:'indoor',addr:'Kutomokuja 4, Pitäjänmäki',n:22,out:11,
   open:'07:00–22:00',price:'From €18/h · Members €9/h',surface:'Hard / Clay (outdoor)',
   feat:'Gym · Sauna · Bistro & bar · Pro shop · Padel',note:'Home of HVS-Tennis · ATP Challenger venue',
   free:['07:00','09:00','11:00','15:00','17:00'],taken:['08:00','10:00','12:00','13:00'],maybe:['14:00','16:00'],bg:'#1a2e5a'},
  {name:'Taivallahti Tennis Centre',type:'indoor',addr:'Paavo Nurmen tie 1, Töölö',n:6,out:1,
   open:'06:30–22:00',price:'From €18/h',surface:'Hard indoor / Clay outdoor',
   feat:'Café · Coaching · Pro shop · Padel',note:'Sister club to Tali · HVS-Tennis home base',
   free:['08:00','10:00','14:00','18:00'],taken:['09:00','11:00','13:00'],maybe:['15:00','17:00'],bg:'#1a3a4a'},
  {name:'Smash Center (Finland TC)',type:'indoor',addr:'Alakiventie 2, Myllypuro',n:12,out:2,
   open:'07:00–22:00',price:'From €16/h',surface:'Hard / Clay (outdoor)',
   feat:'12 indoor + 2 clay outdoor · Badminton · Squash · Padel · Gym',note:'Largest tennis facility in Helsinki',
   free:['07:00','09:00','12:00','16:00','20:00'],taken:['08:00','10:00','14:00'],maybe:['11:00','18:00'],bg:'#2a1a4a'},
  {name:'Herttoniemi Sports Park',type:'outdoor',addr:'Kettutie 8, Herttoniemi',n:3,out:3,
   open:'08:00–21:00 (May–Sep)',price:'€8/h via Varaamo · Free walk-on if empty',surface:'Artificial grass',
   feat:'Floodlights · Free walk-on · City of Helsinki',note:'Book at varaamo.hel.fi',
   free:['09:00','11:00','14:00','17:00','19:00'],taken:['10:00','13:00'],maybe:['16:00'],bg:'#1a3a1a'},
  {name:'Lauttasaari Sports Park',type:'outdoor',addr:'Lauttasaarentie 30, Lauttasaari',n:2,out:2,
   open:'08:00–21:00 (May–Sep)',price:'€8/h via Varaamo · Free walk-on if empty',surface:'Plexipave hard',
   feat:'Scenic waterfront · Free walk-on',note:'City of Helsinki · varaamo.hel.fi',
   free:['09:00','12:00','15:00','18:00'],taken:['10:00','11:00'],maybe:['14:00'],bg:'#1a3a2e'},
  {name:'Siltamäki Sports Park',type:'outdoor',addr:'Siltamäentie 16, Siltamäki',n:2,out:2,
   open:'08:00–21:00 (May–Sep)',price:'€8/h via Varaamo · Free walk-on if empty',surface:'Artificial grass',
   feat:'City courts · Free walk-on',note:'City of Helsinki · varaamo.hel.fi',
   free:['08:00','10:00','13:00','16:00'],taken:['09:00','15:00'],maybe:['11:00'],bg:'#2e1a3a'},
];

const SCHED=[
  {t:'12:00',court:'Court 1',p1:'Anna K',p2:'Mikko L',grp:'Group A'},
  {t:'12:00',court:'Court 2',p1:'Johan B',p2:'Pekka V',grp:'Group B'},
  {t:'12:25',court:'Court 1',p1:'Anna K',p2:'Sara H',grp:'Group A'},
  {t:'12:25',court:'Court 2',p1:'Johan B',p2:'Emma R',grp:'Group B'},
  {t:'12:50',court:'Court 1',p1:'Mikko L',p2:'Sara H',grp:'Group A'},
  {t:'12:50',court:'Court 2',p1:'Pekka V',p2:'Emma R',grp:'Group B'},
  {t:'13:20',court:'Court 1',p1:'A1',p2:'B2',grp:'Quarter-final'},
  {t:'13:20',court:'Court 2',p1:'B1',p2:'A2',grp:'Quarter-final'},
  {t:'13:50',court:'Court 1',p1:'SF1 winner',p2:'SF2 winner',grp:'Semi-final'},
  {t:'14:30',court:'Court 1',p1:'Finalist A',p2:'Finalist B',grp:'🏆 Final'},
];

const CHAT_SECTIONS=[
  {label:'Tournament chats',items:[
    {name:'Tali Open Group Chat',type:'tournament',prev:'Johan: See you all Sunday!',time:'10:42',unread:true,ico:'🏆'},
    {name:'Draw & Schedule',type:'tournament',prev:'Groups posted — check Draw tab',time:'09:30',unread:false,ico:'📋'},
  ]},
  {label:'Match chats',items:[
    {name:'My match vs Anna K.',type:'match',prev:'Anna: Good luck on Sunday!',time:'Yesterday',unread:true,ico:'🎾'},
    {name:'Practice — Tali Court 3',type:'match',prev:'Confirmed: Monday 18:00',time:'Mon',unread:false,ico:'📅'},
  ]},
  {label:'Connections',items:[
    {name:'Anna Korhonen',type:'connection',prev:'Thanks for the practice match!',time:'09:15',unread:false,ico:'👤'},
    {name:'Pekka Virtanen',type:'connection',prev:'Are you joining Sunday?',time:'Yesterday',unread:true,ico:'👤'},
  ]},
];

const CHAT_MSGS={
  'Tali Open Group Chat':[
    {out:false,from:'Anna K',text:'Hi everyone, so excited for Sunday!',time:'10:30'},
    {out:false,from:'Mikko L',text:'Been practising all week.',time:'10:35'},
    {out:true,from:'You',text:'Cannot wait. See you at noon.',time:'10:38'},
    {out:false,from:'Johan B',text:'See you all Sunday!',time:'10:42'},
  ],
  'Draw & Schedule':[
    {out:false,from:'Organiser',text:'Groups confirmed. Check the Draw tab.',time:'09:28'},
    {out:true,from:'You',text:'Group A looks tough. Good luck all.',time:'09:31'},
  ],
  'My match vs Anna K.':[
    {out:false,from:'Anna K',text:'Looking forward to our match!',time:'Yesterday'},
    {out:true,from:'You',text:'May the better player win!',time:'Yesterday'},
  ],
  'Practice — Tali Court 3':[{out:false,from:'Tali',text:'Confirmed: Court 3, Mon 18:00–19:00.',time:'Mon'}],
  'Anna Korhonen':[
    {out:false,from:'Anna',text:'Great match yesterday!',time:'09:10'},
    {out:true,from:'You',text:'Your serves were exceptional.',time:'09:12'},
    {out:false,from:'Anna',text:'Thanks for the practice match!',time:'09:15'},
  ],
  'Pekka Virtanen':[{out:false,from:'Pekka',text:'Are you joining Sunday?',time:'Yesterday'}],
};

// ── NAV BUILDER ──────────────────────────────────────────────────────────────
const TABS=[
  {id:'home',    label:'Home',    icon:'home'},
  {id:'tournaments', label:'Compete', icon:'trophy'},
  {id:'courts',  label:'Courts',  icon:'court'},
  {id:'feed',    label:'Feed',    icon:'feed'},
  {id:'messages',label:'Chat',   icon:'chat'},
  {id:'profile', label:'Me',     icon:'user'},
];

function buildNavs(){
  TABS.forEach(tab=>{
    const navEl=document.getElementById('nav-'+tab.id);
    if(!navEl)return;
    navEl.innerHTML=TABS.map(t=>`
      <button class="ni${t.id===tab.id?' on':''}" onclick="goTab('${t.id}')">
        ${ico(t.icon,22,22)}
        <span>${t.label}</span>
      </button>`).join('');
  });
}

// ── AUTH ─────────────────────────────────────────────────────────────────────
function doLogin(){
  const f=document.getElementById('fn').value.trim();
  const l=document.getElementById('ln').value.trim();
  if(!f||!l){alert('Please enter your full name.');return}
  USER={first:f,last:l,rankLevel:3};
  document.getElementById('heroName').textContent=f+' '+l;
  document.getElementById('pName').textContent=f+' '+l;
  document.getElementById('s-auth').classList.remove('active');
  document.getElementById('s-home').classList.add('active');
  initApp();
}

function doLogout(){
  TABS.forEach(t=>document.getElementById('s-'+t.id).classList.remove('active'));
  document.getElementById('s-auth').classList.add('active');
}

// ── INIT ─────────────────────────────────────────────────────────────────────
function initApp(){
  buildNavs();
  updateRank();
  updateNotifBadge();
  rotateAffirm();
  buildHomeIcons();
  buildTournIcons();
  renderCourts('all');
  renderFeed();
  renderChatList();
  renderConns();
  renderSched();
  renderRankLevels();
  buildProfileMenu();
  buildSendBtn();
  buildChatBack();
}

function buildHomeIcons(){
  // Quick grid
  document.getElementById('qgrid').innerHTML=[
    {tab:'tournaments',ico:'trophy',lbl:'Tournaments'},
    {tab:'courts',ico:'court',lbl:'Find Courts'},
    {tab:'feed',ico:'feed',lbl:'Photos'},
    {tab:'messages',ico:'chat',lbl:'Messages'},
  ].map(q=>`<div class="qcard" onclick="goTab('${q.tab}')"><span>${ico(q.ico,26,26,'display:block;margin:0 auto 8px;stroke:var(--bm);')}</span><span>${q.lbl}</span></div>`).join('');
  // Home pin meta
  document.getElementById('h-pin').innerHTML=ico('pin',14,14,'vertical-align:-1px;stroke:var(--bm);')+'Tali Tennis Center';
}

function buildTournIcons(){
  document.getElementById('t-pin').innerHTML=ico('pin',14,14,'vertical-align:-1px;stroke:var(--bm);')+'Tali Tennis Center';
  document.getElementById('t-users').innerHTML=ico('users',14,14,'vertical-align:-1px;stroke:var(--bm);')+'<span id="signupCount">8</span>/16';
  document.getElementById('h-cnt').textContent=SIGNUP_NAMES.length;
}

function buildSendBtn(){
  const btn=document.getElementById('sendBtn');
  btn.innerHTML=ico('send',16,16,'stroke:#fff;');
}
function buildChatBack(){
  const btn=document.getElementById('chatBack');
  btn.innerHTML=ico('back',20,20,'stroke:var(--bm);');
}

// ── TABS ─────────────────────────────────────────────────────────────────────
function goTab(id){
  TABS.forEach(t=>{
    document.getElementById('s-'+t.id).classList.toggle('active',t.id===id);
  });
}

function tTab(t){
  ['list','draw','sched'].forEach(s=>{
    document.getElementById('tc-'+s).classList.toggle('hidden',s!==t);
    document.getElementById('tt-'+s).classList.toggle('on',s===t);
  });
}

// ── RANK ─────────────────────────────────────────────────────────────────────
function rankInfo(){return RANKS.find(r=>r.level===USER.rankLevel)||RANKS[2]}

function updateRank(){
  const r=rankInfo();
  const txt=r.name+' · Lvl '+r.level;
  [['h-ri','h-rt'],['p-ri','p-rt']].forEach(([ei,ti])=>{
    const e=document.getElementById(ei),t=document.getElementById(ti);
    if(e)e.textContent=r.icon;if(t)t.textContent=txt;
  });
  // Ribbons
  ['t','c','f','m'].forEach(k=>{
    const rr=document.getElementById('rr-'+k);
    const ri=document.getElementById('rr-'+k+'-ico');
    const rt=document.getElementById('rr-'+k+'-tx');
    if(rr){rr.classList.remove('hidden')}
    if(ri){ri.innerHTML=ico('award',14,14,'stroke:var(--pm);vertical-align:-2px;');ri.textContent=r.icon}
    if(rt)rt.textContent=r.name+' · Level '+r.level;
  });
  // Home rank card
  set('h-rn',r.level);set('h-rnm',r.name);set('h-rd',r.desc);set('h-rsk',r.skills);
  const hb=document.getElementById('h-rb');if(hb)hb.style.width=r.pct+'%';
  set('h-rl','Level '+r.level+' of 7');
  // Profile rank card
  set('p-rn',r.level);set('p-rnm',r.name);set('p-rd',r.desc);set('p-rsk',r.skills);
  const pb=document.getElementById('p-rb');if(pb)pb.style.width=r.pct+'%';
  set('p-rl','Level '+r.level+' of 7');
  renderRankLevels();
}

function set(id,v){const e=document.getElementById(id);if(e)e.textContent=v}

function renderRankLevels(){
  const r=rankInfo();
  document.getElementById('rankLevels').innerHTML=RANKS.map(lvl=>`
    <div class="rlv${lvl.level===r.level?' rlv-mine':''}">
      <div class="rlv-ico">${lvl.icon}</div>
      <div style="flex:1">
        <div class="rlv-nm">${lvl.name}${lvl.level===r.level?' <span style="font-size:10px;color:var(--pm);font-style:italic">← you</span>':''}</div>
        <div class="rlv-desc">${lvl.desc}</div>
        <div class="rlv-sk">${lvl.skills}</div>
      </div>
    </div>`).join('');
}

// ── AFFIRMATION ───────────────────────────────────────────────────────────────
function rotateAffirm(){
  const a=AFFIRMS[Math.floor(Math.random()*AFFIRMS.length)];
  const e=document.getElementById('affE'),t=document.getElementById('affT');
  if(e)e.textContent=a.e;if(t)t.textContent=a.t;
}

// ── NOTIFICATIONS ─────────────────────────────────────────────────────────────
function updateNotifBadge(){
  const u=NOTIFS.filter(n=>n.unread).length;
  const btn=document.getElementById('bellBtn');
  if(!btn)return;
  btn.innerHTML=ico('bell',22,22,'stroke:var(--t3);')+(u>0?'<span class="ndot"></span>':'');
  // Profile badge
  const profMenu=document.getElementById('profileMenu');
  if(profMenu)buildProfileMenu();
}

// ── TOURNAMENT ────────────────────────────────────────────────────────────────
function doSignup(){
  if(SIGNEDUP){alert('You are already signed up!');return}
  SIGNEDUP=true;
  const nm=USER.first+' '+USER.last[0]+'.';
  SIGNUP_NAMES.push(nm);
  const cnt=SIGNUP_NAMES.length;
  set('signupCount',cnt);set('h-cnt',cnt);
  document.getElementById('signedList').textContent='Signed up: '+SIGNUP_NAMES.join(', ');
  const btn=document.getElementById('signupBtn');
  btn.textContent='✓ You\'re in!';btn.style.background='#888';btn.disabled=true;
  NOTIFS.unshift({id:Date.now(),ico:'🎾',cls:'ni-g',title:'You joined Tali Open!',
    body:'Signed up for Sun 10 May. Draw posted Saturday.',time:'Just now',unread:true});
  updateNotifBadge();
}

// ── COURTS ────────────────────────────────────────────────────────────────────
function renderCourts(filter){
  const arr=filter==='all'?COURTS:COURTS.filter(c=>c.type===filter);
  document.getElementById('courtsList').innerHTML=arr.map(c=>`
    <div class="crt">
      <div class="crt-banner" style="background:${c.bg}">
        <span class="crt-nm">${c.name}</span>
        <div style="position:absolute;top:9px;right:11px"><span class="badge${c.type==='indoor'?' bb':' bg'}">${c.type}</span></div>
      </div>
      <div class="crt-info">
        <div class="crt-meta"><svg width="13" height="13" viewBox="0 0 24 24" stroke="var(--t3)" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 10c0 7-9 13-9 13S3 17 3 10a9 9 0 0118 0z"/><circle cx="12" cy="10" r="3"/></svg>${c.addr}</div>
        <div class="crt-meta">
          <span><svg width="13" height="13" viewBox="0 0 24 24" stroke="var(--t3)" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/></svg>${c.n} indoor${c.out?' · '+c.out+' outdoor':''}</span>
          <span><svg width="13" height="13" viewBox="0 0 24 24" stroke="var(--t3)" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>${c.open}</span>
        </div>
        <div class="crt-price">${c.price}</div>
        <div class="crt-note">${c.note} · ${c.feat}</div>
        <div class="slots-hd">Today's availability</div>
        <div class="slots">
          ${c.taken.map(s=>`<span class="ts ts-t">${s}</span>`).join('')}
          ${c.maybe.map(s=>`<span class="ts ts-m">${s}?</span>`).join('')}
          ${c.free.map(s=>`<span class="ts ts-f">${s} ✓</span>`).join('')}
        </div>
        <button class="crt-btn" onclick="alert('Opening Varaamo for ${c.name.replace(/'/g,"\\'")}…\\n\\nCity courts: varaamo.hel.fi\\nPrivate: check club website')">Book this court →</button>
      </div>
    </div>`).join('');
}

function filterCourts(filter,btn){
  document.querySelectorAll('.seg').forEach(b=>b.classList.remove('on'));
  btn.classList.add('on');
  renderCourts(filter);
}

// ── FEED ─────────────────────────────────────────────────────────────────────
function renderFeed(){
  document.getElementById('feedContent').innerHTML=POSTS.map(p=>`
    <div class="pcard">
      <div class="phdr">
        <div class="av ${av(p.id)}">${ini(p.author)}</div>
        <div><div style="font-size:14px;font-weight:600">${p.author}</div><div style="font-size:11px;color:var(--t3)">${p.time}</div></div>
      </div>
      <div class="pimg"><span>${p.emoji}</span><span style="font-size:11px;color:var(--t3)">Photo</span></div>
      <div class="pbody">${p.caption}</div>
      <div class="pacts">
        <button class="pact${LIKES[p.id]?' liked':''}" onclick="toggleLike(${p.id},this)">
          <svg width="16" height="16" viewBox="0 0 24 24" stroke="currentColor" fill="${LIKES[p.id]?'currentColor':'none'}" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20.84 4.61a5.5 5.5 0 00-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 00-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 000-7.78z"/></svg>
          <span id="lk${p.id}">${p.likes+(LIKES[p.id]?1:0)}</span>
        </button>
        <button class="pact"><svg width="16" height="16" viewBox="0 0 24 24" stroke="currentColor" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2z"/></svg>Reply</button>
        <button class="pact"><svg width="16" height="16" viewBox="0 0 24 24" stroke="currentColor" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="18" cy="5" r="3"/><circle cx="6" cy="12" r="3"/><circle cx="18" cy="19" r="3"/><line x1="8.59" y1="13.51" x2="15.42" y2="17.49"/><line x1="15.41" y1="6.51" x2="8.59" y2="10.49"/></svg>Share</button>
      </div>
    </div>`).join('');
}

function toggleLike(id,btn){
  LIKES[id]=!LIKES[id];
  const p=POSTS.find(x=>x.id===id);
  set('lk'+id,p.likes+(LIKES[id]?1:0));
  btn.classList.toggle('liked',!!LIKES[id]);
  const svg=btn.querySelector('svg');
  if(svg)svg.setAttribute('fill',LIKES[id]?'currentColor':'none');
}

// ── CHAT LIST ─────────────────────────────────────────────────────────────────
function renderChatList(){
  document.getElementById('chatList').innerHTML=CHAT_SECTIONS.map(sec=>`
    <div class="cshd">${sec.label}</div>
    ${sec.items.map((c,i)=>`
      <div class="crow" onclick="openChat(${JSON.stringify(c.name)},${JSON.stringify(c.type)})">
        <div class="av ${av(i)}" style="font-size:18px">${c.ico}</div>
        <div class="cinfo">
          <div class="cnm">${c.name}</div>
          <div class="cprev">${c.prev}</div>
        </div>
        <div style="display:flex;flex-direction:column;align-items:flex-end;gap:5px">
          <span class="ctm">${c.time}</span>
          ${c.unread?'<div class="udot"></div>':''}
        </div>
      </div>`).join('')}`).join('');
}

function openChat(name,type){
  document.getElementById('s-messages').classList.remove('active');
  document.getElementById('s-chat').classList.add('active');
  set('chatTitle',name);
  document.getElementById('s-chat').dataset.name=name;
  const badge=document.getElementById('chatBadge');
  badge.textContent={tournament:'Tournament',match:'Match',connection:'Connection'}[type]||type;
  badge.className='badge '+(type==='tournament'?'bb':type==='match'?'bg':'bp');
  CHAT_SECTIONS.forEach(s=>s.items.forEach(c=>{if(c.name===name)c.unread=false}));
  renderMsgs(name);
}

function renderMsgs(name){
  const msgs=CHAT_MSGS[name]||[];
  const ml=document.getElementById('msgList');
  ml.innerHTML=msgs.map(m=>`
    <div style="display:flex;flex-direction:column">
      <div class="bbl ${m.out?'bbl-out':'bbl-in'}">${m.text}</div>
      <div class="bbl-meta${m.out?' bbl-r':''}">${m.out?'':m.from+' · '}${m.time}</div>
    </div>`).join('');
  ml.scrollTop=ml.scrollHeight;
}

function sendMsg(){
  const inp=document.getElementById('msgInput'),text=inp.value.trim();
  if(!text)return;
  const name=document.getElementById('s-chat').dataset.name;
  if(!CHAT_MSGS[name])CHAT_MSGS[name]=[];
  const now=new Date();
  CHAT_MSGS[name].push({out:true,from:'You',text,time:now.getHours()+':'+(now.getMinutes()+'').padStart(2,'0')});
  inp.value='';
  renderMsgs(name);
}

function closeChatScreen(){
  document.getElementById('s-chat').classList.remove('active');
  document.getElementById('s-messages').classList.add('active');
  renderChatList();
}

// ── CONNECTIONS ───────────────────────────────────────────────────────────────
function renderConns(){
  document.getElementById('connList').innerHTML=CONNS.map((c,i)=>`
    <div class="con-item">
      <div class="av ${av(i)}">${ini(c)}</div>
      <div style="flex:1"><div style="font-size:14px;font-weight:600">${c}</div><div style="font-size:12px;color:var(--t3)">Helsinki · Tennis player</div></div>
      <button class="btn-sm btn-osm" onclick="openChat(${JSON.stringify(c)},'connection');goTab('messages')">Message</button>
    </div>`).join('');
  set('connCount',CONNS.length);
}

// ── SCHEDULE ──────────────────────────────────────────────────────────────────
function renderSched(){
  document.getElementById('schedList').innerHTML=SCHED.map(s=>`
    <div style="display:flex;align-items:center;gap:11px;background:var(--sur);margin:0 16px 7px;border-radius:var(--rs);border:1px solid var(--bdr);padding:10px 13px">
      <div><div style="font-size:13px;font-weight:700;color:var(--bm)">${s.t}</div><div style="font-size:11px;color:var(--t3);font-weight:500">${s.court}</div></div>
      <div style="flex:1;text-align:center">
        <div style="font-size:13px;font-weight:600">${s.p1} <span style="color:var(--t3)">v</span> ${s.p2}</div>
        <span class="badge ${s.grp.includes('Final')||s.grp.includes('Semi')||s.grp.includes('Quarter')?'bp':'bb'}" style="margin-top:4px">${s.grp}</span>
      </div>
    </div>`).join('');
}

// ── PROFILE MENU ──────────────────────────────────────────────────────────────
function buildProfileMenu(){
  const unread=NOTIFS.filter(n=>n.unread).length;
  document.getElementById('profileMenu').innerHTML=`
    <div class="mnu" onclick="showOvl('notifs')">
      <svg class="mnu-ico" viewBox="0 0 24 24"><path d="M18 8A6 6 0 006 8c0 7-3 9-3 9h18s-3-2-3-9M13.73 21a2 2 0 01-3.46 0"/></svg>
      <span class="mnu-lbl">Notifications</span>
      ${unread>0?'<span class="badge bb" style="font-size:10px;margin-right:6px">'+unread+'</span>':''}
      <svg class="mnu-chev" width="15" height="15" viewBox="0 0 24 24"><path d="M9 18l6-6-6-6"/></svg>
    </div>
    <div class="mnu" onclick="showOvl('settings')">
      <svg class="mnu-ico" viewBox="0 0 24 24"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 00.33 1.82l.06.06a2 2 0 010 2.83 2 2 0 01-2.83 0l-.06-.06a1.65 1.65 0 00-1.82-.33 1.65 1.65 0 00-1 1.51V21a2 2 0 01-4 0v-.09A1.65 1.65 0 009 19.4a1.65 1.65 0 00-1.82.33l-.06.06a2 2 0 01-2.83-2.83l.06-.06A1.65 1.65 0 004.68 15a1.65 1.65 0 00-1.51-1H3a2 2 0 010-4h.09A1.65 1.65 0 004.6 9a1.65 1.65 0 00-.33-1.82l-.06-.06a2 2 0 012.83-2.83l.06.06A1.65 1.65 0 009 4.68a1.65 1.65 0 001-1.51V3a2 2 0 014 0v.09a1.65 1.65 0 001 1.51 1.65 1.65 0 001.82-.33l.06-.06a2 2 0 012.83 2.83l-.06.06A1.65 1.65 0 0019.4 9a1.65 1.65 0 001.51 1H21a2 2 0 010 4h-.09a1.65 1.65 0 00-1.51 1z"/></svg>
      <span class="mnu-lbl">Settings</span>
      <svg class="mnu-chev" width="15" height="15" viewBox="0 0 24 24"><path d="M9 18l6-6-6-6"/></svg>
    </div>
    <div class="mnu" onclick="showOvl('affirms')">
      <svg class="mnu-ico" viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><path d="M8 13s1.5 2 4 2 4-2 4-2M9 9h.01M15 9h.01"/></svg>
      <span class="mnu-lbl">Daily affirmations</span>
      <svg class="mnu-chev" width="15" height="15" viewBox="0 0 24 24"><path d="M9 18l6-6-6-6"/></svg>
    </div>
    <div class="mnu mnu-danger" onclick="doLogout()">
      <svg class="mnu-ico" viewBox="0 0 24 24"><path d="M9 21H5a2 2 0 01-2-2V5a2 2 0 012-2h4M16 17l5-5-5-5M21 12H9"/></svg>
      <span class="mnu-lbl">Sign out</span>
    </div>`;
}

// ── OVERLAY ───────────────────────────────────────────────────────────────────
function showOvl(type){
  const oc=document.getElementById('ovlContent');
  if(type==='new-tourn'){
    oc.innerHTML=`<h3>Create a tournament</h3>
      <div class="fld"><label>Name</label><input type="text" placeholder="Summer Open 2026"></div>
      <div class="fld"><label>Date</label><input type="date" value="2026-05-10"></div>
      <div class="fld"><label>Start time</label><input type="time" value="12:00"></div>
      <div class="fld"><label>End time</label><input type="time" value="15:00"></div>
      <div class="fld"><label>Venue</label><input type="text" value="Tali Tennis Center"></div>
      <div class="fld"><label>Max players</label><select><option>12</option><option>13</option><option>14</option><option>15</option><option selected>16</option></select></div>
      <button class="btn btn-p" onclick="closeOvl()">Create tournament</button>`;
  } else if(type==='invite'){
    oc.innerHTML=`<h3>Invite a player</h3>
      <div class="fld"><label>Search</label><input type="text" placeholder="Player name…"></div>
      ${CONNS.map((c,i)=>`<div class="con-item" style="padding:9px 0;border-bottom:1px solid var(--bdr)"><div class="av ${av(i)}">${ini(c)}</div><div style="flex:1;font-size:14px;font-weight:600">${c}</div><button class="btn-sm btn-bsm">Invite</button></div>`).join('')}`;
  } else if(type==='add-photo'){
    oc.innerHTML=`<h3>Share from the courts</h3>
      <label style="display:flex;height:100px;background:var(--bp);border-radius:var(--r);border:2px dashed var(--bdr2);align-items:center;justify-content:center;margin-bottom:13px;cursor:pointer;flex-direction:column;gap:6px">
        <input type="file" accept="image/*" style="display:none">
        <span style="font-size:28px">📷</span>
        <span style="font-size:12px;color:var(--t3)">Tap to add photo</span>
      </label>
      <div class="fld"><label>Caption</label><textarea placeholder="What happened on court today?" id="newCap"></textarea></div>
      <button class="btn btn-p" onclick="addPost()">Share photo</button>`;
  } else if(type==='add-conn'){
    oc.innerHTML=`<h3>Add a connection</h3>
      <div class="fld"><label>Name</label><input type="text" id="newConnName" placeholder="First and last name"></div>
      <button class="btn btn-p" onclick="addConn()">Add connection</button>`;
  } else if(type==='new-chat'){
    oc.innerHTML=`<h3>New message</h3>
      <div style="font-size:10px;letter-spacing:1px;color:var(--t3);text-transform:uppercase;font-weight:700;margin-bottom:10px">Your connections</div>
      ${CONNS.map((c,i)=>`<div class="con-item" style="padding:10px 0;border-bottom:1px solid var(--bdr);cursor:pointer" onclick="closeOvl();openChat(${JSON.stringify(c)},'connection');goTab('messages')"><div class="av ${av(i)}">${ini(c)}</div><div style="flex:1;font-size:14px;font-weight:600">${c}</div><svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="var(--t3)" stroke-width="2" stroke-linecap="round"><path d="M9 18l6-6-6-6"/></svg></div>`).join('')}`;
  } else if(type==='notifs'){
    NOTIFS.forEach(n=>n.unread=false);
    updateNotifBadge();
    oc.innerHTML=`<h3>Notifications</h3>
      ${NOTIFS.length===0?'<p style="color:var(--t3);font-style:italic;text-align:center;padding:20px 0">No notifications</p>':''}
      ${NOTIFS.map(n=>`<div class="ni-item"><div class="ni-ico ${n.cls}">${n.ico}</div><div style="flex:1"><div class="ni-t">${n.title}</div><div class="ni-b2">${n.body}</div><div class="ni-tm">${n.time}</div></div></div>`).join('')}
      <button class="ni-clr" onclick="NOTIFS=[];closeOvl();updateNotifBadge()">Clear all</button>`;
  } else if(type==='settings'){
    oc.innerHTML=`<h3>Settings</h3>
      <div style="border-radius:var(--r);overflow:hidden;border:1px solid var(--bdr);margin-bottom:12px">
        <div style="font-size:10px;letter-spacing:1px;color:var(--t3);text-transform:uppercase;font-weight:700;padding:9px 14px 7px;background:var(--bp);border-bottom:1px solid var(--bdr)">Notifications</div>
        ${stog('matchN','Match reminders','1h before your match')}
        ${stog('tournN','Tournament updates','Draw, schedule and results')}
        ${stog('msgN','New messages','Push for chat messages')}
      </div>
      <div style="border-radius:var(--r);overflow:hidden;border:1px solid var(--bdr)">
        <div style="font-size:10px;letter-spacing:1px;color:var(--t3);text-transform:uppercase;font-weight:700;padding:9px 14px 7px;background:var(--bp);border-bottom:1px solid var(--bdr)">Experience</div>
        ${stog('affirm','Daily affirmations','Motivational nonsense each morning')}
        ${stog('weekly','Weekly match report','Stats summary every Monday')}
        ${stog('sound','Sound effects','Swoosh on send, pop on like')}
      </div>`;
  } else if(type==='affirms'){
    const a=AFFIRMS[Math.floor(Math.random()*AFFIRMS.length)];
    oc.innerHTML=`<h3>Daily affirmations</h3>
      <p style="font-size:13px;color:var(--t3);margin-bottom:14px;font-style:italic">A fresh one every session. Tap for another.</p>
      <div id="apBox" style="background:linear-gradient(130deg,var(--b),var(--p));border-radius:var(--r);padding:20px;color:#fff;text-align:center;margin-bottom:16px">
        <div style="font-size:36px;margin-bottom:10px" id="apE">${a.e}</div>
        <div style="font-size:14px;line-height:1.6;font-style:italic" id="apT">${a.t}</div>
      </div>
      <button class="btn btn-p" onclick="shuffleAP()">Another one ↻</button>`;
  }
  document.getElementById('ovlWrap').classList.remove('hidden');
}

function stog(key,label,sub){
  return`<div class="strow">
    <div style="flex:1"><div class="strow-nm">${label}</div><div class="strow-sub">${sub}</div></div>
    <label class="toggle"><input type="checkbox" ${SETTINGS[key]?'checked':''} onchange="SETTINGS['${key}']=this.checked"><div class="tog-track"></div></label>
  </div>`;
}

function shuffleAP(){
  const a=AFFIRMS[Math.floor(Math.random()*AFFIRMS.length)];
  const e=document.getElementById('apE'),t=document.getElementById('apT');
  if(e)e.textContent=a.e;if(t)t.textContent=a.t;
}

function addConn(){
  const n=document.getElementById('newConnName').value.trim();
  if(!n)return;CONNS.push(n);closeOvl();renderConns();
}

function addPost(){
  const cap=document.getElementById('newCap').value.trim()||'Fresh from the courts.';
  POSTS.unshift({id:Date.now(),author:USER.first+' '+USER.last,time:'Just now',emoji:'📸',caption:cap,likes:0});
  closeOvl();renderFeed();
}

function closeOvl(){document.getElementById('ovlWrap').classList.add('hidden')}
function closeOvlOutside(e){if(e.target===document.getElementById('ovlWrap'))closeOvl()}

// ── CHAT BACK button inline click ─────────────────────────────────────────────
document.getElementById('chatBack').onclick=closeChatScreen;
</script>
</body>
</html>
