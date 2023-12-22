<template>
  <div>
    <h1>Клавиатурный тренажер</h1>
    <p>Правильный ввод слова: {{ correctPresses }}</p>
    <p>Неправильные ввод слова: {{ wrongPresses }}</p>
    <p>Точность: {{ accuracy }}%</p>
    <h2>{{ currentWord }}</h2>
    <input v-model="typedWord" @keyup.enter="checkWord" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      words: [ "яблоко", "банан", "морковь", "собака", "слон", "цветок", "гитара", "мёд", "остров", "джаз",
        "кенгуру", "луна", "молоко", "носорог", "птица", "дождь", "солнце", "лес", "книга", "компьютер",
        "пират", "мечта", "жираф", "пианино", "радуга", "звезда", "шоколад", "волк", "кошка", "камень",
        "вода", "водопад", "молния", "музыка", "карандаш", "дом", "шапка", "стол", "поле", "зима",
        "лето", "осень", "весна", "песок", "гора", "шарик", "окно", "дверь", "автомобиль", "телевизор"],
      currentWord: '',
      typedWord: '',
      correctPresses: 0,
      wrongPresses: 0,
    };
  },
  mounted() {
    this.setRandomWord();
  },
  computed: {
    accuracy() {
      if (this.correctPresses === 0 && this.wrongPresses === 0) {
        return 100;
      }
      return ((this.correctPresses / (this.correctPresses + this.wrongPresses)) * 100).toFixed(2);
    },
  },
  methods: {
    setRandomWord() {
      const randomIndex = Math.floor(Math.random() * this.words.length);
      this.currentWord = this.words[randomIndex];
    },
    checkWord() {
      if (this.typedWord.toLowerCase() === this.currentWord.toLowerCase()) {
        this.correctPresses++;
      } else {
        this.wrongPresses++;
      }
      this.typedWord = '';
      this.setRandomWord();
    },
  },
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  background-color: #f0f0f0;
  padding: 20px;
}

h1 {
  text-align: center;
  color: #333333;
}

h2 {
  text-align: center;
  color: #888888;
  margin-bottom: 20px;
}

p {
  margin-bottom: 10px;
}

input {
  display: block;
  width: 100%;
  padding: 10px;
  font-size: 18px;
  margin-bottom: 20px;
  border: 1px solid #cccccc;
  border-radius: 5px;
}

input:focus {
  outline: none;
  border-color: #666666;
}
</style>