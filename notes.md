title: 5 Powerful & Non-popular Frameworks
author:
  name: Cherif BOUCHELAGHEM
  twitter: cherif_b
  github: cherifGsoul
  url: http://cherifbouchelaghem.com
output: index.html
controls: false
theme: sudodoki/reveal-cleaver-theme

--

# 5 Powerful & Non-popular Frameworks

--

## KnockoutJS

Knockout is a JavaScript library that helps you to create rich, responsive display and editor user interfaces with a clean underlying data model. Any time you have sections of UI that update dynamically (e.g., changing depending on the user’s actions or when an external data source changes), KO can help you implement it more simply and maintainably.

--
## CujoJS

CujoJS is an architectural toolkit for building highly modular, maintainable web applications that are easy to test and refactor, with zero framework lock-in.

--

## Aria Templates (AT)
A solid foundation for your web applications is what matters.

--
## Aurelia
is a next gen JavaScript client framework for mobile, desktop and web that leverages simple conventions to empower your creativity. 
--
## CanJS

CanJS is a JavaScript library that makes
developing complex applications simple and fast.
Easy-to-learn, small, and unassuming of your
application structure, but with modern features
like custom tags and 2-way binding. Creating
apps is easy and maintainable.

--
### can.Construct.extend(s,p);

```javascript
var Person = can.Construct.extend({
	init: function (name) {
		this.name = name;
	}
});

var cherif = new Person("Cherif");

cherif.name

```

--
### new can.Map(data)

```javascript
var person = new can.Map({name:'Cherif'});

person.attr('name'); //-> 'Cherif'

person.bind('name',function(ev,newVal,oldVal){
	newVal //-> 'Khaled'
	oldVal //-> 'Cherif'
});

person.attr('name','Khaled');
```

--
### new can.List(data)

```javascript
var hobbies = new can.List(['JS']);

hobbies.attr(0); //-> 'JS'

hobbies.bind ('add',function(ev,items,index){
	items //-> ['bball','football']
	index //-> 1
});

hobbies.push('bball','football');
```

--
### can.compute(data)

```javascript
var age = can.compute(30);

age(); //-> 30

age.bind('change', function ( ev,newVal,oldVal ){
	newVal //-> 31
	oldVal //-> 30
});

age(31);
```

--
### can.compute(getter)
```javascript
var hobbies = ["JS, bball, football"]

var info = can.compute(function(){
	return person.attr("name")+" a "+age()+	" ans et aime: "+hobbies.join(', ')
});

info() //-> "Cherif a 31 ans et aime JS, bball, football"

info.bind('change',function(ev,newVal,oldVal){
	newVal //-> "Cherif a 33 ans et aime JS, bball"
});

hobbies.pop();
```

--
### can.Model.extend(s,p)

```javascript
var Task = can.Model.extend({
	findAll: "GET /tasks",
	findOne: "GET /tasks/{id}",
	create: "POST /tasks",
	update: "PUT /tasks/{id}",
	destroy: "DELETE /tasks/{id}"
},{});

Task.findAll ({due:"today"},function(tasks){});
Task.findOne ({id: 51},function(task){});
```

--
```javascript
var task = new Task({name:"Apprendre CanJS."});

task.save(function(){
	task.attr("name","Apprendre JS et CanJS.")
	.save(function(){
		task.destroy()
	})
});
```

--
## can.Model.List(s,p)

```javascript
var tasks= new Task.List();

can.each(tasks,function(task){
});

//custom model list
Task.List = can.Model.List.extend({
	Map: Task
},{});
```

--
## can.route(route,defaults)

```javascript
can.route("tasks/:id",{ type: "tasks"});

can.route.bind("change", function(){
	if(can.route.attr('type') == "tasks"){
		var id = can.route.attr('id');
		if( id ) {
			Task.findOne({id: id});
		}
	}
});
```

--
## can.Control.extend( p )

```javascript
var Tabs = can.Control.extend({
	init: function( el,options ) {
		// Afficher le premier onglet
	},
	'li click': function( el, ev ) {
		// Masquer les autes onglet
		// Afficher l'onglet selectioné
	}
});

new Tabs('#tabs');
```

--
## Mustache / Handlebars

```javascript
{#if devs.length}}
	{{#each devs}}
		<li>{{name}}</li>
	{{/each}}
{{else}}
	<li>pas de développeurs</li>
{{/if}}

$('#my-el').can.view('devs.mustache',{
	devs: new can.List([{name:'Khaled'}])
});
```

-- 
## can.Component.extend(p)

```javascript
can.Component.extend({
	tag:"ui-panel",
	template: "{{#if active}}<content>...",
	viewModel: {
		active: false,
		....
	},
	helpers: {}
	events: {
		inserted: function(){...}
	}
});
```
```javascript
<ui-tabs>
	{{#each foodTypes}}
		<ui-panel title='title'>
			{{content}}
		</ui-panel>
	{{/each}}
</ui-tabs>
```

--
## 2 way binding

```javascript
var Voyage= can.Map.extend({
	voyageTemp:function(){
		return this.attr('dist')/110 //km/h
	}
});
var alger=new Voyage({
	dist:563.67
});

var template=can.view.mustache('<p><lable>distance:</label>\
								<input can-value="dist"/></p>\
								<p>Temp:{{voyageTemp}}</p>'
								);
$('#vo').html(template(alger));
```

--
## can.view.tag & can.view.attr
can.view tag pour implementer le comportement (behavior)

```javascript
can.view.tag('ui-calender',function(el,tagData){

});
```

can.view tag pour mixer le comportement (mix the behavior)
```javascript
can.view.attr('tooltip',function(el,attrData){

});
```
