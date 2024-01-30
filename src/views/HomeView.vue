<script setup lang="ts">

</script>

<template>
  <section>
    <div class="container">
      <h2 class="docs-header">emoji madness</h2>

      <div class="menu">
        <label for="radio-default"><input v-model="radioValue" type="radio" value="default" id="radio-default"   name="asjkdfh">😜 default</label>
        <label for="radio-gothic"><input v-model="radioValue" type="radio" value="gothic" id="radio-gothic" name="asjkdfh">☠️ gothic</label>
        <label for="radio-love"><input v-model="radioValue" type="radio" value="love" id="radio-love" name="asjkdfh">💗 love</label>
        <label for="radio-own"><input v-model="radioValue" type="radio" value="own" id="radio-own" name="asjkdfh">🔎 own set</label>

        <input class="own-input" v-if="isOwnInputShown" v-model="emojiSet" placeholder="set your own emoji set" type="text">
      </div>
      <textarea v-model='textarea' placeholder="type a text" name="" id="" cols="30" rows="20"></textarea>
      <button @click="doShit" class="submit button button-primary">go go go!</button>
    </div>
    

  </section>
  
</template>

<script lang="ts">
  import { defineComponent } from 'vue';

  export default defineComponent({
    data: () => {
      return {
        radioValue: 'default' as ( 'default' | 'love' | 'own' | 'gothic' ),
        emojiSet: '', 
        textarea: ''
      }
    },

    computed: {
      isOwnInputShown: function() {
        return this.radioValue == 'own';
      }
    },

    methods: {
      doShit() {
        let emojiStringToArray = function (str: string) {
          let split = str.split(/([\uD800-\uDBFF][\uDC00-\uDFFF])/);
          let arr = [];
          for (var i=0; i<split.length; i++) {
            let char = split[i]
            if (char !== "") {
              arr.push(char);
            }
          }
          return arr;
        };

        let currentEmojiSet: any = [];
        const gothicPattern = "♱ ✮ ☠︎ † ✧ ☆ ★ ♡ ༒ ⭑๋࣭ ✟ ♬ ♪ ☦ ✞ ✩ 🕷️ 🖤 ⛓ 💉 ✖️ ⚰️ 🕯 🗡 🔗 🎧 📓 ⛓ ☠️ 🎀 🕯️ 🍷 ♰ 🕸️ 🎀 🕷️ 🔪 💀 🗝️ 🖇️ 🎸 ✟ ✖️ 💉";
        const defaultPattern = "😙 😅 🙁 🤔 😭 ☠️ 💬 💣 🧐 😈 💞 🙀 🤧 😴 💦 😢 ☹️ 😵 🤨 😓 💝 😬 😜 🥴 😍 😸 👺 🤣 💭 😰 💛 😹 😋 🤗 😗 💫 🤯 🙄 😐 👾 👽 💖 🙂 🥶 😒 😠 🙉 😳 😘 💟 🥺 🤍 🥳 😌 😔 🤕 🤪 👻 😝 😞 🤎 😎 🤭 😇 😻 😶 😷 😪 🥱 🤩 😧 😏 ❣️ 😨 🤠 💗 😫 🖤 😿 😤 🤖 👹 🤫 😛 🤮 🤡 😺 😲 😩 🤓 😖 😱 😕 😮 💙 🧡 😦 🗨️ 😄 🤑 💓 😁 😑 💨 🙊 🙃 💤 😯 ❤️ 🤬 💯 💌 💕 🥰 😃 🥵 🤥 💀 💔 💜 💥 💋 💘 😀 🤐 😼 😵 😀 😉 👿 🤤 😥 😆 🙈 😽 😾 😚 🤢 🤒 💩 😡 😂 😊 💢 😣 🗯️ 💚";
        const lovePattern = "❤️ 💕 💜 💙 💔 💖 ♥️ 💗 💛 💓 💚 🤍 🖤  💞 ❣️ 💘 🧡 💝 💟 🤎 😍  😭 🥺 🙏 ✨ 🌸 🌺 💋 😘 💦 🥰 ☺️ 🔥 🌹 😋 🦶 🦋 😊"

        if(this.radioValue !== 'own') {
          if(this.radioValue == 'gothic') {
            currentEmojiSet = gothicPattern.split(' ');  
          } else if(this.radioValue == 'default') {
            currentEmojiSet = defaultPattern.split(' ')
          } else if(this.radioValue == 'love') {
            currentEmojiSet = lovePattern.split(' ');
          }
        } else {
          // currentEmojiSet = emojiStringToArray(this.emojiSet) 
          currentEmojiSet = this.emojiSet.split(' ');
        }

        this.textarea = currentEmojiSet[Math.floor(Math.random() * currentEmojiSet.length)] + ' ' + this.textarea.split(' ').map(e => e + ' ' + currentEmojiSet[Math.floor(Math.random() * currentEmojiSet.length)] + ' ').join('')
      }
    }
  })
</script>

<style scoped>
  .container {
    text-align: center;
  }

  .menu label {
    display: inline-block;
    margin-right: 10px;
    margin-bottom: 10px;
  }

  input[type=text] {
    background-color: #f2f3f5;
    padding: 15px 20px;
    border: none;
    border-radius: 15px;
    font-size: 20px;
    height: 50px;
  }

  input[type=radio] {
    opacity: 0;
    width: 0;
    height: 0;
    margin: 0;
  }

  label {
    background-color: #f2f3f5;
    padding: 5px 15px;
    border-radius: 100px;
    font-weight: 500;
    font-family: helvetica;

/*height: 20px*/
  }

  label:has(input[type=radio]:checked) {
    background-color: #5865f2;
    color: white;
  }

  .menu {
    text-align: left;
  }

  .own-input {
/*    display: block;*/
    width: 100%;
  }

  textarea {
    width: 100%;
    height: 200px;
    background-color: #f2f3f5;
    padding: 15px 20px;
    border: none;
    border-radius: 15px;
    font-size: 20px;
  }

  button.submit {
    width: 100%;
    background-color: #5865f2;
    border-radius: 20px;
    border: none;
    font-size: 15px;
    height: 50px;
  }

  button.submit:hover {
    opacity: 0.8;
    background-color: #5865f2;
  }

  h2 {
    margin-top: 30px;
  }

</style>
