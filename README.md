# kriegswerk.github.io
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<!-- EDIT: title + description -->
<title>Your Name - Creative Director</title>
<meta name="description" content="One sentence about what you do.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Questrial&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#ececea; --ink:#000; --mute:#6c6c6a; --line:#000;
  --pad:clamp(16px,2.4vw,32px);
  font-family:"Questrial",Helvetica,Arial,sans-serif;font-synthesis:none;
}
@media (prefers-color-scheme:dark){:root{--bg:#000;--ink:#ececea;--mute:#8a8a88;--line:#ececea}}
*{box-sizing:border-box;margin:0}
h1,h2,button{font-weight:400}
html{scroll-behavior:smooth}
body{background:var(--bg);color:var(--ink);font-size:16px;line-height:1.5;-webkit-font-smoothing:antialiased}
a{color:inherit;text-decoration:none}
a:focus-visible{outline:2px solid var(--ink);outline-offset:3px}
@media (prefers-reduced-motion:reduce){html{scroll-behavior:auto}*{transition:none!important;animation:none!important}}

/* top bar */
.bar{position:fixed;top:0;left:0;right:0;z-index:10;display:grid;grid-template-columns:1fr auto 1fr;gap:16px;
  padding:calc(var(--pad) + env(safe-area-inset-top,0px)) var(--pad) 12px;mix-blend-mode:difference;color:#fff;font-size:14px;}
.bar span{text-align:center}
.bar a{justify-self:start}
@media(max-width:600px){.bar span{display:none}.bar{grid-template-columns:1fr auto}}

/* hamburger */
.burger{justify-self:end;width:40px;height:40px;margin:-8px -8px 0 0;background:none;border:0;color:inherit;cursor:pointer;position:relative}
.burger i{position:absolute;left:8px;right:8px;height:2px;background:currentColor;transition:transform .3s cubic-bezier(.2,.7,.2,1),top .3s}
.burger i:nth-child(1){top:14px}.burger i:nth-child(2){top:24px}
.burger[aria-expanded="true"] i:nth-child(1){top:19px;transform:rotate(45deg)}
.burger[aria-expanded="true"] i:nth-child(2){top:19px;transform:rotate(-45deg)}
.burger:focus-visible{outline:2px solid currentColor;outline-offset:2px}

/* full-screen menu */
.menu{position:fixed;inset:0;z-index:9;background:var(--bg);display:flex;flex-direction:column;justify-content:flex-end;
  padding:var(--pad);padding-bottom:calc(var(--pad) + env(safe-area-inset-bottom,0px));
  clip-path:inset(0 0 100% 0);visibility:hidden;transition:clip-path .55s cubic-bezier(.7,0,.2,1),visibility 0s .55s}
.menu.open{clip-path:inset(0);visibility:visible;transition:clip-path .55s cubic-bezier(.7,0,.2,1),visibility 0s}
.menu a.big{text-transform:lowercase;letter-spacing:-.025em;font-size:clamp(3rem,11vw,10rem);line-height:.9;display:block}
.menu a.big:hover{color:var(--mute)}
.menu .small{display:flex;gap:8px 28px;flex-wrap:wrap;margin-top:var(--pad);padding-top:12px;border-top:1px solid var(--line);font-size:14px}
body.locked{overflow:hidden}

/* parallax video */
.para{position:relative;height:clamp(420px,85svh,900px);overflow:hidden;background:#8f9a9c}
.para video,.para .fallback{position:absolute;left:0;top:-15%;width:100%;height:130%;object-fit:cover;will-change:transform}
.para .fallback{background:linear-gradient(135deg,#b9bfc0,#6f7a7c)}
.para figcaption{position:absolute;left:var(--pad);bottom:var(--pad);color:#fff;font-size:14px;mix-blend-mode:difference}

/* hero */
.hero{min-height:100svh;display:flex;flex-direction:column;justify-content:flex-end;padding:var(--pad);padding-bottom:calc(var(--pad) + env(safe-area-inset-bottom,0px))}
.hero h1{text-transform:lowercase;letter-spacing:-.025em;
  font-size:clamp(3rem,11vw,13rem);line-height:.92;margin-bottom:var(--pad)}
.hero .meta{display:flex;justify-content:space-between;gap:16px;font-size:14px;border-top:1px solid var(--line);padding-top:12px}
.hero .meta span:last-child{color:var(--mute)}
.hero h1{animation:rise .9s cubic-bezier(.2,.7,.2,1) both}
@keyframes rise{from{transform:translateY(40px);opacity:0}to{transform:none;opacity:1}}

/* work */
section{padding:calc(var(--pad)*2) var(--pad)}
h2{font-size:14px;margin-bottom:var(--pad)}
.work{list-style:none;padding:0;border-top:1px solid var(--line)}
.row{position:relative;border-bottom:1px solid var(--line)}
.row a{display:grid;grid-template-columns:3rem 1fr auto;align-items:baseline;gap:16px;padding:20px 0}
.row .n{color:var(--mute);font-size:14px}
.row .t{text-transform:lowercase;letter-spacing:-.02em;font-size:clamp(2rem,7vw,6.5rem);line-height:1;transition:transform .35s cubic-bezier(.2,.7,.2,1)}
.row .c{font-size:14px;color:var(--mute);text-align:right}
.row:hover .t{transform:translateX(12px)}
/* hover preview follows cursor; swap the colored block for <video> or <img> */
.thumb{position:fixed;left:var(--x,50%);top:var(--y,50%);width:clamp(220px,26vw,380px);aspect-ratio:4/5;
  transform:translate(24px,-50%);pointer-events:none;opacity:0;transition:opacity .2s;z-index:5;overflow:hidden;background:var(--c,#888)}
.thumb video,.thumb img{width:100%;height:100%;object-fit:cover;display:block}
.row:hover .thumb{opacity:1}
@media (hover:none){
  .thumb{position:static;opacity:1;width:100%;aspect-ratio:16/10;transform:none;margin-bottom:20px}
  .row a{padding-bottom:12px}
}
.more{display:inline-block;margin-top:var(--pad);border-bottom:1px solid var(--line)}

/* about */
.about{display:grid;grid-template-columns:minmax(0,5fr) minmax(0,7fr);gap:calc(var(--pad)*2);align-items:start}
.photo{aspect-ratio:3/4;background:#999;overflow:hidden}
.photo img{width:100%;height:100%;object-fit:cover;display:block}
.about p{max-width:60ch;font-size:clamp(1.05rem,1.5vw,1.35rem);line-height:1.45;margin-bottom:1.2em}
.about p:first-of-type{font-size:clamp(1.4rem,2.6vw,2.4rem);line-height:1.15;letter-spacing:-.01em}
@media(max-width:800px){.about{grid-template-columns:1fr}}

/* contact */
footer{padding:calc(var(--pad)*2) var(--pad) calc(var(--pad) + env(safe-area-inset-bottom,0px));border-top:1px solid var(--line)}
.mail{display:block;text-transform:lowercase;letter-spacing:-.025em;
  font-size:clamp(2rem,8.5vw,10rem);line-height:.9;margin:var(--pad) 0 calc(var(--pad)*2);overflow-wrap:anywhere}
.mail:hover{color:var(--mute)}
.links{display:flex;flex-wrap:wrap;gap:8px 28px;}
.links a{border-bottom:1px solid transparent}
.links a:hover{border-color:var(--ink)}
.fine{margin-top:calc(var(--pad)*2);display:flex;justify-content:space-between;font-size:14px;color:var(--mute)}
</style>
</head>
<body>

<!-- EDIT: name / role / cities -->
<header class="bar">
  <a href="#top">your name</a>
  <span>creative director</span>
  <button class="burger" aria-label="Open menu" aria-expanded="false" aria-controls="menu"><i></i><i></i></button>
</header>

<!-- EDIT: menu links -->
<nav class="menu" id="menu" aria-label="Main">
  <a class="big" href="projects.html">work</a>
  <a class="big" href="about.html">about</a>
  <a class="big" href="contact.html">contact</a>
  <div class="small"><a href="#">Instagram</a><a href="#">LinkedIn</a><a href="mailto:you@example.com">you@example.com</a></div>
</nav>

<main id="top">
  <!-- EDIT: headline (keep it short, it renders very large) -->
  <div class="hero">
    <h1>creative direction, brand systems &amp; culture</h1>
    <div class="meta"><span>Your Name</span><span>City, City</span><span>Formerly at Company</span></div>
  </div>

  <!-- EDIT: parallax video. Set the src (mp4/webm) and remove the .fallback div -->
  <figure class="para" aria-label="Showreel">
    <video src="" poster="" autoplay muted loop playsinline></video>
    <div class="fallback"></div>
    <figcaption>Showreel</figcaption>
  </figure>

  <!-- EDIT: projects. Add data-c for a placeholder color, or replace .thumb contents with <video src="..." autoplay muted loop playsinline> or <img src="..."> -->
  <section id="work">
    <h2>Selected work</h2>
    <ul class="work">
      <li class="row" data-c="#c9c9c4">
        <a href="#"><span class="n">1</span><span class="t">project one</span><span class="c">Campaign</span></a>
        <div class="thumb" style="--c:#c9c9c4"></div>
      </li>
      <li class="row">
        <a href="#"><span class="n">2</span><span class="t">project two</span><span class="c">Product</span></a>
        <div class="thumb" style="--c:#8f9a9c"></div>
      </li>
      <li class="row">
        <a href="#"><span class="n">3</span><span class="t">project three</span><span class="c">Live experience</span></a>
        <div class="thumb" style="--c:#a79c8f"></div>
      </li>
    </ul>
    <a class="more" href="projects.html">View all work</a>
  </section>

  <!-- EDIT: about copy + photo -->
  <section id="about">
    <h2>About</h2>
    <div class="about">
      <div class="photo"><!-- <img src="you.jpg" alt="Portrait of Your Name"> --></div>
      <div>
        <p>One or two sentences on how you work and what you believe makes good work.</p>
        <p>A short paragraph on your path: where you started, the kinds of teams you have worked with, and what you are known for.</p>
        <p>A short paragraph on how you lead and collaborate.</p>
      </div>
    </div>
  </section>
</main>

<!-- EDIT: contact -->
<footer id="contact">
  <h2>Get in touch</h2>
  <a class="mail" href="mailto:you@example.com">you@example.com</a>
  <div class="links">
    <a href="#">Instagram</a>
    <a href="#">LinkedIn</a>
    <a href="#">Download resume</a>
  </div>
  <div class="fine"><span>&copy; 2026 Your Name</span><a href="#top">Back to top</a></div>
</footer>

<script>
// Hamburger menu
(function(){
  var b=document.querySelector('.burger'), m=document.getElementById('menu');
  function set(o){
    m.classList.toggle('open',o);document.body.classList.toggle('locked',o);
    b.setAttribute('aria-expanded',o);b.setAttribute('aria-label',o?'Close menu':'Open menu');
  }
  b.addEventListener('click',function(){set(!m.classList.contains('open'))});
  m.querySelectorAll('a').forEach(function(a){a.addEventListener('click',function(){set(false)})});
  document.addEventListener('keydown',function(e){if(e.key==='Escape')set(false)});
})();

// Parallax: media drifts slower than the page while the frame scrolls past
(function(){
  var f=document.querySelector('.para');
  if(!f||matchMedia('(prefers-reduced-motion: reduce)').matches)return;
  var els=f.querySelectorAll('video,.fallback'),tick=false;
  function update(){
    var r=f.getBoundingClientRect();
    if(r.bottom>0&&r.top<innerHeight){
      var p=(r.top+r.height/2-innerHeight/2)/innerHeight; /* -1..1 */
      var y=p*-r.height*0.12;
      els.forEach(function(el){el.style.transform='translate3d(0,'+y+'px,0)'});
    }
    tick=false;
  }
  addEventListener('scroll',function(){if(!tick){tick=true;requestAnimationFrame(update)}},{passive:true});
  addEventListener('resize',update);update();
})();

// Preview follows the cursor over each project row
document.querySelectorAll('.row').forEach(function(row){
  var t=row.querySelector('.thumb');
  row.addEventListener('mousemove',function(e){
    var h=t.offsetHeight/2, y=Math.min(Math.max(e.clientY,h+8),innerHeight-h-8);
    t.style.setProperty('--x',Math.min(e.clientX,innerWidth-t.offsetWidth-40)+'px');
    t.style.setProperty('--y',y+'px');
  });
});
</script>
</body>
</html>
