---
date created: Sunday, August 11th 2024, 7:58:53 pm
date modified: Sunday, August 11th 2024, 8:33:19 pm
tags:
  - javascript
  - 100xdevs
  - web-dev
  - moc/web-dev
---

# Learning Today 

1. Classes in JS
2. Revise callbacks
3. Callback Hell
4. Promises
5. Async Await

# Classes in JS

#### Primitive Types
#### Complex Types
- Objects
- Arrays

#### Classes

In JavaScript, classes are a way to define blueprint for creating object (these objects are different from the objects defined in the last section).

```js
class Rectangle {
	constructor(width, height, color) {
		this.width = width;
		this.height = height;
		this.color = color;
	}

	area() {
		const area = this.width * this.height;
		return area;
	}
	paint() {
		console.log(`Painting with color ${this.color}`);
	}
}

const rect = new Rectangle(2, 4, 'red');
const area = rect.area();
console.log(area);
```

Here above we are instantiating the Rectangle class and calling it's methods.
`this` variable above is equal to `rect`.
