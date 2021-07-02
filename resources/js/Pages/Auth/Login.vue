<template>
<el-row :gutter="20" class="login">
    <el-col :span="12"><div class="grid-content">

    </div></el-col>
  <el-col :span="8"><div class="ml-20 grid-content">
<h2 class="intro-x font-bold text-2xl xl:text-3xl text-center xl:text-left"> Sign In </h2>
    <el-form class="space-y-6 mt-6">
      <el-form-item prop="username">
        <span class="svg-container">
          <svg-icon icon-class="user" />
        </span>
        <el-input
            ref="email"
            v-model="form.email"
            placeholder="E-Mail"
            name="email"
            type="text"
            tabindex="1"
            autocomplete="on"
            required
            autofocus
        />
        </el-form-item>
        <el-form-item prop="password">
            <span class="svg-container">
                <svg-icon icon-class="password" />
            </span>
            <el-input
            :key="passwordType"
            ref="password"
            v-model="form.password"
            :type="passwordType"
            placeholder="Password"
            name="password"
            @keyup.enter="submit"
          />
        </el-form-item>
        <el-row justify="end"><el-col :span="12"><el-checkbox v-model:checked="form.remember">remember me</el-checkbox>
        </el-col><el-col :span="12" class="text-right">
        <inertia-link :href="route('password.request')" class="text-sm text-gray-600 hover:text-gray-900">
                    Forgot your password?
        </inertia-link>
        </el-col></el-row>
      <el-button type="primary" style="width:100%;margin-bottom:30px;" :class="{ 'opacity-25': form.processing }" size="medium" :disabled="form.processing" @click.prevent="submit">Login</el-button>
    </el-form>
    </div>
    </el-col>
</el-row>
</template>

<script>
export default {
    name: 'Login',
    data() {
        return {
            form: this.$inertia.form({
                email: '',
                password: '',
                remember: false
            }),
            passwordType: 'password',
            capsTooltip: false,
            loading: false,
            showDialog: false,
            redirect: undefined,
            otherQuery: {}
        }
    },
    methods: {
        submit() {
            this.form
            .transform(data => ({
                ... data,
                remember: this.form.remember ? 'on' : ''
            }))
            .post(
                this.route('login'),
                { onFinish: () => this.form.reset('password'), }
            )
        }
    }
}
</script>
<style lang="scss">
    html, body, #app, .login {
        height: 100%
    }
    .login{
        align-items: center;
    }
    .login:before {
        content: "";
        margin-left: -48%;
        background-image: url('data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSI2Mzk1IiBoZWlnaHQ9IjEwNzkiIHZpZXdCb3g9IjAgMCA2Mzk1IDEwNzkiPgo8ZGVmcz4KPGxpbmVhckdyYWRpZW50IGlkPSJiIiB4MT0iLjciIHgyPSIxIiB5MT0iLjIiIHkyPSIuOCIgZ3JhZGllbnRVbml0cz0ib2JqZWN0Qm91bmRpbmdCb3giPgo8c3RvcCBvZmZzZXQ9IjAiIHN0b3AtY29sb3I9IiMyYjUxYjQiLz4KPHN0b3Agb2Zmc2V0PSIxIiBzdG9wLWNvbG9yPSIjMWMzZmFhIi8+CjwvbGluZWFyR3JhZGllbnQ+CjxjbGlwUGF0aCBpZD0iYSI+CjxwYXRoIGZpbGw9IiNmZmYiIGQ9Ik0wIDBoNjM5NXYxMDc5SDB6IiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtNTM5MSkiLz48L2NsaXBQYXRoPjwvZGVmcz48ZyBjbGlwLXBhdGg9InVybCgjYSkiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDUzOTEpIj48Zz48cGF0aCBmaWxsPSIjZjFmNWY4IiBkPSJNOTc2LTcuM1M3NTMuNSAxODAuNSA5MjAuNyA1NzZjNDUgMTA2LjMgODEuNSAyMDYgODQuNSAyNzcgOC4yIDE5Mi43LTE1NiAyNjguNS0xNTYgMjY4LjVsLTY1My42LTI2LjhMMTc5LjMtMjIuOHoiLz48cGF0aCBmaWxsPSJ1cmwoI2IpIiBkPSJNLTI2MzEuMSAxMDgxLjh2LTEuNmgtNTU5OS44VjBoNjM1OS41cy0xODcuOCAxOTcuNC05MS42IDQ4OC44YzQ5LjEgMTQ5IDk2LjMgMjU2LjMgMTA0LjcgMzYyLjIgOCAxMDAuOC01OCAyMDEuNy0xNjguNyAyNTQuMi02NS44IDMxLjMtMTQ0LjUgNDIuNC0yMjMgNDIuNC0xOTEuMiAwLTM4MS4xLTY1LjgtMzgxLjEtNjUuOHoiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDI4NDAuMiAtLjMpIi8+PC9nPjwvZz48L3N2Zz4K');
        background-repeat: no-repeat;
        background-size: auto 100%;
        background-position: 100%;
        height: 100%;
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
    }
</style>
