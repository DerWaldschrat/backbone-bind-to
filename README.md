Backbone.BindTo
===============

[Backbone.js](http://documentcloud.github.com/backbone/) extension for automatic binding and unbinding of model events to views.

### Features

#### BindToModel

In a lot of [Backbone.js](http://documentcloud.github.com/backbone/) applications when you want to react to __model__ events you have to write:

```javascript
window.UserCard = Backbone.View.extend({
  initialize: function() {
    this.model.bind('change:name',  this.renderName,  this);
    this.model.bind('change:email', this.renderEmail, this);
  },
  remove: function() {
    this.model.unbind('change:name',  this.renderName,  this);
    this.model.unbind('change:email', this.renderEmail, this);
    Backbone.View.prototype.remove.call(this);
  },
  renderName:  function() { /* ... code ... */ },
  renderEmail: function() { /* ... code ... */ }
});
```

With Backbone.BindTo you can just do:

```javascript
window.UserCard = Backbone.View.extend({
  bindToModel: {
    'change:name':  'renderName',
    'change:email': 'renderEmail'
  },
  renderName:  function() { /* ... code ... */ },
  renderEmail: function() { /* ... code ... */ }
});
```

#### BindToCollection

Of course, there is a similar method for binding to collection events:

```javascript
window.TodoListView = Backbone.View.extend({
  bindToCollection: {
    'add': 'renderNewTask'
  },
  renderNewTask: function() { /* ... code ... */ }
});
```

#### Remove

Backbone.BindTo automatically ```unbinds``` from all model and collection events when the view element is removed via ```Backbone.View#remove```.

#### noConflict

If extending directly ```Backbone.View``` bothers you. You can use the ```Backbone.BindTo.noConflict``` method. It  restores ```Backbone.View``` to its original value. And returns the ```Backbone.BindTo.View``` object which has the ```bindToModel``` and ```bindToCollection``` helpers.

```javascript
window.BindToView = Backbone.BindTo.noConflict()
```

### Installing

Just copy ```lib/backone_bind_to.js``` into your project. Or if you are using [CoffeeScript](http://http://coffeescript.org/) you can use directly - ```src/backbone_bind_to.coffee```.

### Requirements

```
Backbone.js - 0.9.2+
```

### Running the tests

Just open - ```test/runner.html```

### Contributing

Every fresh idea and contribution will be highly appreciated.

If you are making changes please do so in the ```coffee``` files. And then compile them with:

```
cake build
```

### License

MIT License.
