<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email"/>

    <label>Password:</label>
    <input type="password" required v-model="password">
    <div class="error" v-if="passwordError">{{ passwordError }}</div>

    <label>Role:</label>
    <select v-model="role">
        <option value="Developer">Web Developer</option>
        <option value="Designer">Web Designer</option>
    </select>

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill">
    <div v-for="skill in skills" :key="skill" class="pill">
        <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>

    <div class="terms">
        <input type="checkbox" v-model="terms" required>
        <label>Accept the Terms and Conditions</label>
    </div>

    <div class="submit">
        <button>Submit</button>
    </div>

  </form>

  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms: {{ terms }}</p>
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            terms: false,
            tempSkill: '',
            skills: [],
            passwordError: '',
        };
    },
    methods: {
        addSkill(e) {
            if(e.key === ' ' && this.tempSkill) {
                if(!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill);
                };
                this.tempSkill = '';
            };
        },
        deleteSkill(skill) {
            this.skills = this.skills.filter((item) => {
                return skill !== item;
            });
        },
        handleSubmit() {
            if(this.password.length > 5) {
                this.passwordError = '';
            } else {
                this.passwordError = 'Password must be more than 5 characters.';
            };
            // this is another way of writing the if statement above.
            // this.passwordError = this.passwordError.length > 5 ? 
            // '' : 'Password must be more than 5 characters.'
            if(!this.passwordError) {
                // this method runs when the passwordError return empty which means is false.
                console.log("Email:", this.email);
                console.log("Password:", this.password);
                console.log("Role:", this.role);
                console.log("Skills:", this.skills);
                console.log("Terms & Conditions Accepted.", this.terms);

            }
        },
    },
};
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
    input ,select {
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }
    input[type="checkbox"] {
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
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
    button {
        background: #0b6dff;
        border: 0;
        padding: 10px;
        margin-top: 20px;
        color: white;
        border-radius: 20px;
    }
    .submit {
        text-align: center;
    }
    .error {
        color: #ff0062;
        margin-top: 10px;
        font-size: 0.8em;
        font-weight: bold;
    }
</style>