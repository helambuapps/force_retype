#Force Retype HTML forms


Ways to force users to retype the email address and passwords in a HTML form

Imagine you want people to retype the email addresses or/and a password on one of your registration forms

##Method 1: Pure HTML
```html
<input name="retype-email" type="text" onDrop="return false" 
    onPaste="return false" autocomplete=off />
```

##Method 2: Zepto/jQuery plugin
I haven't tested the Zepto version at all.

HTML
```html
<input name="retype-email" type="text" class=".disable-copy" />
```
Javascript
```javascript
var Zepto = Zepto || null;

(function($){
	$.fn.disableCopy = function() {
		$(this).attr({
			autocomplete: 'off',
			onPaste: 'return false',
			onDrop: 'return false'
		});

		return this;
	};
})(Zepto || jQuery);


$(".disable-copy").disableCopy();
```

##Method 3: Simple Javascript
HTML
```html
<input name="retype-email" type="text" class=".disable-copy" />
```

Javascript
```javascript
var nodes = document.querySelectorAll(".disable-copy");

for (index in nodes) {
	nodes[index].setAttribute('autocomplete', 'off');
	nodes[index].setAttribute('onPaste', 'return false');
	nodes[index].setAttribute('onDrop', 'return false');
}
```

##Method 4: Javascript prototype
HTML
```html
<input name="retype-email" type="text" class=".disable-copy" />
```

Javascript
```javascript
function edQuery(selector) {
	return document.querySelectorAll(selector);
}

NodeList.prototype.disableCopy = function() {
	for (var index = 0; index < this.length; ++index) {
		var node = this[index];

		// Ignore if it is not a text field
		if (node.nodeName != "INPUT" && node.type != "text")
			continue;

		node.setAttribute('autocomplete', 'off');
		node.setAttribute('onPaste', 'return false');
		node.setAttribute('onDrop', 'return false');
	}
}

(function($) {
	$(".disable-copy").disableCopy();
})(edQuery);
```
