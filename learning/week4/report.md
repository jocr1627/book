{% data src="fcq.clean.json" %}
{% enddata %}

# Report

As a class, we brainstormed and came up with a long list of further questions we
can ask based on the FCQ data. Out of these questions, our team chose to tackle on
the following questions. Each member on our team is reponsible for one question.

# What classes have very different workloads compared to credit hours?

{% lodash %}
return _.filter(data, function(course) {
	var thresh = 3
	return ((course.Workload.Raw - course.Hours > thresh) ||
	(course.Workload.Raw - course.Hours < -1*thresh) &&
	course.Workload.Raw > 0)
})
{% endlodash %}

<table>
	<tr>
		<td>Subject</td>
		<td>Course Number</td>
		<td>Hours</td>
		<td>Workload</td>
	</tr>
{% for course in result %}
    <tr>
        <td>{{course.Subject}}</td>
        <td>{{course.Course}}</td>
		<td>{{course.Hours}}</td>
        <td>{{course.Workload.Raw}}</td>
    </tr>
{% endfor %}
</table>

# (Question 2) by (Name)

{% lodash %}
return "[answer]"
{% endlodash %}


# (Question 3) by (Name)

{% lodash %}
return "[answer]"
{% endlodash %}

# (Question 4) by (Name)

{% lodash %}
return "[answer]"
{% endlodash %}

# (Question 5) by (Name)

{% lodash %}
return "[answer]"
{% endlodash %}
