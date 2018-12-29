<template>
    <main id="app">
        <div class="title">vue-flashcards</div>
        <br>
        <h2 class="description">If you have ever wanted to learn something, you used flashcards. Vue Flashcards is a fun way to test your knowledge of Vue.<br>Select a topic, then pick a card.
        </h2>
        <br>
        <!--<flash-cards></flash-cards>-->
        <nav class="demo-buttons" >
            <span v-for="(button, b) in buttons" :key="b">
                <span>
                    <a :class="setClass(button)" @click="updateQuestions(button)">{{button}}</a>
                </span>
            </span>
        </nav>
        <div class="scene scene--card">
            <div class="card" @click="card.toggle = !card.toggle" v-bind:class="{ isFlipped: card.toggle }"
                 v-for="(card, i) in cards" :key="i">
                <div class="card__face card__face--front">{{i + 1}}</div>
                <div class="card__face card__face--back">
                    <div class="question">{{card.question}}</div>
                    <div class="options" >
                        <div v-for="(answer, i) in card.choices" :key="i">{{answer}}</div>
                    </div>
                    <div class="answer">Answer: {{card.answer}}</div>
                </div>
            </div>
        </div>
    </main>
</template>

<script>
import questions from '@/data/index.json';

export default {
    name: 'App',
    data() {
        return {
            toggle: false,
            cards: [],
            currentButton: ''
        };
    },
    computed: {
        buttons() {
            return Object.keys(questions);
        }
    },
    methods: {
        createInitialDeck(topic) {
            this.cards = [];

            questions[topic].forEach(item => {
                this.cards.push(item);
            });
        },
        setClass(key) {
            return key === this.currentButton ? 'currentDemo' : '';
        },
        updateQuestions(key) {
            this.currentButton = key;
            this.createInitialDeck(key);
        }
    }
};
</script>
<style>
*,
:after,
:before {
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
}
body {
    color: #fffce1;
    font-family: 'Roboto', sans-serif;
    margin: 0;
    height: 100vh;
}
#app {
    background: #b4bad2;
    height: 100%;
    overflow: auto;
    padding: 3em 2em;
    text-align: center;
}
a {
    color: #4e4a36;
    text-decoration: none;
}
a:focus,
a:hover {
    color: #c94e50;
}
.title {
    font-size: 3.75em;
    font-weight: 800;
    color: #4e4a36;
    text-transform: uppercase;
}
.description {
    font-weight: 400;
    line-height: 1.3em;
    margin: 1.2em auto 1em;
    max-width: 30em;
    font-size: 1.5em;
}
.demo-buttons {
    font-size: 1em;
    margin: 2em auto 3em;
    max-width: 1200px;
}
.demo-buttons a {
    background: #fffce1;
    border-bottom-left-radius: 20px 50px;
    border-bottom-right-radius: 20px 50px;
    border-top-left-radius: 20px 50px;
    border-top-right-radius: 20px 50px;
    cursor: pointer;
    display: inline-block;
    font-weight: 800;
    letter-spacing: 1px;
    margin: 0.75em;
    padding: 1.35em 1.1em;
    text-transform: uppercase;
    width: 15em;
}
.demo-buttons a.currentDemo {
    background: #c94e50;
    color: #fffce1;
}
.scene {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}

.card {
    width: 400px;
    max-width: 90%;
    height: 500px;
    margin: 10px 10px;
    transition: transform 1s;
    transform-style: preserve-3d;
    cursor: pointer;
    position: relative;
    box-sizing: border-box;
}

.card.isFlipped {
    transform: rotateY(180deg);
}

.card__face {
    position: absolute;
    width: 100%;
    height: 100%;
    font-weight: bold;
    border: 5px solid #4e4a36;
    border-radius: 8px;
    box-sizing: border-box;
    backface-visibility: hidden;
    font-size: 5em;
    color: #fffce1;
    background: #c94e50;
    display: flex;
    justify-content: center;
    align-items: center;
}

.card__face--back {
    background: #fffce1;
    color: #4e4a36;
    transform: rotateY(180deg);
    font-size: 1.5em;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    padding: 20px;
}
.question {
    text-align: center;
}
.options {
    text-align: left;
}
.answer {
    text-align: right;
    transform: rotateY(180deg);
    font-size: 0.75em;
}
</style>
