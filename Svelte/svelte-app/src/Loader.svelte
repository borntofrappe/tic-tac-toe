<!-- component describing the svg loader -->
<script>
  // following the animationiteration event dispatch a fitting method
  // this allows the parent component to know when the animation iterates
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();
  function iteration() {
    dispatch('iteration');
  }
</script>
<style>
  svg {
    display: block;
    width: 350px;
    height: auto;
  }

  /* animate the shapes to rotate around the center of the svg */
  .rotate-shapes {
    animation: rotateShapes 5s cubic-bezier(0.645, 0.045, 0.355, 1) infinite;
  }
  @keyframes rotateShapes {
    12.5% {
      transform: rotate(0deg);
    }
    25%,
    62.5% {
      transform: rotate(180deg);
    }
    75%,
    100% {
      transform: rotate(360deg);
    }
  }
  /* rotate the x sign in between the keyframes describing the shapes' own rotation */
  .rotate-x {
    animation: rotateX 5s cubic-bezier(0.645, 0.045, 0.355, 1) infinite;
  }
  @keyframes rotateX {
    12.5%,
    25% {
      transform: rotate(45deg);
    }
    37.5%,
    50% {
      transform: rotate(90deg);
    }
    62.5%,
    75% {
      transform: rotate(135deg);
    }
    87.5%,
    100% {
      transform: rotate(180deg);
    }
  }
  /* translate the two signs, once again in between the keyframes describing the rotation */
  .translate-zero {
    animation: translateZero 5s cubic-bezier(0.645, 0.045, 0.355, 1) infinite;
  }
  @keyframes translateZero {
    12.5%,
    25% {
      transform: translate(0);
    }
    37.5%,
    50% {
      transform: translate(-20px);
    }
    62.5%,
    75% {
      transform: translate(0);
    }
    87.5%,
    100% {
      transform: translate(-20px);
    }
  }

  /* scale the goo to appear / disappear in between the translations of the two shapes */
  .scale-goo {
    animation: scaleGoo 5s cubic-bezier(0.645, 0.045, 0.355, 1) infinite;
  }
  @keyframes scaleGoo {
    /* hide the shape by default and once again 5% before and after every time the shape is shown  */
    0%,
    7.5%,
    30%,
    57.5%,
    80%,
    100% {
      transform: scale(0);
      opacity: 0;
    }
    /* show the shape as the two signs connect */
    12.5%,
    25%,
    62.5%,
    75% {
      transform: scale(1);
      opacity: 1;
    }
  }
</style>

<!-- following the animationiteration event (and only once) call the function to dispatch the iteration event -->
<svg on:animationiteration|once={iteration} viewBox="0 0 144 104" width="144" height="104">
    <!-- center the shapes in the svg -->
    <g transform="translate(72 52)">
        <g class="rotate-shapes" transform="rotate(0)"><!-- rotate this group to rotate the shapes around the center -->
            <g class="translate-zero" transform="translate(-20 0)"><!-- translate this group to 0 to have the x approach the center and connect with the o -->
                <g transform="translate(-26 0)">
                    <g class="rotate-x"><!-- rotate this group to rotate the x sign -->
                        <g transform="rotate(45)">
                            <use href="#x"></use>
                        </g>
                    </g>
                </g>
            </g>
            <g transform="scale(-1 1)"><!-- create a mirrored group to have the .translate-zero elements animated with the same value, but in opposite directions -->
                <g class="translate-zero" transform="translate(-20 0)"><!-- translate this group to 0 to have the o approach the center and connect with the x -->
                    <g transform="scale(-1 1)">
                        <g transform="translate(26 0)">
                            <g>
                                <use href="#o"></use>
                            </g>
                            <!-- position the goo shape in between the x and o -->
                            <g transform="translate(-25.5 0)">
                                <g class="scale-goo" transform="scale(0)"><!-- scale this group as the x and o connect -->
                                    <use href="#goo" x="0" y="0"></use>
                                </g>
                            </g>
                        </g>
                    </g>
                </g>
            </g>
        </g>
    </g>
</svg>