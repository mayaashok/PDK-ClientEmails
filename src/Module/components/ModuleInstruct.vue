<template>
<!--  TODO: make the inputs into actual components -->
  <v-container class="module-instruct">
    <div class="module-instruct__container">
      <h2 class="preview_instructions_title">INSTRUCTIONS</h2>
              <p id="instructionsBox">As you near the end of working
                on your project for your employer, use the linked tutorials,
                create your own email template, and save the templates to help you send
                emails to clients for client engagement.</p>
              <div class="circleOne">
                <p>1</p>
              </div>
              <div class="circleTwo">
                <p>2</p>
              </div>
              <div class="circleThree">
                <p>3</p>
              </div>
              <p class="instructionsOne">Click and read the links that explain how to
                create and send engaging emails to clients.
                <br/>
                <br/>
                Write an email subject line and email message
                body for a client engagement template that you will create using what
                  you learned from the links provided in Step 1.
                <br/>
                <br/>
                Save multiple versions of your email templates for your team to use
                to send client engagement emails.
                </p>
              <br/>
              <br/>
    </div>
  </v-container>
  <!-- <v-btn class="firstButton" depressed large outlined color="grey lighten-3"
      style="
            border: 1px solid #828282;
            border-radius: 10px;
            padding-top:0px;
            height: 40px;
            width: 200px;
            font-weight: 800;
            font-size: 16px;
            color:#828282 !important;">Discard</v-btn>
      <v-btn class="secondButton" depressed large outlined color="grey darken-4"
      style="
            border: 1px solid #828282;
            border-radius: 10px;
            padding-top:0px;
            height: 40px;
            width: 200px;
            font-weight: 800;
            font-size: 16px;
            color:#000000 !important;">Save</v-btn> -->

</template>

<script lang="ts">
import Vue from 'vue';
import gql from 'graphql-tag';

export default Vue.extend({
  name: 'ModuleInstruct',
  props: {
    readonly: {
      type: Boolean,
      default: false,
    },
  },
  apollo: {
  },
  data: () => ({
  }),
  methods: {
  },
});
</script>

<style>
h2.preview_instructions_title {
  font-family: 'Raleway', sans-serif;
  font-size: 15px;
  font-weight: 900;
  padding-left: 10px;
}
#instructionsBox {
  background: #FFFFFF;
  border: 1px solid #BDBDBD;
  border-radius: 10px;
  padding: 15px;
  padding-top: 10px;
  width: 500px;
  height: 110px;
  font-family: 'Raleway', sans-serif;
  /* font-style: normal; */
  font-weight: 800;
  font-size: 15px;
}
p.instructionsOne {
  background: #FFFFFF;
  border: 1px solid #FFFFFF;
  border-radius: 10px;
  padding: 15px;
  padding-top: 10px;
  width: 500px;
  height: 110px;
  font-family: 'Raleway', sans-serif;
  /* font-style: normal; */
  font-weight: 800;
  font-size: 15px;
}
.circleOne {
  position: absolute;
  left: -2%;
  top: 40%;
  width: 35px;
  height: 35px;
  border-radius: 50%;
  font-family: 'Raleway', sans-serif;
  font-weight: 800;
  font-size: 12px;
  line-height: 30px;
  color: #000000;
  text-align: center;
  background: #FFFFFF;
  border: 1px solid #BDBDBD;
}
.circleTwo {
  position: absolute;
  left: -2%;
  top: 54%;
  width: 35px;
  height: 35px;
  border-radius: 50%;
  font-family: 'Raleway', sans-serif;
  font-weight: 800;
  font-size: 12px;
  line-height: 30px;
  color: #000000;
  text-align: center;
  background: #FFFFFF;
  border: 1px solid #BDBDBD;
}
.circleThree {
  position: absolute;
  left: -2%;
  top: 73%;
  width: 35px;
  height: 35px;
  border-radius: 50%;
  font-family: 'Raleway', sans-serif;
  font-weight: 800;
  font-size: 12px;
  line-height: 30px;
  color: #000000;
  text-align: center;
  background: #FFFFFF;
  border: 1px solid #BDBDBD;
}
.v-btn.firstButton {
 left: 70px;
}
.v-btn.secondButton {
  left: 110px;
}
</style>
