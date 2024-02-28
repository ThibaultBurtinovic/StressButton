

<template>
  <div>
    <div class="homeWrapper">
      <h1>Stress Button !</h1>
      <img :class="{ 'button': !isClicked, 'buttonHide': isClicked }" id="buttonNotClicked" src="@/assets/button.svg" alt="Bouton"
        draggable="false" @click="toggleButtonClick">
      <img :class="{ 'button': isClicked, 'buttonHide': !isClicked }" src="@/assets/buttonClick.svg" alt="Bouton click"
        draggable="false"  @click="toggleButtonClick">
    </div>
    <div class="count">
      <p>Nombre de clics : {{ clickCount }}</p>
      <p>Timer : {{ timerCount }}</p>
    </div>
  </div>
</template>
  
<script>
import './home.scss';

export default {
  name: 'HomePage',
  data() {
    return {
      isClicked: false,
      clickCount: 0, // Propriété pour stocker le nombre de clics
      isCounting: false,
      timerCount: 0
    };
  },
  methods: {
    toggleButtonClick() {
      if (!this.isCounting) {
        this.isCounting = true; // Marque le début du compte
        this.startCounting();
      }
      this.isClicked = !this.isClicked;
      this.clickCount++; // Incrémente le nombre de clics à chaque clic
    },
    startCounting() {
      const timer = setInterval(() => {
        this.timerCount++; // Incrémente le temps écoulé à chaque seconde
        if (this.timerCount >= 5) {
          clearInterval(timer); // Arrête le comptage après 5 secondes
          this.isCounting = false; // Réinitialise le compte après 5 secondes
          this.clickCount = 0;
          this.timerCount = 0;
        }
      }, 1000); // Met à jour timerCount chaque seconde
    }
  }
};
</script>
  
  