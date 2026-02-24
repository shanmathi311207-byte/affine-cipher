<!DOCTYPE html>
<html>
<head>
    <title>Shan☀️ Affine Cipher Tool</title>
</head>
<body>

<h1>🔐 Shan☀️ Affine Cipher Tool</h1>

<label>Enter Text:</label><br>
<input type="text" id="text"><br><br>

<label>Key a (coprime with 26):</label><br>
<input type="number" id="keyA"><br><br>

<label>Key b:</label><br>
<input type="number" id="keyB"><br><br>

<button onclick="encrypt()">Encrypt</button>
<button onclick="decrypt()">Decrypt</button>

<h3>Result:</h3>
<p id="result"></p>

<script>

function gcd(a,b){
    while(b!=0){
        let t=b;
        b=a%b;
        a=t;
    }
    return a;
}

function modInverse(a, m){
    a = a % m;
    for(let x=1; x<m; x++){
        if((a*x)%m==1) return x;
    }
}

function encrypt(){
    let text = document.getElementById("text").value.toUpperCase();
    let a = parseInt(document.getElementById("keyA").value);
    let b = parseInt(document.getElementById("keyB").value);
    let result = "";

    if(gcd(a,26)!=1){
        alert("Key 'a' must be coprime with 26!");
        return;
    }

    for(let i=0;i<text.length;i++){
        let char = text[i];
        if(char.match(/[A-Z]/)){
            let x = char.charCodeAt(0) - 65;
            let encrypted = (a*x + b) % 26;
            result += String.fromCharCode(encrypted + 65);
        } else {
            result += char;
        }
    }

    document.getElementById("result").innerText = result;
}

function decrypt(){
    let text = document.getElementById("text").value.toUpperCase();
    let a = parseInt(document.getElementById("keyA").value);
    let b = parseInt(document.getElementById("keyB").value);
    let result = "";

    if(gcd(a,26)!=1){
        alert("Key 'a' must be coprime with 26!");
        return;
    }

    let a_inv = modInverse(a,26);

    for(let i=0;i<text.length;i++){
        let char = text[i];
        if(char.match(/[A-Z]/)){
            let y = char.charCodeAt(0) - 65;
            let decrypted = (a_inv*(y-b+26))%26;
            result += String.fromCharCode(decrypted + 65);
        } else {
            result += char;
        }
    }

    document.getElementById("result").innerText = result;
}

</script>

</body>
</html>
