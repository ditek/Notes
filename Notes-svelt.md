# Svelt

In Svelte, an application is composed from one or more components.
A component is a reusable self-contained block of code that encapsulates HTML, CSS and JavaScript that belong together, written into a `.svelte` file.

```html
<script>
	let name = 'world';
</script>

<p>Hello {name}!</p>
 
<style>
	p {
		color: goldenrod;
	}
</style>
```

Variables declared in `script` can be used directly as HTML text or as attributes. See [Variables](#variables).

Apps are usually composed in several components each in its own file. See [Nested Components](#nested-components) for nesting one component under another.

[Reactivity](#reactivity) is achieved simply by referring to variables declared in the script. [Reactive declarations](#reactive-declarations) are used when a variable is dependent on other variables. [Statements](#reactive-statements) can also be reactive and reevaluated when the state changes.

^/(?!.DS_Store)$ 
___

## Variables
- Variables defined in the `script` section can be used directly inside html using curly braces.
- HTML code can be inserted as `{@html var}` (make sure it's html that you trust).

```html
<script>
	let name = 'world';
	let stringWithHTML = `this string contains some <strong>HTML!!!</strong>`;
	let src = '/tutorial/image.gif';
</script>

<h1>Hello {name.toUpperCase()}!</h1>
<p>{@html string}</p>
<img src={src}>
<!-- OR when the attribute name is the same as the var name-->
<img {src}>
```

___

## Nested Components
_Notes_
- Component names are always capitalised, to distinguish them from HTML elements.
- Styles are local to the componet they are declared in, so styles in `Nested.svelt` won't affect `App.svelt`.

In `Nested.svelt`:
```html
<p>Imported paragraph</p>
```

In `App.svelt`:
```html
<script>
	import Nested from './Nested.svelte';
</script>

<Nested/>
```

___

## Reactivity

### Assignments
Events can trigger event handler that can modify variables (component state).

```html
<script>
	let count = 0;
	function increment() {
		count +=1;
	}
</script>

<button on:click={increment}>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>
```

### Reactive declarations
If a certain part of the state is computed from other parts, we use a `reactive declaration` that is recomputed when they change.

```js
let count = 0;
$: doubled = count * 2;
```

### Reactive statements
```js
let count = 0;
$: console.log(`the count is ${count}`);
$: {
	console.log(`the count is ${count}`);
	console.log(`this will also be logged whenever count changes`);
}
$: if (count >= 10) {
	alert('count is dangerously high!');
	count = 0;
}
```
