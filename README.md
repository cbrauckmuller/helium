#Welcome to Helium

Helium is a frontend responsive web framework built using HTML5 and CSS3. In many ways it is similar to both Twitter Bootstrap and ZURB Foundation - in fact, it uses bits of their code.

# The Grid

Helium uses a nestable grid based on fluid-width columns, based largely off the one found in ZURB Foundation. Each column's width is expressed as a percentage rather than a fixed number of pixels, so as the width of the viewport grows or shrinks, the grid does too.

## Selectively Responsive

By default, Helium uses a fixed-width layout. However, making it responsive is as simple as adding a class of `responsive` to the `<body>` element of your page. Responsive design is by its nature rather resource-intensive, so I built Helium to allow you to toggle responsive behavior on a per page basis so you can build out responsive pages as time and budgets permit. You can also use the `responsive` class as a hook to target only responsive pages with your SCSS. 

	<body class="responsive">

## SASS Variables

There are three SASS variables that will determine the makeup of your grid. As with nearly every other variable in Helium, these are stored in `scss/config.scss`

### $page-width

(pixels) This is the width of your content if you are using a fixed-width design, or the maximum width of your content if you are using a responsive design.

### $column-count

(positive integer) The number of columns you would like in your grid. Some designs call for 12, others for 16, or for a simple site you might just want 3 or 6.

### $column-gutter

(pixels) The amount of space between your columns.

If you are clever with your math, you can ensure that the column widths are round multiples of 10 pixels. This can be helpful on a fixed-width design. For example, a $page-width of 940px, $column-count of 12 and $column-gutter of 20px will give you 60px wide columns. These are the same values used by the popular 960 grid system.

## Grid Markup

The markup for building a grid in Helium is very lightweight and should look familiar to you if you've ever used ZURB Foundation, 960gs or Bootstrap. Keep in mind that the sum total of the `spanX` elements in a row must not exceed the value set for the `$column-count` variable in `config.scss`. The markup below would be appropriate for a 12 column grid.

	<div class="container">
		<div class="row">
			<div class="span4">
			</div>
			
			<div class="span4">
			</div>
			
			<div class="span4">
			</div>
		</div>
	</div>


## The Breakpoint

### $responsive-breakpoint

(pixels) At a certain point, you are going to want your multi-column grid to collapse into a single column as the individual columns will start to become too narrow. By default, this is set to 767px, so anything smaller than an iPad in portrait mode with get a single-column layout. Feel free to adjust this value as your design requires.

# Buttons

Buttons are a big component of any UI. Helium tries to include many common button patterns without making too many assumptions about how you will use them.

## Basic button style

A clean, uniform button style for all kinds of UI tasks. Keep in mind that you can use the `button` class on both `<a>` and `<button>` elements.

	<a class="button>Here's a button</a>
	
	<button class="button>Here's another</button>
	
## Large buttons

Often times, you want your primary call to action button to be larger than other UI buttons. Just append an additional class of `button-large`.

	<a class="button button-large">I’m a call to action!</a>
	
## Small buttons

Sometimes you need to fit buttons in a smaller space or de-emphasize them. Just append a class of `button-small`.

	<a class="button button-small">I'm a small button</a>
	
## Pill buttons

Perfect for centered buttons or buttons that hang out by themselves. Just append a class of `button-pill`.

	<a class="button button-pill">Take the red pill</a>

## Button groups

These work great for toolbars, sub-navigation, toggling view options, etc.

	<div class="button-group">
		<a class="button">One if by land</a>
		<a class="button">Two if by sea</a>
		<a class="button">Three if by teleporter</a>
	</div>

## Buttons with icons

It’s easy to add an icon of your choice to your buttons.

In this case, the icon is the only thing in the button.
	
	<a class="button"><i class="icon"></i></a>
	
You can also prepend icons to button text. Icons will center themselves vertically.

	<a class="button"><i class="icon icon-prepend"></i>I have an icon</a>
	
## Button icons with dividers

Sometimes, you want a divider between icon and button text

	<button class="button has-icon-divider"><i class="icon icon-prepend"></i>I have a divided icon</button>
	
## Buttons with dropdowns

Adding a nicely-styled dropdown menu to a button is dead easy. The markup for the dropdown itself is identical to that used on the navbar.

	<div class="has-dropdown button-dropdown">
		<a href="#" class="button" data-toggle="dropdown">I am another <span class="caret"></span></a>
		<ul class="dropdown right">
			<li><a href="#">Dropdown item one</a></li>
			<li><a href="#">Here is another</a></li>
			<li><a href="#">Wait, one more</a></li>
		</ul>
	</div>
	
## Custom buttons

Perhaps the most powerful component of the buttons module in Helium is the ability for you to create custom-styled buttons by just four arguments to a SASS mixin.

	&.button-facebook {
		@include button-custom(
			$theme: $button-theme, 
			$background-color: $facebook-blue, 
			$text-color: #fff, 
			$reversed: true	
		);
	}

You can see in the example above that we call the `button-custom` mixin and pass four arguments.

### $theme

This argument can take one of two values, `glossy` or `flat`. Of course, you can also pass in `$button-theme` so it inherits whatever you have the global default set to, which is what I have done here.

### $background-color

This can take a hex value or a solid CSS color like `blue`. If `$button-theme` is set to `glossy`, the mixin will automatically build nice gradients and highlights for you.

### $text-color

The color of the button text. Pretty self-explanatory.

### $reversed

Boolean. If set to `true` it means that the button's background color is dark whilst the text is light (often white). If set to `false` it means the opposite is the case. Setting this variable helps the mixin add subtle shadows that enhance the contrast of the button.

# Forms

Forms in Helium are build to be responsive-ready from the start. Two common design patterns are available out of the box - labels above fields and labels to the left of fields. Both of these are useful in different scenarios. At the `$responsive-breakpoint`, however, the labels left of fields style collapses to labels above fields to ensure the design doesn't break on mobile devices.

## Basic form markup

Forms in Helium are split into `field-group` elements which consist of a `field-label` and its accompanying `fields`, plus any help or error text that may appear based on validation (more on that later).

	<form>
		<div class="field-group">
			<label class="field-label">Email address</label>
			
			<div class="fields">
				<input type="email" placeholder="name@example.com">
			</div>
		</div>
	</form>
	
## Labels left of fields

Putting labels to the left of fields is as simple as adding the `labels-left` class to your `<form>` and then incorporating the Helium grid markup. In the example below, I've wrapped the `field-labels` with a `span3` and the `fields` with a `span9` but you can adjust those to compensate for longer or shorter label text.

	<form class="labels-left">

		<div class="field-group">
			<div class="row">
			
				<div class="span3">
					<label class="field-label">First name</label>
				</div>
				
				<div class="span9">								
					<div class="fields">
						<input type="text">
					</div>
				</div>
			</div>
		</div>
	
	</form>
	
In the same manner as the rest of the fluid grid, the "labels left of fields" form style will collapse into a traditional "labels on top of fields" design when the viewport width drops below the `$responsive-breakpoint` (767px by default).

## Additional form styles

Helium comes with a suite of additional form styles to make your life easier.

### Instructional/help text under the field

This is useful for additional, clarifying instructions that won't fit in the label.

	<div class="fields">
		<input type="number">
		
		<div class="field-instructions block">
			This is a small 3 digit number on the back of your card.
		</div>
	</div>

### Radio/checkbox lists

For lists containing multiple radio or checkbox options.

	<div class="fields">
		<ul class="radio-checkbox-list">
			<li>
				<label><input type="radio" name="example-radio">Product inquiry</label>
			</li>
			<li>
				<label><input type="radio" name="example-radio">Product inquiry</label>
			</li>
			<li>
				<label><input type="radio" name="example-radio">Here&rsquo;s a really, really long item that goes onto two lines</label>
			</li>
		</ul>
	</div>

### Error messages

As you can see below, we've appended a class of `error` to the `field-group` and added a new object with a class of `error-message` directly after the input.

	<div class="field-group error">
		<label class="field-label">Last name</label>
		<div class="fields">
			<input type="text" />
			<div class="error-message">You&rsquo;ve got some problems, man.</div>
		</div>
	</div>