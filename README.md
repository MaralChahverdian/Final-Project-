# Final-Project-
<!DOCTYPE html>
<html>
<head>
	<title>GPA calculator</title>
	<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
	<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap-theme.min.css">
</head>
<body>
	<div class="container" >
		<h1>GPA Calculator</h1>
		<table id="grades" class="form-group">
			<tr>
				<th>Course Name</th>
				<th>Credits</th>
				<th>Grade</th>
				<th></th>
			</tr>
		</table>
		<button class="btn btn-default" id="newLine">Add course</button>
		<button class="btn btn-default" id="calculateGpa">Calculate GPA</button>
		<h3 id="totalGpa"></h3>
	</div>

	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
	<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
	<script>
		$(document).ready(function() {
			var newLineHtml = `<tr>
				<td><input type="text" class="form-control course" placeholder="Course Name"></td>
				<td><input type="text" class="form-control credits" placeholder="Credits"></td>
				<td><input type="text" class="form-control grade" placeholder="Grade"></td>
				<td><button class="btn btn-default removeCourse">X</button></td>
			</tr>`;

			function addNewCourse() {
				var $newel = $(newLineHtml);
				$('#grades').append($newel);
				$newel.find('.removeCourse').click(removeThisCourse);
			}

			function removeThisCourse(e) {
				var $el = $(this);
				$el.parent().parent().remove();
			}

			function calculateGpa() {
				var weightedGrade = 0;
				var totalCredits = 0;
				var gradeRanges =
					[4.3,	4.0,	3.7,	3.3,	3.0,	2.7,	2.3,	2.0,	1.7,	1.3,	1.0,	0.7,	0];
				var gpaNames =
					['A+',	'A',	'A-',	'B+',	'B',	'B-',	'C+',	'C',	'C-',	'D+',	'D',	'D-',	'F'];
				var averageGrade, gpa;

				$('#grades tr:not(:first-child)').each(function(i, el) {
					// var course = $(el).children('.course').val();
					var grade = $(el).find('.grade').val();
					var credits = $(el).find('.credits').val();

					weightedGrade = weightedGrade + parseFloat(grade)*parseFloat(credits);
					totalCredits = totalCredits + parseFloat(credits);
				});

				averageGrade = weightedGrade / totalCredits;
				for (var i = 0; i < gradeRanges.length; i++) {
					if (averageGrade >= gradeRanges[i]) {
						gpa = gpaNames[i];
						break;
					}
				}

				$('#totalGpa').html(gpa);
			}

			$('#newLine').click(addNewCourse);
			$('#calculateGpa').click(calculateGpa);

			addNewCourse();
		});
	</script>
</body>
</html>
