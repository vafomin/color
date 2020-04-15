<template>
    <div id="app">
        <header>
            <div>
                <a @click="go(color)" v-for="color in colors" :key="color" :style="{backgroundColor: color}"></a>
            </div>
        </header>
        <h1>{{ mycolor }}</h1>
        <button @click="generator()">New Color</button>
        <p><a href="https://enotcode.com">Made with <i class="far fa-heart"></i> by enotcode</a></p>
    </div>
</template>

<script>
    export default {
        name: 'App',
        data() {
            return {
                mycolor: '#' + (Math.random() * 0xFFFFFF << 0).toString(16),
                colors: []
            }
        },
        mounted() {
            document.body.style.background = this.mycolor;
            if (localStorage.getItem('colors')) {
                this.colors = JSON.parse(localStorage.getItem('colors'));
            }
        },
        methods: {
            generator() {
                this.save();
                this.mycolor = '#' + (Math.random() * 0xFFFFFF << 0).toString(16);
                document.body.style.background = this.mycolor;
            },
            save() {
                if (this.colors.indexOf(this.mycolor) === -1) {
                    if (this.colors.length > 30) {
                        this.colors.splice(0, 1);
                    }
                    this.colors.push(this.mycolor);
                    let arr = JSON.stringify(this.colors);
                    localStorage.setItem('colors', arr);
                }
            },
            go(color) {
                this.mycolor = color;
                document.body.style.background = this.mycolor;
            }
        }
    }

</script>