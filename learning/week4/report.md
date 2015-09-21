{% data src="../../hackathons/fcq/fcq.clean.json" %}
{% enddata %}

# Report

As a class, we brainstormed and came up with a long list of further questions we
can ask based on the FCQ data. Out of these questions, our team chose to tackle on
the following questions. Each member on our team is reponsible for one question.

# What classes have very different workloads compared to credit hours? by John Cronk

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

# What department has the lowest average GPA? by Nicole Woytarowicz

{% lodash %}
var subjects = _.groupBy(data, 'Subject')
var departments = _.pick(_.mapValues(subjects, function(d){
return (_.sum(_.pluck(d, "AVG_GRD")))/(d.length)
}), function(x){
return x > 0
})

var worst = _.min(departments)

return {Department: (_.invert(departments))[worst], Average_GPA: worst}
{% endlodash %}

{{result.Department}} has the lowest GPA at {{result.Average_GPA}}.

# Which classes(with specific professors) damaged the most students (sort by:C + D + F rating)? by Denis Kazakov

{% lodash %}
var clean = _.filter(data, function(n){
    return n.PCT.D != ""
})

var map = _.map(clean, function(n){
  return {course: n.CourseTitle, ratio: n.PCT.C + n.PCT.D + n.PCT.F, name: _.pluck(n.Instructors, "name")}
})

return _.sortBy(map, function(n){
  return n.ratio
}).reverse()
{% endlodash %}

<table>
	<td>Course</td>
	<td>Grade Ratio</td>
	<td>Instructor Name</td>
{% for value in result %}
    <tr>
        <td>{{value.course}}</td>
        <td>{{value.ratio}}</td>
		<td>{{value.name}}</td>
    </tr>
{% endfor %}
</table>

# What department should I take classes in if I want to boost my GPA? by Caleb Hsu

{% lodash %}
var subjects = _.groupBy(data, 'Subject_Label')

var avgA = _.mapValues(subjects, function(s) {
return _.sum(_.pluck(s, 'PCT.A')) / s.length
})

var highest =  _.last(_.sortBy(_.pairs(avgA), function(d) {
return d[1]
}))

return highest[0]
{% endlodash %}

The {{result}} department can best help you raise your GPA.

# Which classes have the maximum Hours spent (16+) per week? by Parker Illig

{% lodash %}
var result = _.groupBy(data, function(d){
var dept = d.Subject
var num = d.Course
var combine = dept +  " " + num    
return combine
})
var classes = _.mapValues(result, function(d){
var wk = _.first(_.pluck(d, 'Workload.Hrs_Wk'))
return _.includes(wk, '16+')
})
return _.pick(classes, function(x){
return x==true
})
{% endlodash %}

<table>
	<td>Course</td>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
    </tr>
{% endfor %}
</table>
