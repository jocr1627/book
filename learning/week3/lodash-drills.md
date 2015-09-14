# Lodash Drills

Complete the following Lodash exercises. The goal is to become really good at
functional programming paradigm (e.g., `_.map`, `_.filter`, `_.all`, `_.any` ...etc) and
a number of really useful Lodash methods (e.g., `_.find`, `_.pluck` ... etc).

* enter your solution in the `solution` block
* utilize lodash functions as much as possible
* no `for/while` loop is allowed

Familiarity with programming in this way will not only make you a super productive
programmer but also will pave the way for you to learn MapReduce and MongoDB.

# Examples

{% lodashexercise %}

{% title %}

How many people?

{% data %}

[{name: 'John'}, {name: 'Mary'}, {name: 'Joe'}, {name: 'Ben'}]

{% output %}

4

{% solution %}

return data.length

{% endlodashexercise %}


{% lodashexercise %}

{% title %}

What are the names?

{% data %}

[{name: 'John'}, {name: 'Mary'}, {name: 'Joe'}, {name: 'Ben'}]

{% output %}

['John', 'Mary','Joe','Ben']

{% solution %}

return _.map(data, function(d){
    return d.name
})

{% endlodashexercise %}

# Exercises

{% lodashexercise %}

{% title %}

What names begin with the letter J?

{% data %}

[{name: 'John'}, {name: 'Mary'}, {name: 'Joe'}, {name: 'Ben'}]

{% output %}

['John','Joe']

{% solution %}

return _.filter(_.pluck(data, 'name'), function(name) {
	if (name[0] == 'J') return true
	else return false
})

{% endlodashexercise %}



{% lodashexercise %}

{% title %}

How many Johns?

{% data %}

[{name: 'John'}, {name: 'John'}, {name: 'John'}, {name: 'Ben'}]

{% output %}

3

{% solution %}
return _.size(_.filter(_.pluck(data, 'name'), function(name) {
	if (name == 'John') return true
	else return false
}))

{% endlodashexercise %}




{% lodashexercise %}

{% title %}

What are all the first names?

{% data %}

[{name: 'John Smith'}, {name: 'Mary Kay'}, {name: 'Peter Pan'}, {name: 'Ben Franklin'}]

{% output %}

["John","Mary","Peter","Ben"]

{% solution %}
return _.map(_.pluck(data, 'name'), function(name) {
	return name.split(' ')[0]
})

{% endlodashexercise %}







{% lodashexercise %}

{% title %}

What are the first names of Smith?

{% data %}

[{name: 'John Smith'}, {name: 'Mary Smith'}, {name: 'Peter Pan'}, {name: 'Ben Smith'}]

{% output %}

["John","Mary","Ben"]

{% solution %}
return _.map(_.filter(_.pluck(data, 'name'), function(name) {
	if (name.split(' ')[1] == 'Smith') return true
	else return false
}), function (name) {
	return name.split(' ')[0]
})
{% endlodashexercise %}







{% lodashexercise %}

{% title %}

Change the format to lastname, firstname

{% data %}

[{name: 'John Smith'}, {name: 'Mary Kay'}, {name: 'Peter Pan'}]

{% output %}

[{name: 'Smith, John'}, {name: 'Kay, Mary'}, {name: 'Pan, Peter'}]

{% solution %}
return _.map(data, function(person) {
	var splitName = person.name.split(' ')
	return {name: splitName[1] + ', ' + splitName[0]}
})
{% endlodashexercise %}



{% lodashexercise %}

{% title %}

How many women?

{% data %}

[{name: 'John Smith', gender: 'm'}, {name: 'Mary Smith', gender: 'f'}, {name: 'Peter Pan', gender: 'm'}, {name: 'Ben Smith', gender: 'm'}]

{% output %}

1

{% solution %}

return _.size(_.filter(_.pluck(data, 'gender'), function(gender) {
	if (gender == 'f') return true
	else return false
}))

{% endlodashexercise %}







{% lodashexercise %}

{% title %}

How many men whose last name is Smith?

{% data %}

[{name: 'John Smith', gender: 'm'}, {name: 'Mary Smith', gender: 'f'}, {name: 'Peter Pan', gender: 'm'}, {name: 'Ben Smith', gender: 'm'}]

{% output %}

2

{% solution %}

return _.size(_.filter(data, function(person) {
	if (person.gender == 'm' && person.name.split(' ')[1] == 'Smith') return true
	else return false
}))

{% endlodashexercise %}







{% lodashexercise %}

{% title %}

Are there more men than women?

{% data %}

[{name: 'John Smith', gender: 'm'}, {name: 'Mary Smith', gender: 'f'}, {name: 'Peter Pan', gender: 'm'}, {name: 'Ben Smith', gender: 'm'}]

{% output %}

true

{% solution %}

return _.size(_.filter(_.pluck(data, 'gender'), function(gender) {
	if (gender == 'm') return true
	else return false
})) > _.size(_.filter(_.pluck(data, 'gender'), function(gender) {
	if (gender == 'f') return true
	else return false
}))

{% endlodashexercise %}







{% lodashexercise %}

{% title %}

What is Peter Pan's gender?

{% data %}

[{name: 'John Smith', gender: 'm'}, {name: 'Mary Smith', gender: 'f'}, {name: 'Peter Pan', gender: 'm'}, {name: 'Ben Smith', gender: 'm'}]

{% output %}

'm'

{% solution %}

return _.find(data, 'name', 'Peter Pan').gender

{% endlodashexercise %}





{% lodashexercise %}

{% title %}

What is the oldest age?

{% data %}

[{name: 'John Smith', age: 54}, {name: 'Mary Smith', age: 42}, {name: 'Peter Pan', age: 15}, {name: 'Ben Smith', age: 35}]

{% output %}

54

{% solution %}

return _.max(_.pluck(data, 'age'))

{% endlodashexercise %}






{% lodashexercise %}

{% title %}

Is it true everyone is younger than 60?

{% data %}

[{name: 'John Smith', age: 54}, {name: 'Mary Smith', age: 42}, {name: 'Peter Pan', age: 15}, {name: 'Ben Smith', age: 35}]

{% output %}

true

{% solution %}

return _.all(_.pluck(data, 'age'), function(age) {
	if (age < 60) return true
	else return false
})

{% endlodashexercise %}




{% lodashexercise %}

{% title %}

Is it true someone is not an adult (younger than 18)?

{% data %}

[{name: 'John Smith', age: 54}, {name: 'Mary Smith', age: 42}, {name: 'Peter Pan', age: 15}, {name: 'Ben Smith', age: 35}]

{% output %}

true

{% solution %}

return _.some(_.pluck(data, 'age'), function(age) {
	if (age < 18) return true
	else return false
})

{% endlodashexercise %}




{% lodashexercise %}

{% title %}

How many people whose favorites include food?

{% data %}

[{name: 'John Smith', age: 54, favorites: ['food', 'movies']},
 {name: 'Mary Smith', age: 42, favorites: ['food', 'travel']},
 {name: 'Peter Pan', age: 15, favorites: ['minecraft', 'pokemo']},
 {name: 'Ben Smith', age: 35, favorites: ['craft', 'food']}]

{% output %}

3

{% solution %}

return _.size(_.filter(_.pluck(data, 'favorites'), function(favorites) {
	return _.includes(favorites, 'food')
}))

{% endlodashexercise %}





{% lodashexercise %}

{% title %}

Who are over 40 and love travel?

{% data %}

[{name: 'John Smith', age: 54, favorites: ['food', 'movies']},
 {name: 'Mary Smith', age: 42, favorites: ['food', 'travel']},
 {name: 'Peter Pan', age: 15, favorites: ['minecraft', 'pokemo']},
 {name: 'Joe Johnson', age: 46, favorites: ['travel', 'movies']},
 {name: 'Ben Smith', age: 35, favorites: ['craft', 'food']}]

{% output %}

['Mary Smith', 'Joe Johnson']

{% solution %}

return _.pluck(_.filter(data, function(person) {
	if (person.age > 40 && _.includes(person.favorites, 'travel')) return true
	else return false
}), 'name')

{% endlodashexercise %}




{% lodashexercise %}

{% title %}

Who is the oldest person loving food?

{% data %}

[{name: 'John Smith', age: 54, favorites: ['food', 'movies']},
 {name: 'Mary Smith', age: 42, favorites: ['food', 'travel']},
 {name: 'Peter Pan', age: 15, favorites: ['minecraft', 'pokemo']},
 {name: 'Joe Johnson', age: 46, favorites: ['travel', 'movies']},
 {name: 'Ben Smith', age: 35, favorites: ['craft', 'food']}]

{% output %}

'John Smith'

{% solution %}

return _.last(_.sortBy(_.filter(data, function(person) {
	if (_.includes(person.favorites, 'food')) return true
	else return false
}), function(person) {
	return person.age
})).name

{% endlodashexercise %}



{% lodashexercise %}

{% title %}

What are all the unique favorites?

{% data %}

[{name: 'John Smith', age: 54, favorites: ['food', 'movies']},
 {name: 'Mary Smith', age: 42, favorites: ['food', 'travel']},
 {name: 'Peter Pan', age: 15, favorites: ['minecraft', 'pokemo']},
 {name: 'Joe Johnson', age: 46, favorites: ['travel', 'movies']},
 {name: 'Ben Smith', age: 35, favorites: ['craft', 'food']}]

{% output %}

[
  "food",
  "movies",
  "travel",
  "minecraft",
  "pokemo",
  "craft"
]

{% solution %}

return _.uniq(_.flatten(_.pluck(data, 'favorites')))

{% endlodashexercise %}



{% lodashexercise %}

{% title %}

What are all the unique last names?

{% data %}

[{name: 'John Smith', age: 54, favorites: ['food', 'movies']},
 {name: 'Mary Smith', age: 42, favorites: ['food', 'travel']},
 {name: 'Peter Pan', age: 15, favorites: ['minecraft', 'pokemo']},
 {name: 'Joe Johnson', age: 46, favorites: ['travel', 'movies']},
 {name: 'Ben Smith', age: 35, favorites: ['craft', 'food']}]

{% output %}

[
  "Smith",
  "Pan",
  "Johnson"
]

{% solution %}

return _.uniq(_.flatten(_.map(_.pluck(data, 'name'), function(name) {
	return name.split(' ')[1]
})))

{% endlodashexercise %}
