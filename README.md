# sgpa-calcuator
please use this website and calculate sgpa and cgpa
<!DOCTYPE html>
<html>
<head>
    <title>JNTUK SGPA Calculator</title>
    <style>
        body {
            text-align: center;
            background-color: #f5f5f5; /* Light gray background color */
        }
        #container {
            display: inline-block;
            text-align: left;
        }
        .course-section {
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
        label, input {
            display: block;
            margin-bottom: 10px;
        }
        .color-picker {
            width: 24px;
            height: 24px;
            border-radius: 50%;
            margin-right: 10px;
        }
        #calculate-button {
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <h1>JNTUK SGPA Calculator</h1>
    <p>Enter your course details for a semester to calculate SGPA:</p>
    <div id="container">
        <div>
            <label for="num-courses">Number of Courses:</label>
            <input type="number" id="num-courses" min="1">
        </div>
        <div id="course-details"></div>
        <button id="calculate-button">Calculate SGPA</button>
        <p>SGPA: <span id="sgpa-result"></span></p>
    </div>

    <script>
        document.getElementById("num-courses").addEventListener("input", function () {
            const numCourses = parseInt(this.value);
            const courseDetailsDiv = document.getElementById("course-details");
            courseDetailsDiv.innerHTML = "";

            for (let i = 0; i < numCourses; i++) {
                courseDetailsDiv.innerHTML += `
                    <div class="course-section">
                        <div>
                            <label for="course-name${i}">Course Name:</label>
                            <input type="text" id="course-name${i}">
                        </div>
                        <div>
                            <label for="course-credits${i}">Course Credits:</label>
                            <input type="number" id="course-credits${i}" min="1">
                        </div>
                        <div>
                            <label for="grade${i}">Grade:</label>
                            <input type="text" id="grade${i}">
                        </div>
                        <div>
                            <input type="color" class="color-picker" id="color${i}" value="#ffffff">
                        </div>
                    </div>
                `;
            }
        });

        document.getElementById("calculate-button").addEventListener("click", function () {
            const numCourses = parseInt(document.getElementById("num-courses").value);
            let sgpaNumerator = 0;
            let totalCredits = 0;

            for (let i = 0; i < numCourses; i++) {
                const credits = parseFloat(document.getElementById(`course-credits${i}`).value);
                const grade = document.getElementById(`grade${i}`).value.toUpperCase();
                const gradePoints = {
                    'A+': 10, 'A': 9, 'B': 8, 'C': 7, 'D': 6, 'E': 5, 'F': 0, 'AB': 0
                };
                const gradePoint = gradePoints[grade] || 0;
                sgpaNumerator += credits * gradePoint;
                totalCredits += credits;
                
                const color = document.getElementById(`color${i}`).value;
                document.querySelectorAll(".course-section")[i].style.backgroundColor = color;
            }

            const sgpa = sgpaNumerator / totalCredits;
            document.getElementById("sgpa-result").textContent = sgpa.toFixed(2);
        });
    </script>
</body>
</html>
