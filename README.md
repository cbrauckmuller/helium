# The Grid

Helium uses a grid based on fluid-width columns, based largely off the one found in ZURB Foundation. Each column's width is expressed as a percentage rather than a fixed number of pixels, so as the width of the viewport grows or shrinks, the grid does too.

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

At a certain point, you are going to want your multi-column grid to collapse into a single column as the individual columns will start to become too narrow. By default, this is set to 767px, so anything smaller than an iPad in portrait mode with get a single-column layout. Feel free to adjust this value as your design requires is.