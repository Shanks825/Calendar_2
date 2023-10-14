
<!DOCTYPE html>
<html>
<head>
    <title>Student Calendar</title>
    <style>
        body {
            font-family: courier, courier;
            background-color: #f2f2f2;
        }
        .calendar {
            width: 600px;
            margin: 0 auto;
            padding: 20px;
            background-color: #fff;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }
        h1 {
            text-align: center;
        }
        .event-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border: 1px solid #ccc;
            padding: 5px 10px;
            margin-bottom: 5px;
            background-color: #f9f9f9;
            animation: fadeIn 0.5s;
        }
        .remove-button {
            cursor: pointer;
            color: red;
        }
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(-10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
            animation-fill-mode: both;
        }
        @keyframes fadeOut {
            from {
                opacity: 1;
                transform: translateY(0);
            }
            to {
                opacity: 0;
                transform: translateY(-10px);
            }
            animation-fill-mode: both;
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        table, th, td {
            border: 1px solid #ccc;
        }
        th, td {
            padding: 10px;
            text-align: left;
        }
        .event-description {
            font-size: 0.9em;
        }
        .event-category {
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="calendar">
        <h1>Student Calendar</h1>
        <input type="date" id="event-date" placeholder="Select a date">
        <input type="text" id="event-input" placeholder="Add an event">
        <input type="text" id="event-description" placeholder="Event description">
        <select id="event-category">
            <option value="exam">Exam</option>
            <option value="assignment">Assignment</option>
            <option value="meeting">Meeting</option>
            <option value="celebration">Celebration</option>

            <!-- Add more categories here -->
        </select>
        <button id="add-event">Add Event</button>
        <ul id="event-list"></ul>
        <table>
            <thead>
                <tr>
                    <th>Date</th>
                    <th>Event</th>
                    <th>Description</th>
                    <th>Category</th>
                </tr>
            </thead>
            <tbody id="event-table"></tbody>
        </table>
    </div>

    <script>
        const eventDateInput = document.getElementById('event-date');
        const eventInput = document.getElementById('event-input');
        const eventDescriptionInput = document.getElementById('event-description');
        const eventCategorySelect = document.getElementById('event-category');
        const eventList = document.getElementById('event-list');
        const eventTable = document.getElementById('event-table');
        const addEventButton = document.getElementById('add-event');

        addEventButton.addEventListener('click', addEventFromInputs);

        function addEventFromInputs() {
            const date = eventDateInput.value;
            const name = eventInput.value;
            const description = eventDescriptionInput.value;
            const category = eventCategorySelect.value;

            if (date && name) {
                addEvent(date, name, description, category);
                addToTable(date, name, description, category);
                resetInputs();
            }
        }

        function addEvent(eventDate, eventName, eventDescription, eventCategory) {
            const eventItem = document.createElement('li');
            eventItem.className = 'event-item';
            eventItem.innerHTML = `
                <span class="event-date">${eventDate}</span>
                <span class="event-name">${eventName}</span>
                <span class="event-description">${eventDescription}</span>
                <span class="event-category">${eventCategory}</span>
                <span class="remove-button" onclick="removeEvent(this)">Remove</span>
            `;
            eventList.appendChild(eventItem);
        }

        function addToTable(eventDate, eventName, eventDescription, eventCategory) {
            const newRow = eventTable.insertRow(eventTable.rows.length);
            const cell1 = newRow.insertCell(0);
            const cell2 = newRow.insertCell(1);
            const cell3 = newRow.insertCell(2);
            const cell4 = newRow.insertCell(3);
            cell1.innerHTML = eventDate;
            cell2.innerHTML = eventName;
            cell3.innerHTML = eventDescription;
            cell4.innerHTML = eventCategory;
        }

        function resetInputs() {
            eventDateInput.value = '';
            eventInput.value = '';
            eventDescriptionInput.value = '';
        }

        function removeEvent(button) {
            const eventItem = button.parentElement;
            eventItem.style.animation = 'fadeOut 0.5s';
            eventItem.addEventListener('animationend', () => {
                eventItem.remove();
                const eventDate = eventItem.querySelector('.event-date').textContent;
                const eventRows = eventTable.rows;
                for (let i = 0; i < eventRows.length; i++) {
                    if (eventRows[i].cells[0].textContent === eventDate) {
                        eventTable.deleteRow(i);
                        break;
                    }
                }
            });
        }
    </script>
</body>
</html>
         
       
     
  

  
             
