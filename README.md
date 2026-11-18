# Java-Tutor-for-Intermediate-
Some fundamentals for java
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Java Tutor</title>
<meta name="claude:viewport-fit-sides" content="cover">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500&family=Space+Grotesk:wght@500;600;700&display=swap">
<style>
/* Layout: sticky top bar, lesson index on the left (slide-in drawer on phones), one lesson column on the right with code, output and a quiz. */
:root{
  --bg:#F5F7FA; --surface:#FFFFFF; --surface-2:#EDF1F6; --fg:#14202E; --muted:#556476; --line:#D8E0EA;
  --accent:#0B5FD8; --accent-ink:#FFFFFF; --accent-soft:#E3EEFF; --warm:#B84A0B;
  --good:#17713B; --good-bg:#E4F5EA; --bad:#B3261E; --bad-bg:#FDE8E6;
  --code-bg:#0F1A2A; --code-fg:#E6EDF6; --code-line:#233449; --code-muted:#8196AE; --out-bg:#0A121E;
  --t-kw:#7CB7FF; --t-ty:#F2B36B; --t-str:#8FD6A0; --t-num:#F59E8B; --t-com:#7F93AB; --t-fn:#C9B6FF; --t-ann:#F2B36B;
  --font-display:'Space Grotesk',system-ui,sans-serif;
  --font-body:'Inter',system-ui,-apple-system,'Segoe UI',sans-serif;
  --font-code:'JetBrains Mono',ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;
  --hh:60px;
}
@media (prefers-color-scheme: dark){
  :root:not([data-theme="light"]){
    --bg:#0C1320; --surface:#131D2D; --surface-2:#1A2638; --fg:#E7EDF5; --muted:#9AABC0; --line:#26354A;
    --accent:#5AA2FF; --accent-ink:#06142B; --accent-soft:#16294A; --warm:#F29B5C;
    --good:#5FD38B; --good-bg:#12301F; --bad:#FF8E85; --bad-bg:#3A1816;
    --code-bg:#08101C; --code-line:#1E2E44; --out-bg:#050B14;
    color-scheme:dark;
  }
}
:root[data-theme="dark"]{
  --bg:#0C1320; --surface:#131D2D; --surface-2:#1A2638; --fg:#E7EDF5; --muted:#9AABC0; --line:#26354A;
  --accent:#5AA2FF; --accent-ink:#06142B; --accent-soft:#16294A; --warm:#F29B5C;
  --good:#5FD38B; --good-bg:#12301F; --bad:#FF8E85; --bad-bg:#3A1816;
  --code-bg:#08101C; --code-line:#1E2E44; --out-bg:#050B14;
  color-scheme:dark;
}
[hidden]{display:none!important}
*,*::before,*::after{box-sizing:border-box}
html{scroll-behavior:smooth;-webkit-text-size-adjust:100%}
body{margin:0;background:var(--bg);color:var(--fg);font:16px/1.65 var(--font-body)}
body::before{content:"";position:fixed;inset:0 0 auto;height:env(safe-area-inset-top,0px);background:var(--surface);z-index:50}
a{color:var(--accent)}
:focus-visible{outline:2px solid var(--accent);outline-offset:2px}
code{font-family:var(--font-code)}
.wrap{max-width:1200px;margin:0 auto;padding-left:max(16px,env(safe-area-inset-left,0px));padding-right:max(16px,env(safe-area-inset-right,0px))}

/* top bar */
.top{position:sticky;top:env(safe-area-inset-top,0px);z-index:20;background:var(--surface);border-bottom:1px solid var(--line)}
.top .wrap{display:flex;align-items:center;gap:12px;height:var(--hh)}
.brand{display:flex;align-items:center;gap:10px;color:var(--fg);text-decoration:none;font:700 20px/1 var(--font-display);letter-spacing:-.01em}
.brand svg{color:var(--accent)}
.brand .steam{stroke:var(--warm)}
.sp{flex:1}
.btn{font:500 14px/1 var(--font-body);padding:10px 14px;border-radius:8px;border:1px solid var(--accent);background:var(--accent);color:var(--accent-ink);cursor:pointer}
.btn.ghost{background:transparent;color:var(--fg);border-color:var(--line)}
.btn.ghost:hover{border-color:var(--accent)}
.btn.on{background:var(--good-bg);border-color:var(--good);color:var(--good)}
.icon-btn{display:none;align-items:center;justify-content:center;width:40px;height:40px;border-radius:8px;border:1px solid var(--line);background:transparent;color:var(--fg);cursor:pointer}

/* layout */
.layout{display:grid;grid-template-columns:280px minmax(0,1fr);gap:40px;padding-block:28px 56px}
.side{position:sticky;top:calc(var(--hh) + env(safe-area-inset-top,0px) + 20px);align-self:start;max-height:calc(100vh - var(--hh) - env(safe-area-inset-top,0px) - 40px);overflow:auto;min-width:0}
.search{width:100%;font:inherit;font-size:14px;padding:10px 12px;border-radius:8px;border:1px solid var(--line);background:var(--surface);color:var(--fg)}
.search::placeholder{color:var(--muted)}
.prog{margin:16px 0 8px}
.bar{height:6px;border-radius:6px;background:var(--surface-2);overflow:hidden}
.bar i{display:block;height:100%;width:0;background:var(--good);transition:width .3s}
.prog p{margin:6px 0 0;font-size:13px;color:var(--muted)}
.grp{margin:20px 0 6px;font:600 11px/1 var(--font-body);text-transform:uppercase;letter-spacing:.09em;color:var(--muted)}
.item{display:flex;align-items:center;gap:10px;padding:8px 10px;border-radius:8px;color:var(--fg);text-decoration:none;font-size:15px;line-height:1.35}
.item:hover{background:var(--surface-2)}
.item.on{background:var(--accent-soft);color:var(--accent);font-weight:600}
.item .num{font:500 12px/1 var(--font-code);color:var(--muted);font-variant-numeric:tabular-nums}
.item.on .num{color:var(--accent)}
.item .ttl{flex:1;min-width:0}
.item .ck{width:16px;color:var(--good);font-weight:700;text-align:center}
.none{font-size:14px;color:var(--muted)}

/* lesson */
.main{min-width:0;outline:none}
.lesson{max-width:760px}
.eyebrow{margin:0 0 8px;font:600 12px/1 var(--font-body);text-transform:uppercase;letter-spacing:.09em;color:var(--warm)}
h1{margin:0;font:700 clamp(28px,5vw,40px)/1.12 var(--font-display);letter-spacing:-.02em;text-wrap:balance;outline:none}
.meta{margin:10px 0 0;font-size:14px;color:var(--muted)}
.lead{margin:20px 0 0;font-size:18px;line-height:1.6}
.lesson h2{margin:36px 0 8px;font:600 22px/1.25 var(--font-display);letter-spacing:-.01em;text-wrap:balance}
.lesson p{margin:12px 0;max-width:68ch}
.lesson ul{margin:12px 0;padding-left:22px;max-width:68ch}
.lesson li{margin:6px 0}
.ic{font-size:.88em;padding:2px 6px;border-radius:5px;background:var(--surface-2);border:1px solid var(--line);overflow-wrap:anywhere}
.tip{margin:20px 0;padding:12px 16px;border-radius:10px;background:var(--surface-2);border:1px solid var(--line);max-width:68ch}
.tip strong{display:block;font:600 11px/1 var(--font-body);text-transform:uppercase;letter-spacing:.09em;color:var(--warm);margin-bottom:6px}
.tip p{margin:0}

.code{margin:20px 0;border-radius:10px;overflow:hidden;background:var(--code-bg);color:var(--code-fg);border:1px solid var(--code-line)}
.code-head{display:flex;align-items:center;justify-content:space-between;gap:12px;padding:8px 8px 8px 16px;border-bottom:1px solid var(--code-line);font:500 12px/1 var(--font-code);color:var(--code-muted)}
.copy{font:500 12px/1 var(--font-body);padding:7px 10px;border-radius:6px;border:1px solid var(--code-line);background:transparent;color:var(--code-fg);cursor:pointer}
.copy:hover{border-color:var(--t-kw)}
.code pre{margin:0;padding:14px 16px;overflow-x:auto;font:400 14px/1.65 var(--font-code);tab-size:4}
.code pre code{font:inherit}
.out{border-top:1px solid var(--code-line);background:var(--out-bg)}
.out span{display:block;padding:8px 16px 0;font:600 11px/1 var(--font-body);text-transform:uppercase;letter-spacing:.09em;color:var(--code-muted)}
.out pre{padding-top:8px;color:var(--t-str)}
.t-kw{color:var(--t-kw)}.t-ty{color:var(--t-ty)}.t-str{color:var(--t-str)}.t-num{color:var(--t-num)}.t-com{color:var(--t-com);font-style:italic}.t-fn{color:var(--t-fn)}.t-ann{color:var(--t-ann)}

.task{margin:36px 0 0;padding:16px 20px;border-radius:12px;background:var(--surface);border:1px solid var(--line);max-width:68ch}
.task h2{margin:0 0 4px;font-size:18px}
.task p{margin:4px 0 0}

.quiz{margin:36px 0 0}
.quiz h2{margin-top:0}
.q{margin:16px 0 22px}
.qt{margin:0 0 10px!important;font-weight:500}
.qn{display:inline-block;margin-right:6px;font:600 12px/1 var(--font-code);color:var(--accent)}
.opts{display:grid;gap:8px;max-width:68ch}
.opt{display:flex;gap:12px;align-items:flex-start;width:100%;text-align:left;padding:10px 14px;border-radius:8px;border:1px solid var(--line);background:var(--surface);color:var(--fg);font:inherit;font-size:15px;line-height:1.45;cursor:pointer}
.opt:hover:not(:disabled){border-color:var(--accent)}
.opt:disabled{cursor:default;color:var(--fg);opacity:1}
.opt .ltr{flex:none;width:22px;font:600 12px/1.7 var(--font-code);color:var(--muted)}
.opt.right{border-color:var(--good);background:var(--good-bg)}
.opt.wrong{border-color:var(--bad);background:var(--bad-bg)}
.why{margin:10px 0 0!important;font-size:14px;color:var(--muted)}
.why strong{color:var(--fg)}
.score{margin:8px 0 12px!important;font-weight:600}

.pager{display:flex;flex-wrap:wrap;gap:12px;align-items:center;justify-content:space-between;margin-top:44px;padding-top:20px;border-top:1px solid var(--line)}
.pager a{display:inline-flex;flex-direction:column;gap:2px;padding:10px 14px;border:1px solid var(--line);border-radius:8px;text-decoration:none;color:var(--fg);max-width:100%;min-width:0;font-size:15px;font-weight:500}
.pager a small{font:500 11px/1 var(--font-body);text-transform:uppercase;letter-spacing:.09em;color:var(--muted)}
.pager a:hover{border-color:var(--accent)}
.pager .nx{text-align:right;align-items:flex-end}
.foot{padding-bottom:max(28px,env(safe-area-inset-bottom,0px));font-size:13px;color:var(--muted)}

.scrim{position:fixed;inset:0;background:rgba(5,10,20,.5);z-index:30}

@media (max-width:860px){
  .layout{grid-template-columns:minmax(0,1fr);gap:0;padding-block:20px 40px}
  .icon-btn{display:inline-flex}
  .side{position:fixed;z-index:40;top:0;bottom:0;left:0;width:min(88vw,330px);max-height:none;background:var(--surface);border-right:1px solid var(--line);
    padding:calc(16px + env(safe-area-inset-top,0px)) 16px calc(16px + env(safe-area-inset-bottom,0px)) calc(16px + env(safe-area-inset-left,0px));
    transform:translateX(-102%);visibility:hidden;transition:transform .2s,visibility 0s .2s}
  body.nav-open .side{transform:none;visibility:visible;transition:transform .2s,visibility 0s}
  .lead{font-size:17px}
}
@media (min-width:861px){.scrim{display:none!important}}
@media (prefers-reduced-motion:reduce){html{scroll-behavior:auto}*{transition:none!important}}
</style>
</head>
<body>

<header class="top">
  <div class="wrap">
    <button id="menu" class="icon-btn" type="button" aria-label="Open lesson list" aria-expanded="false" aria-controls="side">
      <svg width="20" height="20" viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><path d="M3 5h14M3 10h14M3 15h14"/></svg>
    </button>
    <a class="brand" href="#intro" aria-label="Java Tutor, first lesson">
      <svg width="26" height="26" viewBox="0 0 26 26" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
        <path class="steam" d="M9 2.5c-1.2 1.4 1.2 2.2 0 3.8M14 2.5c-1.2 1.4 1.2 2.2 0 3.8"/>
        <path d="M4 10h14v5a5 5 0 0 1-5 5H9a5 5 0 0 1-5-5z"/>
        <path d="M18 11.5h1.5a2.5 2.5 0 0 1 0 5H18"/>
        <path d="M6 23.5h10"/>
      </svg>
      <span>Java Tutor For intermediate</span>
    </a>
    <span class="sp"></span>
    <button id="theme" class="btn ghost" type="button">Dark mode</button>
  </div>
</header>

<div class="scrim" id="scrim" hidden></div>

<div class="wrap layout">
  <nav class="side" id="side" aria-label="Lessons">
    <label for="q" class="sr" style="position:absolute;left:-9999px">Search lessons</label>
    <input id="q" class="search" type="search" placeholder="Search lessons, e.g. loop" autocomplete="off">
    <div class="prog">
      <div class="bar"><i id="barfill"></i></div>
      <p id="progtxt"></p>
    </div>
    <div id="nav"></div>
  </nav>
  <main id="main" class="main" tabindex="-1"></main>
</div>
<footer class="wrap foot">Java Tutor. Code examples target Java 17 or newer.</footer>

<script>
(function(){
'use strict';

function T(s){return s.replace(/^\n+|\s+$/g,'');}

var LESSONS=[
{
  id:'intro', group:'Foundations', title:'Your first Java program', min:6,
  keys:'hello world jdk jvm compile javac main install',
  lead:'Java runs Android apps, bank back ends and huge web services. This lesson gets your first program running.',
  blocks:[
    {t:'p', x:'You write source code in a {{.java}} file. The compiler {{javac}} turns it into bytecode, and the Java Virtual Machine (JVM) runs that bytecode. That is why the same program runs on Windows, macOS and Linux.'},
    {t:'p', x:'Install a JDK (version 17 or newer), for example from Adoptium, then check it by typing {{java -version}} in a terminal.'},
    {t:'h', x:'Hello, Java'},
    {t:'code', f:'Main.java', c:T(`
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, Java!");
    }
}
`), o:'Hello, Java!'},
    {t:'ul', x:[
      '{{public class Main}} declares a class. The file must be named {{Main.java}}.',
      '{{main}} is the method where the JVM starts running your program.',
      '{{System.out.println}} prints text and moves to a new line.'
    ]},
    {t:'h', x:'Compile and run'},
    {t:'code', f:'Terminal', lang:'shell', c:'javac Main.java\njava Main', o:'Hello, Java!'},
    {t:'tip', l:'Shortcut', x:'Since Java 11 you can skip the compile step for a single file: {{java Main.java}} compiles and runs it in one go.'},
    {t:'tip', l:'Common slip', x:'Java is case-sensitive, so {{Main}} and {{main}} are different names. Every statement ends with a semicolon.'}
  ],
  task:'Change the message so it prints your own name, then add a second {{System.out.println}} line underneath.',
  quiz:[
    {q:'Which tool turns {{Main.java}} into bytecode?', o:['java','javac','jvm','jdoc'], a:1, why:'{{javac}} is the compiler. {{java}} starts the JVM and runs the compiled bytecode.'},
    {q:'Which line is the correct entry point of a Java program?', o:['public void start()','static int main()','public static void main(String[] args)','public static main()'], a:2, why:'The JVM looks for exactly this signature to begin execution.'}
  ]
},
{
  id:'variables', group:'Foundations', title:'Variables and data types', min:8,
  keys:'int double boolean char string cast primitive type var',
  lead:'A variable is a named box that holds a value. In Java the type of the box is fixed when you declare it.',
  blocks:[
    {t:'h', x:'Primitive types'},
    {t:'ul', x:[
      '{{int}}: whole numbers (32-bit), such as {{21}}.',
      '{{long}}: bigger whole numbers (64-bit), written with an L suffix, such as {{5000000000L}}.',
      '{{double}}: decimal numbers, such as {{99.50}}.',
      '{{boolean}}: only {{true}} or {{false}}.',
      '{{char}}: one character in single quotes, such as {{\'A\'}}.'
    ]},
    {t:'code', f:'Main.java', c:T(`
int age = 21;
double price = 99.50;
boolean isStudent = true;
char grade = 'A';
String name = "Aarav";   // String is a class, not a primitive

System.out.println(name + " is " + age + " years old.");
System.out.println("Price: " + price + ", grade " + grade);
`), o:'Aarav is 21 years old.\nPrice: 99.5, grade A'},
    {t:'h', x:'Converting between types'},
    {t:'p', x:'Going from a smaller type to a larger one happens automatically. Going the other way needs a cast, and decimals are cut off, not rounded.'},
    {t:'code', f:'Main.java', c:T(`
int whole = 7;
double wide = whole;       // automatic: 7.0
double pi = 3.99;
int cut = (int) pi;        // cast: 3, decimals dropped
System.out.println(wide + " " + cut);
`), o:'7.0 3'},
    {t:'tip', l:'Shortcut', x:'{{var count = 10;}} lets the compiler work out the type. The variable is still an {{int}}; it is not dynamic like in JavaScript.'}
  ],
  task:'Declare variables for your name, age and height in metres, then print one sentence that uses all three.',
  quiz:[
    {q:'Which type is best for the value {{3.14}}?', o:['int','boolean','char','double'], a:3, why:'{{double}} stores numbers with a fractional part.'},
    {q:'What does {{(int) 9.99}} give?', o:['10','9','9.9','A compile error'], a:1, why:'A cast to {{int}} drops the decimals. It never rounds.'}
  ]
},
{
  id:'operators', group:'Foundations', title:'Operators', min:6,
  keys:'arithmetic modulus remainder compare logical and or not increment',
  lead:'Operators combine values. You will use arithmetic ones to calculate and logical ones to make decisions.',
  blocks:[
    {t:'h', x:'Arithmetic'},
    {t:'p', x:'The operators are {{+ - * / %}}. When both sides are {{int}}, division throws away the remainder, and {{%}} gives that remainder.'},
    {t:'code', f:'Main.java', c:T(`
int a = 17, b = 5;
System.out.println(a / b);    // 3
System.out.println(a % b);    // 2
System.out.println(a / 5.0);  // 3.4
a++;                          // same as a = a + 1
System.out.println(a);
`), o:'3\n2\n3.4\n18'},
    {t:'h', x:'Comparison and logic'},
    {t:'p', x:'Comparisons ({{==  !=  <  >  <=  >=}}) produce a {{boolean}}. Join them with {{&&}} (and), {{||}} (or) and {{!}} (not).'},
    {t:'code', f:'Main.java', c:T(`
int marks = 72;
boolean passed = marks >= 40 && marks <= 100;
System.out.println(passed);
System.out.println(!passed);
System.out.println(marks != 72);
`), o:'true\nfalse\nfalse'},
    {t:'tip', l:'Common slip', x:'Use {{==}} to compare numbers, but never to compare Strings. The strings lesson explains why.'}
  ],
  task:'Write code that checks whether a number is even, using {{%}}, and prints the boolean result.',
  quiz:[
    {q:'What does {{17 % 5}} return?', o:['3','3.4','2','12'], a:2, why:'17 divided by 5 is 3 with a remainder of 2, and {{%}} returns the remainder.'},
    {q:'What is the result of {{7 / 2}} when both are {{int}}?', o:['3.5','4','3.0','3'], a:3, why:'Integer division discards the fractional part, so the answer is {{3}}.'}
  ]
},
{
  id:'conditions', group:'Control flow', title:'Making decisions', min:7,
  keys:'if else switch ternary condition branch',
  lead:'Programs get interesting when they choose between paths. Java gives you {{if}}, {{switch}} and the short ternary form.',
  blocks:[
    {t:'h', x:'if, else if, else'},
    {t:'code', f:'Main.java', c:T(`
int score = 82;
if (score >= 90) {
    System.out.println("Grade A");
} else if (score >= 75) {
    System.out.println("Grade B");
} else {
    System.out.println("Keep practising");
}
`), o:'Grade B'},
    {t:'p', x:'Java checks the conditions from top to bottom and runs only the first block whose condition is true.'},
    {t:'h', x:'switch'},
    {t:'p', x:'A {{switch}} is tidier when you compare one value against many fixed options. The arrow form needs Java 14 or newer.'},
    {t:'code', f:'Main.java', c:T(`
int day = 3;
String name = switch (day) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    case 3 -> "Wednesday";
    default -> "Another day";
};
System.out.println(name);
`), o:'Wednesday'},
    {t:'tip', l:'Shortcut', x:'The ternary operator picks one of two values in a single line: {{String r = score >= 40 ? "Pass" : "Fail";}}'}
  ],
  task:'Read a temperature value and print "Cold" below 15, "Pleasant" up to 28, and "Hot" above that.',
  quiz:[
    {q:'In an if / else-if / else chain, how many blocks run?', o:['Every block with a true condition','Only the first block whose condition is true','Always the last block','Always the first block'], a:1, why:'Once a condition matches, Java skips the remaining branches.'},
    {q:'When does the {{default}} branch of a switch run?', o:['Always','Never','When no case matches','Only if it is the first label'], a:2, why:'{{default}} is the fallback for values that match none of the cases.'}
  ]
},
{
  id:'loops', group:'Control flow', title:'Loops', min:8,
  keys:'for while do while break continue iteration repeat',
  lead:'Loops repeat work so you do not copy and paste code. Pick the loop that matches what you know in advance.',
  blocks:[
    {t:'h', x:'for loop'},
    {t:'p', x:'Use {{for}} when you know how many times to repeat. It has three parts: a start, a condition and a step.'},
    {t:'code', f:'Main.java', c:T(`
for (int i = 1; i <= 5; i++) {
    System.out.print(i + " ");
}
`), o:'1 2 3 4 5 '},
    {t:'h', x:'while and do-while'},
    {t:'p', x:'Use {{while}} when you repeat until something changes. A {{do-while}} checks its condition after the body, so it always runs at least once.'},
    {t:'code', f:'Main.java', c:T(`
int n = 1;
while (n < 100) {
    n *= 2;
}
System.out.println(n);

int tries = 0;
do {
    tries++;
} while (tries < 3);
System.out.println(tries);
`), o:'128\n3'},
    {t:'h', x:'break and continue'},
    {t:'code', f:'Main.java', c:T(`
for (int i = 1; i <= 10; i++) {
    if (i % 2 == 0) continue;   // skip even numbers
    if (i > 7) break;           // stop the whole loop
    System.out.print(i + " ");
}
`), o:'1 3 5 7 '},
    {t:'tip', l:'Common slip', x:'A loop whose condition never becomes false runs forever. Check that something inside the loop changes the condition.'}
  ],
  task:'Print the multiplication table of 7, from 7 x 1 up to 7 x 10, using a {{for}} loop.',
  quiz:[
    {q:'Which loop always runs its body at least once?', o:['for','while','do-while','All of them'], a:2, why:'{{do-while}} tests its condition only after the body has run.'},
    {q:'What does {{continue}} do inside a loop?', o:['Ends the loop','Skips the rest of this round and starts the next','Restarts the program','Nothing'], a:1, why:'{{continue}} jumps to the next iteration. {{break}} is the one that ends the loop.'}
  ]
},
{
  id:'arrays', group:'Building blocks', title:'Arrays', min:7,
  keys:'array index length foreach 2d grid',
  lead:'An array stores several values of the same type under one name. Its size is fixed when you create it.',
  blocks:[
    {t:'code', f:'Main.java', c:T(`
int[] marks = {70, 85, 90, 65};
System.out.println(marks.length);   // 4
System.out.println(marks[0]);       // 70

int total = 0;
for (int m : marks) {               // for-each loop
    total += m;
}
System.out.println(total / (double) marks.length);
`), o:'4\n70\n77.5'},
    {t:'p', x:'Indexes start at 0, so an array of length 4 has indexes 0 to 3. Using {{marks[4]}} throws an {{ArrayIndexOutOfBoundsException}}.'},
    {t:'h', x:'Creating empty and 2D arrays'},
    {t:'code', f:'Main.java', c:T(`
int[] empty = new int[3];           // {0, 0, 0}
String[] names = new String[2];     // {null, null}
int[][] grid = {{1, 2}, {3, 4}};
System.out.println(grid[1][0]);
`), o:'3'},
    {t:'tip', l:'Remember', x:'An array cannot grow. When you need a list that changes size, use {{ArrayList}} from the collections lesson.'}
  ],
  task:'Find the largest number in an array of five values without using any library method.',
  quiz:[
    {q:'What is the last valid index of an array of length 5?', o:['5','6','0','4'], a:3, why:'Indexes run from 0 to length - 1.'},
    {q:'What does {{new int[3]}} contain right after creation?', o:['null, null, null','0, 0, 0','1, 1, 1','Random values'], a:1, why:'Numeric arrays are filled with zeros. Object arrays are filled with {{null}}.'}
  ]
},
{
  id:'strings', group:'Building blocks', title:'Strings', min:7,
  keys:'string equals substring length immutable text stringbuilder',
  lead:'Text in Java is an object of the {{String}} class. It comes with many helpful methods.',
  blocks:[
    {t:'code', f:'Main.java', c:T(`
String s = "Java Tutor";
System.out.println(s.length());           // 10
System.out.println(s.toUpperCase());      // JAVA TUTOR
System.out.println(s.substring(0, 4));    // Java
System.out.println(s.indexOf("Tutor"));   // 5
System.out.println(s.replace("Java", "Kotlin"));
`), o:'10\nJAVA TUTOR\nJava\n5\nKotlin Tutor'},
    {t:'h', x:'Comparing strings'},
    {t:'p', x:'The {{==}} operator checks whether two variables point to the same object. To compare the text itself, call {{equals}}.'},
    {t:'code', f:'Main.java', c:T(`
String a = new String("hi");
String b = new String("hi");
System.out.println(a == b);        // false: different objects
System.out.println(a.equals(b));   // true: same text
`), o:'false\ntrue'},
    {t:'tip', l:'Remember', x:'Strings are immutable. Methods such as {{toUpperCase}} return a new String and leave the original unchanged. For heavy text building inside loops, use {{StringBuilder}}.'}
  ],
  task:'Take a name such as "riya sharma" and print it with the first letter of each word capitalised.',
  quiz:[
    {q:'How should you compare the contents of two Strings?', o:['{{==}}','{{=}}','{{a.equals(b)}}','{{a.same(b)}}'], a:2, why:'{{equals}} compares the characters. {{==}} compares object references.'},
    {q:'What does {{"Java Tutor".substring(0, 4)}} return?', o:['Jav','Java ','ava ','Java'], a:3, why:'The start index is included and the end index is excluded, so you get characters 0 to 3.'}
  ]
},
{
  id:'methods', group:'Building blocks', title:'Methods', min:7,
  keys:'function return void parameter overload static call',
  lead:'A method is a named block of code you can run whenever you need it, with inputs and an optional result.',
  blocks:[
    {t:'code', f:'Main.java', c:T(`
public class Main {
    static int square(int x) {
        return x * x;
    }

    static void greet(String name) {
        System.out.println("Hi, " + name);
    }

    public static void main(String[] args) {
        greet("Riya");
        System.out.println(square(6));
    }
}
`), o:'Hi, Riya\n36'},
    {t:'ul', x:[
      'The word before the method name is the return type. {{void}} means it returns nothing.',
      'Values inside the brackets are parameters. The caller passes arguments to fill them.',
      '{{return}} sends a value back and ends the method.'
    ]},
    {t:'h', x:'Overloading'},
    {t:'p', x:'You may reuse a method name if the parameter lists differ. Java picks the version that fits the arguments.'},
    {t:'code', f:'Main.java', c:T(`
public class Main {
    static int add(int a, int b) { return a + b; }
    static double add(double a, double b) { return a + b; }

    public static void main(String[] args) {
        System.out.println(add(2, 3));
        System.out.println(add(2.5, 1.5));
    }
}
`), o:'5\n4.0'}
  ],
  task:'Write a method {{isPrime(int n)}} that returns a boolean, then print the primes below 30.',
  quiz:[
    {q:'Which return type means a method gives nothing back?', o:['null','empty','none','void'], a:3, why:'{{void}} is the return type of methods that only perform an action.'},
    {q:'What is method overloading?', o:['Calling a method from itself','Using the same name with different parameters','A method that is too long','Replacing a parent method in a subclass'], a:1, why:'Overloads share a name but differ in the number or types of parameters. The last option is overriding.'}
  ]
},
{
  id:'classes', group:'Objects', title:'Classes and objects', min:9,
  keys:'class object constructor this encapsulation private getter new',
  lead:'A class is a blueprint. An object is one thing built from that blueprint, with its own data.',
  blocks:[
    {t:'code', f:'Student.java', c:T(`
public class Student {
    private String name;
    private int marks;

    public Student(String name, int marks) {
        this.name = name;
        this.marks = marks;
    }

    public String getName() { return name; }

    public boolean hasPassed() {
        return marks >= 40;
    }
}
`)},
    {t:'code', f:'Main.java', c:T(`
public class Main {
    public static void main(String[] args) {
        Student s = new Student("Kabir", 58);
        System.out.println(s.getName() + " passed? " + s.hasPassed());
    }
}
`), o:'Kabir passed? true'},
    {t:'ul', x:[
      'Fields ({{name}}, {{marks}}) hold the data of each object.',
      'A constructor has the class name, no return type, and runs when you write {{new}}.',
      '{{this}} means the current object, which separates the field from the parameter with the same name.',
      'Marking fields {{private}} and giving access through methods is called encapsulation.'
    ]},
    {t:'tip', l:'Why it matters', x:'With private fields the class controls how its data changes. You can later add a check, such as rejecting negative marks, without touching any other code.'}
  ],
  task:'Add a {{Book}} class with a title, price and a method {{discounted(double percent)}} that returns the new price.',
  quiz:[
    {q:'What is a constructor?', o:['A static helper method','A field of the class','A special method with the class name that runs on {{new}}','An interface'], a:2, why:'Constructors set up a new object. They have no return type.'},
    {q:'Why are fields usually marked {{private}}?', o:['To hide data and control how it changes','To make the program faster','Because Java requires it','To make them static'], a:0, why:'This is encapsulation. Other classes must go through your methods.'}
  ]
},
{
  id:'inheritance', group:'Objects', title:'Inheritance and interfaces', min:10,
  keys:'extends implements override polymorphism interface abstract super',
  lead:'Inheritance lets one class reuse and specialise another. Interfaces describe what a class can do without saying how.',
  blocks:[
    {t:'h', x:'extends and @Override'},
    {t:'code', f:'Main.java', c:T(`
class Animal {
    void speak() {
        System.out.println("Some sound");
    }
}

class Dog extends Animal {
    @Override
    void speak() {
        System.out.println("Woof");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal pet = new Dog();   // parent type, child object
        pet.speak();
    }
}
`), o:'Woof'},
    {t:'p', x:'This is polymorphism. The variable has the type {{Animal}}, but Java runs the {{speak}} of the real object, which is a {{Dog}}.'},
    {t:'h', x:'Interfaces'},
    {t:'code', f:'Main.java', c:T(`
interface Shape {
    double area();
}

class Circle implements Shape {
    private final double r;
    Circle(double r) { this.r = r; }
    public double area() { return Math.PI * r * r; }
}

public class Main {
    public static void main(String[] args) {
        Shape s = new Circle(2);
        System.out.println(s.area());
    }
}
`), o:'12.566370614359172'},
    {t:'ul', x:[
      'A class can {{extends}} only one parent class.',
      'A class can {{implements}} many interfaces.',
      'Use {{super}} to call the parent constructor or method.'
    ]}
  ],
  task:'Create a {{Shape}} interface with {{area()}}, then add {{Rectangle}} and {{Circle}} and print the areas from one array of {{Shape}}.',
  quiz:[
    {q:'Which keyword makes a class inherit from another class?', o:['implements','inherits','extends','super'], a:2, why:'{{extends}} is for classes. {{implements}} is for interfaces.'},
    {q:'For {{Animal pet = new Dog(); pet.speak();}}, whose {{speak}} runs?', o:['Animal','Dog','Both','Neither, it is an error'], a:1, why:'The actual object decides at runtime, which is the core of polymorphism.'}
  ]
},
{
  id:'exceptions', group:'Real programs', title:'Handling errors', min:8,
  keys:'exception try catch finally throw throws error checked unchecked',
  lead:'Things go wrong: files are missing, input is bad, indexes are too big. Exceptions let your program respond instead of crashing.',
  blocks:[
    {t:'code', f:'Main.java', c:T(`
public class Main {
    public static void main(String[] args) {
        try {
            int[] nums = {1, 2, 3};
            System.out.println(nums[5]);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Bad index: " + e.getMessage());
        } finally {
            System.out.println("Always runs");
        }
    }
}
`), o:'Bad index: Index 5 out of bounds for length 3\nAlways runs'},
    {t:'ul', x:[
      '{{try}} holds the code that might fail.',
      '{{catch}} handles one kind of exception.',
      '{{finally}} runs whether or not an exception happened, which makes it good for cleanup.'
    ]},
    {t:'h', x:'Throwing your own'},
    {t:'code', f:'Main.java', c:T(`
static void setAge(int age) {
    if (age < 0) {
        throw new IllegalArgumentException("Age cannot be negative");
    }
}
`)},
    {t:'tip', l:'Remember', x:'Checked exceptions such as {{IOException}} must be caught or declared with {{throws}}. Unchecked ones, which extend {{RuntimeException}}, do not have to be.'}
  ],
  task:'Parse a String into an int with {{Integer.parseInt}} and catch {{NumberFormatException}} to print a friendly message.',
  quiz:[
    {q:'When does a {{finally}} block run?', o:['Only when an exception happens','Only when nothing goes wrong','Whether or not an exception happens','Never'], a:2, why:'It is meant for cleanup that must always happen.'},
    {q:'Which exception does {{10 / 0}} throw for ints?', o:['NullPointerException','ArithmeticException','IOException','NumberFormatException'], a:1, why:'Integer division by zero throws {{ArithmeticException}}.'}
  ]
},
{
  id:'collections', group:'Real programs', title:'ArrayList and HashMap', min:9,
  keys:'collections list arraylist map hashmap generics put get',
  lead:'Real programs need lists that grow and lookups by key. The collections framework provides both.',
  blocks:[
    {t:'h', x:'ArrayList'},
    {t:'code', f:'Main.java', c:T(`
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> langs = new ArrayList<>();
        langs.add("Java");
        langs.add("Python");
        langs.add("C++");
        langs.remove("Python");

        for (String l : langs) {
            System.out.println(l);
        }
        System.out.println(langs.size());
    }
}
`), o:'Java\nC++\n2'},
    {t:'h', x:'HashMap'},
    {t:'p', x:'A {{HashMap}} stores key and value pairs and finds a value quickly from its key.'},
    {t:'code', f:'Main.java', c:T(`
import java.util.HashMap;
import java.util.Map;

public class Main {
    public static void main(String[] args) {
        Map<String, Integer> stock = new HashMap<>();
        stock.put("pen", 12);
        stock.put("book", 5);
        stock.put("pen", 20);   // replaces the old value

        System.out.println(stock.get("pen"));
        System.out.println(stock.containsKey("bag"));
    }
}
`), o:'20\nfalse'},
    {t:'tip', l:'Remember', x:'Generics such as {{List<String>}} need object types, so use {{Integer}} instead of {{int}}. A {{HashMap}} does not promise any particular order.'}
  ],
  task:'Count how many times each word appears in a sentence using a {{HashMap<String, Integer>}}.',
  quiz:[
    {q:'Which of these can grow after it is created?', o:['{{int[]}}','{{ArrayList}}','{{char[]}}','{{String}}'], a:1, why:'{{ArrayList}} resizes itself. Arrays have a fixed length.'},
    {q:'What happens on {{stock.put("pen", 20)}} when "pen" already exists?', o:['It throws an exception','It adds a second "pen"','It is ignored','The old value is replaced'], a:3, why:'Keys are unique, so {{put}} overwrites the existing value.'}
  ]
}
];

/* ---------- helpers ---------- */
function esc(s){return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');}
function fmt(s){return esc(s).replace(/\{\{([\s\S]+?)\}\}/g,'<code class="ic">$1</code>');}
function pad(n){return n<10?'0'+n:''+n;}
function $(s){return document.querySelector(s);}

var KW={};
('abstract boolean break byte case catch char class continue default do double else enum extends final finally float for if implements import instanceof int interface long new null package private protected public return short static super switch this throw throws try void while var true false').split(' ').forEach(function(k){KW[k]=1;});

function hl(code){
  var re=/(\/\/[^\n]*|\/\*[\s\S]*?\*\/)|("(?:\\.|[^"\\\n])*")|('(?:\\.|[^'\\\n])*')|(@[A-Za-z]+)|\b(\d+(?:\.\d+)?[fFdDlL]?)\b|\b([A-Za-z_][A-Za-z0-9_]*)\b/g;
  var out='',last=0,m,cls,t;
  while((m=re.exec(code))){
    out+=esc(code.slice(last,m.index));
    t=m[0];cls='';
    if(m[1])cls='com';
    else if(m[2]||m[3])cls='str';
    else if(m[4])cls='ann';
    else if(m[5])cls='num';
    else if(KW[t])cls='kw';
    else if(/^[A-Z]/.test(t))cls='ty';
    else if(code.charAt(re.lastIndex)==='(')cls='fn';
    out+=cls?'<span class="t-'+cls+'">'+esc(t)+'</span>':esc(t);
    last=re.lastIndex;
  }
  return out+esc(code.slice(last));
}

/* ---------- state ---------- */
var nav=$('#nav'), main=$('#main'), side=$('#side'), scrim=$('#scrim'), menu=$('#menu');
var done={}, picks={}, current=0, filter='';
try{JSON.parse(localStorage.getItem('javatutor-done')||'[]').forEach(function(id){done[id]=true;});}catch(e){}
function saveDone(){try{localStorage.setItem('javatutor-done',JSON.stringify(Object.keys(done)));}catch(e){}}

/* ---------- nav ---------- */
function renderNav(){
  var f=filter.trim().toLowerCase(), html='', lastG='', shown=0;
  LESSONS.forEach(function(l,i){
    if(f && (l.title+' '+l.group+' '+l.keys).toLowerCase().indexOf(f)<0)return;
    if(l.group!==lastG){html+='<div class="grp">'+esc(l.group)+'</div>';lastG=l.group;}
    shown++;
    html+='<a class="item'+(i===current?' on':'')+'" href="#'+l.id+'"'+(i===current?' aria-current="page"':'')+'>'+
      '<span class="num">'+pad(i+1)+'</span><span class="ttl">'+esc(l.title)+'</span>'+
      '<span class="ck" title="'+(done[l.id]?'Completed':'')+'">'+(done[l.id]?'✓':'')+'</span></a>';
  });
  if(!shown)html='<p class="none">No lesson matches "'+esc(filter)+'".</p>';
  nav.innerHTML=html;
  var n=Object.keys(done).length;
  $('#barfill').style.width=Math.round(100*n/LESSONS.length)+'%';
  $('#progtxt').textContent=n+' of '+LESSONS.length+' lessons completed';
}

/* ---------- lesson ---------- */
function block(b){
  switch(b.t){
    case 'p':return '<p>'+fmt(b.x)+'</p>';
    case 'h':return '<h2>'+esc(b.x)+'</h2>';
    case 'ul':return '<ul>'+b.x.map(function(i){return '<li>'+fmt(i)+'</li>';}).join('')+'</ul>';
    case 'tip':return '<aside class="tip"><strong>'+esc(b.l||'Remember')+'</strong><p>'+fmt(b.x)+'</p></aside>';
    case 'code':
      return '<figure class="code" style="margin:20px 0"><div class="code-head"><span>'+esc(b.f||'Main.java')+'</span>'+
        '<button type="button" class="copy" data-action="copy">Copy</button></div>'+
        '<pre><code>'+(b.lang==='shell'?esc(b.c):hl(b.c))+'</code></pre>'+
        (b.o!==undefined?'<div class="out"><span>Output</span><pre>'+esc(b.o)+'</pre></div>':'')+'</figure>';
  }
  return '';
}

function quizHtml(l){
  var p=picks[l.id]||(picks[l.id]={}), answered=0, right=0;
  var h=l.quiz.map(function(q,qi){
    var chosen=p[qi], has=chosen!==undefined;
    if(has){answered++;if(chosen===q.a)right++;}
    return '<div class="q"><p class="qt"><span class="qn">Q'+(qi+1)+'</span>'+fmt(q.q)+'</p><div class="opts">'+
      q.o.map(function(o,oi){
        var c='opt';
        if(has){if(oi===q.a)c+=' right';else if(oi===chosen)c+=' wrong';}
        return '<button type="button" class="'+c+'" data-q="'+qi+'" data-o="'+oi+'"'+(has?' disabled':'')+'><span class="ltr">'+'ABCD'.charAt(oi)+'</span><span>'+fmt(o)+'</span></button>';
      }).join('')+'</div>'+
      (has?'<p class="why"><strong>'+(chosen===q.a?'Correct.':'Not quite.')+'</strong> '+fmt(q.why)+'</p>':'')+'</div>';
  }).join('');
  if(answered===l.quiz.length){
    h+='<p class="score">Score: '+right+' of '+l.quiz.length+'. '+(right===l.quiz.length?'Full marks, so this lesson is marked complete.':'Reset the quiz to try again.')+'</p>';
  }
  if(answered)h+='<button type="button" class="btn ghost" data-action="reset">Reset quiz</button>';
  return h;
}

function completeBtn(l){
  return done[l.id]?'<button type="button" class="btn on" data-action="complete">✓ Completed</button>':'<button type="button" class="btn" data-action="complete">Mark as complete</button>';
}

function show(i,first){
  current=i;
  var l=LESSONS[i], prev=LESSONS[i-1], next=LESSONS[i+1];
  main.innerHTML='<article class="lesson">'+
    '<p class="eyebrow">'+esc(l.group)+'</p><h1 id="ttl" tabindex="-1">'+esc(l.title)+'</h1>'+
    '<p class="meta">Lesson '+(i+1)+' of '+LESSONS.length+' · '+l.min+' min</p>'+
    '<p class="lead">'+fmt(l.lead)+'</p>'+
    l.blocks.map(block).join('')+
    '<section class="task"><h2>Try it yourself</h2><p>'+fmt(l.task)+'</p></section>'+
    '<section class="quiz" aria-labelledby="qh"><h2 id="qh">Check yourself</h2><div id="quiz">'+quizHtml(l)+'</div></section>'+
    '<div class="pager">'+
      (prev?'<a href="#'+prev.id+'"><small>Previous</small>'+esc(prev.title)+'</a>':'<span></span>')+
      '<span id="cbox">'+completeBtn(l)+'</span>'+
      (next?'<a class="nx" href="#'+next.id+'"><small>Next</small>'+esc(next.title)+'</a>':'<span></span>')+
    '</div></article>';
  renderNav();
  if(!first){window.scrollTo(0,0);var h=$('#ttl');if(h)h.focus({preventScroll:true});}
}

main.addEventListener('click',function(e){
  var t=e.target.closest('button');
  if(!t)return;
  var l=LESSONS[current], a=t.getAttribute('data-action');
  if(t.classList.contains('opt')){
    var qi=+t.getAttribute('data-q'), oi=+t.getAttribute('data-o');
    var p=picks[l.id]||(picks[l.id]={});
    if(p[qi]!==undefined)return;
    p[qi]=oi;
    var all=l.quiz.every(function(q,k){return p[k]===q.a;});
    if(all&&!done[l.id]){done[l.id]=true;saveDone();renderNav();$('#cbox').innerHTML=completeBtn(l);}
    $('#quiz').innerHTML=quizHtml(l);
    return;
  }
  if(a==='reset'){picks[l.id]={};$('#quiz').innerHTML=quizHtml(l);}
  else if(a==='complete'){
    if(done[l.id])delete done[l.id];else done[l.id]=true;
    saveDone();renderNav();$('#cbox').innerHTML=completeBtn(l);
  }
  else if(a==='copy'){
    var code=t.closest('figure').querySelector('pre code');
    var reset=function(label){t.textContent=label;setTimeout(function(){t.textContent='Copy';},1600);};
    var select=function(){
      var r=document.createRange();r.selectNodeContents(code);
      var s=window.getSelection();s.removeAllRanges();s.addRange(r);
      reset('Selected');
    };
    try{navigator.clipboard.writeText(code.textContent).then(function(){reset('Copied');},select);}catch(err){select();}
  }
});

/* ---------- routing ---------- */
function route(first){
  var id=location.hash.replace('#','');
  var i=0;
  LESSONS.forEach(function(l,k){if(l.id===id)i=k;});
  show(i,first);
  closeNav();
}
window.addEventListener('hashchange',function(){route(false);});

/* ---------- drawer ---------- */
function openNav(){document.body.classList.add('nav-open');scrim.hidden=false;menu.setAttribute('aria-expanded','true');}
function closeNav(){document.body.classList.remove('nav-open');scrim.hidden=true;menu.setAttribute('aria-expanded','false');}
menu.addEventListener('click',function(){document.body.classList.contains('nav-open')?closeNav():openNav();});
scrim.addEventListener('click',closeNav);
document.addEventListener('keydown',function(e){if(e.key==='Escape')closeNav();});
$('#q').addEventListener('input',function(e){filter=e.target.value;renderNav();});

/* ---------- theme ---------- */
var root=document.documentElement, mq=window.matchMedia('(prefers-color-scheme: dark)');
function effective(){var t=root.getAttribute('data-theme');return t||(mq.matches?'dark':'light');}
function themeLabel(){$('#theme').textContent=effective()==='dark'?'Light mode':'Dark mode';}
try{var st=localStorage.getItem('javatutor-theme');if(st==='dark'||st==='light')root.setAttribute('data-theme',st);}catch(e){}
$('#theme').addEventListener('click',function(){
  var n=effective()==='dark'?'light':'dark';
  root.setAttribute('data-theme',n);
  try{localStorage.setItem('javatutor-theme',n);}catch(e){}
  themeLabel();
});
if(mq.addEventListener)mq.addEventListener('change',themeLabel);
themeLabel();

route(true);
})();
</script>

</body>
</html>
