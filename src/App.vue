<template>
    <div id="app">
        <codemirror ref="CM" :value="input" :options="cmOption" @update="onUpdate"></codemirror>
    </div>
</template>

<script>
    import {codemirror} from 'vue-codemirror'
    import formatter from "vkbeautify"
    import 'codemirror/lib/codemirror.css'
    import 'codemirror/mode/xml/xml.js'
    import 'codemirror/theme/base16-light.css'
    import 'codemirror/addon/selection/active-line.js'
    import 'codemirror/addon/edit/closetag.js'

    export default {
        name: 'formatter',
        data() {
            return {
                input: "",
                cmOption: {
                    tabSize: 2,
                    styleActiveLine: true,
                    lineNumbers: true,
                    autoCloseTags: true,
                    line: true,
                    mode: 'application/xml',
                    theme: 'base16-light',
                    viewportMargin: true,
                    smartIndent: true,
                    lineWrapping: true,
                }
            }
        },
        components: {codemirror, formatter},
        methods: {
            onUpdate(codemirror) {
                try {
                    this.input = formatter.xml(codemirror.doc.getValue(), 2);
                } catch (e) {

                }
            },
        },
        mounted() {
            utools.onPluginEnter(({code, type, payload}) => {
                if (type === "over") {
                    this.input = payload;
                }
            });
        },
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
