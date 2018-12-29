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
            <card v-for="(card, i) in cards" :key="i" :card="card" :card-number="i + 1"></card>
        </div>
    </main>
</template>

<script>
import questions from '@/data/index.json';

import Card from '@/components/Card';

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
    },
    components: {
        Card
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
</style>
