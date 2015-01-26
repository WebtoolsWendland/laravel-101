# Blade

## Blade Templating

Blade is a simple, yet powerful templating engine provided with Laravel. Unlike controller layouts, Blade is driven by _template inheritance_ and _sections_. All Blade templates should use the `.blade.php` extension.

### Defining A Blade Layout

	<!-- Stored in app/views/layouts/master.blade.php -->

	<html>
		<body>
			@section('sidebar')
				This is the master sidebar.
			@show

			<div class="container">
				@yield('content')
			</div>
		</body>
	</html>

### Using A Blade Layout

	@extends('layouts.master')

	@section('sidebar')
		@parent

		<p>This is appended to the master sidebar.</p>
	@stop

	@section('content')
		<p>This is my body content.</p>
	@stop

Note that views which `extend` a Blade layout simply override sections from the layout. Content of the layout can be included in a child view using the `@parent` directive in a section, allowing you to append to the contents of a layout section such as a sidebar or footer.

Sometimes, such as when you are not sure if a section has been defined, you may wish to pass a default value to the `@yield` directive. You may pass the default value as the second argument:

	@yield('section', 'Default Content')

### Stacking Section

You can use `@push` and `@stack` to combine multiple snippet (useful for JavaScript or Widget).

	@push('footer.script')
	<script>
	jQuery(function ($) {
	$('.date').datepicker();
	});
	</script>
	@endpush

Make sure the name of you "stack" does not clash with available section name.

	@stack('footer.script')

## Other Blade Control Structures

### Echoing Data

	Hello, {{{ $name }}}.

	The current UNIX timestamp is {{{ time() }}}.

### Echoing Raw Data

	Hello, {!! $name !!}
	
	The current UNIX timestamp is {!! time() !!}

### Echoing Data After Checking For Existence

Sometimes you may wish to echo a variable, but you aren't sure if the variable has been set. Basically, you want to do this:

	{{{ isset($name) ? $name : 'Default' }}}

However, instead of writing a ternary statement, Blade allows you to use the following convenient short-cut:

	{{{ $name or 'Default' }}}

### Displaying Raw Text With Curly Braces

If you need to display a string that is wrapped in curly braces, you may escape the Blade behavior by prefixing your text with an `@` symbol:

	@{{ This will not be processed by Blade }}

Of course, all user supplied data should be escaped or purified. To escape the output, you may use the triple curly brace syntax:

	Hello, {{{ $name }}}.

If you don't want the data to be escaped, you may use double curly-braces:

	Hello, {{ $name }}.

> **Note:** Be very careful when echoing content that is supplied by users of your application. Always use the triple curly brace syntax to escape any HTML entities in the content.

### If Statements

	@if (count($records) === 1)
		I have one record!
	@elseif (count($records) > 1)
		I have multiple records!
	@else
		I don't have any records!
	@endif

	@unless (Auth::check())
		You are not signed in.
	@endunless

### Loops

	@for ($i = 0; $i < 10; $i++)
		The current value is {{ $i }}
	@endfor

	@foreach ($users as $user)
		<p>This is user {{ $user->id }}</p>
	@endforeach

	@forelse($users as $user)
	  	<li>{{ $user->name }}</li>
	@empty
	  	<p>No users</p>
	@endforelse

	@while (true)
		<p>I'm looping forever.</p>
	@endwhile

### Including Sub-Views

	@include('view.name')

You may also pass an array of data to the included view:

	@include('view.name', array('some'=>'data'))

### Looping Sub-Views

A common way to approach this in Blade could be to do something like this:

	@if (count($records))
	@foreach ($records as $record)
		@include('record.item', $record)
	@endforeach
	@else
		@include('record.no-items')
	@endif

Sure that works but kind of gross with all the nesting and in the wild I’ve seen code like this become unwieldily. To help make this cleaner Blade includes an often overlooked `@each()` option. Here is how that same code could be rewritten.

	// record/list.blade.php
	<ul>
		@each('record.item', $records, 'record', 'record.no-items')
	</ul>

	// record/item.blade.php
	<li>{{ $record->title }}</li>

	// record/no-items.blade.php
	<li>Sorry Charlie, No posts here.</li>

### Overwriting Sections

To overwrite a section entirely, you may use the `overwrite` statement:

	@extends('list.item.container')

	@section('list.item.content')
		<p>This is an item of type {{ $item->type }}</p>
	@overwrite

### Displaying Language Lines

	@lang('language.line')

	@choice('language.line', 1)

### Comments

	{{-- This comment will not be in the rendered HTML --}}

## Extending Blade

Blade even allows you to define your own custom control structures. When a Blade file is compiled, each custom extension is called with the view contents, allowing you to do anything from simple `str_replace` manipulations to more complex regular expressions.

The Blade compiler comes with the helper methods `createMatcher` and `createPlainMatcher`, which generate the expression you need to build your own custom directives.

The `createPlainMatcher` method is used for directives with no arguments like `@endif` and `@stop`, while `createMatcher` is used for directives with arguments.

The following example creates a `@datetime($var)` directive which simply calls `->format()` on `$var`:

	Blade::extend(function($view, $compiler)
	{
		$pattern = $compiler->createMatcher('datetime');

		return preg_replace($pattern, '$1<?php echo $2->format(\'m/d/Y H:i\'); ?>', $view);
	});
