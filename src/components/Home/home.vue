

<template>
  <div class="home">
    <div class="homeWrapper">
      <h1>Stress Button !</h1>
      <img :class="{ 'button': !isClicked, 'buttonHide': isClicked }" id="buttonNotClicked" src="@/assets/button.svg" alt="Bouton"
        draggable="false" @click="toggleButtonClick">
      <img :class="{ 'button': isClicked, 'buttonHide': !isClicked }" src="@/assets/buttonClick.svg" alt="Bouton click"
        draggable="false"  @click="toggleButtonClick">
    </div>
    <div class="count">
      <p>Nombre de clics sec : {{ clicksPerSecond }}</p>
      <p>Timer : {{ timerCount }}</p>
    </div>
    <div  class="gauge">
        <div class="gaugeFill" :style="{ width: (clicksPerSecond * 20) + 'px' }"></div>
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
      timerCount: 0,
      clicksPerSecond: 0, // Propriété pour stocker le nombre de clics par seconde
      clicksInLastUpdate: 0
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
        this.clicksPerSecond = this.clickCount; // Met à jour le nombre de clics par seconde
        this.clickCount = 0; // Réinitialise le nombre de clics
        if (this.timerCount >= 10) {
          clearInterval(timer); // Arrête le comptage après 10 secondes
          this.isCounting = false; // Réinitialise le compte après 10 secondes
          this.timerCount = 0;
          this.clicksPerSecond = 0; // Réinitialise le nombre de clics par seconde
        }
      }, 1000); // Met à jour timerCount chaque seconde
    },
    updateClickPerSecond() {
      // Met à jour le nombre de clics par seconde toutes les 0.1 secondes
      setInterval(() => {
        this.clickPerSecond = this.clicksInLastUpdate / 0.1;
        this.clicksInLastUpdate = 0; // Réinitialise le nombre de clics depuis le dernier rafraîchissement
      }, 300);
    }
  }
};
</script>
  