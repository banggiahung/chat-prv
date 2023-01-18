<template>
    <div class="main-p">
        <div class="login-page">
            <div class="card-1">
                <form @submit.prevent="login">
                    <div class="title">Login</div>
                    <input placeholder="Username" type="text" v-model="username" />
                    <br />
                    <input placeholder="Password" type="password" v-model="password" />
                    <br />
                    <button type="submit">Login</button>
                </form>

                <form @submit.prevent="signup">
                    <div class="title">Sign Up</div>
                    <input class="input" placeholder="Username" type="text" v-model="username" />
                    <br />
                    <input placeholder="Password" type="password" v-model="password" />
                    <br />
                    <input placeholder="Email" type="text" v-model="email" />
                    <br />
                    <input placeholder="First name" type="text" v-model="first_name" />
                    <br />
                    <input placeholder="Last name" type="text" v-model="last_name" />
                    <br />
                    <button type="submit">Sign Up</button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
import { loginRest, signupRest } from "./api";

export default {
    data() {
        return {
            username: "",
            password: "",
            email: "",
            first_name: "",
            last_name: "",
        };
    },
    methods: {
        login() {
            loginRest(this.username, this.password)
                .then((response) =>
                    this.$emit("onAuth", { ...response.data, secret: this.password })
                )
                .catch((error) => console.log("Login error", error));
        },
        signup() {
            signupRest(
                this.username,
                this.password,
                this.email,
                this.first_name,
                this.last_name
            )
                .then((response) =>
                    this.$emit("onAuth", { ...response.data, secret: this.password })
                )
                .catch((error) => console.log("Sign up error", error));
        },
    },
};
</script>
<style scoped>
* {
    font-family: Avenir;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    margin: 0px;
}

.main-p,
.login-page {
    height: 100vh;
    background: url(../assets/1406_anh-meo-cute-hoat-hinh-222.jpg);
}

.card-1 {
    width: 200px;
    position: relative;
    left: calc(50vw - 100px);
    text-align: center;
    padding-top: 6vw;
}

.title {
    padding-top: 32px;
    font-size: 22px;
    color: #3366FF;
    font-weight: 700;
}

input {
    width: calc(100% - 16px);
    margin-top: 12px;
    padding: 8px;
    background-color: #e6f7ff;
    outline: none;
    border: 1px solid #e6f7ff;
}

button {
    margin-top: 12px;
    width: 100%;
    padding: 8px;
}
</style>