<template>
  <div class="modalWrapper">
    <div class="modal">
      <!---Component 3-->
      <div class="modal-content">
        <div class="modal-header">
          <h2>{{GroupName}} Takımı'nın Reaksiyonları</h2>
          <button class="close" @click="closeModal">x</button>
        </div>
        <div class="modal-body">
          <div class="popularMessage" style="border-bottom: 2px solid #eeee;">
            <p class="popularMessageParags"> <b>En çok reaksiyon alan kişi </b>: {{ Name }}  </p>
            <p class="popularMessageParags"> <b>En çok reaksiyon alan mesaj</b> :  {{ MaxMessage }}</p>
            <div class="iconsParag popularMessageIcons">
              <img src="../assets/ReactionIcons/like.png" alt="like" class="icons" />: {{ MaxMessageReactions[0]}}
              <img src="../assets/ReactionIcons/heart.png" alt="heart" class="icons" />: {{ MaxMessageReactions[4]}}
              <img src="../assets/ReactionIcons/laugh.png" alt="laugh" class="icons" />: {{ MaxMessageReactions[3]}}
              <img src="../assets/ReactionIcons/suprise.png" alt="suprised" class="icons" />: {{ MaxMessageReactions[5]}}
              <img src="../assets/ReactionIcons/sad.png" alt="sad" class="icons" />: {{ MaxMessageReactions[2]}}
              <img src="../assets/ReactionIcons/angry.png" alt="angry" class="icons" />: {{ MaxMessageReactions[1]}}
            </div>
          </div>

          <!--- <p> Toplam reaksiyon sayısı: {{ selectedCardIndex }}</p>-->
          <p class="totalReactionParag"><b> Takımdaki toplam reaksiyon sayısı</b> : {{TotalGroupReactions[0]+TotalGroupReactions[1]+TotalGroupReactions[2]+TotalGroupReactions[3]+TotalGroupReactions[4]+TotalGroupReactions[5]}}</p>
        </div>
        <div class="modal-footer">
          <p class="iconsParag">
            <img src="../assets/ReactionIcons/like.png" alt class="icons" />: {{TotalGroupReactions[0]}}
          </p>
          <p class="iconsParag">
            <img src="../assets/ReactionIcons/heart.png" alt class="icons" />: {{TotalGroupReactions[4]}}
          </p>
          <p class="iconsParag">
            <img src="../assets/ReactionIcons/laugh.png" alt class="icons" />: {{TotalGroupReactions[3]}}
          </p>
          <p class="iconsParag">
            <img src="../assets/ReactionIcons/suprise.png" alt class="icons" />: {{TotalGroupReactions[5]}}
          </p>
          <p class="iconsParag">
            <img src="../assets/ReactionIcons/sad.png" alt class="icons" />: {{TotalGroupReactions[2]}}
          </p>
          <p class="iconsParag">
            <img src="../assets/ReactionIcons/angry.png" alt class="icons" />: {{TotalGroupReactions[1]}}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { eventBus } from "../main";

export default {
  name: "Modal",

  props: ["selectedCardIndex", "GroupName", "CalculatedReactions", "Name", "Reactions","MaxMessage", "MaxCalculatedIndex", "TotalGroupReactions", "MaxMessageReactions"],
  methods: {
    closeModal() {
      this.selectedCardIndex = -1;
      eventBus.$emit("indexChanged", this.selectedCardIndex);
    }
  }
};
</script>
 
<style scoped>
</style>
