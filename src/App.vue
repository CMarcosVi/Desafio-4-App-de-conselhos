<template>
  <div class="app">
    <h1 class="adviceNumber">ADVICE #{{ this.id }}</h1>
    <p class="advice">{{ this.advicer }}</p>
    <svg width="444" height="16" xmlns="http://www.w3.org/2000/svg">
      <g fill="none" fill-rule="evenodd">
        <path fill="#4F5D74" d="M0 8h196v1H0zM248 8h196v1H248z" />
        <g transform="translate(212)" fill="#CEE3E9">
          <rect width="6" height="16" rx="3" />
          <rect x="14" width="6" height="16" rx="3" />
        </g>
      </g>
    </svg>
    <button class="buttonProcurar" @click="procurar">
      <svg
        class="dado"
        width="24"
        height="24"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M20 0H4a4.005 4.005 0 0 0-4 4v16a4.005 4.005 0 0 0 4 4h16a4.005 4.005 0 0 0 4-4V4a4.005 4.005 0 0 0-4-4ZM7.5 18a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm0-9a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm4.5 4.5a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm4.5 4.5a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm0-9a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Z"
          fill="#1f2632"
        />
      </svg>
    </button>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      advicer: "",
      id: "",
    };
  },
  methods: {
    procurar() {
      fetch(`https://api.adviceslip.com/advice`)
        .then((r) => r.json())
        .then((r) => {
          this.advicer = r.slip.advice;
          this.id = r.slip.id;
        })
        .catch((error) => {
          console.error(error);
          this.advicer = "Desculpe, não foi possível carregar o conselho.";
        });
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Manrope:wght@800&display=swap");

* {
  font-family: "Manrope", sans-serif;
  padding: 0;
  margin: 0;
}
body {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #1f2632;
}
.app {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  background-color: hsl(217, 19%, 24%);
  border-radius: 1rem;
  padding: 2rem;
  height: 15rem;
}
.adviceNumber {
  color: #51ffa8;
  letter-spacing: 5px;
  font-size: 10px;
  text-align: center;
}
.advice {
  color: hsl(193, 38%, 86%);
  font-size: 20px;
  text-align: center;
  width: 20rem;
  height: 5rem;
  margin: 1rem;
}
.buttonProcurar {
  position: Relative;
  top: 60px;
  display: flex;
  background-color: #51ffa8;
  border: none;
  border-radius: 5rem;
  padding: 1rem;
}
.dado {
  margin: 0;
}
svg {
  margin-top: 2rem;
  z-index: 1;
}
</style>
