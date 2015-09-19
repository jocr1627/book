{% data src="fcq.clean.json" %}
{% enddata %}

# Warmup

Next, complete the following warmup exercises as a team.

## How many unique subject codes?

{% lodash %}
return _.size(_.uniq(_.pluck(data, 'Subject')))
{% endlodash %}

They are {{ result }} unique subject codes.

## How many computer science (CSCI) courses?

{% lodash %}
return _.size(_.filter(_.pluck(data, 'Subject'), function(subject) {
	if (subject == 'CSCI') return true
	else return false
}))
{% endlodash %}

They are {{ result }} computer science courses.

## What is the distribution of the courses across subject codes?

{% lodash %}
return _.countBy(_.pluck(data, 'Subject'))
{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>

## What subset of these subject codes have more than 100 courses?

{% lodash %}
var grps = _.groupBy(data, 'Subject')
var ret = _.pick(_.mapValues(grps, function(d){
	return d.length
}), function(x){
    return x > 100
})
return ret
{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>

## What subset of these subject codes have more than 5000 total enrollments?

{% lodash %}
var grps = _.groupBy(data, 'Subject')
var ret = _.pick(_.mapValues(grps, function(d){
	return _.sum(_.pluck(d, 'N.ENROLL'))
}), function(x){
    return x > 5000
})
return ret
{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>

## What are the course numbers of the courses Tom (PEI HSIU) Yeh taught?

{% lodash %}
return _.pluck(_.filter(data, function(course) {
	return _.includes(_.pluck(course.Instructors, 'name'), "YEH, PEI HSIU")
}), 'Course')
{% endlodash %}

They are {{result}}.
