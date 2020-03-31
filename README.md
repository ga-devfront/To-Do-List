# To Do List
correction school project and improvement of a to-do list app.

## Badges
![GitHub repo size](https://img.shields.io/github/repo-size/ga-devfront/To-Do-List)
![GitHub last commit](https://img.shields.io/github/last-commit/ga-devfront/To-Do-List)
![GitHub top language](https://img.shields.io/github/languages/top/ga-devfront/To-Do-List)

![GitHub](https://img.shields.io/github/license/ga-devfront/To-Do-List)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/97f077c5858a4ca99ce973e1868966c9)](https://www.codacy.com/manual/ga-devfront/To-Do-List?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=ga-devfront/To-Do-List&amp;utm_campaign=Badge_Grade)
[![time tracker](https://wakatime.com/badge/github/ga-devfront/To-Do-List.svg)](https://wakatime.com/badge/github/ga-devfront/To-Do-List)

## Detailed App
You will find below the tree structure of the application's main files 
followed by their detailed description. 

```
📄 index.html

📁 js
↳ 📄 helpers.js
↳ 📄 app.js
↳ 📄 store.js
↳ 📄 model.js
↳ 📄 template.js
↳ 📄 view.js
↳ 📄 controller.js

📁 node_modules

📁 test
↳ 📄 ControllerSpec.js
↳ 📄 SpecRunner.html
```
### 📄 [index.html](index.html) :
HTML file structuring the display of the application and imports JS files.

### 📁 [js](js) :
Core folder containing all the JS files useful for the proper functioning of the application.

- ### 📄 [helper.js](js/helpers.js) :
  Helper is a homemade framework, lighter thant a complete framework (like JQuery) because it only contains the useful functions for the application. It's important to know it for understund the others JS files.
  - ```qs (selector, scope)``` : contraction of `querySelector`. Return the first element matching in the DOM.
    
    ***note:** if `scope` is not defined `document` is used.*
  - ```qsa (selector, scope)``` : contraction of `querySelectorAll`. Return a list of elements matching in the DOM.
  
    ***note:** if `scope` is not defined `document` is used.*
  - ```$on (target, type, callback, useCapture)``` : it's an `addEventListener` function. Add a eventListener to the target.

    ***note:** `useCapture` is optional.*
  - ```$delegate (target, selector, type, handler)``` : it's an complex `addEventListener`. He use ```qsa``` & ```$on``` helper function. Add eventListener to an actual DOM element or a future DOM element.
  - ```$parent (element, tagName)``` : this function return the parent of the element if he got it.

- ### 📄 [app.js](js/app.js) :
  This file initialise the app, with his store, model, template, view & controller. He update the view at page load or in changed url with ```$on``` defined on helper.js.

- ### 📄 [store.js](js/store.js) :
  Store as his name suggest create a local storage if no storage has created before. He use `name` and `callback` *(callback only be used if we make AJAX calls)* parameters for run it. This constructor only be used on `model.js`, it brings several methods that you can find below.
  - ```Store.prototype.find (query, callback)``` :  used to finds items.
  - ```Store.prototype.findAll (callback)``` : for recover all data from the store.
  - ```Store.prototype.save (updateData, callback, id)``` : can be used for save or udpate data in the storage.

    ***note:** `id` is used for update existing item.*
  - ```Store.prototype.remove (id, callback)``` : remove an item from the Store by this ID.
  - ```Store.prototype.drop (callback)``` : used for remove all the Store and create a fresh one.

- ### 📄 [model.js](js/model.js) :
  This file initialise the model, he recover the store and manage the data. He use `storage` for run it. This constructor only be used on `controller.js`, you will find below these methods.
  - ```Model.prototype-create (title, callback)``` : create a new todo model.

    ***note:** use `save` method from `store.js`.*
  - ```Model.prototype.read (query, callback)``` : finds and returns a model in storage. If no `query` is given it return all model in storage.
  
    ***note:** use `find` and `findAll`method from `store.js`.*
  - ```Model.prototype.update (id, data, callback)``` : update a model in storage by this ID.

    ***note:** use `save` method from `store`.*
  - ```Model.prototype.remove (id, callback)``` : remove a model from storage by this ID.

    ***note:** use `remove` method from `store`.*
  - ```Model.prototype.removeAll (callback)``` : this method remove all the model from storage.

    ***note:** use `drop` method from `store`.*
  - ```Model.prototype.getCount (callback)``` : use the actuel number of all todos (active, completed, total) in the storage in a callback parameter.

    ***note:** use `findAll` method from `store`.*

- ### 📄 [template.js](js/template.js) :
  Template is the HTML code manager. He used some functions for catch escaped HTML. This constructor only be used on `view.js`, you will find below these methods.
  - ```Template.prototype.show (data)``` : create a `<li>` element and return it for placement in the app.
  - ```Template.prototype.itemCounter (activeTodos)``` : return a display counter of how many todos are left to complete.
  - ```Template.prototype.clearCompletedButton (completedTodos)``` : manage the clear completed button.

- ### 📄 [view.js](js/view.js) :
  This file will take care of the display. It will recover template as well as the various elements of the DOM with the `qs` and `qsa` from `helper.js`. He is only used on `controller.js` with `model.js`. He has two principal methods `View.prototype.render` and `View.prototype.vind` wich use the other methods present in this file and `template.js` methods, details are below.
  - ```View.prototype._removeItem (id)``` : suppress a todo from the DOM by is ID.
  - ```View.prototype._clearCompletedButton (completedCount, visible)``` : takes care of the display or not of the clearCompleted button.
  - ```View.prototype._setFilter (currentPage)``` : add the selection class to the right button.
  - ```View.prototype._elementComplete (id, completed)``` : add or remove the completed class at the todo.
  - ```View.prototype._editItem (id, title)``` : add the editing class and input.
  - ```View.prototype._editItemDone (id, title)``` : remove editing class and input.
  - ```View.prototype.render (viewCmd, parameter)``` : use the viewCmd parameter to launch a specific function with the parameters entered.
    - ```showEntries``` : display a todo.

      ***note:** use `show` method from `template`.*
    - ```removeItem``` : suppress a todo from the DOM.
    - ```updateElementCount``` : update the todo number.

      ***note:** use `itemCounter` method from `template`.*
    - ```clearCompletedButton``` : update the clear completed todo button.
    - ```contentBlockVisibility``` : display or not the bottom of todo list (filter, count, clear button).
    - ```toggleAll``` : check all todo.
    - ```setFilter``` : manage the actual filter.
    - ```clearNewTodo``` : clear the new todo's input text.
    - ```elementComplete``` : manage the actual status of a todo.
    - ```editItem``` : change todo to edit it.
    - ```editItemDone``` : exits the todo editing mode.
  - ```View.prototype._itemId (element)``` : recover an ID of a DOM todo.
  - ```View.prototype._bindItemEditDone (handler)``` : end the edit mode of a todo if enter key is pressed or if the todo is unfocus.
  - ```View.prototype._bindItemEditCancel (handler)``` : cancel the edit mode of a todo if escape key is pressed.
  - ```View.prototype.bind (event, handler)``` : adds a selected event to the element passed in parameter.

- ### 📄 [controller.js](js/controller.js) :
  Controller performs the link between the database with `model.js` and the display with `view.js` . At the beginning of this file events are given to the elements of the DOM to use the methods that can be found below.
  - ```Controller.prototype.setView (locationHash)``` : loads and initialises the view.
  - ```Controller.prototype.showAll ()``` : load and display all items in todo list.

    ***note:** use `read` method from `model` & `render` method from `view`.*
  - ```Controller.prototype.showActive ()``` : load and display only active items in todo list.

    ***note:** use `read` method from `model` & `render` method from `view`.*
  - ```Controller.prototype.showCompleted ()``` : load and display only completed items in todo list.

    ***note:** use `read` method from `model` & `render` method from `view`.*
  - ```Controller.prototype.addItem (title)``` : create a new todo model and clear the input of new todo after.

    ***note:** use `create` method from `model` & `render` method from `view`.*
  - ```Controller.prototype.editItem (id)``` : take a model from data by is ID and start editing is title.

    ***note:** use `read` method from `model` & `render` method from `view`.*
  - ```Controller.prototype.editItemSave (id, title)``` : finish the editing mode and save it in data or delete it if no title is passed.

    ***note:** use `update` method from `model` & `render` method from `view`.*
  - ```Controller.prototype.editItemCancel (id)``` : cancel the editing mode.

    ***note:** use `read` method from `model` & `render` method from `view`.*
  - ```Controller.prototype.removeItem (id)``` : remove an item in data and in the DOM by is ID.

    ***note:** use `remove` method from `model` & `render` method from `view`.*
  - ```Controller.prototype.removeCompletedItems ()``` : search the item completed in the data and remove it from the DOM and the data.

    ***note:** use `read` method from `model`.*
  - ```Controller.prototype.toggleComplete (id, completed, silent)``` : switch an item to completed in data and DOM.

    ***note:** use `update` method from `model` & `render` method from `view`.*
  - ```Controller.prototype.toggleAll (completed)``` : switch all item to completed in data and DOM.

    ***note:** use `read` method from `model`.*
  - ```Controller.prototype._updateCount ()``` : manage display of all bottom element with the active, completed and total todos count.

    ***note:** use `getCount` method from `model` & `render` method from `view`.*
  - ```Controller.prototype._filter (force)``` : filter the todos items by is active url.
  - ```Controller.prototype._updateFilterState (currentPage)``` : updates the filter nav's selected states.

    ***note:** use `render` method from `view`.*

### 📁 [node_modules](node_modules) :
Contain only the **Jasmine** test framework and his dependency for see it in navigator.

### 📁 [test](test) :
Contain the **Jasmine** tests.

- ### 📄 [ControllerSpec.js](test/ControllerSpec.js) :
  This file contain the **Jasmine** tests for each method we use in the others files.

- ### 📄 [SpecRunner.html](test/SpecRunner.html) :
  This is the html result of **Jasmine** tests.

## Fixes
This is the non-exhaustive list of fixes applied to the project with their issues, commit and pull requests :
- **typo problem :** [issue](https://github.com/ga-devfront/To-Do-List/issues/4) → [commit](https://github.com/ga-devfront/To-Do-List/commit/123f7e321338e34de983cd545dbc03f233aed4cc) → pull request
- **ID conflict :** [issue](https://github.com/ga-devfront/To-Do-List/issues/4) → [commit](https://github.com/ga-devfront/To-Do-List/commit/778317f5d67faa0a27408b7ecc7517f95d4e457f) → pull request

## Improuvements
This is the non-exhaustive list of improuvements applied to the project with their issues and pull requests :
- *Empty*

## Authors
- Guyomar Alexis - [ga-devfront](https://github.com/ga-devfront/)

See also the list of [contributors](https://github.com/ga-devfront/To-Do-List/graphs/contributors) who participated in this project

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
