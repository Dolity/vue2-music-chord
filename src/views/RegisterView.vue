<template>
  <section class="bg-light p-3 p-md-5 p-xl-5 pt-4">
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-12 col-md-9 col-lg-7 col-xl-6 col-xxl-5">
          <div class="card border border-light-subtle rounded-4">
            <div class="card-body p-3 p-md-4 p-xl-5">
              <form
                @submit.prevent="handleRegister"
                class="needs-validation"
                novalidate
              >
                <div class="mb-3">
                  <div class="fw-bold fs-2 text-center">Register</div>
                </div>
                <div class="form-floating has-validation mb-3">
                  <input
                    v-model="email"
                    type="text"
                    class="form-control"
                    placeholder=""
                    :class="{
                      'is-invalid': !email.includes('@'),
                      'is-valid': email.includes('@'),
                    }"
                    required
                  />
                  <label class="form-label">Email address</label>
                  <div id="emailHelp" class="form-text">
                    We'll never share your email with anyone else.
                  </div>
                  <div class="invalid-feedback">Please input a email.</div>
                </div>

                <div class="form-floating mb-3">
                  <input
                    v-model="password"
                    type="password"
                    class="form-control"
                    placeholder=""
                    :class="{
                      'is-invalid': password.length < 8,
                      'is-valid': password.length >= 8,
                    }"
                    required
                  />
                  <label>Password</label>
                  <div class="invalid-feedback">
                    Please input a password at lest 8 digit.
                  </div>
                </div>
                <div class="form-floating mb-3">
                  <input
                    v-model="rePassword"
                    type="password"
                    class="form-control"
                    placeholder=""
                    :class="{
                      'is-invalid': rePassword.length < 8,
                      'is-valid': rePassword.length >= 8,
                    }"
                    required
                  />
                  <label class="form-label">Re-Password</label>
                  <div class="invalid-feedback">
                    Please input a re-password at lest 8 digit.
                  </div>
                </div>

                <div class="d-grid">
                  <button type="submit" class="btn btn-primary mb-3">
                    Register
                  </button>
                </div>

                <div v-if="error" class="text-danger">{{ error }}</div>
                <div v-if="success" class="text-success">{{ success }}</div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import authenticationService from "@/services/authenticationService"

export default {
  data() {
    return {
      email: "",
      password: "",
      rePassword: "",
      success: null,
      error: null,
    }
  },

  methods: {
    async handleRegister() {
      try {
        if (this.password !== this.rePassword) {
          this.error = "Passwords do not match"
          return
        }
        await authenticationService.register({
          email: this.email,
          password: this.password,
        })

        this.error = null
        this.handleClearRegister()
        this.success = "User registered successfully"
      } catch (error) {
        this.success = null
        this.error = error.response.data.error
      }
    },
    handleClearRegister() {
      this.email = ""
      this.password = ""
      this.rePassword = ""
      this.success = null
      this.error = null
    },
  },
}
</script>

<style></style>
