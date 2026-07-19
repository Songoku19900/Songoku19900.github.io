<!DOCTYPE html>
<html lang="fr">

<head>

<meta charset="UTF-8">
<title>Mon Livre Secret</title>

<style>

body {

    margin:0;
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;

    background:#222;

    font-family:Georgia,serif;

}


.book {

    width:600px;
    height:450px;

}


.page {

    width:600px;
    height:450px;

    padding:40px;

    box-sizing:border-box;

    background:#fff8e7;

    box-shadow:0 10px 30px #000;

    border-radius:8px;

    text-align:center;

}



.cover {

    background:linear-gradient(135deg,#5a2600,#d2691e);

    color:white;

}



.cover h1 {

    margin-top:70px;

    font-size:45px;

}



.cover p {

    font-size:25px;

}



input {

    padding:12px;

    font-size:18px;

    border-radius:8px;

    border:none;

    text-align:center;

}



textarea {

    width:100%;

    height:280px;

    resize:none;

    border:none;

    outline:none;

    background:transparent;

    font-size:20px;

    font-family:Georgia,serif;

}



button {

    padding:12px 25px;

    margin:8px;

    background:#d2691e;

    color:white;

    border:none;

    border-radius:8px;

    cursor:pointer;

    font-size:18px;

}


button:hover {

    background:#8b4513;

}


.erreur {

    color:#ffdddd;

}


</style>


</head>



<body>



<div class="book">



<!-- COUVERTURE -->

<div class="page cover" id="couverture">


<h1>📖 Mon Histoire</h1>

<p>
Livre secret
</p>


<input 
id="codeSecret"
type="text"
placeholder="Code secret">


<br>


<button onclick="ouvrirLivre()">
🔓 Ouvrir le livre
</button>


<p id="erreur" class="erreur"></p>


</div>





<!-- PAGES DU LIVRE -->

<div class="page" id="pageLivre" style="display:none;">


<h2 id="titre">
Page 1
</h2>


<textarea 
id="texte"
placeholder="Écris ton histoire ici...">
</textarea>


<br>


<button onclick="pageAvant()">
⬅ Retour
</button>


<button onclick="pageSuivante()">
Nouvelle page ➡
</button>


</div>




</div>





<script>


let numeroPage = 1;


let couverture = document.getElementById("couverture");

let pageLivre = document.getElementById("pageLivre");

let texte = document.getElementById("texte");

let titre = document.getElementById("titre");




// OUVRIR LE LIVRE AVEC LE CODE

function ouvrirLivre(){


    let code = document.getElementById("codeSecret").value;


    if(code === "22 août"){


        couverture.style.display="none";

        pageLivre.style.display="block";


        chargerPage();


    }

    else {


        document.getElementById("erreur").textContent =
        "❌ Code incorrect";


    }


}




// CHARGER UNE PAGE

function chargerPage(){


    titre.textContent="Page "+numeroPage;


    texte.value =
    localStorage.getItem("page"+numeroPage) || "";


}




// SAUVEGARDE AUTOMATIQUE

texte.addEventListener("input",function(){


    localStorage.setItem(

        "page"+numeroPage,

        texte.value

    );


});





// PAGE SUIVANTE

function pageSuivante(){


    localStorage.setItem(

        "page"+numeroPage,

        texte.value

    );


    numeroPage++;


    chargerPage();


}




// PAGE PRECEDENTE

function pageAvant(){


    if(numeroPage > 1){


        localStorage.setItem(

            "page"+numeroPage,

            texte.value

        );


        numeroPage--;


        chargerPage();


    }


}



</script>



</body>

</html>
