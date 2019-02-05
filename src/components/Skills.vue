<template>
  <div clas="Hello">
    <div class="holder">
      <form @submit.prevent="addSkill">
      <input type="text" placeholder="Enter skill you have" v-model="skill" v-validate="'min: 5'" name="skill"/>
      <!--<input type="checkbox" id="checkbox" v-model="checked"/>-->
        <p  class="alert" v-if="errors.has('skill')"> {{ errors.first('skill') }}</p>
      </form>
      <ul>
        <li v-for="(data, index) in skills" :key="index"> {{data.skill }}</li>
        <!--<li v-if="skills.length > 1">You have more than one skill</li>-->
        <!--<li v-else>You have one skill</li>-->
      </ul>
      <!--Skills {{ message }}, {{ name }}-->
      <!--{{ btnState ? "The button is diasbled": "The button is enabled"}}-->
      <!--<button v-on:click="changeName" v-bind:disabled="btnState"> Change Name</button>-->
      <!--<div v-bind:class="alertObject"></div>-->
      <p> These are the skills you poses</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Skills',
  props: {
    message: String
  },
  data(){
    // return {
    //   skills: [{"skill": "vue-js"}, {"skill": "front-end-developer"}],
    //   name: "coursetro",
    //   btnState: false, showAlert: true, showClass: true,
    //   alertObject: {alert: true, 'another-class': true}
    // }
    return{
      checked: false,
      skill: '',
      skills: [{"skill": "vue-js"}, {"skill": "front-end-developer"}]
    }
  },
  methods: {
    addSkill() {
    this.$validator.validateAll().then((result) =>{
    if(result){
      this.skills.push({skill: this.skill});
      this.skill = '';
    }else{
      console.log("Not valid")
    }
  })

    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<!--<style src="./Skills.css" scoped> </style>-->
<style scoped>
  /*.alert{*/
    /*background-color: yellow;*/
    /*width: 100%;*/
    /*height: 30px;*/
  /*}*/
  /*.another-class{*/
    /*border: 5px solid black;*/
  /*}*/
  .holder {
    background: #fff;
  }
  ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }

  ul li {
    padding: 20px;
    font-size: 1.3em;
    background-color: #E0EDF4;
    border-left: 5px solid #3EB3F6;
    margin-bottom: 2px;
    color: #3E5252;
  }
  p {
    text-align:center;
    padding: 30px 0;
    color: gray;
  }
  .container {
    box-shadow: 0px 0px 40px lightgray;
  }

  input {
    width: calc(100% - 40px);
    border: 0;
    padding: 20px;
    font-size: 1.3em;
    background-color: #323333;
    color: #687F7F;
  }
  .alert {
    background: yellow;
    font-weight: bold;
    display: inline-block;
    padding: 5px;
    margin-top: -20px;
  }
  .alert-in-enter-active {
    animation: bounce-in .5s;
  }
  .alert-in-leave-active {
    animation: bounce-in .5s reverse;
  }

  @keyframes bounce-in {
    0% {
      transform: scale(0);
    }
    50% {
      transform: scale(1.5);
    }
    100% {
      transform: scale(1);
    }
  }


</style>