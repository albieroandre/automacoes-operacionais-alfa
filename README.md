<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Guia de Automações Operacionais</title>

<style>
body{
  font-family:Arial, sans-serif;
  background:#f3f4f6;
  margin:0;
  padding:20px;
}
.container{
  max-width:900px;
  margin:auto;
  background:#ffffff;
  padding:30px;
  border-radius:8px;
}
h1{color:#1f2937;}
h2{color:#2563eb;margin-top:35px;}
p,li{color:#374151;line-height:1.6;}
ul{margin-left:20px;}
pre{
  background:#111827;
  color:#e5e7eb;
  padding:15px;
  border-radius:6px;
  overflow-x:auto;
}
.step{
  background:#f9fafb;
  border-left:4px solid #2563eb;
  padding:12px;
  margin:15px 0;
}
button{
  margin-top:8px;
  padding:8px 14px;
  background:#2563eb;
  color:white;
  border:none;
  border-radius:5px;
  cursor:pointer;
}
button:hover{background:#1e40af;}
footer{
  margin-top:50px;
  font-size:12px;
  color:#6b7280;
  text-align:center;
}
</style>
</head>

<body>
<div class="container">

<h1>Guia de Automações Operacionais</h1>

<p style="background:#fff7ed;border-left:4px solid #f97316;padding:10px;">
<b>Uso interno:</b> automações criadas apenas como apoio operacional.
Não alteram dados do sistema e não acessam banco de dados.
</p>

<hr>

<h2>📌 O que é um Bookmarklet?</h2>
<p>
Bookmarklet é um pequeno script salvo como favorito no navegador.
Ao clicar nele, o script é executado diretamente na tela aberta.
</p>

<hr>

<h2>⚙️ Passo a passo – Instalação</h2>

<div class="step">
<b>1.</b> Pressione <b>Ctrl + Shift + O</b> para abrir o Gerenciador de Favoritos.
</div>

<div class="step">
<b>2.</b> Crie dois novos favoritos com os nomes:
<ul>
<li><b>🔔 Alerta Workflows</b></li>
<li><b>📋 Copiar SMP</b></li>
</ul>
</div>

<div class="step">
<b>3.</b> No campo URL, cole o script correspondente (inicia com <b>javascript:</b>).
</div>

<div class="step">
<b>4.</b> Ative a barra de favoritos com <b>Ctrl + Shift + B</b>.
</div>

<div class="step">
<b>5.</b> Uso correto:
<ul>
<li>Na <b>Tela do Operador</b>, clique em <b>🔔 Alerta Workflows</b></li>
<li>Com a <b>SMP aberta</b>, clique em <b>📋 Copiar SMP</b></li>
</ul>
</div>

<hr>

<h2>🔔 Script 1 – Alerta de Workflows</h2>

<p><b>Nome do favorito:</b> 🔔 Alerta Workflows</p>
<p><b>Quando usar:</b> durante o atendimento na Tela do Operador.</p>
<p><b>O que faz:</b> emite alerta sonoro sempre que surgir novo workflow.</p>

<pre id="workflow">
javascript:(function(){
const audio=new Audio('https://actions.google.com/sounds/v1/alarms/beep_short.ogg');
let last=null;
setInterval(()=>{
const el=document.getElementById('lblTotalSMP');
if(!el)return;
const m=el.innerText.match(/Workflows:\s*(\d+)/);
if(!m)return;
const cur=parseInt(m[1]);
if(last!==null && cur>last){
audio.play();
alert('Novo Workflow detectado!');
}
last=cur;
},3000);
})();
</pre>

<button onclick="copiar('workflow')">📋 Copiar script</button>

<hr>

<h2>📋 Script 2 – Cópia Automática da SMP</h2>

<p><b>Nome do favorito:</b> 📋 Copiar SMP</p>
<p><b>Quando usar:</b> após abrir uma SMP.</p>
<p><b>O que faz:</b> copia automaticamente os principais dados da SMP.</p>

<ul>
<li>SMP (somente números)</li>
<li>Cavalo</li>
<li>Carreta</li>
<li>Cidade de origem</li>
<li>Cidade de destino</li>
</ul>

<pre id="smp">
javascript:(function(){
function copiar(t){navigator.clipboard.writeText(t);}
const b=document.body.innerText;
const smp=(b.match(/Dados SMP\s*-\s*(\d+)/)||[])[1]||'';
const cav=(b.match(/Cavalo\s*([A-Z0-9]+)/)||[])[1]||'';
const car=(b.match(/Carreta\s*([A-Z0-9]+)/)||[])[1]||'';
const ori=(b.match(/Cidade \/ UF \/ País Origem\s*([A-Z]+)/)||[])[1]||'';
const des=(b.match(/Cidade \/ UF \/ País Destino\s*([A-Z]+)/)||[])[1]||'';
copiar(`${smp}\t${cav}\t${car}\t${ori}\t${des}`);
alert('Dados da SMP copiados!');
})();
</pre>

<button onclick="copiar('smp')">📋 Copiar script</button>

<hr>

<h2>🧭 Fluxo recomendado</h2>
<ul>
<li>Abrir Tela do Operador</li>
<li>Ativar 🔔 Alerta Workflows</li>
<li>Abrir SMP</li>
<li>Clicar 📋 Copiar SMP</li>
<li>Colar no controle interno</li>
</ul>

<footer>
Uso interno • Automação local • Versão 1.0 • Desenvolvido por André
</footer>

</div>

<script>
function copiar(id){
const texto=document.getElementById(id).innerText;
navigator.clipboard.writeText(texto);
alert("Script copiado!");
}
</script>

</body>
</html>

