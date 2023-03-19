<template>
    <div class="chatbot">
        <input 
            class="chatbot__input"
            v-model="message"
            @keyup.enter="submitMessage"
            placeholder="Inserisci il tuo messaggio" />
        <button
            class="chatbot__button" 
            @click="submitMessage">Invia</button>
        <p class="chatbot__response">{{ response }}</p>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    data() {
        return {
            message: '',
            response: ''
        }
    },
    methods: {
        async submitMessage() {
            try {
                const result = await axios.post('/api/chatbot', { message: this.message });
                this.response = result.data.response;
            } catch (error) {
                console.error('Error: ', error);
            }
        }
    },
}
</script>

<style scoped>
.chatbot {
  display: flex;
  flex-direction: column;
  align-items: center;
  max-width: 400px;
  margin: 0 auto;
  padding: 2rem;
  font-family: Arial, sans-serif;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  border-radius: 5px;
}

.chatbot__input {
  width: 100%;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.chatbot__button {
  width: 100%;
  margin-top: 1rem;
  padding: 0.5rem;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.chatbot__button:hover {
  background-color: #2980b9;
}

.chatbot__response {
  margin-top: 1rem;
  text-align: center;
}
</style>