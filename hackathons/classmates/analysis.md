# Analysis

{% import './data.html' as data %}

After completing the warmup exercises, your task is to do four more slightly
more challenges analyses.

## How many students like sushi as their favorite food?

{% lodash %}
return _.size(_.filter(_.pluck(data.comments, 'body'), function(comment) {
	return _.includes(comment.toLowerCase(), 'sushi')
}))
{% endlodash %}

The answer is {{result}}.

## Who are the students liking Python the most?

{% lodash %}
var pythonUsers = _.filter(_.pluck(data.comments, 'body'), function(comment) {
	return _.includes(comment.toLowerCase(), 'python')
})

return _.map(pythonUsers, function(comment) {
	var splitText = comment.toLowerCase().split('name:')

	if (_.size(splitText) == 2) {
		var name = splitText[1].split('\r\n')[0]
		return name.trim()
	}
})
{% endlodash %}

Their names are {{result}}.

## Are there more Javascript lovers or Java lovers?

{% lodash %}
var javascriptUsers = _.filter(_.pluck(data.comments, 'body'), function(comment) {
	return (_.includes(comment.toLowerCase(), 'javascript') || _.includes(comment.toLowerCase(), 'js'))
})
var javaUsers = _.filter(_.pluck(data.comments, 'body'), function(comment) {
	if (!_.includes(comment.toLowerCase(), 'javascript')) {
		return _.includes(comment.toLowerCase(), 'java')
	}
	
	return false
})

if (_.size(javascriptUsers) > _.size(javaUsers)) { return 'JavaScript'}
else if (_.size(javaUsers) > _.size(javascriptUsers)) { return 'Java'}
else { return 'They are equal!'}
{% endlodash %}

The answer is {{result}}.

## Who like the same food as `kjblakemore`?

{% lodash %}
var user = 'willzfarmer'

var userComment = _.find(data.comments, function(comment) {
	return comment.user.login == user
})
var food = userComment.body.toLowerCase().split('food:')[1]

var foodMatch = _.filter(data.comments, function(comment) {
	if (comment.user.login != user) {
		var splitText = comment.body.toLowerCase().split('food:')

		if (_.size(splitText) == 2) {
			return _.includes(splitText[1], food)
		}
	}
	
	return false
})

return _.map(_.pluck(foodMatch, 'body'), function(comment) {
	var splitText = comment.toLowerCase().split('name:')

	if (_.size(splitText) == 2) {
		var name = splitText[1].split('\r\n')[0]
		return name.trim()
	}
})
{% endlodash %}

Their names are {{result}}.
