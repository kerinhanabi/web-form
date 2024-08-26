<template>
    <form @submit.prevent="handleSubmit">
        <label>Email:</label>
        <input type="email" required v-model="emailInput">

        <label>Password:</label>
        <input type="password" required v-model="pswdInput">
        <div v-if="passwordError" class="error">{{ passwordError }}</div>

        <!-- selection-box -->
        <label>Role:</label>
        <select v-model="roleInput">
            <option value="developer">Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>

        <!-- Boolean checkbox-->
        <div class="terms">
            <input type="checkbox" v-model="termsInput" required>
            <label>Accept terms and conditions</label>
        </div>

        <!-- textbox input add skills-->
        <label>Skills</label>
        <input type="text" v-model="skillInput" @keyup.ctrl="addSkill"><!-- key.alt is event modifier --><!-- add in skills in skills list array with key press event like key down, key up, or key modifier like a comma, to signal the input to be taken as data etc-->
        <div v-for="skillput in skills" :key="skillput" class="pill">
            <span @click="deleteSkill(skillput)">{{ skillput }}</span>
        </div>

        <!-- normal checkbox -->
        <!--div>
            <input type="checkbox" value="adrian" v-model="nameInput">
            <label>Adrian</label>
        </div>
        <div>
            <input type="checkbox" value="jane" v-model="nameInput">
            <label>Jane</label>
        </div>
        <div>
            <input type="checkbox" value="yoshi" v-model="nameInput">
            <label>Yoshi</label>
        </div-->

        <div class="submit">
            <button>Create an Account</button>
        </div>
  </form>
  
  <p>Email: {{ emailInput }}</p>
  <p>Password: {{ pswdInput }}</p>
  <p>Role: {{ roleInput }}</p>
  <p>Terms Accepted: {{ termsInput }}</p>
  <p>Skills: {{ skills }}</p>
  <!-- output names selected -->
  <!--p>Names: {{ nameInput }}</p-->

</template>

<script>
export default {
    data() {
        return {
            emailInput: '',
            pswdInput: '',
            roleInput: 'designer',
            termsInput: false,
            //nameInput: [],
            skillInput: '',
            skills: [],
            passwordError: '',
        }
    },
    methods: {
        addSkill(e) {
            //console.log(e); //to check if the e: event-listener is picking up the input
            if (e.key === ',' && this.skillInput) {
                if (!this.skills.includes(this.skillInput)) {
                    // to check if there is anyy skill input duplicated
                    this.skills.push(this.skillInput)
                }
                this.skillInput = ''
            }
        },
        deleteSkill(skillput) {
            this.skills = this.skills.filter((item) => {
                return skillput !== item
            })
        },
        handleSubmit() {
            //validate password
            this.passwordError = this.pswdInput.length > 5 ? '' : 'Password must be at least 6 chars long'
            
            if(!this.passwordError) {
                console.log('email: ', this.emailInput)
                console.log('password: ', this.pswdInput)
                console.log('role: ', this.roleInput)
                console.log('skills: ', this.skills)
                console.log('terms accepted: ', this.termsInput)
            }
            //console.log("form submitted!")
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
    display: inline-block;
    padding: 15px 0 25px;
    color: #aaa;
    font-size: 16px;
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
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}

div.terms label{
    font-weight: normal;
    font-size: 14px;
}
.pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}
.submit {
    text-align: center;
}
.submit button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: #fff;
    border-radius: 20px;
    font-size:18px;
}
.error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 16px;
    font-weight: bold;
}
</style>