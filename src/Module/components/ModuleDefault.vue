<template>
  <v-container class="module-default">
    <div class="module-default__instructions">
      <v-expansion-panels class="module-default__instructions" flat v-model="showInstructions">
        <v-expansion-panel>
          <v-expansion-panel-header v-show="showInstructions" @click="showInstructions = false"
          hide-actions class="pa-0">
            <template v-slot="{open}">
              <v-scroll-y-transition hide-on-leave>
                <div v-if="!open" class="d-flex flex-column justify-center">
                  <v-icon  class="d-flex justify-center secondary--text">
                    mdi-chevron-down
                  </v-icon>
                  <div
                  class="text-uppercase
                  font-weight-bold text-subtitle-2
                  secondary--text text-center">
                      Instructions
                  </div>
                </div>
              </v-scroll-y-transition>
            </template>
          </v-expansion-panel-header>
          <v-expansion-panel-content>
            <module-instruct readonly/>
            <div @click="showInstructions = true">
              <br/>
              <br/>
              <div class="text-uppercase
              font-weight-bold text-subtitle-2
              secondary--text text-center">
                close
              </div>
              <!-- <div class="hr"/> OPTIONAL -->
              <v-icon class="d-flex secondary--text justify-center">
                mdi-chevron-up
              </v-icon>
            </div>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>
    </div>
    <div class="module-default__container">
    </div>
    <h1 class="stepOneTitle">Step 1: Learn How to Formulate an Email to Clients</h1>
      <v-treeview selectable selected-color="#78BFDB" :items="items">
        <template v-slot:append="{ item }">
          <v-icon>
            {{ files[item.file] }}
          </v-icon>
        </template>
      </v-treeview>
      <br/>
      <br/>
    <h1 class="stepTwoTitle">Step 2: Create an Email Template</h1>
      <v-form ref="form" v-model="valid" lazy-validation>
        <v-text-field
          label="Email Template Subject"
          v-model="subject"
          :rules="subjectRules"
          required
          color="#4B97C7"
        ></v-text-field>
        <v-textarea
          label="Email Template Body"
          v-model="body"
          :rules="bodyRules"
          required
          auto-grow
          color="#4B97C7"
        ></v-textarea>
        <div class="field center">
          <v-btn :disabled="!valid" color="#78BFDB" large @click="saveTemplate">
            <p class="buttonText">Save Template</p>
          </v-btn>
        </div>
      </v-form>
      <div style="display: none;">
        <v-textarea id="hiddenTextArea" ></v-textarea>
      </div>
      <br/>
      <br/>
      <br/>
    <h1 class="stepThreeTitle">Step 3: Saving Email Templates</h1>
      <br/>
      <v-expansion-panels accordion>
        <v-expansion-panel v-for="(item,i) in count" :key="i">
          <v-expansion-panel-header>Email Template {{ i + 1 }}</v-expansion-panel-header>
            <v-expansion-panel-content>
              <div class="templateBody">
                <h2 class="subjectBox">
                  <!-- <p :id="'subjectBox' + i">{{subjects[i]}}</p> -->
<v-text-field class="savedSubject" color="blue-grey darken-2"
style="top: 10px; width:430px;" type="text" :value="subjects[i]"
:id="'subjectBox' + i"></v-text-field>
                    <!-- <v-input id="'subjectBox' + i" disabled>{{ subjects[i] }}</v-input> -->
                    <v-btn class="copySubject" text icon color="blue-grey darken-2"
                    style="left: 400px; bottom:57px;" @click="copySubjectText(i)">
                      <v-icon>mdi-content-copy</v-icon>
                    </v-btn>
                </h2>
              </div>
              <br/>
              <div class="templateBody">
                <h2 class="bodyBox">
                  <!-- <p :id="'bodyBox' + i">{{bodies[i]}}</p> -->
<v-textarea rows="15" class="savedBody" color="blue-grey darken-2" style="" type="text"
:value="bodies[i]" :id="'bodyBox' + i"></v-textarea>
                    <!-- <v-textarea disabled :id="'bodyBox' + i">{{ bodies[i] }}</v-textarea> -->
                    <v-btn class="copyBody" text icon color="blue-grey darken-2"
                    style="left: 400px; bottom:5px;" @click="copyBodyText(i)">
                      <v-icon>mdi-content-copy</v-icon>
                    </v-btn>
                </h2>
              </div>
            </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>
  </v-container>
</template>

<script lang="ts">
import Vue from 'vue';
// import gql from 'graphql-tag';
// import Clipboard from 'v-clipboard';
import Instruct from './ModuleInstruct.vue';

// Vue.use(Clipboard);

export default Vue.extend({
  name: 'ModuleDefault',
  components: {
    'module-instruct': Instruct,
  },
  apollo: {
  },
  // vuetify: new Vuetify(),
  data: () => ({
    valid: true,
    subject: '',
    body: '',
    subjects: [],
    subjectRules: [
      (v) => !!v || 'Template subject is required',
      (v) => (v && v.trim().length !== 0) || 'Template subject is required',
    ],
    bodies: [],
    bodyRules: [
      (v) => !!v || 'Template body is required',
      (v) => (v && v.trim().length !== 0) || 'Template body is required',
    ],
    count: 0,
    open: ['public'],
    files: {
      png: 'mdi-open-in-new',
    },
    items: [
      {
        id: 1,
        name: 'Importance of Emailing Clients ',
        file: 'png',
      },
      {
        id: 2,
        name: 'Creating an Email Template ',
        file: 'png',
      },
      {
        id: 3,
        name: 'Sending Emails to Clients ',
        file: 'png',
      },
    ],
    showInstructions: true,
  }),
  methods: {
    saveTemplate() {
      console.log('entered save template', this.valid);
      this.validate();
      console.log('after this.validate', this.valid);
      if (this.subject.trim().length === 0 || this.body.trim().length === 0) {
        this.valid = false;
        this.validate();
      }
      if (this.valid) {
        this.subjects[this.count] = this.subject;
        this.bodies[this.count] = this.body;
        this.count += 1;
        this.subject = '';
        this.body = '';
        this.resetValidation();
      }
    },
    validate() {
      console.log('value of valid before', this.valid);
      this.$refs.form.validate();
      console.log('value of valid after', this.valid);
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    },
    copySubjectText(i) {
      // const subjectParagraph = document.getElementById(`'subjectBox'${i}`);
      console.log('value of i =', i);
      const subjectID = `subjectBox${i}`;
      console.log('subjectID = ', subjectID);
      // const copySubject = document.getElementById(subjectID).innerHTML;
      const copyText = document.getElementById(subjectID);
      // const copySubject = this.subjects[i];
      // console.log('copySubject', copySubject);
      // document.getElementById('hiddenTextArea').value = copySubject;
      // const copyText = document.getElementById('hiddenTextArea');
      copyText.select();
      copyText.setSelectionRange(0, 99999);
      document.execCommand('copy');
      alert(`Copied the text: ${copyText.value}`);
      // alert("Copied the text: " + copyText.value);
    },
    copyBodyText(i) {
      // const subjectParagraph = document.getElementById(`'subjectBox'${i}`);
      console.log('value of i =', i);
      const bodyID = `bodyBox${i}`;
      console.log('bodyID = ', bodyID);
      // const copyBody = document.getElementById(bodyID).innerHTML;
      const copyText = document.getElementById(bodyID);
      // console.log('copyBody', copyBody);
      // document.getElementById('hiddenTextArea').value = copyBody;
      // const copyText = document.getElementById('hiddenTextArea');
      copyText.select();
      copyText.setSelectionRange(0, 99999);
      document.execCommand('copy');
      // this.$clipboard(copyText);
      alert(`Copied the text: ${copyText.value}`);
      // alert("Copied the text: " + copyText.value);
    },
  },
});
</script>

<style>
div.container.module-default {
  max-height: 3000px;
}
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
h1.stepOneTitle {
  font-family: 'Raleway', sans-serif;
  font-weight: 800;
  font-size: 25px;
  text-align: center;
  color: #404142;
}
h1.stepTwoTitle {
  font-family: 'Raleway', sans-serif;
  font-weight: 800;
  font-size: 25px;
  text-align: center;
  color: #404142;
}
p.buttonText {
  font-family: 'Raleway', sans-serif;
  color: #FFFFFF;
  padding-top: 16px;
}
.v-text-field input {
  min-width: 400px !important;
}
div.field.center {
  padding-left: 115px;
}
h1.stepThreeTitle {
  font-family: 'Raleway', sans-serif;
  font-weight: 800;
  font-size: 25px;
  text-align: center;
  color: #404142;
}
/* .v-item-group {
  max-width: 80%;
} */
div.v-item-group.theme--light.v-expansion-panels.v-expansion-panels--accordion {
  max-width: 75%;
}
div.templateBody {
  white-space: pre-wrap;
}
h2.subjectBox {
  background: #FAFAFA;
  border: 0.5px solid #D0D0D0;
  border-radius: 1px;
  padding: 10px;
  height: 50px;
  font-family: 'Raleway', sans-serif;
  font-weight: 300;
  font-size: 15px;
}
h2.bodyBox {
  background: #FAFAFA;
  border: 0.5px solid #D0D0D0;
  border-radius: 1px;
  padding: 10px;
  font-family: 'Raleway', sans-serif;
  font-weight: 300;
  font-size: 15px;
}
.v-text-field.savedSubject {
  padding-top: 0px;
  margin-top:-2px;
}
.v-textarea.savedBody {
  padding-top: 0px;
  margin-top:2px;
  padding-bottom: 0px;
  margin-bottom:-58px;
}
</style>
