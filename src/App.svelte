<script>
  import Counter from './lib/Counter.svelte'

  let styles = {
		'cursorXpos': '50vw',
		'cursorYpos': '50vh',
	};
	
	$: cssVarStyles = Object.entries(styles)
		.map(([key, value]) => `--${key}:${value}`)
		.join(';');

	function handleMousemove(event) {
		styles['cursorXpos'] = event.clientX + 'px';
		styles['cursorYpos'] = event.clientY + 'px';
	}
</script>

<div class="outer-container" style={cssVarStyles}/>
<div class="tracking" on:mousemove={handleMousemove}/>
<button>hi button</button>
<Counter/>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    width: 100%;
    height: 100%;
    cursor: none;
  }

  .outer-container {
    width: 100%;
    height: 100%;
    position: absolute;
    background: radial-gradient(
        circle 8rem at var(--cursorXpos) var(--cursorYpos),
        rgba(0, 0, 0, 0) 0%, rgba(0, 0, 0, 1) 100%
    );
    z-index: 11;
    pointer-events: none;
  }

  .tracking ~ * {
    z-index: -11;
  }

  .tracking {
    position: absolute;
    width: 100%;
    height: 100%;
    z-index: -999;
  }

</style>
