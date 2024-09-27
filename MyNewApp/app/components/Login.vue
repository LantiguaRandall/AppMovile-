<template>
    <StackLayout>
        <Label text="Iniciar Sesión" class="h1" />
        <TextField v-model="username" hint="Usuario" />
        <TextField v-model="password" hint="Contraseña" secure="true" />
        <Button @tap="login" text="Iniciar Sesión" />
        <Label v-if="error" text="{{ error }}" class="error" />
    </StackLayout>
</template>

<script>
export default {
    data() {
        return {
            username: '',
            password: '',
            error: null,
        };
    },
    methods: {
        async login() {
            this.error = null;
            try {
                const response = await fetch('http://tu-api-url/login', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        username: this.username,
                        password: this.password,
                    }),
                });
                if (!response.ok) {
                    throw new Error('Credenciales inválidas');
                }
                const data = await response.json();
                // Manejar el éxito del inicio de sesión, por ejemplo, guardando el token
                console.log(data);
            } catch (error) {
                this.error = error.message;
            }
        },
    },
};
</script>

<style scoped>
.error {
    color: red;
}
</style>
