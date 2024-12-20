<script setup lang="ts">

</script>

<template>
  <section>
    <div class="content">
      <p class="mt-5 docs-header uppecase has-text-centered">EMOJI MADNESS</p>
    </div>

    <hr class="hr mb-0">
    <div class="container">

      <div class="menu">
        <div class="tabs is-toggle is-medium mb-4">
          <ul class="is-large">
            <li @click="tabClick(item)" v-for="item in emojiSets" :key="item.name"
              :class="{ 'is-active': item.isActive }">
              <a><span>{{ item.name }}</span></a>
            </li>
          </ul>
        </div>

        <input class="own-input input is-large mb-4" v-if="isOwnInputShown" v-model="emojiSets.ownSet.set"
          placeholder="set your own emoji map" type="text">
      </div>

      <textarea class="textarea is-large mb-4" v-model='textarea' placeholder="type a text" name="" id=""
        rows="10"></textarea>
      <button @click="doShit" class="container submit button is-outlined is-mobile max-width is-primary is-large">
        go go go!
      </button>
    </div>


  </section>

</template>

<script lang="ts">
import { defineComponent } from 'vue';
type EmojiSet = { name: string, set: string, isActive: boolean }
type EmojiSets = Record<string, EmojiSet>

export default defineComponent({
  data: () => {
    return {
      radioValue: 'default' as ('default' | 'love' | 'own' | 'gothic'),
      emojiSet: '',
      textarea: '',
      emojiSets: {
        default: {
          name: "😜 default",
          set: "😙 😅 🙁 🤔 😭 ☠️ 💬 💣 🧐 😈 💞 🙀 🤧 😴 💦 😢 ☹️ 😵 🤨 😓 💝 😬 😜 🥴 😍 😸 👺 🤣 💭 😰 💛 😹 😋 🤗 😗 💫 🤯 🙄 😐 👾 👽 💖 🙂 🥶 😒 😠 🙉 😳 😘 💟 🥺 🤍 🥳 😌 😔 🤕 🤪 👻 😝 😞 🤎 😎 🤭 😇 😻 😶 😷 😪 🥱 🤩 😧 😏 ❣️ 😨 🤠 💗 😫 🖤 😿 😤 🤖 👹 🤫 😛 🤮 🤡 😺 😲 😩 🤓 😖 😱 😕 😮 💙 🧡 😦 🗨️ 😄 🤑 💓 😁 😑 💨 🙊 🙃 💤 😯 ❤️ 🤬 💯 💌 💕 🥰 😃 🥵 🤥 💀 💔 💜 💥 💋 💘 😀 🤐 😼 😵 😀 😉 👿 🤤 😥 😆 🙈 😽 😾 😚 🤢 🤒 💩 😡 😂 😊 💢 😣 🗯️ 💚",
          isActive: true,
        } as EmojiSet,
        depressed: {
          name: "😥 depressed",
          set: "😣 😥 🤧 💦 😓 😾 😵 😰 🤐",
          isActive: false
        } as EmojiSet,
        gothic: {
          name: "⛓ gothic",
          set: "♱ ✮ ☠︎ † ✧ ☆ ★ ♡ ༒ ⭑๋࣭ ✟ ♬ ♪ ☦ ✞ ✩ 🕷️ 🖤 ⛓ 💉 ✖️ ⚰️ 🕯 🗡 🔗 🎧 📓 ⛓ ☠️ 🎀 🕯️ 🍷 ♰ 🕸️ 🎀 🕷️ 🔪 💀 🗝️ 🖇️ 🎸 ✟ ✖️ 💉",
          isActive: false
        } as EmojiSet,
        love: {
          name: "💕 love",
          set: "❤️ 💕 💜 💙 💔 💖 ♥️ 💗 💛 💓 💚 🤍 🖤  💞 ❣️ 💘 🧡 💝 💟 🤎 😍  😭 🥺 🙏 ✨ 🌸 🌺 💋 😘 💦 🥰 ☺️ 🔥 🌹 😋 🦶 🦋 😊",
          isActive: false
        } as EmojiSet,
        ownSet: {
          name: "🔎 own set",
          set: '',
          isActive: false
        } as EmojiSet
      } as EmojiSets
    }
  },

  computed: {
    isOwnInputShown: function () {
      return this.emojiSets.ownSet.isActive;
    }
  },

  methods: {
    tabClick(item: EmojiSet) {
      // set active tab
      for (const name in this.emojiSets) {
        this.emojiSets[name].isActive = false;
      }

      item.isActive = true;
    },

    doShit() {
      let currentEmojiSet: Array<string> = [];

      const splitEmoji = (string: string) => [...new (Intl as any).Segmenter().segment(string)].map(x => x.segment);

      for (const name in this.emojiSets) {
        if (this.emojiSets[name].isActive) {
          currentEmojiSet = splitEmoji(this.emojiSets[name].set);
          break;
        }
      }

      currentEmojiSet = currentEmojiSet.map(e => e.trim()).filter(e => e != '')

      this.textarea = currentEmojiSet[Math.floor(Math.random() * currentEmojiSet.length)] + ' ' + this.textarea.split(' ').map(e => e + ' ' + currentEmojiSet[Math.floor(Math.random() * currentEmojiSet.length)] + ' ').join('')
    }
  }
})
</script>

<style scoped>
.container {
  padding: 15px
}

* {
  box-sizing: border-box !important;
}
</style>
