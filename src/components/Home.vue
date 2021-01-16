<template>
  <p id="titleText">{{titletext}}</p>
  <div class="main_input">
    <div class="example_span"></div>
    <input
    :disabled="isDisabled" 
    type="text"
    name="inputText"
    class="inputText"
    id="inputText"
    v-model="inputText"
    @keydown="checkValue"/>
    <div class="result">
      <p>Time : {{ totalTime / 1000 }}s</p><br>
      <p v-if="testCompleted">
        Speed : {{ wpmFormatted }} words per minute</p>
    </div>
  </div>
  <div class="btn_div">
    <button class="btn_restart" @click="restartTest">Restart</button>
    <button class="btn_home" @click="reloadPage">Go back</button>
  </div>
</template>

<script>
import Sentences from "../assets/TestSentences.json";

export default {
  data() {
    return {
      titletext: 'Complete the following text to know your speed',
      sentenceList: Sentences,
      fetchedText: "",
      inputText: "",
      timer: null,
      totalTime: 0,
      totalTimeInMin: 0,
      testCompleted: false,
      wpm: 0,
      wpmFormatted:'',
      wordsLength: 0,
      random_index: 0,
      sample_text: null,
      current_input_arr: [],
      quote_span_arr: [],
      typed_char: "",
      isDisabled: false,
      widthOfDiv: 0,
    };
  },

  mounted() {
    this.fetchSentence();
    this.startTimer();
  },

  methods: {
    startTimer() {
      this.totalTime = 0
      this.timer = setInterval(() => {
        this.totalTime += 1000;
      }, 1000);
    },

    stopTimer() {
      clearInterval(this.timer);
      this.totalTimeInMin = this.totalTime / 1000 / 60;
      this.wpm = this.wordsLength / this.totalTimeInMin;
      this.wpmFormatted = this.wpm.toFixed(0)
      this.testCompleted = true;
      this.$emit("end", this.totalTime);
      this.inputText = "";
    },

    fetchSentence() {
      document.getElementById('inputText').focus()
      this.sample_text = document.querySelector(".example_span");

      // Random number generator between 0 and 19
      this.random_index = Math.floor(Math.random() * 19);

      // Getting Type-Test sentence from the JSON File
      this.fetchedText = this.sentenceList[this.random_index].text;
      this.wordsLength = this.fetchedText.split(" ").length;

      // Splitting the text and adding a span element for each character
      this.fetchedText.split("").forEach((char) => {
        const charSpan = document.createElement("span");
        charSpan.innerText = char;
        this.sample_text.appendChild(charSpan);
      });
    },

    restartTest() {
      console.log(this.totalTimeInMin);
      this.testCompleted = false
      while (this.sample_text.hasChildNodes()) {
        this.sample_text.removeChild(this.sample_text.firstChild);
      }
      clearInterval(this.timer)
      this.inputText=''
      this.quote_span_arr = []
      this.current_input_arr = []
      this.isDisabled = false
      this.fetchSentence();
      this.startTimer();
    },

    reloadPage() {
      window.location.reload();
    },

    checkValue(e) {
      if (!(e.key === "Shift" || e.key === "Alt")) {
        this.current_input_arr.push(e.key);

        if (e.key === "Backspace") {
          this.current_input_arr.pop();
          this.current_input_arr.pop();
        }

        this.quote_span_arr = this.sample_text.querySelectorAll("span");
        this.quote_span_arr.forEach((char, index) => {
          this.typed_char = this.current_input_arr[index];

          // For null value
          if (this.typed_char == null) {
            char.classList.remove("correct_input");
            char.classList.remove("incorrect_input");
          }
          // If Correct character
          else if (this.typed_char === char.innerText) {
            char.classList.add("correct_input");
            char.classList.remove("incorrect_input");
          }
          // If incorrect character
          else {
            char.classList.add("incorrect_input");
            char.classList.remove("correct_input");
          }
        });
      }
      if (this.current_input_arr.length == this.fetchedText.length) {
        this.stopTimer()
        this.isDisabled = true
      }
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Red+Hat+Display:wght@400;500;900&display=swap");

body {
  background-color: #55c5ff;
  text-align: center;
}

span {
  font-size: 30px;
  font-family: "Red Hat Display", sans-serif;
  font-weight: 500;
}

#titleText{
  text-align: start;
  margin: 0px 15px 10px 45px;
  font-size: 24px;
}

.btn_div{
  text-align: end;
  margin-top: 24px;
  padding-right: 12px;
}

.btn_div .btn_home{
  width: 10%;
  padding: 12px;
  border-radius: 18px;
  font-size: 20px;
  font-family: 'Red Hat Display', sans-serif;
  font-weight: 700;
  background-color: white;
  border: 10px;
  color: #55c5ff;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  border-radius: 30px;
  cursor: pointer;
}


.btn_div .btn_restart{
  width: 10%;
  margin-right: 12px;
  padding: 12px;
  font-size: 20px;
  font-family: 'Red Hat Display', sans-serif;
  font-weight: 700;
  background-color: white;
  border: 10px;
  color: #55c5ff;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  border-radius: 30px;
  cursor: pointer;
}


.main_input {
  position: relative;
  margin: 0px 15px 10px 40px;
  color: black;
  border: 2px solid white;
  background-color: white;
  border-radius: 18px;
  padding: 36px;
  letter-spacing: 0.25px;
  text-align: justify;
}

.example_span {
  color: black;
  border-radius: 18px;
  letter-spacing: 0.25px;
  text-align: justify;
}

.main_input p {
  display: inline-block;
  color: black;
  font-size: 1.5em;
  margin-bottom: 0;
  margin-top: 18px;
}

.main_input .inputText{
  font-size: 24px;
  font-family: "Red Hat Display", sans-serif;
  border: none;
  width: 100%;
  padding: 4px 0;
  margin: 15px auto 0;
  box-sizing: border-box;
  border-bottom: 3px solid darkgray;
}

.main_input .inputText:focus{
  outline: none;
  border-color: #55c5ff;
}

.incorrect_input {
  color: red;
  background-color: #ffcccb;
}

.correct_input {
  color: green;
  background-color: lightgreen;
}
</style>
