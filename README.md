<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FOV Central</title>

<style>
:root{
  --purple:#a100ff;
  --purple2:#6d00b8;
  --text:#fff;
}

*{box-sizing:border-box;font-family:Arial,Helvetica,sans-serif}

body{
  margin:0;
  min-height:100vh;
  background:#000;
  overflow:hidden;
}

/* ===== BOLA DO FOV ===== */
.fov-ball{
  position:fixed;
  top:50%;
  left:50%;
  transform:translate(-50%,-50%);
  width:120px;
  height:120px;
  border-radius:50%;
  border:2px solid var(--purple);
  box-shadow:
    0 0 25px var(--purple),
    inset 0 0 20px var(--purple2);
  pointer-events:none;
  opacity:0;
  transition:.15s ease;
}

/* ===== CROSSHAIR ===== */
.crosshair::before,
.crosshair::after{
  content:"";
  position:fixed;
  top:50%;
  left:50%;
  background:var(--text);
  transform:translate(-50%,-50%);
  pointer-events:none;
}

.crosshair::before{
  width:2px;
  height:16px;
}

.crosshair::after{
  width:16px;
  height:2px;
}

/* ===== PAINEL ===== */
.panel{
  position:fixed;
  bottom:20px;
  left:50%;
  transform:translateX(-50%);
  width:320px;
  background:#141414;
  border-radius:16px;
  padding:16px;
  color:#fff;
  box-shadow:0 0 35px rgba(161,0,255,.5);
}

h1{
  font-size:16px;
  text-align:center;
  margin:0 0 10px;
}

.option{
  display:flex;
  justify-content:space-between;
  align-items:center;
  margin-bottom:10px;
}

input[type=range]{
  width:100%;
}

.switch{
  position:relative;
  width:44px;
  height:22px;
}

.switch input{display:none}

.slider{
  position:absolute;
  inset:0;
  background:#333;
  border-radius:20px;
}

.slider:before{
  content:"";
  position:absolute;
  width:18px;
  height:18px;
  left:2px;
  top:2px;
  background:#fff;
  border-radius:50%;
  transition:.3s;
}

input:checked + .slider{
  background:linear-gradient(135deg,var(--purple),var(--purple2));
}

input:checked + .slider:before{
  transform:translateX(22px);
}
</style>
</head>

<body>

<div class="fov-ball" id="fov"></div>
<div class="crosshair"></div>

<div class="panel">
  <h1>FOV Central (Visual)</h1>

  <div class="option">
    <label>Mostrar FOV</label>
    <label class="switch">
      <input type="checkbox" onchange="toggleFov(this.checked)">
      <span class="slider"></span>
    </label>
  </div>

  <input type="range" min="40" max="400" value="120"
         oninput="resizeFov(this.value)">
</div>

<script>
const fov = document.getElementById("fov");

function toggleFov(on){
  fov.style.opacity = on ? "1" : "0";
}

function resizeFov(size){
  fov.style.width = size + "px";
  fov.style.height = size + "px";
}
</script>

</body>
</html>
