<template>
  <div>
    <ul>
      <li v-for="(emoji, key) in emojis" :key="key">
        {{ key }} - <img :src="emoji" alt="emoji" />
      </li>
    </ul>
  </div>
</template>

<script>
import emojiJson from "../emoji.json";

export default {
  name: 'EmojiPicker',
  data() {
    return {
      emojis: emojiJson
    };
  }
};
</script>

