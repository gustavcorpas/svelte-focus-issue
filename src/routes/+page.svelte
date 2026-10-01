<script>
	let frameContainer;

	function loadIframe() {
		const iframe = document.createElement('iframe');
		iframe.id = 'iframe';
		iframe.title = 'Embedded page';
		iframe.src = './iframe';

		frameContainer.appendChild(iframe);
	}

	function unloadIframe() {
		document.getElementById('iframe')?.remove();
	}
</script>

<h1>Iframe focus reproduction</h1>

<h2>Steps to reproduce</h2>

<ol>
	<li>Click <strong>Load iframe</strong>.</li>
	<li>Press <kbd>Tab</kbd> to move focus to the next focusable element.</li>
</ol>

<h2>Expected</h2>

<p>
	The <strong>Focusable button</strong> below the iframe receives focus.
</p>

<h2>Actual</h2>

<p>
	When server-side rendering is disabled, the <strong>button inside the iframe</strong>
	receives focus instead.
</p>

<p>
	This does not occur when server-side rendering is enabled.
</p>

<p>
	<button onclick={unloadIframe}>Unload iframe</button>
	<button onclick={loadIframe}>Load iframe</button>
</p>

<p>
	<button>Focusable</button>
</p>

<div class="frame-container" bind:this={frameContainer}></div>

