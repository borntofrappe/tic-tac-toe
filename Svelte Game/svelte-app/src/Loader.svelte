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

<svg viewBox="0 0 144 104" width="144" height="104">
    <defs>
        <circle
            id="o"
            cx="0"
            cy="0"
            r="18"
            fill="none"
            stroke-width="16"
            stroke="currentColor">
        </circle>
        <!-- plus sign with rounded corners
        ! for the size consider the space occupied by the circle (18 for the radius, (16 / 2) for the stroke's width, 26 in total)
        -->
        <path
            id="x"
            fill="currentColor"
            d="M -26 0 v -6 a 2 2 0 0 1 2 -2 h 14 a 2 2 0 0 0 2 -2 v -14 a 2 2 0 0 1 2 -2 h 12 a 2 2 0 0 1 2 2 v 14 a 2 2 0 0 0 2 2 h 14 a 2 2 0 0 1 2 2 v 12 a 2 2 0 0 1 -2 2 h -14 a 2 2 0 0 0 -2 2 v 14 a 2 2 0 0 1 -2 2 h -12 a 2 2 0 0 1 -2 -2 v -14 a 2 2 0 0 0 -2 -2  h -14 a 2 2 0 0 1 -2 -2">
        </path>

        <!-- shape used to connect the two signs -->
        <path
            id="goo"
            fill="currentColor"
            d="M -2.5 -8 a 5 5 0 0 0 5 -5 v 26 a 5 5 0 0 0 -5 -5"><!-- start at (-2.5 -8) to have the shape scaled from its center -->
        </path>

    </defs>

    <!-- center the shapes in the svg -->
    <g transform="translate(72 52)">
        <g class="rotate-shapes" transform="rotate(0)"><!-- rotate this group to rotate the shapes around the center -->
            <g class="translate-zero" transform="translate(-20 0)"><!-- translate this group to 0 to have the x approach the center and connect with the o -->
                <g  transform="translate(-26 0)">
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