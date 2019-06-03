<template>
  <div class="row">
    <h1>Vidalytics Chat Test Project</h1>
    <form @submit.prevent="sendMessage">
      <div class="form-group">
        <input 
        class="form-control"
        type="text" 
        name="message" 
        v-model="message"
        id="message">
      </div>
      <div class="form-group">
        <button type="submit" class="btn btn-primary">Send</button>
      </div>
    </form>
    <div class="col-lg-6 col-md-6 col-sm-12">
      <table class="table">
        <thead>
          <td>Date & Time</td>
          <td>Message</td>
        </thead>
        <tbody>
          <tr v-for="message in messages" :key="message.id">
            <td>{{ message.datetime }}</td>
            <td>{{ message.text }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Chatbox',
  data() {
    return {
      apiEndpoint: 'http://localhost:9000/chat',
      message: 'Type something   sdfsdfsdffhere',
      messages: []
    };
  },
  methods: {
    sendMessage() {
      this.$http.post(this.apiEndpoint, {
        text: this.message
      }).then(response => {
        if (this.messages.length === 10) {
          this.messages.pop();
        }
        this.messages.unshift(response.body);
        this.message = '';
      }, response => {
        console.error(response.body);
      });
    }
  },
  mounted() {
    this.$http.get(this.apiEndpoint).then(response => {
      this.messages = response.body;
    }, response => {
      console.error(response.body);
    });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
