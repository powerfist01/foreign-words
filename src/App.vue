<template>
  <div id="flashcard-app" class="container">
    <h1>Learn Foreign Words</h1>
    <hr />
    <div class="flashcard-form">
      <label for="front">Front
        <input v-model="newFront" type="text" id="front">
      </label>
      <label for="back">Back
        <input v-on:keypress.enter="addNew" v-model="newBack" type="text" id="back">
      </label>
      <button v-on:click="addNew">Add a New Card</button>
      <span v-show="error" class="error">Oops! Flashcards need a front and a back.</span>
    </div>

    <ul class="flashcard-list">
      <li
        @click="toggleCard(card)"
        v-for="(card, index) in cards"
        v-bind:key="index"
      >
        <transition name="flip">
          <p v-bind:key="card.flipped" class="card">
            {{ card.flipped ? card.back : card.front }}
            <span v-on:click="cards.splice(index, 1)" class="delete-card"
              >X</span
            >
          </p>
        </transition>
      </li>
    </ul>

    <button v-on:click="previous">Previous</button>
    
    <button v-on:click="next">Next</button>
  </div>
</template>

<script>
export default {
  data() {
    const cards = [
      {
        front: "bon voyage",
        back: "have a nice trip",
        flipped: false,
      },
      {
        front: "bona fide",
        back: "genuine",
        flipped: false,
      },
      {
        front: "carte blanche",
        back: "unlimited authority or complete freedom to act as one wishes",
        flipped: false,
      },
      {
        front: "en masse",
        back: "in a large group",
        flipped: false,
      },
      {
        front: "faux pas",
        back: "a social blunder",
        flipped: false,
      },
      {
        front: "ipso facto",
        back: "by the fact itself",
        flipped: false,
      },
      {
        front: "modus operandi",
        back: "method of operating",
        flipped: false,
      },
      {
        front: "persona non grata",
        back: "an unacceptable person",
        flipped: false,
      },
      {
        front: "prima donna",
        back: "a temperamental and conceited person",
        flipped: false,
      },
      {
        front: "pro bono",
        back: "done or donated without charge",
        flipped: false,
      },
      {
        front: "quid pro quo",
        back: "something for something, usually an equal exchange",
        flipped: false,
      },
      {
        front: "status quo",
        back: "the existing condition",
        flipped: false,
      },
      {
        front: "carpe diem",
        back: "make the most of the present time",
        flipped: false,
      },
      {
        front: "déjà vu",
        back: "the sense of having experienced the present situation before",
        flipped: false,
      },
      {
        front: "en passant",
        back: "by the way",
        flipped: false,
      },
      {
        front: "magnum opus",
        back: "the most important work of an artist, writer, etc.",
        flipped: false,
      },
      {
        front: "vis-à-vis",
        back: "in relation to; as compared with",
        flipped: false,
      },
      {
        front: "vox populi",
        back: "public opinion",
        flipped: false,
      },
      {
        front: "ad hoc",
        back: "made or done for a particular purpose",
        flipped: false,
      },
      {
        front: "masse",
        back: "group",
        flipped: false,
      },
      {
        front: "masse",
        back: "group",
        flipped: false,
      },
    ];
    return {
      cards: cards,
      newFront: "",
      newBack: "",
      error: false,
    };
  },
  methods: {
    toggleCard: function (card) {
      card.flipped = !card.flipped;
    },
    addNew: function () {
      if (!this.newFront || !this.newBack) {
        this.error = true;
      } else {
        this.cards.push({
          front: this.newFront,
          back: this.newBack,
          flipped: false,
        });
        // set the field empty
        this.newFront = "";
        this.newBack = "";
        // Make the warning go away
        this.error = false;
      }
    },
  },
};
</script>

<style>
body {
  font-family: "Montserrat", sans-serif;
  text-align: center;
}
ul {
  padding-left: 0;
  display: flex;
  flex-flow: row wrap;
}

li {
  list-style-type: none;
  padding: 10px 10px;
  transition: all 0.3s ease;
}

.container {
  max-width: 100%;
  padding: 2em;
}

.card {
  display: block;
  width: 150px;
  height: 175px;
  padding: 80px 50px;
  background-color: #51aae5;
  border-radius: 7px;
  margin: 5px;
  text-align: center;
  line-height: 27px;
  cursor: pointer;
  position: relative;
  color: #fff;
  font-weight: 600;
  font-size: 20px;
  -webkit-box-shadow: 9px 10px 22px -8px rgba(209, 193, 209, 0.5);
  -moz-box-shadow: 9px 10px 22px -8px rgba(209, 193, 209, 0.5);
  box-shadow: 9px 10px 22px -8px rgba(209, 193, 209, 0.5);
  will-change: transform;
}

li:hover {
  transform: scale(1.1);
}

li:nth-child(-n + 3) .card {
  background-color: #e65f51;
}

li:nth-child(2n + 1) .card {
  background-color: #a17de9;
}

li:nth-child(4n) .card {
  background-color: #feca34;
}

li:nth-child(5n-2) .card {
  background-color: #51aae5;
}

li:nth-child(4n + 4) .card {
  background-color: #feca34;
}

li:nth-child(-7n + 7) .card {
  background-color: #e46055;
}

.delete-card {
  position: absolute;
  right: 0;
  top: 0;
  padding: 10px 15px;
  opacity: 0.4;
  transition: all 0.5s ease;
}

.delete-card:hover,
.error {
  opacity: 1;
  transform: rotate(360deg);
}

.flip-enter-active {
  transition: all 0.4s ease;
}

.flip-leave-active {
  display: none;
}

.flip-enter,
.flip-leave {
  transform: rotateY(180deg);
  opacity: 0;
}

/* Form */
.flashcard-form {
  position: relative;
}

label {
  font-weight: 400;
  color: #333;
  margin-right: 10px;
}

input {
  border-radius: 5px;
  border: 2px solid #eaeaea;
  padding: 10px;
  outline: none;
}

button {
  border-radius: 5px;
  border: 1px solid #87cb84;
  background-color: #87cb84;
  padding: 8px 15px;
  outline: none;
  font-size: 14px;
  font-weight: 700;
  color: #fff;
  cursor: pointer;
  transition: all 0.3s ease;
}

button:hover {
  background-color: #70a66f;
}

.error {
  margin-top: 10px;
  display: block;
  color: #e44e42;
  font-weight: 600;
}
</style>
