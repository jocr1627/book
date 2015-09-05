{% import '../../hackathons/classmates/data.html' as data %}

# Report

As a class, we brainstormed and came up with a long list of further questions we can ask based
on the "self-introduction" data. Out of these questions, our team chose to tackle on
the following:

# How many applied math majors are there in the class?

{% lodash %}
return _.size(_.filter(_.pluck(data.comments, 'body'), function(comment) {
	if (_.includes(comment.toLowerCase(), 'applied math')) {
		return true
	} else {
		return false
	}
}))
{% endlodash %}

There are {{result}} applied math majors.

# How many students submitted after the first day of class?

{% lodash %}
return _.size(_.filter(_.pluck(data.comments, 'created_at'), function(comment) {
	if (comment.split('T')[0].split('-')[2] > 24) {
		return true
	} else {
		return false
	}
}))
{% endlodash %}

There were {{result}} submissions after the first day of class.

# Who was the first person to submit Sushi as their favorite food?

{% lodash %}
var sushiComment = _.find(_.pluck(data.comments, 'body'), function(comment) {
	return _.includes(comment.toLowerCase(), 'sushi')
})

return sushiComment.toLowerCase().split('name:')[1].split('\r\n')[0].trim()
{% endlodash %}

{{result}} was the first person to submit "Sushi" as their favorite food.

# How many people submitted before noon overall?

{% lodash %}
return _.size(_.filter(_.pluck(data.comments, 'created_at'), function(comment) {
	if (comment.split('T')[1].split(':')[0] < 12) {
		return true
	} else {
		return false
	}
}))
{% endlodash %}

There were {{result}} submissions made before noon on their day of submission.
