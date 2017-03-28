{% highlight javascript %}
;(function (factory) {
	// Factory run with jQuery.
	if (typeof define === 'function' && define.amd) {
		// AMD. Register as anonymous module.
		define(['jquery'], factory);
	} else if (typeof exports === 'object') {
		// Node / CommonJS
		factory(require('jquery'));
	} else {
		// Browser globals.
		factory(jQuery);
	}
})(function ($) {

	'use strict';

	var $window = $(window),
		$document = $(document);

	var console = window.console || { log: function () {} };

	function XXX(argument) {

		// body...

	}

	XXX.prototype = {

		// body...

		constructor: XXX,

		// body...
	};

	// Save the other cropper
	XXX.other = $.fn.xxx;

	// Register as jQuery plugin
	$.fn.xxx = function (options) {
		var args = toArray(arguments, 1),
			result;

		this.each(function () {
			var $this = $(this),
				data = $this.data('cropper'),
				fn;

			if (!data) {
				$this.data('cropper', (data = new Cropper(this, options)));
			}

			if (typeof options === 'string' && $.isFunction((fn = data[options]))) {
				result = fn.apply(data, args);
			}
		});

		return isUndefined(result) ? this : result;
	};

	// No conflict
	$.fn.xxx.noConflict = function () {
		// $.fn.xxx = XXX.other;
		// return this;
	};

	$(function () {
		return new XXX(argument);
	});

});
{% endhighlight javascript %}