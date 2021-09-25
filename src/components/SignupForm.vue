<template>
  <form @submit.prevent="handleSubmit">
      <label>Email:</label>
      <input type="email" required v-model="email">

      <label>Password:</label>
      <input type="password" required v-model="password">
      <div v-if="passwordError" class="error">
          {{ passwordError }}
      </div>

      <label>Role:</label>
      <select v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
      </select>

      <label>Skill:(Press Enter to add skill)</label>
      <input type="text" v-model="tempSkill" @keydown="addSkill">
      <div class="pill" v-for="skill in skills" @click="deleteSkill(skill)" :key="skill">
          {{ skill }}
      </div>

      <div class="terms">
          <input type="checkbox" v-model="terms" required>
          <label>Accept terms and conditions</label>
      </div>

      <div class="submit">
        <button>Create an Account</button>
      </div>

  </form>
   <p>Email: {{ email }}</p>
   <p>Password: {{ password }}</p>
   <p>Role: {{ role }}</p>
   <p>Role: {{ terms }}</p>
   <p>Skill: {{ skills }}</p>
</template>

<script>
export default {
    data(){
        return {
            email:"",
            password:"",
            role:"",
            terms:false,
            tempSkill:"",
            skills:[],
            passwordError:""
        }
    },
    methods:{
        addSkill(e){
            if(e.key === "Enter"){
                if(!this.skills.includes(this.tempSkill)){
                    this.skills.push(this.tempSkill)
                    this.tempSkill = ""
                }
                this.tempSkill = ""
            }
        },
        deleteSkill(skill){
            this.skills = this.skills.filter(skl => skl !== skill)
        },
        handleSubmit(){
            this.passwordError = this.password.length > 5 ? '' : "password must at least 5 character long"
            if(!this.passwordError){
                console.log("Email: ", this.email)
                console.log("Password: ", this.password)
                console.log("role: ", this.role)
                console.log("Skills: ", this.skills)
                console.log("terms and conditions: ", this.terms)
            }
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
  input[type="checkbox"]{
      display:inline-block;
      width:16px;
      margin:0 10px 0 0;
      position:relative;
      top:2px;
  }
  .pill{
      display:iniline-block;
      margin:20px 10px 0 0;
      padding: 6px 12px;
      background:#eee;
      border-radius:20px;
      font-size:12px;
      letter-spacing:1px;
      font-weight:bold;
      color:#777;
      cursor:pointer
  }
  button{
      background:#0b6dff;
      border:0;
      padding:10px 20px;
      margin-top:20px;
      color:white;
      border-radius:20px;
  }
  .submit{
      text-align:center;
  }
  .error{
      color:#ff0062;
      margin-top:10px;
      font: size 0.8em;
      font-weight:bold;
  }
</style>