<!DOCTYPE html>


<html lang="fr">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1.0">


<title> MemoNINI </title>


<title> <3Kennst du NINI<3 </title>



<style>





/* 🌲 FOND FORET */


/* FOND FORET */

body {

    font-family: Arial, sans-serif;

    background-image: url("tout-savoir-sur-la-foret.jpg");

@@ -17,8 +17,6 @@ body {

    color: white;

    margin: 0;

}





/* Overlay sombre pour lisibilité */

body::before {

    content: "";

    position: fixed;

@@ -27,18 +25,13 @@ body::before {

    z-index: -1;

}




h1 {


    margin-top: 20px;


}


/* TITRE & COMPTEUR */


h1 { margin-top: 20px; }


#moves { margin-top: 10px; font-size: 18px; }




#moves {


    margin-top: 10px;


    font-size: 18px;


}





/* 🏆 IMAGE FINALE */


/* ÉCRAN DE VICTOIRE */

#winScreen {


    display: none;   /* IMPORTANT */


    display: none;

    position: fixed;

    inset: 0;

    background: rgba(0,0,0,0.85);

@@ -47,38 +40,20 @@ h1 {

    align-items: center;

    flex-direction: column;

    z-index: 999;


    animation: fadeIn 0.6s ease forwards;

}




#winScreen img {

    width: 60%;

    max-width: 600px;

    border-radius: 25px;

    box-shadow: 0 20px 50px rgba(0,0,0,0.8);

    animation: zoomIn 0.6s ease forwards;

}





@keyframes fadeIn {


    from { opacity: 0; }


    to { opacity: 1; }


}




@keyframes zoomIn {

    from { transform: scale(0.7); opacity: 0; }

    to { transform: scale(1); opacity: 1; }

}


    width: 300px;


    border-radius: 20px;


    box-shadow: 0 10px 30px rgba(0,0,0,0.6);


    animation: pop 0.6s ease forwards;


}





@keyframes pop {


    0% { transform: scale(0); opacity: 0; }


    100% { transform: scale(1); opacity: 1; }


}




/* 🎴 PLATEAU */


/* PLATEAU & CARTES */

.game-board {

    display: grid;

    grid-template-columns: repeat(4, 1fr);

@@ -90,7 +65,7 @@ h1 {

/* CARTES */

.card {

    width: 100%;


    aspect-ratio: 2 / 3;


    aspect-ratio: 2/3;

    position: relative;

    transform-style: preserve-3d;

    transition: transform 0.6s;

@@ -99,33 +74,28 @@ h1 {

    overflow: hidden;

    box-shadow: 0 8px 20px rgba(0,0,0,0.5);

}




.card.flip {

    transform: rotateY(180deg);


    animation: popCard 0.3s ease;

}




.front, .back {


.card img {

    position: absolute;

    width: 100%;

    height: 100%;


    backface-visibility: hidden;


    -webkit-backface-visibility: hidden; /* iOS */


    object-fit: cover;

    border-radius: 20px;


    backface-visibility: hidden;


    -webkit-backface-visibility: hidden;

}


.front-img { transform: rotateY(0deg); z-index:2; }


.back-img { transform: rotateY(180deg); }




.front {


    background-image: url("bbm7jpg.JPG");


    background-size: cover;


    background-position: center;


    transform: rotateY(0deg);


    z-index: 2;


}





.back {


    background-image: url("1.jpg")


    transform: rotateY(180deg);


    background-size: cover;


    background-position: center;


/* POP FLIP */


@keyframes popCard {


    0% { transform: scale(0.8); }


    50% { transform: scale(1.2); }


    100% { transform: scale(1); }

}



/* BOUTON */

@@ -138,80 +108,80 @@ button {

    cursor: pointer;

    margin-top: 20px;

}




</style>

</head>



<body>




<h1> <3Kennst du NINI<3</h1>


<h1> MeMoNINI </h1>

<div id="moves">Coups : 0</div>



<div class="game-board" id="gameBoard"></div>



<button onclick="restartGame()">Recommencer</button>




<!-- IMAGE FINALE -->


<!-- ÉCRAN DE VICTOIRE -->

<div id="winScreen">

    <h2>🌟 NINIMASTER 🌟</h2>

    <img src="victoire.jpg" alt="Victoire">


    <button onclick="restartGame()">Rejouer</button>

</div>



<script>





const images = [


    "1.jpg",


    "2.jpg",


    "3.jpg",


    "4.jpg"


    "5.jpg"


    "6.jpg"


    "7.jpg"



];





// Images des cartes


const images = ["1.jpg","2.jpg","3.jpg","4.jpg","5.jpg","6.jpg","7.jpg"];

let cardsArray = [...images, ...images];

let firstCard, secondCard;

let lockBoard = false;

let moves = 0;




// Sélecteurs

const board = document.getElementById("gameBoard");

const movesDisplay = document.getElementById("moves");

const winScreen = document.getElementById("winScreen");




function shuffle(array) {


    array.sort(() => 0.5 - Math.random());


}


// Son succès


const successSound = new Audio("success.mp3");





// Mélanger cartes


function shuffle(array){ array.sort(() => 0.5 - Math.random()); }




function createBoard() {


// Créer plateau


function createBoard(){

    board.innerHTML = "";

    shuffle(cardsArray);




    cardsArray.forEach(image => {

        const card = document.createElement("div");

        card.classList.add("card");

        card.dataset.image = image;




        const front = document.createElement("div");


        front.classList.add("front");


        // Recto unique


        const frontImg = document.createElement("img");


        frontImg.classList.add("front-img");


        frontImg.src = "bbm7jpg.JPG";




        const back = document.createElement("div");


        back.classList.add("back");


        back.style.backgroundImage = `url(${image})`;


        // Verso différent


        const backImg = document.createElement("img");


        backImg.classList.add("back-img");


        backImg.src = image;




        card.appendChild(front);


        card.appendChild(back);


        card.appendChild(frontImg);


        card.appendChild(backImg);



        card.addEventListener("click", flipCard);

        board.appendChild(card);

    });

}




function flipCard() {


    if (lockBoard) return;


    if (this === firstCard) return;


// Flip carte


function flipCard(){


    if(lockBoard) return;


    if(this === firstCard) return;



    this.classList.add("flip");




    if (!firstCard) {


        firstCard = this;


        return;


    }


    if(!firstCard){ firstCard = this; return; }



    secondCard = this;

    moves++;

@@ -220,44 +190,48 @@ function flipCard() {

    checkMatch();

}




function checkMatch() {


// Vérifier paire


function checkMatch(){

    let isMatch = firstCard.dataset.image === secondCard.dataset.image;


    if(isMatch){


        successSound.currentTime = 0;


        successSound.play();




    if (isMatch) {

        firstCard.removeEventListener("click", flipCard);

        secondCard.removeEventListener("click", flipCard);

        resetBoard();

        checkWin();

    } else {

        lockBoard = true;


        setTimeout(() => {


        setTimeout(()=>{

            firstCard.classList.remove("flip");

            secondCard.classList.remove("flip");

            resetBoard();

        }, 1000);

    }

}




function resetBoard() {


    [firstCard, secondCard, lockBoard] = [null, null, false];


}


// Réinitialiser board


function resetBoard(){ [firstCard, secondCard, lockBoard] = [null,null,false]; }




function checkWin() {


// Vérifier victoire


function checkWin(){

    const flippedCards = document.querySelectorAll(".flip");


    if (flippedCards.length === cardsArray.length) {


        winScreen.style.display = "block";


    if(flippedCards.length === cardsArray.length){


        winScreen.style.display = "flex";

    }

}




function restartGame() {


// Recommencer


function restartGame(){

    moves = 0;

    movesDisplay.textContent = "Coups : 0";

    winScreen.style.display = "none";

    createBoard();

}




// Démarrer jeu

createBoard();




</script>



</body>

