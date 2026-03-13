<!DOCTYPE html>
<html>
<head>
<title>BhenzFlix File Sharing</title>

<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js"></script>

<style>

body{
margin:0;
font-family:Arial;
background:linear-gradient(135deg,#000000,#1a0000,#000000);
color:white;
display:flex;
justify-content:center;
align-items:center;
height:100vh;
}

.container{
background:#0d0d0d;
padding:40px;
border-radius:15px;
text-align:center;
box-shadow:0 0 20px red;
width:300px;
}

.logo{
font-size:35px;
color:#ff0000;
text-shadow:0 0 10px red,0 0 20px red;
margin-bottom:20px;
}

button{
background:#ff0000;
border:none;
padding:12px 20px;
color:white;
font-size:16px;
border-radius:8px;
cursor:pointer;
box-shadow:0 0 10px red;
}

button:hover{
background:#cc0000;
}

#link{
margin-top:20px;
word-break:break-all;
color:#00ffcc;
}

</style>
</head>

<body>

<div class="container">

<div class="logo">BhenzFlix</div>

<input type="file" id="fileInput">

<br><br>

<button onclick="uploadFile()">Upload</button>

<div id="link"></div>

</div>

<script>

const supabase = supabase.createClient(
"PASTE_PROJECT_URL",
"PASTE_PUBLIC_KEY"
)

async function uploadFile(){

const file=document.getElementById("fileInput").files[0]

const fileName=Date.now()+"_"+file.name

await supabase.storage
.from("File")
.upload(fileName,file)

const url=supabase.storage
.from("File")
.getPublicUrl(fileName).data.publicUrl

document.getElementById("link").innerHTML=
"Share link:<br>"+url

}

</script>

</body>
</html>
