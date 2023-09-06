<script setup>
import { ref,} from 'vue'

const win_player1 = ref(0)
const draw_player1 = ref(0)
const loss_player1 = ref(0)

const win_player2 = ref(0)
const draw_player2 = ref(0)
const loss_player2 = ref(0)



const control_game = {
	'ค้อน': {
		'ค้อน': 'เสมอ',
		'กระดาษ': 'แพ้',
		'กรรไกร': 'ชนะ',
    'ความรัก': 'แพ้'
	},
	'กระดาษ': {
		'ค้อน': 'ชนะ',
		'กระดาษ': 'เสมอ',
		'กรรไกร': 'แพ้',
    'ความรัก': 'แพ้'
	},
	'กรรไกร': {
		'ค้อน': 'แพ้',
		'กระดาษ': 'ชนะ',
		'กรรไกร': 'เสมอ',
    'ความรัก': 'แพ้'
	},
  'ความรัก': {
		'ค้อน': 'ชนะ',
		'กระดาษ': 'ชนะ',
		'กรรไกร': 'ชนะ',
    'ความรัก': 'เสมอ'
	}

}



const player1 = ref('');
const player2 = ref('');
const result = ref('');

const img = {
  'ค้อน': '/src/assets/hammer.svg',
  'กระดาษ': '/src/assets/paper.svg',
  'กรรไกร': '/src/assets/scissors.svg',
  'ความรัก':'/src/assets/hearts.svg'
};



function getRandomChoice() {
  const choices = ['ค้อน', 'กระดาษ', 'กรรไกร','ความรัก'];
  return choices[Math.floor(Math.random() * choices.length)];
}

function display_answer() {
  player1.value = getRandomChoice();
  player2.value = getRandomChoice();

  const out_result = control_game[player1.value][player2.value];

  if (out_result === 'ชนะ') {
    win_player1.value++;
    loss_player2.value++;
    result.value = 'Player 1 ชนะ';
  } else if (out_result === 'แพ้') {
    win_player2.value++;
    loss_player1.value++;
    result.value = 'Player 2 ชนะ';
  } else {
    draw_player1.value++;
    draw_player2.value++;
    result.value = 'เสมอ';
  }
}

function reset_round() {
  player1.value = '';
  player2.value = '';
  result.value = '';
  win_player1.value = 0;
  draw_player1.value = 0;
  loss_player1.value = 0;
  win_player2.value = 0;
  draw_player2.value = 0;
  loss_player2.value = 0;
}

</script>

<template>

    <div class="box_title">
			<h1 class="text_title">เกมเป่ายิ๊งฉุบเดิมพัน </h1>
      </div>

      <div class="contrainer_game">
        <div class="box1" id="play1">
          <img v-if="player1" :src="img[player1]" alt="ผู้เล่นที่1 เลือก" class="img"/><br>
          ผู้เล่นที่1 เดิมพันด้วย: {{ player1 }}
        </div>
        <div class="box2" id="play2">
          <img v-if="player2" :src="img[player2]" alt="ผู้เล่นที่2 เลือก" class="img" /><br>
          ผู้เล่นที่2 เดิมพันด้วย : {{ player2 }}
        </div>
      </div>

    <div class="start_buttom">
      <button @click="display_answer" class="buttom_start"> เป่ายิ๊งฉุบบบบบ </button>
    </div>

  <div class="contrainer_all_score"> 
    <div class="contrainer_score">
      <div class="box_score"> ผู้เล่นที่1 ชนะ <br> {{ win_player1 }}  </div>  
      <div class="box_score"> ผู้เล่นที่1 แพ้ <br> {{ loss_player1 }} </div>
      <div class="box_score"> เสมอ <br>{{ draw_player1 }} </div>
    </div>
    <div class="contrainer_score">
      <div class="box_score"> ผู้เล่นที่2 ชนะ <br> {{ win_player2 }}  </div>  
      <div class="box_score"> ผู้เล่นที่2 แพ้ <br> {{ loss_player2 }} </div>
      <div class="box_score"> เสมอ <br>{{ draw_player2 }} </div>
    </div>
  </div> 
    <div class="box_newgame">
      <button @click="reset_round" class="buttom_new"> เริ่มเกมใหม่ </button>
    </div>
   

</template>

<style>

@import url('https://fonts.googleapis.com/css2?family=Chakra+Petch:wght@600&family=IBM+Plex+Sans+Thai:wght@400;600&family=Noto+Sans+Thai:wght@300&family=Taviraj:ital,wght@0,200;0,600;1,500&display=swap');



/*ALl body*/
:root {
  font-family: 'IBM Plex Sans Thai', sans-serif;
  font-size: 24px;
  line-height: 1.5;
  font-weight: 400;
  background-image: linear-gradient(to right, #0f0c29, #302b63, #24243e);

  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-text-size-adjust: 100%;

}

#app {
  max-width: 1280px;
  margin:  auto;
  padding: 1rem;
  text-align: center;
}

*{
  padding: 10px;
}


/*background*/

.contrainer_game{
  display: grid;
  grid-template-columns: 1000fr 1000fr;
  margin-left: 300px;
  margin-right: 250px;
  padding: 20px;
  justify-content: space-between;
}

.img {
  width: 140px;
  height: 140px; 
}


.contrainer_score{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}

.contrainer_all_score{
  border:2px solid white;

  margin-left: 50px;
  margin-right: 50px;
}


.text_title{
  width: 500px;
  height: 70px;
  border-radius: 50px;
  margin: auto; 
  display: flex;
  align-items: center;
  justify-content: center;  
  font-size: 32px;

}


.buttom_new{
  padding: 20px;
  width: 7rem;
  height: 2.5rem;
  background-image: radial-gradient(circle farthest-side, #fceabb, #f8b500);
  border-radius: 8px;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  color: #242424;
  cursor: pointer;
  transition: border-color 0.25s;
}

.buttom_new:hover{
  box-shadow: 0 3px 6px rgb(0, 0, 0.16),
  0 3px 6px rgb(0, 0, 0.23);
  transform:translate(0px, -8px) ;
  transition: 0.4s;
  padding: 15px;
  border: 2px solid var(--text--color);
  background-image: linear-gradient(to right, #0f0c29, #302b63, #24243e);
  color: rgb(232, 134, 13);


}


.buttom_start:hover{
  box-shadow: 0 3px 6px rgb(0, 0, 0.16),
  0 3px 6px rgb(0, 0, 0.23);
  transform:translate(0px, -8px) ;
  transition: 0.4s;
  padding: 15px;
  border: 2px solid var(--text--color);
  background-image: linear-gradient(to right, #0f0c29, #302b63, #24243e);
  color: rgb(232, 134, 13);
}


.buttom_start{
  padding: 20px;
  width: 9rem;
  height: 2.5rem;
  background-image: radial-gradient(circle farthest-side, #fceabb, #f8b500);
  border-radius: 8px;
  border: 1px solid transparent;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  color: #242424;
  cursor: pointer;
  transition: border-color 0.25s;
}

.box_newgame,.start_buttom{
  display: flex;
  justify-content: center;
  align-items: center; 
  margin-top: 20px;
}

</style>