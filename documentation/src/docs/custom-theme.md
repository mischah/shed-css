<p class="m-b:3">To generate a set of colors in the shed style, you can use this Sass mixin, which can be found in the core.</p>

### SCSS
```scss
@import "shed-css/lib/generate-theme.scss";

$natural-black: #111111;
$darker-gray: #333333;
$dark-gray: #666666;
$gray: #999999;
$light-gray: #CCCCCC;
$lighter-gray: #F3F3F3;
$white: #FFFFFF;
$ted-red: #E62B1E;


// expects a map of colors like this:
$my_colors: (
	black: $natural-black,
	gray-dd: $darker-gray,
	gray-d: $dark-gray,
	gray: $gray,
	gray-l: $light-gray,
	gray-ll: $lighter-gray,
	white: $white,
	red: $ted-red
);


// expects a map of breakpoints like this:
$my_breakpoints: (
	n: 'none',
	xs: "min-width: 500px",
	sm: "min-width: 700px",
	md: "min-width: 900px",
	lg: "min-width: 1100px",
	xl: "min-width: 1300px"
);

// execute the mixin outside of a selector
@include generate-theme($my_breakpoints, $my_colors);
```

### POSTCSS
While there's no convenice for creating themes, you can use this code along with the necessary postcss plugins to generate your own theme:

```css
:root {
	--black: #111111;
	--gray-dd: #333333;
	--gray-d: #666666;
	--gray: #999999;
	--gray-l: #CCCCCC;
	--gray-ll: #F3F3F3;
	--white: #FFFFFF;
	--red: #E62B1E;
	--black-g: linear-gradient(to bottom, var(--gray-dd), var(--black));
	--gray-d-g: linear-gradient(to bottom, var(--gray-d), var(--gray-dd));
}

@custom-media --mq-xs (min-width: 24em);
@custom-media --mq-sm (min-width: 30em);
@custom-media --mq-md (min-width: 40em);
@custom-media --mq-lg (min-width: 48em);
@custom-media --mq-xl (min-width: 54em);

@each $mq in n, xs, sm, md, lg, xl {
	@if $mq == n {
		@each $color in black, gray-dd, gray-d, gray, gray-l, gray-ll, white, red, black-g, gray-d-g {
			.c\:$color {
				color: var(--$color);
			}

			.bg\:$color,
			.bg-c\:$color {
				background: var(--$color);

			}

			.hover\/c\:$color:hover {
				color: var(--$color);
			}

			.hover\/bg\:$color:hover,
			.hover\/bg-c\:$color:hover {
				background: var(--$color);
			}

			@for $i from 1 to 9 {
				.bg\:$color\.$i {
					background-color: color(var(--$color) alpha(calc($i / 10)));
				}

				.c\:$color\.$i {
					color: color(var(--$color) alpha(calc($i / 10)));
				}

				.hover\/bg\:$color\.$i:hover {
					background-color: color(var(--$color) alpha(calc($i / 10)));
				}

				.hover\/c\:$color\.$i:hover {
					color: color(var(--$color) alpha(calc($i / 10)));
				}
			}
		}
	}
	@else {
		@media(--mq-$mq) {
			@each $color in black, gray-dd, gray-d, gray, gray-l, gray-ll, white, red, black-g, gray-d-g {
				.c\:$color\@$mq {
					color: var(--$color);
				}

				.bg\:$color\@$mq,
				.bg-c\:$color\@$mq {
					background: var(--$color);
				}

				.hover\/c\:$color\@$mq:hover {
					color: var(--$color);
				}

				.hover\/bg\:$color\@$mq:hover,
				.hover\/bg-c\:$color\@$mq:hover {
					background: var(--$color);
				}

				@for $i from 1 to 9 {
					.bg\:$color\.$i\@$mq {
						background-color: color(var(--$color) alpha(calc($i / 10)));
					}

					.c\:$color\.$i\@$mq {
						color: color(var(--$color) alpha(calc($i / 10)));
					}

					.hover\/bg\:$color\.$i\@$mq:hover {
						background-color: color(var(--$color) alpha(calc($i / 10)));
					}

					.hover\/c\:$color\.$i\@$mq:hover {
						color: color(var(--$color) alpha(calc($i / 10)));
					}
				}
			}
		}
	}
}

```
