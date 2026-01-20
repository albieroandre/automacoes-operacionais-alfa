<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Guia de Automações Operacionais</title>
<style>
body {
  font-family: Arial, sans-serif;
  background: #f5f5f5;
  color: #333;
  margin: 0;
  padding: 0;
}
.container {
  max-width: 900px;
  margin: 40px auto;
  padding: 20px;
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 6px 18px rgba(0,0,0,0.1);
}
h1, h2 {
  text-align: center;
  margin-bottom: 20px;
}
h2 {
  color: #555;
  margin-top: 40px;
}
p {
  line-height: 1.6;
}
.card {
  background: #fefefe;
  border-radius: 10px;
  padding: 20px;
  margin: 20px 0;
  box-shadow: 0 4px 10px rgba(0,0,0,0.05);
}
.button {
  padding: 12px 20px;
  font-size: 16px;
  font-weight: bold;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  margin: 10px 5px 0 0;
  transition: transform 0.2s, box-shadow 0.2s;
}
.button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 12px rgba(0,0,0,0.2);
}
.alerta { background-color: #f1c40f; color: #000; }
.smp { background-color: #3498db; color: #fff; }
.code-box {
  background: #222;
  color: #eee;
  padding: 15px;
  border-radius: 8px;
  overflow-x: auto;
  font-family: monospace;
  margin-top: 10px;
}
</style>
</head>
<body>
<div class="container">
<h1>Guia de Automações Operacionais</h1>
<p>Uso interno: automações criadas apenas como apoio operacional. Não alteram dados do sistema e não acessam banco de dados.</p>

<h2>Botões Interativos</h2>
<div class="card">
<p>Clique nos botões abaixo para executar a automação correspondente:</p>
<button class="button alerta"
onclick="(function(){
  const audio=new Audio('https://actions.google.com/sounds/v1/alarms/beep_short.ogg');
  let last=null;
  setInterval(()=>{
    const el=document.getElementById('lblTotalSMP');
    if(!el) return;
    const m=el.innerText.match(/Workflows:\s*(\d+)/);
    if(!m) return;
    const cur=parseInt(m[1]);
    if(last!==null && cur>last){
      audio.play();
      alert('Novo Workflow detectado!');
    }
    last=cur;
  },3000);
})()">🔔 Alerta Workflows</button>

<button class="button smp"
onclick="(function(){
  function copiar(texto){navigator.clipboard.writeText(texto);}
  const b=document.body.innerText;

  const smp=(b.match(/Dados SMP[\s\S]*?(\d{5,})/)||b.match(/SMP[:\s-]*?(\d{5,})/)||[])[1]||'';
  const cav=(b.match(/Cavalo\s*([A-Z0-9]+)/)||[])[1]||'';
  const car=(b.match(/Carreta\s*([A-Z0-9]+)/)||[])[1]||'';
  const ori=(b.match(/Cidade \/ UF \/ País Origem\s*([A-Z\s]+)/)||[])[1]||'';
  const des=(b.match(/Cidade \/ UF \/ País Destino\s*([A-Z\s]+)/)||[])[1]||'';

  copiar(`${smp}\t${cav}\t${car}\t${ori.trim()}\t${des.trim()}`);
  alert('Dados da SMP copiados!');
})()">📋 Copiar SMP</button>
</div>

<h2>Fluxo recomendado</h2>
<div class="card">
<p>Siga este fluxo para usar as automações:</p>
<ul>
<li>Abrir Tela do Operador</li>
<li>Clicar em 🔔 Alerta Workflows</li>
<li>Abrir SMP</li>
<li>Clicar em 📋 Copiar SMP</li>
<li>Colar os dados no controle interno</li>
</ul>
</div>

<h2>Scripts Originais (opcional)</h2>
<div class="card">
<p>Se quiser ver o código completo usado pelos botões:</p>

<div class="code-box">
// Script 1 – Alerta Workflows
javascript:(function(){
  const audio=new Audio('https://actions.google.com/sounds/v1/alarms/beep_short.ogg');
  let last=null;
  setInterval(()=>{
    const el=document.getElementById('lblTotalSMP');
    if(!el) return;
    const m=el.innerText.match(/Workflows:\s*(\d+)/);
    if(!m) return;
    const cur=parseInt(m[1]);
    if(last!==null && cur>last){
      audio.play();
      alert('Novo Workflow detectado!');
    }
    last=cur;
    },3000);
})();
</div>

<div class="code-box">
// Script 2 – Copiar SMP
javascript:(function(){
  function copiar(texto){navigator.clipboard.writeText(texto);}
  const b=document.body.innerText;

  const smp=(b.match(/Dados SMP[\s\S]*?(\d{5,})/)||b.match(/SMP[:\s-]*?(\d{5,})/)||[])[1]||'';
  const cav=(b.match(/Cavalo\s*([A-Z0-9]+)/)||[])[1]||'';
  const car=(b.match(/Carreta\s*([A-Z0-9]+)/)||[])[1]||'';
  const ori=(b.match(/Cidade \/ UF \/ País Origem\s*([A-Z\s]+)/)||[])[1]||'';
  const des=(b.match(/Cidade \/ UF \/ País Destino\s*([A-Z\s]+)/)||[])[1]||'';

  copiar(`${smp}\t${cav}\t${car}\t${ori.trim()}\t${des.trim()}`);
  alert('Dados da SMP copiados!');
})();
</div>
</div>

<p style="text-align:center; margin-top:40px;">Uso interno • Automação local • Versão finalizada • Desenvolvido por André</p>
</div>
</body>
</html>
