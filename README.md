<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>ST NAYEEM LOGIN</title>

<style>
body{
  margin:0;
  font-family:Arial;
  background:#050814;
  color:white;
  display:flex;
  justify-content:center;
  align-items:center;
  height:100vh;
}

.box{
  background:#0d1328;
  padding:30px;
  border-radius:20px;
  box-shadow:0 0 20px #2f7cff55;
  width:320px;
  text-align:center;
}

input{
  width:100%;
  padding:12px;
  margin-top:10px;
  border-radius:10px;
  border:none;
  background:#111a3a;
  color:white;
  font-size:15px;
}

button{
  margin-top:15px;
  padding:12px;
  width:100%;
  border:none;
  border-radius:12px;
  background:#2f7cff;
  color:white;
  font-weight:bold;
  cursor:pointer;
  transition:.2s;
}

button:hover{
  transform:scale(1.05);
}

#msg{
  margin-top:10px;
  color:#ff6b6b;
  font-size:14px;
}

#main{
  display:none;
  text-align:center;
}

.success{
  color:#27e08a;
}
</style>
</head>

<body>

<div class="box" id="loginBox">
  <h2>ST NAYEEM ACCESS</h2>

  <input id="user" placeholder="Username">
  <input id="key" placeholder="Key">

  <button onclick="login()">ENTER</button>
  <div id="msg"></div>
</div>

<div id="main">
  <h1 class="success">✅ ACCESS GRANTED</h1>
  <p>Welcome to ST NAYEEM BOT</p>
</div>


<script>

// 🔥 Remote control file URL বসাবে এখানে
const CONTROL_URL = "https://example.com/access.json";

// Demo fallback (offline mode)
const DEMO = {
  users:[
    {user:"nayeem",key:"12345",active:true}
  ]
};


async function login(){

  const u = document.getElementById("user").value.trim().toLowerCase();
  const k = document.getElementById("key").value.trim();

  if(!u || !k){
    msg("Enter username & key");
    return;
  }

  let data;

  try{
    const res = await fetch(CONTROL_URL);
    data = await res.json();
  }catch(e){
    data = DEMO; // offline fallback
  }

  const ok = data.users.some(x =>
    x.user.toLowerCase()===u &&
    x.key===k &&
    x.active===true
  );

  if(ok){
    document.getElementById("loginBox").style.display="none";
    document.getElementById("main").style.display="block";
  }else{
    msg("Wrong or disabled");
  }
}


function msg(t){
  document.getElementById("msg").innerText=t;
}

</script>

</body>
</html>
