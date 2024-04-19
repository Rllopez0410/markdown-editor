<script>
	import { marked } from 'marked';
    import { writable } from 'svelte/store';

	let value = `Some words are *italic*, some are **bold**\n\n- lists\n- are\n- cool`;
    let count = writable(value.length);
    
    $: {
        count.set(value.length);
    }
</script>

<div class="container">
    <header>
        <p>
        <span><i>Markify</i></span>: Your Gateway to Markdown Mastery!
        </p>
    </header>

    <main>
        <div class="editor-head">
            <div class="left-side"><p>Markdown</p></div>
            <div class="right-side"><p>Preview</p><p>Characters:<i style="color: black;">{$count}</i></p></div>
        </div>

        <div class="ui">
            <div class="txt-input">
                <div class="number-line">
                    {#each Array.from({ length: value.split('\n').length }) as _, i}
                        <div>{i + 1}</div>
                    {/each}
                </div>
                <textarea bind:value={value}></textarea>
            </div>
        
            <div class="txt-output">
                {@html marked(value)}
            </div>
        </div>

    </main>
    <footer>
        footer
    </footer>
</div>

<style>
.container {
    display: flex;
    flex-direction: column;
    height: 100vh;
    border: 1px solid orangered;
}

header {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #ffffff;
    box-shadow: 0px .5px 4px rgb(156, 156, 156);
    flex: .3;
}

header p {
  color: #999999;
  font-family: "Source Code Pro", monospace;
  font-size: 24px;
  overflow: hidden;
  border-right: .15em solid orangered;
  white-space: nowrap;
  margin: 0 auto;
  letter-spacing: .15em;
  animation: 
    typing 10s steps(28, end) infinite,
    blink-caret 1s step-end infinite,
    infinite
}

span {
    color: orangered;
    text-shadow: 0px 0px 2px rgb(173, 173, 173);
}

@keyframes typing {
  0% { width: 0 }
  25% { width: 0 }
  50% { width: 750px }
  70% { width: 750px }
  75% { width: 750px }
  100% { width: 0 }
}

@keyframes blink-caret {
  from, to { border-color: transparent }
  50% { border-color: orangered }
}


main {
    display: flex;
    flex-direction: column;
    flex: 5;
}

.editor-head {
    display: flex;
    border-bottom: 1.5px solid rgb(215, 215, 215);
    font-family: "Source Code Pro", monospace;
    color: #b6b6b6;
}

.left-side {
    flex: 1;
    padding-left: 10px;
    padding-right: 10px;
}

.right-side {
    display: flex;
    justify-content: space-between;
    flex: 1;
    border-left: 1.5px solid rgb(215, 215, 215);
    padding-left: 10px;
    padding-right: 10px;
}

.ui {
    display: flex;
    flex: 1;
}

.txt-input {
    display: flex;
    overflow: hidden;
    flex: 1;
}

.number-line {
    display: flex;
    flex-direction: column;
    align-items: center;
    flex: .2;
    gap: 3.09px;
    box-shadow: .5px 0px 4px rgb(156, 156, 156);
    z-index: 1;
}

.number-line :nth-child(n + 1) {
    height: 16px;
}

textarea {
    resize: none;
    flex: 5;
    border: none;
    background-color: #f2f7ff;
    font-size: 16px;
    padding-left: 10px;
    padding-right: 10px;
}

textarea:focus {
    outline: none;
}

.txt-output {
    display: flex;
    text-align: left;
    flex-direction: column;
    flex: 1;
}

footer {
    flex: .2;
    border-top: 1.5px solid rgb(215, 215, 215);
}
</style>