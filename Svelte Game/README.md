# Svelte

The application is set up in **svelte-app** through the `degit` scaffolding tool.

```
npx degit sveltejs/template svelte-app
```

## Project Structure

The game itself is structured as follows:

- the player is welcomed by the SVG loader.

- after an arbitrary number of iterations, the loader stops, to show a form with two radio buttons. These allow to make a selection between **x** and **o** for the player.

- once a selection is made, the form is removed in favor of a grid, to play the actual game. Here a grid of 9 buttons can be populated alternatively with **x**(s) and **o**(s).

- after every move, the game checks for a victory and finally for a tie. If none occurs, the game continues alternating the choice. If one occurs, the game ends.

The flow is purposefully straightforward to focus on the implementation of each step. Ideally, in the final version and before I focus on the AI portion of the project, it should be possible to return to previous steps, not to mention play more than one game.
