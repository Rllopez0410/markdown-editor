<script>
	import { marked } from 'marked';
	let value = `Some words are *italic*, some are **bold**\n\n- lists\n- are\n- cool`;
</script>

<div class="container">
    <header>
        <p>
        <span><i>Markify</i></span>: Your Gateway to Markdown Mastery!
        </p>
    </header>

    <main>
        <div class="txt-input">
            input
            <textarea bind:value={value}></textarea>
        </div>
    
        <div class="txt-output">
            output
            <div>{@html marked(value)}</div>
        </div>
    </main>
    <footer>footer</footer>
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
  border-right: .15em solid orange;
  white-space: nowrap;
  margin: 0 auto;
  letter-spacing: .15em;
  animation: 
    typing 10s steps(28, end) infinite,
    blink-caret .6s step-end infinite,
    infinite
}

span {
    color: orangered;
    text-shadow: 0px 0px 2px rgb(173, 173, 173);
}

@keyframes typing {
  0% { width: 0 }
  25% { width: 0; }
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
    flex: 5;
}

footer {
    flex: .2;
}
</style>