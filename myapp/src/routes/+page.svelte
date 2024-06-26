<script>
	import { marked } from 'marked';
    import { writable } from 'svelte/store';
    import gitIcon from '../icons/social.png';
    import linkinIcon from '../icons/linkedin.png'
    import discordIcon from '../icons/discord.png'

	let value = `Some words are *italic*, some are **bold**\n\n- lists\n- are\n- cool`;
    let count = writable(value.length);
    let darkMode = false;
    
    $: {
        count.set(value.length);
    }

    function copyToClipboard(text) {
        navigator.clipboard.writeText(text)
    }

    function isDarkMode() {
        darkMode = !darkMode;
    }
</script>

<div class="container">
    <header class={darkMode === false ? "header" : "header-dark-mode"}>
        <div class="menu">
            <button class="menu-btn">
                <span class="material-symbols-outlined">
                    menu
                </span>
            </button>
        </div>

    <div class="title">
        <p><span><i>Markify</i></span>: Your Gateway to Markdown Mastery!</p>
    </div>
        <div class = {darkMode === false ? "darkmode" : "lightmode"}>
            <button class="switch" on:click={isDarkMode}>
                <div class= {darkMode === false ? "switch-light" : "switch-dark"}></div>
            </button>
        </div>
    </header>

    <main>
        <div class={darkMode === false ? "editor-head-light" : "editor-head-dark"}>
            <div class="left-side">
                <p>Markdown</p>
                <button class="copy-btn" on:click={() => copyToClipboard(value)}>
                    <span class="material-symbols-outlined">
                        content_copy
                    </span>
                </button>
            </div>
            <div class={darkMode === false ? "right-side" : "right-side-dark"}><p>Preview</p><p>Characters:<i style="color: black;">{$count}</i></p></div>
        </div>

        <div class="ui">
            <div class="txt-input">
                <div class={darkMode === false ? "number-line-light" : "number-line-dark"}>
                    {#each Array.from({ length: value.split('\n').length }) as _, i}
                        <div>{i + 1}</div>
                    {/each}
                </div>
                <textarea class={darkMode === false ? "" : "textarea-dark"} bind:value={value}></textarea>
            </div>
        
            <div class={darkMode === false ? "txt-output" : "txt-output-dark"}>
                {@html marked(value)}
            </div>
        </div>

    </main>
    <footer class={darkMode === false ? "" : "footer-dark"}>
        <div class="icons">
            <a href="https://github.com/Rllopez0410"><img src="{gitIcon}" alt="" style="width: 30px; height: 30px;"></a>
            <a href="https://www.linkedin.com/in/roger-lopez-98b5492b6/"><img src="{linkinIcon}" alt="" style="width: 30px; height: 30px;"></a>
            <a href="https://github.com/Rllopez0410"><img src="{discordIcon}" alt="" style="width: 30px; height: 30px;"></a>
        </div>
        <div>© 2024 made by Roger Lopez. Powered by <a href="https://svelte.dev/">Svelte</a></div>
    </footer>
</div>

<style>
.container {
    display: flex;
    flex-direction: column;
    height: 100vh;
}

.header {
    display: flex;
    justify-content: center;
    align-items: center;
    box-shadow: 0px .5px 4px #9c9c9c;
    flex: .3;
    transition: 500ms;
}

.header-dark-mode {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #373737;
    flex: .3;
    transition: 500ms;
}

.menu {
    flex: 1;
}

.menu-btn {
    background-color: inherit;
    border: none;
    cursor: pointer;
}

.title {flex: 6;}

.darkmode {
    display: flex;
    justify-content: end;
    align-items: center;
    flex: 1;
    padding-right: 5px;
    transition: 1s;
}
.lightmode {
    display: flex;
    justify-content: end;
    align-items: center;
    flex: 1;
    padding-right: 5px;
    transition: 1s;
}

.switch {
    display: flex;
    align-items: center;
    border-radius: 50px;
    background-color: rgb(154, 154, 154);
    width: 40px;
    height: 20px;
    box-shadow: 1px 1px 5px #585858 inset;
    padding: 1px;
    border: none;
}

.switch-light {
    position: relative;
    left: 0;
    width: 15px;
    height: 15px;
    background-color: white;
    border-radius: 100px;
    transition: 500ms;
}
.switch-dark {
    position: relative;
    left: 23px;
    width: 15px;
    height: 15px;
    background-color: orangered;
    border-radius: 100px; 
    transition: 500ms;
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

.editor-head-light {
    display: flex;
    border-bottom: 1.5px solid rgb(215, 215, 215);
    font-family: "Source Code Pro", monospace;
    color: #b6b6b6;
    transition: 600ms;
}
.editor-head-dark {
    display: flex;
    border-bottom: 1.5px solid rgb(215, 215, 215);
    font-family: "Source Code Pro", monospace;
    background-color: #373737;
    color: #b6b6b6;
    transition: 600ms;
}

.left-side {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex: 1;
    padding-left: 10px;
    padding-right: 10px;
}

.left-side button {
    cursor: pointer;
    background-color: inherit;
}

.right-side {
    display: flex;
    justify-content: space-between;
    flex: 1;
    border-left: 1.5px solid rgb(215, 215, 215);
    padding-left: 10px;
    padding-right: 10px;
    transition: 700ms;
}
.right-side-dark {
    display: flex;
    justify-content: space-between;
    flex: 1;
    padding-left: 10px;
    padding-right: 10px;
    transition: 700ms;
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

.number-line-light {
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: rgb(212, 212, 212);
    flex: .3;
    color: orangered;
    flex: .2;
    gap: 3.09px;
    box-shadow: .5px 0px 4px rgb(156, 156, 156);
    z-index: 1;
    transition: 800ms;
}
.number-line-dark {
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: #373737;
    flex: .3;
    color: orangered;
    flex: .2;
    gap: 3.09px;
    box-shadow: .5px 0px 4px rgb(156, 156, 156);
    z-index: 1;
    transition: 800ms;
}

.number-line-light :nth-child(n + 1) {
    height: 16px;
}
.number-line-dark :nth-child(n + 1) {
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
    transition: 900ms
}
.textarea-dark {
    resize: none;
    flex: 5;
    border: none;
    background-color: #292b2b;
    color: orangered;
    font-size: 16px;
    padding-left: 10px;
    padding-right: 10px; 
    transition: 900ms
}

textarea:focus {
    outline: none;
}

.txt-output {
    display: flex;
    text-align: left;
    flex-direction: column;
    font-size: 22px;
    flex: 1;
    transition: 1200ms;
}
.txt-output-dark {
    display: flex;
    text-align: left;
    color: rgb(222, 222, 222);
    background-color: #525456;
    flex-direction: column;
    font-size: 22px;
    flex: 1;
    transition: 1200ms
}

footer {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    font-family: "Source Code Pro", monospace;
    flex: .5;
    border-top: 1.5px solid rgb(215, 215, 215);
    transition: 1100ms;
}
.footer-dark {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    color: white;
    font-family: "Source Code Pro", monospace;
    background-color: #373737;
    flex: .5;
    border-top: 1.5px solid rgb(215, 215, 215);
    transition:1100ms;
}

.icons {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 8px;
    width: 200px;
}

.copy-btn {
    background-color: white;
    border: none;
}

a {
    text-decoration: none;
    color: orangered;
}

img {
    border-radius: 100px;
}
</style>