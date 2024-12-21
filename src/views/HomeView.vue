<script setup lang="ts">

</script>

<template>
  <section>

    <p class="mt-3 mb-2 docs-header uppecase has-text-centered"><span>EMOJI MADNESS</span></p>

    <hr class="hr m-0">
    <div class="container">

      <div class="menu">
        <div class="tabs is-toggle is-primary is-fullwidth is-medium mb-4">
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

      <textarea class="textarea is-large mb-4" v-model="textarea"
        @focusin="(e) => { (e.target as HTMLElement).classList.add('is-primary'); }"
        @focusout="(e: Event) => (e.target as HTMLElement).classList.remove('is-primary')" placeholder="type a text"
        name="" id="" rows="10">
      </textarea>
      <button @click="doShit" class="container submit button  is-mobile max-width is-primary is-large">
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
        },
        depressed: {
          name: "😥 depressed",
          set: "😣 😥 🤧 💦 😓 😾 😵 😰 🤐",
          isActive: false
        },
        gothic: {
          name: "⛓ gothic",
          set: "♱ ✮ ☠︎ † ✧ ☆ ★ ♡ ༒ ⭑๋࣭ ✟ ♬ ♪ ☦ ✞ ✩ 🕷️ 🖤 ⛓ 💉 ✖️ ⚰️ 🕯 🗡 🔗 🎧 📓 ⛓ ☠️ 🎀 🕯️ 🍷 ♰ 🕸️ 🎀 🕷️ 🔪 💀 🗝️ 🖇️ 🎸 ✟ ✖️ 💉",
          isActive: false
        },
        love: {
          name: "💕 love",
          set: "❤️ 💕 💜 💙 💔 💖 ♥️ 💗 💛 💓 💚 🤍 🖤  💞 ❣️ 💘 🧡 💝 💟 🤎 😍  😭 🥺 🙏 ✨ 🌸 🌺 💋 😘 💦 🥰 ☺️ 🔥 🌹 😋 🦶 🦋 😊",
          isActive: false
        },
        ownSet: {
          name: "🔎 own set",
          set: '',
          isActive: false
        }
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



      currentEmojiSet = currentEmojiSet.map(e => e.trim()).filter(e => e != '');

      console.log(currentEmojiSet);

      this.textarea = currentEmojiSet[Math.floor(Math.random() * currentEmojiSet.length)] + ' ' + this.textarea.split(' ').map(e => e + ' ' + currentEmojiSet[Math.floor(Math.random() * currentEmojiSet.length)] + ' ').join('')
    }
  }
})
</script>

<style scoped>
.is-toggle .is-active a {
  background-color: var(--bulma-primary) !important;
  border-color: var(--bulma-border) !important;
}

.container {
  padding: 15px
}

* {
  box-sizing: border-box !important;
}

textarea {
  /* background-color: #092d104f; */
  /* border-width: 1px; */
  /* border-color: #7fffd46d; */
  border-radius: 12px;
  /* background-color: #002e279b; */
}
</style>
