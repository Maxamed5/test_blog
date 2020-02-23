+++
title = "The Most important thing about Vue.js"
date = "2020-02-24"
draft = false
pinned = false
description = "*Vue .js allows you to simply bind data models to the representation layer.\n*it also allows you to easily reuse components throughout the application.\n\n*you don't need to create special models or collections and to register events object in there.\n *you don't need to follow some special syntax. You don't need to install any of the never-ending dependencies. \n\n\n\n "
+++
```
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta http-equiv="X-UA-Compatible" content="ie=edge">
<title>ShoppinList</title>
<!--Css-->
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
<link rel="stylesheet" type="text/css" href="ShoppinList/ShoppinList.css">
<!--JQuery-->
<script
  src="https://code.jquery.com/jquery-3.4.1.js"
  integrity="sha256-WpOohJOqMqqyKL9FccASB9O0KwACQJpFTUBLTYOVvVU="
  crossorigin="anonymous"></script>
</head>
<body>
<div class="container">
<h2>My Shopping List</h2>
<div class="input-group">
<input placeholder="add shopping list item"
type="text" class="js-new-item form-control">
<span class="input-group-btn">
<button @click="addItem" class="js-add btn btn-default"
type="button">Add!</button>
</span>
</div>
<ul>
<li>
<div class="checkbox">
<label>
<input class="js-item" name="list"
type="checkbox"> Carrot
</label>
</div>
</li>
<li>
<div class="checkbox">
<label>
<input class="js-item" name="list" type="checkbox"> Book
</label>
</div>
</li>
<li class="removed">
<div class="checkbox">
<label>
<input class="js-item" name="list" type="checkbox"
checked> Gift for aunt's birthday
</label>
</div>
</li>
</ul>
</div>

<div class="container">
    <h2>My Shopping List</h2>
    <!-- ... -->
    <div class="footer">
    <hr/>
    <em>Change the title of your shopping list here</em>
    <input class="js-change-title" type="text"
    value="My Shopping List"/>
    </div>
   </div>

<!--JavaScript-->
<script>
    $(document).ready(function () {
 /**
 * Add button click handler
 */
 function onAdd() {
 var $ul, li, $li, $label, $div, value;
 value = $('.js-new-item').val();
 //validate against empty values
 if (value === '') {
 return;
 }
 $ul = $('ul');
 $li = $('<li>').appendTo($ul);
 $div = $('<div>')
 .addClass('checkbox')
 .appendTo($li);
 $label = $('<label>').appendTo($div);
 $('<input>')
 .attr('type', 'checkbox')
 .addClass('item')
 .attr('name', 'list')
 .click(toggleRemoved)
 .appendTo($label);
 $label
 .append(value);
 $('.js-new-item').val('');
 }
 /**
 * Checkbox click handler -
 * toggles class removed on li parent element
 * @param ev
 */
 function toggleRemoved(ev) {
 var $el;
 $el = $(ev.currentTarget);
 $el.closest('li').toggleClass('removed');
 }
 $('.js-add').click(onAdd);
 $('.js-item').click(toggleRemoved);
});

//And javascript code:
function onChangeTitle() {
 $('h2').text($('.js-change-title').val());
}
$('.js-change-title').keyup(onChangeTitle);
</script>
</body>
</html>
```

```
.container {
    width: 40%;
    margin: 20px auto 0px auto;
   }
   .removed {
    color: gray;
   }
   .removed label {
    text-decoration: line-through;
   }
   ul li {
    list-style-type: none;
   }
  
```
