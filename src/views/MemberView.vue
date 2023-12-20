<template>
  <div>
    <input type="text" v-model="inputText" placeholder="Type a message..." />
    <button @click="toggleEmojiPanel">😀</button>

    <div v-if="showEmojis" class="emoji-container">
      <span v-for="(emoji, index) in emojis" :key="index" @click="addEmojiToInput(emoji)">
        {{ emoji }}
      </span>
    </div>
  </div>
</template>

<script>
import emojiData from "../emoji.json";

export default {
  data() {
    return {
      inputText: '',
      showEmojis: false,
      emojis: emojiData.data.split(',')
    };
  },
  methods: {
    addEmojiToInput(emoji) {
      this.inputText += emoji;
      this.showEmojis = false; // 隐藏表情面板
    },
    toggleEmojiPanel() {
      this.showEmojis = !this.showEmojis;
    }
  }
};
</script>

<style>
.emoji-container {
  border: 1px solid #ccc;
  padding: 10px;
  display: flex;
  flex-wrap: wrap;
}

.emoji-container span {
  cursor: pointer;
  margin: 5px;
}
</style>
