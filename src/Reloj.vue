<template>
    <div>
        <h1>Reloj Cuenta Regresiva</h1>
        <h1>{{reloj(time)}}</h1>
        <button class="boton" v-for="btn in botones" :key="btn" @click="cuentaRegresiva(btn.tiempo)">
          {{btn.name}}
        </button>
    </div>
</template>

<script>
export default {
    name: 'Reloj',
    data() {
        return {
            time: 0,
            botones: [
                {name: '3s', tiempo: 3},
                {name: '1m', tiempo: 60},
                {name: '5m', tiempo: 300},
                {name: '10m', tiempo: 600},
                {name: '30m', tiempo: 1800},
            ],
            intervalo: '',
            estado: {activo: false},

        }
    },
    methods: {
        reloj: function(crono) {
            let segundos = ('0' + Math.floor(crono % 60)).slice(-2);
            let minutos = ('0' + Math.floor(crono / 60 % 60)).slice(-2);
            return `${minutos}:${segundos} Minutos/Segundos`
        },
        cuentaRegresiva: function(seg) {
            this.time = seg;
            this.estado.activo = true;
            this.intervalo = setInterval(() => {
                if (this.time > 0) {
                    this.time --;
                } else {
                    clearInterval(this.intervalo)
                }
            },2000)
        }
    },
}
</script>
