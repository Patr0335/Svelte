<script>
import ArrayObject from "./components/ArrayObject.svelte";
import Nested from './components/Nested.svelte';
//import UseofSpread from '.components/UseofSpread.svelte';
//import Thing from '.components/Thing.svelte';
//import Inner from '.components/Inner.svelte';

  export let name;

  let src = "Rick.gif";

  let string = `this string contains some <strong>HTML!!!</strong>`;

  let count = 0;

  function incrementCount() {
    count += 1;
  }

  // $ makes it reactive. auto updates DOM
  $: doubled = count * 2;

  $: if (count >= 10) {
    alert("count is dangerously high!");
    count = 9;
  }

  $: console.log("the count is " + count);

  
	const pkg = {
		name: 'svelte',
		version: 3,
		speed: 'blazing',
		website: 'https://svelte.dev'
	};

  let user = { loggedIn: false };

	function toggle() {
		user.loggedIn = !user.loggedIn;
	}

  let x = 13;

  let cats = [
		{ id: 'J---aiyznGQ', name: 'Keyboard Cat' },
		{ id: 'z_AbfPXTKms', name: 'Maru' },
		{ id: 'OUtn3pvWmpg', name: 'Henri The Existential Cat' }
	];


  	/*let things = [
		{ id: 1, name: 'apple' },
		{ id: 2, name: 'banana' },
		{ id: 3, name: 'carrot' },
		{ id: 4, name: 'doughnut' },
		{ id: 5, name: 'egg' },
	];

	function handleClick() {
		things = things.slice(1);
	}*/

  let m = { x: 0, y: 0 };

	function handleMousemove(event) {
		m.x = event.clientX;
		m.y = event.clientY;
	}

  function handleClick() {
		alert('no more alerts')
	}


	/*function handleMessage(event) {
		alert(event.detail.text);
	}*/
</script>

<main>
  <h1>Hello {name}!</h1>

  <img {src} alt="A legend dances." />

  <!--Scoped to the component. Wont change p tag style anywhere else in my app-->
  <p>I always welcome a Rick Roll.</p>
  

  <p>{@html string}</p>

  <button on:click={incrementCount}>
    Clicked {count}
    {count === 1 ? "time" : "times"}
  </button>

  <p>{count} doubled is {doubled}</p>

  <ArrayObject />

  <Nested answer={69}/>
  <Nested/>

  <!--The use of spread-->
  
  <!--<UseofSpread {...pkg}/>-->
  
  
  <!--The use of if blocks.
    
    {#if user.loggedIn}
	<button on:click={toggle}>
		Log out
	</button>
{/if}

{#if !user.loggedIn}
	<button on:click={toggle}>
		Log in
	</button>
{/if}

Can be simplified with if else-->

{#if user.loggedIn}
	<button on:click={toggle}>
		Log out
	</button>
{:else}
	<button on:click={toggle}>
		Log in
	</button>
{/if}

{#if x > 10}
	<p>{x} is greater than 10</p>
{:else if 5 > x}
	<p>{x} is less than 5</p>
{:else}
	<p>{x} is between 5 and 10</p>
{/if}

<h1>The Famous Cats of YouTube</h1>

<ul>
	<!--{#each cats as cat}
		<li><a target="_blank" href="https://www.youtube.com/watch?v={cat.id}">
			{cat.name}
		</a></li>
	{/each}-->

<!--current index as a second argument-->
  {#each cats as cat, i}
	<li><a target="_blank" href="https://www.youtube.com/watch?v={cat.id}">
		{i + 1}: {cat.name}
	</a></li>
{/each}
</ul>

<!--<button on:click={handleClick}>
	Remove first thing
</button>

{#each things as thing (thing.id)}
	<Thing name={thing.name}/>
{/each}>-->

<!--Listening with on: DOM event-->
<div on:mousemove={handleMousemove}>
	The mouse position is {m.x} x {m.y}
</div>

<!--inline handlers-->
<div on:mousemove="{e => m = { x: e.clientX, y: e.clientY }}">
	The mouse position is {m.x} x {m.y}
</div>

<button on:click|once={handleClick}>
	Click me
</button>

<!--<Inner on:message={handleMessage}/>-->

<!--<Outer on:message={handleMessage}/>-->

</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  p {
    color: purple;
    font-family: "Comic Sans MS", cursive;
    font-size: 2em;
  }
</style>
