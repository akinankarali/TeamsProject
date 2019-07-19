<template>
  <div class="column">
    <div class="load">
      <div class="Logo-Click">
        <h4 class="Logo-Click-h" v-if="code.length < 1">Login Olmak İçin Logoya Tıklayın.</h4>
      </div>
      <div class="loading">
        <div class="loading-action" v-if="code.length != 0 && posts.length < 1">
          <hollow-dots-spinner
            :animation-duration="1000"
            :dot-size="15"
            :dots-num="3"
            color="#ff1d5e"
          />          
        </div>
        <div class="loading-text" v-if="code.length != 0 && posts.length < 1">
          <h4>Veri Bekleniyor...</h4>
        </div>
        
      </div>
    </div>

    <div v-if="posts && posts.length > 0" style="display: contents;">
      <div
        class="card"
        v-for="(post, index) in posts"
        :key="post.id"
        @click="startOpenModal(index)"
      >
        <!---Component 2-->
        <h1>{{ post.GroupName }}</h1>
        <p>Reaksiyonlar için lütfen tıklayın...</p>
      </div>
    </div>

    <modal
      v-if="selectedCardIndex > -1"
      :selectedCardIndex="selectedCardIndex[selectedCardIndex]"
      :GroupName="posts[selectedCardIndex].GroupName"
      :CalculatedReactions="posts[selectedCardIndex].CalculatedReactions"
      :TotalGroupReactions="posts[selectedCardIndex].TotalGroupReactions"
      :MaxCalculatedReaction="posts[selectedCardIndex].MaxCalculatedReaction"
      :MaxCalculatedIndex="posts[selectedCardIndex].MaxCalculatedIndex"
      :MaxMessageReactions="posts[selectedCardIndex].CalculatedReactions[posts[selectedCardIndex].MaxCalculatedIndex].MaxMessageReactions"
      :Name="posts[selectedCardIndex].CalculatedReactions[posts[selectedCardIndex].MaxCalculatedIndex].Name"
      :Reactions="posts[selectedCardIndex].CalculatedReactions[posts[selectedCardIndex].MaxCalculatedIndex].Reactions"
      :MaxMessage="posts[selectedCardIndex].CalculatedReactions[posts[selectedCardIndex].MaxCalculatedIndex].MaxMessage"
    />
  </div>
</template>

<script>
import axios from "axios";
import modal from "./Modal";
import { eventBus } from "../main";
import { HollowDotsSpinner } from "epic-spinners";
export default {
  name: "Cards",
  components: {
    modal,
    HollowDotsSpinner
  },
  props: ["MaxCalculatedIndex"],
  data() {
    return {
      posts: [],
      selectedCardIndex: -1,
      code: []
    };
  },
  methods: {
    startOpenModal(index) {
      this.selectedCardIndex = index;
    },
    closeModal() {
      this.$emit("closeModal");
    }
  },
  mounted() {
    var self = this;
    axios({
      method: "get",
      url: "http://192.168.17.186/api/Auth?code=" + this.code.code
    }).then(function(response) {
      self.posts = response.data;
      console.log("Response Data: ", response.data);
    });
  },
  created() {
    eventBus.$on("indexChanged", value => {
      this.selectedCardIndex = value;
    });

    let uri = window.location.href.split("?");
    if (uri.length == 2) {
      let vars = uri[1].split("&");
      let getVars = {};
      let tmp = "";
      vars.forEach(function(v) {
        tmp = v.split("=");
        if (tmp.length == 2) getVars[tmp[0]] = tmp[1];
      });
      this.code = getVars;
      console.log(this.code);
    }
  }
};
</script>

<style scoped>
</style>