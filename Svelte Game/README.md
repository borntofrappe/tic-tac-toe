# Svelte

The application is set up in **svelte-app** through the `degit` scaffolding tool.

```
npx degit sveltejs/template svelte-app
```

## Project Structure

The game itself is structured as follows:

- [x] the player is welcomed by the SVG loader.

- [x] after an arbitrary number of iterations, the loader stops, to show a form with two radio buttons. These allow to make a selection between **x** and **o** for the player.

- [x] once a selection is made, the form is removed in favor of a grid, to play the actual game. Here a grid of 9 buttons can be populated alternatively with **x**(s) and **o**(s).

- [ ] after every move, the game checks for a victory and finally for a tie. If none occurs, the game continues alternating the choice. If one occurs, the game ends.

The flow is purposefully straightforward to focus on the implementation of each step. Ideally, in the final version and before I focus on the AI portion of the project, it should be possible to return to previous steps, not to mention play more than one game.

## Update

Upon building the first few components, here's a few notes on the development:

- the flow from loader to selection is made to be seamless by playing around with the size of the SVG element and the position of the shapes. To this end, I've extracted the path elements used in the loader in an `SVG.svelte` component. In this way, the `defs` block is included atop the page and the shapes can be readily used by any component which follows.

- it is necessary to highlight how the loading screen becomes a form. It is paramount to highlight that the player can select between one of the two options and proceed. Ideally, this would be achieved with visual cues outside of text-based hints.

- the variables are often named with little care and this doesn't help with the sustainability or expansion of the project. Comments might also help to clarify the framework and most importantly focus on the essential parts (think of the Loader component and how the main feature is the dispatcher).