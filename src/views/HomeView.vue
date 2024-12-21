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

        <input class="own-input input is-large mb-4" v-if="isOwnInputShown" @input="textareaError = false"
          @focusout="textareaError = false" :class="{ 'is-danger': textareaError }" v-model="emojiSets.ownSet.set"
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
      <button @click="changeTheme" class="mt-4 container change-theme button is-pimary is-large is-rounded">
        <svg xmlns="http://www.w3.org/2000/svg" height="20" width="15" viewBox="0 0 384 512">
          <path fill="#63E6BE"
            d="M144.7 98.7c-21 34.1-33.1 74.3-33.1 117.3c0 98 62.8 181.4 150.4 211.7c-12.4 2.8-25.3 4.3-38.6 4.3C126.6 432 48 353.3 48 256c0-68.9 39.4-128.4 96.8-157.3zm62.1-66C91.1 41.2 0 137.9 0 256C0 379.7 100 480 223.5 480c47.8 0 92-15 128.4-40.6c1.9-1.3 3.7-2.7 5.5-4c4.8-3.6 9.4-7.4 13.9-11.4c2.7-2.4 5.3-4.8 7.9-7.3c5-4.9 6.3-12.5 3.1-18.7s-10.1-9.7-17-8.5c-3.7 .6-7.4 1.2-11.1 1.6c-5 .5-10.1 .9-15.3 1c-1.2 0-2.5 0-3.7 0l-.3 0c-96.8-.2-175.2-78.9-175.2-176c0-54.8 24.9-103.7 64.1-136c1-.9 2.1-1.7 3.2-2.6c4-3.2 8.2-6.2 12.5-9c3.1-2 6.3-4 9.6-5.8c6.1-3.5 9.2-10.5 7.7-17.3s-7.3-11.9-14.3-12.5c-3.6-.3-7.1-.5-10.7-.6c-2.7-.1-5.5-.1-8.2-.1c-3.3 0-6.5 .1-9.8 .2c-2.3 .1-4.6 .2-6.9 .4z" />
        </svg>
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
      textareaError: false,
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
    changeTheme() {
      const html = document.querySelector('html');
      if (html?.getAttribute('data-theme') == 'light') {
        html.setAttribute('data-theme', 'dark')
      } else {
        html?.setAttribute('data-theme', 'light')
      }
    },

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

      if (currentEmojiSet.length === 0) {
        this.textareaError = true;
        return;
      }

      this.textareaError = false;

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
