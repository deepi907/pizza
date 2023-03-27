<!DOCTYPE html>
<html>
<head>
	<title>Pizza Designer</title>
	<style>
		.container {
			display: flex;
			align-items: center;
			justify-content: center;
			height: 500px;
			border: 2px solid black;
			border-radius: 50%;
			margin: 50px;
		}
		
		.pizza-base {
			position: absolute;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
			z-index: 1;
		}
		
		.ingredients {
			display: flex;
			flex-wrap: wrap;
			justify-content: center;
			margin: 50px;
		}
		
		.ingredient {
			width: 100px;
			height: 100px;
			background-size: cover;
			background-repeat: no-repeat;
			background-position: center;
			margin: 10px;
			cursor: pointer;
		}
	</style>
</head>
<body>
	<div class="container" ondrop="drop(event)" ondragover="allowDrop(event)">
		<div id="pizza-base" class="pizza-base"></div>
	</div>
	
	<div class="ingredients">
		<div id="thin-crust" class="ingredient" draggable="true" ondragstart="drag(event)" style="background-image: url('thin-crust.jpg')"></div>
		<div id="deep-dish" class="ingredient" draggable="true" ondragstart="drag(event)" style="background-image: url('deep-dish.jpg')"></div>
		<div id="mushrooms" class="ingredient" draggable="true" ondragstart="drag(event)" style="background-image: url('mushrooms.jpg')"></div>
		<div id="pepperoni" class="ingredient" draggable="true" ondragstart="drag(event)" style="background-image: url('pepperoni.jpg')"></div>
		<div id="onions" class="ingredient" draggable="true" ondragstart="drag(event)" style="background-image: url('onions.jpg')"></div>
	</div>

	<script src="pizza.js"></script>
</body>
</html>






java script


var selectedBase = null;
var ingredients = [];

function allowDrop(event) {
	event.preventDefault();
}

function drag(event) {
	event.dataTransfer.setData("text", event.target.id);
}

function drop(event) {
	event.preventDefault();
	var data = event.dataTransfer.getData("text");
	var ingredient = document.getElementById(data);
	if (event.target.id === "pizza-base" && selectedBase != null) {
		ingredients.push(ingredient);
		updatePizza();
	} else {
		alert("Please select a pizza base first.");
	}
}

function selectBase(event, base) {
	selectedBase = base;
	event.dataTransfer.setData("text", event.target.id);
	event.dataTransfer.setDragImage(event.target, 0, 0);
	var pizzaBase = document.getElementById("pizza-base");
	pizzaBase.style.backgroundImage = "url('" + base + ".jpg')";
}

function updatePizza() {
	var pizzaBase = document.getElementById("pizza-base");
	pizzaBase.innerHTML = "";
	pizzaBase.appendChild(selectedBase.cloneNode(true));
	for (var i = 0; i < ingredients.length; i++) {
		pizzaBase.appendChild(ingredients[i].cloneNode(true));
	}
}

document.getElementById("thin-crust").addEventListener("click", function() {
	if (selectedBase != null) {
		var
