<template>
    <div id="app">
        <codemirror :value="input" :options="cmOption"
                    @cursorActivity="onCmCursorActivity"
                    @ready="onCmReady"
                    @focus="onCmFocus"
                    @blur="onCmBlur"></codemirror>
    </div>
</template>

<script>
    import {codemirror} from 'vue-codemirror'
    import formatter from "vkbeautify"
    import highlight from 'vue-highlight.js'
    import 'codemirror/lib/codemirror.css'
    import 'codemirror/mode/xml/xml.js'
    import 'codemirror/theme/base16-light.css'
    import 'codemirror/addon/selection/active-line.js'
    import 'codemirror/addon/edit/closetag.js'

    export default {
        name: 'formatter',
        data() {
            return {
                input: "asdfsadtasdr",
                cmOption: {
                    tabSize: 4,
                    styleActiveLine: true,
                    lineNumbers: true,
                    autoCloseTags: true,
                    line: true,
                    mode: 'application/xml',
                    theme: 'base16-light',
                    viewportMargin: true,
                    lineWrapping: true,
                }
            }
        },
        components: {codemirror, formatter, highlight},
        methods: {
            onCmCursorActivity(codemirror) {
                console.log('onCmCursorActivity', codemirror)
            },
            onCmReady(codemirror) {
                console.log('onCmReady', codemirror)
            },
            onCmFocus(codemirror) {
                console.log('onCmFocus', codemirror)
            },
            onCmBlur(codemirror) {
                console.log('onCmBlur', codemirror)
            }
        }
    }
</script>

<style>
    #app {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        height: 95vh;
    }

    .CodeMirror {
        height: 100%;
    }

    .CodeMirror-code {
        font-size: 1.5rem;
    }
</style>
