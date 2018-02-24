```html
/*vue*/
<desc>
Hello `world`
* a
* b
</desc>
<template>
    <div>
        <div className='wrapper'>
            <div>
                <p>author: {{globalVariable}}</p>
                <button :style="style" @click="onClick">test</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                globalVariable,
                style: {
                    color: 'blue'
                }
            }
        },
        methods: {
            onClick() {
                alert('author: ' + this.globalVariable)
                this.style.color = 'red'
            }
        }
    }
</script>

<style>
.wrapper {
    background: #000;
}
</style>
```