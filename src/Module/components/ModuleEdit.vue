<template>
  <v-container class="module-edit">
    <div class="module-edit__container">
      <v-card>
        <v-card-title>
          Participants Progress
          <v-spacer></v-spacer>
          <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Search"
            single-line
            hide-details
            color="#78BFDB"
          ></v-text-field>
        </v-card-title>
        <v-data-table
          :headers="headers"
          :items="participantName"
          :search="search"
        >
        <template v-slot:item.icons="">
          <v-icon color="#A4D3E2">mdi-open-in-new</v-icon>
        </template>
          </v-data-table>
      </v-card>
      <br/>
      <br/>
      <br/>
      <div class="editTitle">
        <h2 class="field center">EDIT/ADD LINKS</h2>
      </div>
        <v-card max-width="600px" v-for="(item,i) in count" :key="i">
          <v-btn color="#78BFDB" fab x-small dark style="top: 5px; left:550px;">
            <v-icon>mdi-pencil</v-icon>
          </v-btn>
          <v-btn text icon color="grey lighten-1" x-large style="top: 4px; left:460px;"
          @click="deleteLink(i)">
            <v-icon>mdi-delete</v-icon>
          </v-btn>
            <h2 style="font-weight: 500; font-size: 18px; color:#00000; padding-left: 20px;
            padding-top: 0px; padding-right: 20px; margin-top:-20px;">
            Link {{ i + 1 }} - {{linkDescriptions[i]}}:</h2>
          <div class="link">
            <h3 style="font-weight: 300; font-size: 16px; text-decoration-line: underline;
            color:#3C9CCC; padding-left: 20px; padding-right: 20px;">
            {{hyperLinks[i]}}</h3>
          </div>
          <br/>
        </v-card>
        <v-btn class="addLink" fab dark color="#78BFDB" style="bottom: -20px; left:520px;"
        @click="showForm">
          <v-icon dark>mdi-file-plus</v-icon>
        </v-btn>
      <div class="addLinkForm" style="width:80%; padding-left:100px;">
        <v-btn v-if="showLinkForm" text icon color="grey darken-1" style="left:340px; bottom:23px;"
        @click="closeForm()">
          <v-icon>mdi-close</v-icon>
        </v-btn>
        <v-form ref="form" v-model="valid" lazy-validation v-if="showLinkForm">
          <v-text-field
            label="Link Description"
            :rules="descriptionRules"
            required
            v-model="linkDescription"
            color="#78BFDB"
          ></v-text-field>
          <v-textarea
            label="Hyperlink"
            :rules="linkRules"
            required
            v-model="hyperLink"
            color="#78BFDB"
            auto-grow
          ></v-textarea>
          <div class="field center" style="padding-left:140px;">
            <v-btn color="#78BFDB" large  @click="addLink" :disabled="!valid">
              <p class="buttonText">Submit</p>
            </v-btn>
          </div>
        </v-form>
      </div>
    </div>
  </v-container>
</template>

<script lang="ts">
import Vue from 'vue';
// import gql from 'graphql-tag';

export default Vue.extend({
  name: 'ModuleEdit',
  apollo: {
  },
  data() {
    return {
      valid: true,
      linkDescription: '',
      hyperLink: '',
      linkDescriptions: [],
      descriptionRules: [
        (v) => !!v || 'Link description is required',
        (v) => (v && v.trim().length !== 0) || 'Link description is required',
      ],
      hyperLinks: [],
      linkRules: [
        (v) => !!v || 'Hyperlink is required',
        (v) => (v && v.trim().length !== 0) || 'Hyperlink is required',
      ],
      count: 0,
      showLinkForm: false,
      search: '',
      headers: [
        {
          text: 'PARTICIPANT NAME',
          align: 'start',
          sortable: false,
          value: 'name',
        },
        { text: 'LINKS READ', value: 'numberOfLinks' },
        { text: 'EMAIL TEMPLATE LINKS', value: 'templateLinks' },
        { text: '', value: 'icons', sortable: false },
      ],
      participantName: [
        {
          name: 'Participant Name 1',
          numberOfLinks: '3/3',
          templateLinks: 'P1’s Email Templates',
        },
        {
          name: 'Participant Name 2',
          numberOfLinks: '3/3',
          templateLinks: 'P2’s Email Templates',
        },
        {
          name: 'Peter Parker',
          numberOfLinks: '2/3',
          templateLinks: 'Peter P.’s Email Templates',
        },
        {
          name: 'Tom Holland',
          numberOfLinks: '1/3',
          templateLinks: 'Tom H.’s Email Templates',
        },
        {
          name: 'Marie Jane',
          numberOfLinks: '3/3',
          templateLinks: 'Marie J’s Email Templates',
        },
        {
          name: 'Zendaya Coleman',
          numberOfLinks: '2/3',
          templateLinks: 'Zendaya C.’s Email Templates',
        },
        {
          name: 'Harry Potter',
          numberOfLinks: '2/3',
          templateLinks: 'Harry P.’s Email Templates',
        },
        {
          name: 'Hermione Granger',
          numberOfLinks: '3/3',
          templateLinks: 'Hermione G.’s Email Templates',
        },
        {
          name: 'Emma Watson',
          numberOfLinks: '1/3',
          templateLinks: 'Emma W.’s Email Templates',
        },
        {
          name: 'Ron Weasley',
          numberOfLinks: '1/3',
          templateLinks: 'Ron W.’s Email Templates',
        },
      ],
    };
  },
  methods: {
    showForm() {
      this.showLinkForm = true;
    },
    closeForm() {
      this.showLinkForm = false;
    },
    validate() {
      console.log('value of valid before', this.valid);
      this.$refs.form.validate();
      console.log('value of valid after', this.valid);
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    },
    addLink() {
      this.validate();
      if (this.linkDescription.trim().length === 0 || this.hyperLink.trim().length === 0) {
        this.valid = false;
        this.validate();
      }
      if (this.valid) {
        this.linkDescriptions[this.count] = this.linkDescription;
        this.hyperLinks[this.count] = this.hyperLink;
        this.count += 1;
        this.showLinkForm = false;
        this.linkDescription = '';
        this.hyperLink = '';
        this.resetValidation();
      }
    },
    deleteLink(index) {
      console.log('deleteLink index=', index);
      console.log('count before', this.count);
      if (index > -1) {
        this.linkDescriptions.splice(index, 1);
        this.hyperLinks.splice(index, 1);
        this.count -= 1;
        console.log('count after', this.count);
      }
    },
  },
});
</script>

<style>
.module-edit__container {
  max-width: 600px;
  width:100%;
}
h1.field.center{
 text-align: margin-left;
 font-size: 20px !important;
 font-family: 'Raleway', sans-serif !important;
 font-weight: 600 !important;
 padding-right: 100px;
}
h2.field.center{
 text-align: margin-left;
 color: rgba(0, 0, 0, 0.86);
 font-size: 20px !important;
 font-family: 'Raleway', sans-serif !important;
 font-weight: 600 !important;
 padding-left: 20px;
 padding-bottom: 5px;
}
/* i.v-data-table{
 width: 300px;
 display: -webkit-box;
 -webkit-box-orient: vertical;
 -webkit-line-clamp: 2;
 overflow: hidden;
} */
i.v-icon.nontranslate.mid.mdi-pencil{
  position:absolute;
  bottom:-2px;
  left:-7px;
  font-size:25px;
};
form.v-form {
  width: 60%;
}
.v-sheet.v-card {
  border-radius: 0px !important;
}
</style>
