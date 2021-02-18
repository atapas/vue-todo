<template>
  <div class="hello">
    <button @click="sendFeedback()">Send Feedback</button>
  </div>
</template>

<script>
import { Bugfender } from '@bugfender/sdk';
export default {
  name: 'HelloWorld',
  methods: {
    sendFeedback() {
      console.log('Sending Feedback');
      Bugfender.getUserFeedback().then((result) => {
        if (result.isSent) {
            // User sent the feedback
            // `result.feedbackURL` contains the Bugfender feedback URL
            Bugfender.info('User has sent the Feedback to Bugfender', result.feedbackURL);
        } else {
            Bugfender.warn('User feedback has not been sent.');
        }
      });
    },
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
