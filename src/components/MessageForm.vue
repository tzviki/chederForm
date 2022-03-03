<template>
  <form v-if="notSubmitted" @submit.prevent="handleSubmit">
      <label>Name</label>
      <input type="text" name="" id="" v-model="name">
      <label>Message</label>
      <p>
        <textarea name="" id="" required v-model="message"></textarea>
      </p>
      <label>Question for</label>
      <select v-model="recipient">
          <option value="Rabbi Baumgarten">Rabbi Baumgarten</option>
          <option value="Rabbi Chazzan">Rabbi Chazzan</option>
          <option value="Board">Board</option>
      </select>
      <div class="submit"><button>Submit</button></div>
  </form>
  <h1 v-else>Thank you for your submission!</h1>
</template>

<script>
export default {
    data() {
        return {
            name: '',
            message: '',
            recipient: 'Board',
            notSubmitted: true
        }
    },
    methods: {
        handleSubmit() {
            this.notSubmitted = false;
            var str = JSON.stringify({
                    name: this.name,
                    message: this.message,
                    recipient: this.recipient
                });
                console.log(str);
            const res = fetch('https://api.pumble.com/workspaces/6216e83055f715369cc0707a/incomingWebhooks/postMessage/6216e83055f715369cc0707d/ethcCDMBj4YDfffcrDLx9v5f', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ text: str })
            });
            return res;
        }
    }
}
</script>

<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }

    textarea {
        width: 100%;
        min-height: 200px;
    }

    label {
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }

    input, select {
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }

    button {
        background: #0b6dff;
        border: 0;
        padding: 10px 20px;
        margin-top: 20px;
        color: white;
        border-radius: 20px;
    }

    .submit {
        text-align: center;
    }

</style>