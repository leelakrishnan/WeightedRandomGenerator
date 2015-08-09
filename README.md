# WeightedRandomGenerator

http://codetheory.in/weighted-biased-random-number-generation-with-javascript-based-on-probability/

https://jsfiddle.net/b33bgeLv/2/

/*
Open the console and keep on refreshing the demo to check
the randomness of items picked.
*/

var rand = function(min, max) {
	return Math.random() * (max - min) + min;
};

var getRandomItem = function(list, weight) {
	var total_weight = weight.reduce(function (prev, cur, i, arr) {
		return prev + cur;
	});
	
	var random_num = rand(0, total_weight);
	var weight_sum = 0;
	//console.log(random_num)
	
	for (var i = 0; i < list.length; i++) {
		weight_sum += weight[i];
		weight_sum = +weight_sum.toFixed(2);
		
		if (random_num <= weight_sum) {
			return list[i];
		}
	}
	
	// end of function
};

var list = ['javascript', 'php', 'ruby', 'python'];
var weight = [0.5, 0.2, 0.2, 0.1];
var random_item = getRandomItem(list, weight);

console.log(random_item)

var random_check = {
	javascript: 0,
	php: 0,
	ruby: 0,
	python: 0
};

var random_num
	, item;

for (var i = 0; i < 100; i++) {
	item = getRandomItem(list, weight);
	++random_check[item];
}

console.log(random_check);
