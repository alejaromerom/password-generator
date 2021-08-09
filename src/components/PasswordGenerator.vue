<template>
    <div class="card mx-auto">
        <h1>Generador de contraseñas</h1>
        <div class="pass">
            <p>{{ generatedPassword }}</p>
        </div>
        <button class="boton" @click="refreshPassword = !refreshPassword">Actualizar</button>
    </div>
</template>

<script>
    export default {
        data: function() {
            return {
                passwordLength: 10,
                refreshPassword: false,
                optiondata: [
                {
                    name: 'lowercase',
                    status: true,
                    chars: 'abcdefghijklmnopqrstuvwxyz'
                },
                {
                    name: 'uppercase',
                    status: true,
                    chars: 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
                },
                {
                    name: 'numbers',
                    status: true,
                    chars: '0123456789'
                },
                {
                    name: 'specialchars',
                    status: true,
                    chars: '![]{}()%&*$#^<>~@|'
                }]
            }
        },
        computed: {
            charset() {
                return [...this.optiondata]
                        .map(element => {
                        if(element.status === true)
                            return element.chars;
                        }).join('');
            },
            generatedPassword() {
                this.refreshPassword;
                return [...window.crypto.getRandomValues(new Uint32Array(this.passwordLength))]
                        .map(value => this.charset[value % this.charset.length])
                        .join('');
            }
        }
    }
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Lato:wght@400&family=Raleway&display=swap');

    .card {
        background-color:#7E4CFF;
        border-radius: 25px;
        width: 400px;
        padding: 50px 30px;
        margin-top: 100px;
        text-align: center;
    }

    h1{
        font-family:'raleway',sans-serif;
        font-weight: 400;
        font-size: 2em;
        color: #fff;
    }

    p{
        font-family:'Lato',sans-serif;
        font-weight: 400;
        font-size: 1.2em;
        color: #fff;
    }

    .mx-auto{
        margin-left: auto;
        margin-right: auto;
    }

    .boton {
        background-color: #3C3AE8;
        border: 0px solid;
        border-radius: 10px;
        color:#fff;
        font-family: 'raleway', sans-serif;
        font-weight: 400;
        text-transform: uppercase;
        letter-spacing: 1px;
        padding: 10px;
        margin: 10px;
    }

    .boton:hover{
        background-color: #4070FF;
        color:#000;
    }

    .pass{
        background-color: #9B3AE8;
        padding: 10px;
        border: 0px solid;
        border-radius: 10px;
    }

</style>