<template> 
  <v-container>
    <v-row justify="center">
      <v-col cols="12" sm="8" lg="6">
        <v-card class="elevation-12">
          <v-toolbar dark color="primary">
            <v-toolbar-title>Registration</v-toolbar-title>
          </v-toolbar>
          <v-card-text>
            <v-form v-model="valid" ref="form" lazy-validation>
              <v-text-field
                prepend-icon="mdi-account" 
                name="email" 
                label="Email" 
                type="email" 
                v-model="email"
                :rules="emailRules"
              ></v-text-field>
              <v-text-field  
                prepend-icon="mdi-lock" 
                name="password" 
                label="Password" 
                type="password" 
                v-model="password"
                :rules="passwordRules"
              ></v-text-field>
              <v-text-field  
                prepend-icon="mdi-lock" 
                name="confirm-password" 
                label="Confirm Password" 
                type="password" 
                v-model="confirmPassword"
                :rules="confirmPasswordRules"
              ></v-text-field>
            </v-form> 
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn 
              color="primary"
              @click="onSubmit"
              :disabled="!valid"
            >
              Create Account
            </v-btn>
          </v-card-actions>  
        </v-card>
      </v-col>
    </v-row> 
  </v-container>
</template>

<script>
export default {
  data () { 
    return {
      email: "",
      password: "",
      confirmPassword: "",
      valid: false,
      emailRules: [
        v => !!v || "E-mail is required",
        v => /.+@.+\..+/.test(v) || "E-mail must be valid",
      ],
      passwordRules: [
        v => !!v || "Password is required",
        v => (v && v.length >= 6) || "Password must be at least 6 characters",
      ],
      confirmPasswordRules: [
        v => !!v || "Password confirmation is required",
        v => v === this.password || "Passwords must match",
      ],
    };  
  },
  methods: {
    onSubmit() {
      if (this.$refs.form.validate()) {
        const user = {
          email: this.email,
          password: this.password,
        };
        console.log("User registered:", user);
      }
    },
  },
};
</script>
