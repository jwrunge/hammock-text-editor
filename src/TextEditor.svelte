<script>
    import {onMount, onDestroy} from "svelte"

    export let data

    let editor
    let quill
    let initial_load = true

    function reload_data(skip) {
        if(skip) return
        quill.root.innerHTML = data
    }

    onMount(()=> {
        let options = {
            modules: {
                toolbar: [
                    [{header: [1,2,3,false]}],
                    ["bold", "italic", "underline", "strike"],
                    ["link", "code-block"]
                ]
            },
            placeholder: "Type something...",
            theme: "snow"
        }

        console.log(editor)
        console.log(data)

        quill = new Quill(editor, options)
        reload_data(initial_load)
        initial_load = false
    })

    $: data, reload_data(initial_load)
</script>

<div class="editor-container">
    <div class="ed" bind:this={editor}></div>
</div>

<style lang='scss'>
    .editor-container {
        margin: 1em 0;
    }
</style>