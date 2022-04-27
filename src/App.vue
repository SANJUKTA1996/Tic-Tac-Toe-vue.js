<template>
<h1 class="text">
    <center><u> Tic Tac Toe Game</u></center>
</h1>
<div v-if="!gameOver" id="board">
    <div class="square" v-for="n in 9" v-bind:key="n" @click="clickedSquare(n)">
        {{ square[n] }}
    </div>
</div>

<div v-if="gameOver" class="btn-container">
    <div class="player-container">
        <div class="box">
            <div>
                <label for="player1">PLAYER1 </label>

                <input type="text" id="player1" placeholder="player1" name="player1" class="player-input" />
            </div>
            <div>
                <label for="player2">PLAYER2 </label>
                <input type="text" id="player2" placeholder="player2" name="player2" class="player-input" />
            </div>
        </div>
    </div>
    <div class="play_btn_container">
        <button @click="startGame()" class="play_btn">play a new game</button>
    </div>
</div>
</template>

<script>
import {
    ref
} from "vue";
export default {
    name: "App",
    setup() {
        let currentTurn = "X";
        let square = ref([]);
        let gameOver = ref(true);
        for (let i = 0; i <= 9; i++) square.value.push("empty");
        square.value[0] = "nothing";

        function clickedSquare(n) {
            if (square.value[n] !== "empty") return;
            square.value[n] = currentTurn;
            isWinner();
            isCat();
            currentTurn === "X" ? (currentTurn = "O") : (currentTurn = "X");
            console.log(currentTurn);
        }

        function isWinner() {
            const lines = [
                [1, 2, 3],
                [4, 5, 6],
                [7, 8, 9],
                [1, 4, 7],
                [2, 5, 8],
                [3, 6, 9],
                [1, 5, 9],
                [3, 5, 7],
            ];
            for (let i = 0; i < lines.length; i++) {
                const [a, b, c] = lines[i];
                if (
                    square.value[a] !== "empty" &&
                    square.value[a] === square.value[b] &&
                    square.value[a] === square.value[c]
                )
                    gameOver.value = true;
            }
        }

        function isCat() {
            let isCat = true;
            square.value.forEach((s) => {
                if (s === "empty") isCat = false;
            });
            if (isCat === true) gameOver.value = true;
        }

        function startGame() {
            /* square.value.splice(0, square.value.length);*/
            gameOver.value = false;
        }
        return {
            gameOver,
            square,
            clickedSquare,
            startGame
        };
    },
};
</script>

<style>
#board {
    background-color: gray;
    height: 600px;
    width: 600px;
    margin: 0 auto;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
}

.text {
    justify-content: center;
    color: black;
}

body {
    padding: 0;
    margin: 0;

    color: white;
    background-image: url("https://thumbs.dreamstime.com/b/white-snow-pattern-light-blue-background-patern-texture-winter-theme-35030570.jpg");

    opacity: 0.9;
    z-index: 99;
    text-align: center;

}

.square {
    width: 32.8%;
    background-color: grey;
    border: 1px solid black;
}

.play_btn_container {
    width: 100%;
    height: 100px;
    display: flex;
    justify-content: center;
}

.play_btn {
    width: 15%;
    background-color: rgb(83, 78, 78);
    padding: 7px;
    color: white;
    font-size: 22px;
    border: none;
    border-radius: 12px;
    cursor: pointer;
    box-shadow: -1px 6px 117px -17px rgba(237, 237, 10, 0.79);
    -webkit-box-shadow: -1px 6px 117px -17px rgba(237, 237, 10, 0.79);
    -moz-box-shadow: -1px 6px 117px -17px rgba(237, 237, 10, 0.79);
}

.play_btn:hover {
    color: rgb(214, 200, 200);
    background-color: rgb(114, 86, 86);
}

.box {
    width: 60%;
    height: 80%;
    background-color: rgb(83, 83, 90);
    color: antiquewhite;
    padding: 12px 20px;
    margin: 8px 0;
    /* display: inline-block; */
    /* border: 1px solid #fff; */
    border-radius: 4px;
    /* box-sizing: border-box; */
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    border-radius: 20px;
    box-shadow: -1px 6px 117px -17px rgba(237, 237, 10, 0.79);
    -webkit-box-shadow: -1px 6px 117px -17px rgba(237, 237, 10, 0.79);
    -moz-box-shadow: -1px 6px 117px -17px rgba(237, 237, 10, 0.79);
}

.player-container {
    width: 100%;
    height: 400px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.player-input {
    width: 375px;
    padding: 12px 5px 12px 13px;
    margin-bottom: 40px;
    margin-left: 25px;
    border-radius: 5px;
    font-size: 20px;
    color: gray;
}

.player-input::placeholder {
    font-size: 18px;
}

.player-input:focus {
    outline: none;
}
</style>
