<template>
    <div class="card" @click="card.toggle = !card.toggle" v-bind:class="{ isFlipped: card.toggle }">
        <div class="card__face card__face--front">
            <div class="number">{{cardNumber}}</div>
            <div class="question">{{card.question}}</div>
            <div class="options" >
                <div v-for="(answer, i) in card.choices" :key="i">{{answer}}</div>
            </div>
        </div>
        <div class="card__face card__face--back">
            <div class="answer">Answer: {{card.answer}}</div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        card: Object,
        cardNumber: Number
    }
};
</script>

<style lang="scss">
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

    &.isFlipped {
        transform: rotateY(180deg);
    }

    &__face {
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

        &--front {
            font-size: 1.5em;
            display: flex;
            flex-direction: column;
            justify-content: space-around;
        }

        &--back {
            background: #fffce1;
            color: #4e4a36;
            transform: rotateY(180deg);
            font-size: 1.5em;
            display: flex;
            flex-direction: column;
            justify-content: space-around;
            padding: 20px;
        }
    }
}

.question {
    text-align: center;
}
.options {
    text-align: left;
}
.answer {
    text-align: right;
    font-size: 2em;
}
</style>
