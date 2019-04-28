<template>
  <div class="hello">
    <div class="holder">
      <form @submit.prevent="addSkill">
        <input
          type="text"
          placeholder="Enter a skill you have..."
          v-model="skill"
          v-validate="'min:5'"
          name="skill"
        >

        <transition
          name="alert-in"
          enter-active-class="animated flipInX"
          leave-active-class="animated flipOutX"
        >
          <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill')}}</p>
        </transition>
      </form>

      <ul>
        <transition-group
          name="list"
          enter-active-class="animated bounceInUp"
          leave-active-class="animated bounceOutUp"
        >
          <li v-for="(data, index) in skills" :key="index">
            {{ data.skill }}
            <i class="fas fa-minus-circle" v-on:click="remove(index)"></i>
          </li>
        </transition-group>
      </ul>

      <p v-if="skills.length > 1">These are the skills that you possess.</p>
      <p v-if="skills.length === 0">Enter a skill to get started :)</p>
      <p v-if="skills.length === 1">This is the skill that you posess.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Skills",
  data() {
    return {
      skill: "",
      skills: []
    };
  },
  mounted() {
    if (localStorage.getItem("skill")) {
      try {
        this.skills = JSON.parse(localStorage.getItem("skill"));
      } catch (e) {
        localStorage.removeItem("skill");
      }
    }
  },
  methods: {
    saveSkills() {
      const parsed = JSON.stringify(this.skills);
      localStorage.setItem("skill", parsed);
    },
    addSkill() {
      this.$validator.validateAll().then(result => {
        if (result) {
          this.skills.push({ skill: this.skill });
          this.skill = "";
          this.saveSkills();
        } else {
          console.log("Not valid");
        }
      });
    },
    remove(id) {
      this.skills.splice(id, 1);
      this.saveSkills();
    }
  }
};
</script>

<style scoped>
@import "https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.min.css";
@import "https://use.fontawesome.com/releases/v5.8.1/css/all.css";

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
  background-color: #e0edf4;
  border-left: 5px solid #3eb3f6;
  margin-bottom: 2px;
  color: #3e5252;
}

p {
  text-align: center;
  padding: 30px 0;
  color: gray;
}

.container {
  box-shadow: 0px 0px 40px lightgray;
}

form {
  position: relative;
}

input {
  width: calc(100% - 40px);
  border: 0;
  padding: 20px;
  font-size: 1.3em;
  background-color: #323333;
  color: #687f7f;
}

.alert {
  background: #fdf2ce;
  font-weight: bold;
  display: inline-block;
  padding: 5px;
  margin-top: -20px;
  position: absolute;
  bottom: 0;
  right: 0;
}

i {
  float: right;
  cursor: pointer;
  transition: opacity 0.3s;
}

i:hover {
  opacity: 0.5;
}
</style>
