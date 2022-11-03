<template>
    <div class="page-sign-up">
        <div class="column is-4 is-offset-4">
            <h1 class="title">Регистрация</h1>

            <form @submit.prevent="submitForm">
                <div class="field">
                    <label>Имя пользователя</label>
                    <div class="control">
                        <input type="text" class="input" v-model="username">
                    </div>
                </div>

                <div class="field">
                    <label>Пароль</label>
                    <div class="control">
                        <input type="password" class="input" v-model="password">
                    </div>
                </div>

                <div class="field">
                    <label>Повторите пароль</label>
                    <div class="control">
                        <input type="password" class="input" v-model="password2">
                    </div>
                </div>

                <div class="notification is-danger" v-if="errors.length">
                    <p v-for="error in errors" v-bind:key="error">{{ error }}</p>
                </div>

                <div class="field">
                    <div class="control">
                        <button class="button is-dark">Зарегистрироваться</button>
                    </div>
                </div>
                
                <hr>

                Или <router-link to="/log-in">нажмите здесь</router-link> что бы войти.
            </form>
        </div>

    </div>
</template>

<script>
import axios from 'axios'
import { toast } from 'bulma-toast'

export default {
    name: 'SignUp',
    data() {
        return {
            username: '',
            password: '',
            password2: '',
            errors: []
        }
    },
    methods: {
        submitForm() {
            this.errors = []

            if (this.username === '') {
                this.errors.push('Заполните имя пользователя')
            }

            if (this.password === '') {
                this.errors.push('Заполните пароль')
            }

            if (this.password !== this.password2) {
                this.errors.push('Пароли не совпадают')
            }

            if (!this.errors.length) {
                const formData = {
                    username: this.username,
                    password: this.password
                }

                axios
                    .post("/api/v1/users/", formData)
                    .then(response => {
                        toast({
                            message: 'Аккаунт успешно создан. Можете авторизироваться',
                            type: 'is-success',
                            dismissible: true,
                            pauseOnHover: true,
                            duration: 2000,
                            position: 'bottom-right',
                        })

                        this.$router.push('/login')
                    })
                    .catch(error => {
                        if (error.response) {
                            for (const property in error.response.data) {
                                this.errors.push(`${property}: ${error.response.data[property]}`)
                            }

                            console.log(JSON.stringify(error.response.data))
                        } else if (error.message) {
                            this.errors.push('Произошла ошибка. Попробуйте снова.')

                            console.log(JSON.stringify(error))
                        }
                    })
            }
        }
    }
}
</script>