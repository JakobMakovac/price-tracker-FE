<template>
    <div>
        <div class="header">
            <h1>Login</h1>
            <router-link
                :to="{ name: 'register' }"
            >
                Register
            </router-link>
        </div>
        <div class="login-form">
            <ul v-if="errors" class="error-messages">
                <li>{{ errors }}</li>
            </ul>
            <form @submit.prevent="onSubmit(username, password)">
            <div class="form-group">
                <input
                type="text"
                v-model="username"
                required="true"
                />
                <div class="placeholder">USERNAME</div>
            </div>
            <div class="form-group">
                <input
                type="password"
                v-model="password"
                required="true"
                />
                <div class="placeholder">PASSWORD</div>
            </div>
            <button>
              Sign in
            </button>
          </form>
        </div>
    </div>
</template>

<style lang="scss">
    @import '../assets/styles/login.scss';
</style>

<script>
var mapState = require('vuex').default.mapState;
var LOGIN = require('../store/actions.type').LOGIN;
export default {
    name: "login",
    data() {
        return {
            username: null,
            password: null,
        };
    },
    methods: {
        onSubmit(username, password) {
        this.$store
            .dispatch(LOGIN, { username, password })
            .then(() => this.$router.push({ name: "home" }));
        }
    },
    computed: {
        ...mapState({
            errors: (state) => state.auth.errors,
        }),
    },
};
</script>