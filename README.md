# Openinapp
1-To call the API and build the UI components based on the response, follow these steps:

Display Greeting from Local Time:

Use JavaScript to get the current local time and display a greeting (e.g., "Good Morning", "Good Afternoon", "Good Evening").

const getGreeting = () => {
    const hours = new Date().getHours();
    if (hours < 12) return "Good Morning";
    else if (hours < 18) return "Good Afternoon";
    else return "Good Evening";
};

document.getElementById('greeting').innerText = getGreeting();


2-Create a Chart:

Use a library like Chart.js to create a chart based on the API response

fetch('https://api_inopenapp.com/api/v1/dashboardNew', {
    method: 'GET',
    headers: {
        'Authorization': 'Bearer eyJhbGciOiJIUzIlNilsInR5cCI6IkpXVCJ9.eyJpZCI6MjU5MjesImlhdCI6MTY3NDU1MDQ1MH0.dCkW0x8t bjJA2GgUx2UEwNIbTZ7Rr38PVFJevYXFI'
    }
})
.then(response => response.json())
.then(data => {
    const ctx = document.getElementById('myChart').getContext('2d');
    new Chart(ctx, {
        type: 'bar',
        data: {
            labels: data.labels,
            datasets: [{
                label: 'Dataset Label',
                data: data.values,
                backgroundColor: 'rgba(75, 192, 192, 0.2)',
                borderColor: 'rgba(75, 192, 192, 1)',
                borderWidth: 1
            }]
        },
        options: {
            scales: {
                y: {
                    beginAtZero: true
                }
            }
        }
    });
});

3-Add a Tab and List View:

Create a tab component for "Top Links" and "Recent Links".
Populate the lists using the API response.

<div class="tabs">
    <button class="tablink" onclick="openTab('TopLinks')">Top Links</button>
    <button class="tablink" onclick="openTab('RecentLinks')">Recent Links</button>
</div>

<div id="TopLinks" class="tabcontent">
    <ul id="top-links-list"></ul>
</div>

<div id="RecentLinks" class="tabcontent">
    <ul id="recent-links-list"></ul>
</div>

<script>
    function openTab(tabName) {
        var i;
        var x = document.getElementsByClassName("tabcontent");
        for (i = 0; i < x.length; i++) {
            x[i].style.display = "none";
        }
        document.getElementById(tabName).style.display = "block";
    }

    fetch('https://api_inopenapp.com/api/v1/dashboardNew', {
        method: 'GET',
        headers: {
            'Authorization': 'Bearer eyJhbGciOiJIUzIlNilsInR5cCI6IkpXVCJ9.eyJpZCI6MjU5MjesImlhdCI6MTY3NDU1MDQ1MH0.dCkW0x8t bjJA2GgUx2UEwNIbTZ7Rr38PVFJevYXFI'
        }
    })
    .then(response => response.json())
    .then(data => {
        const topLinksList = document.getElementById('top-links-list');
        const recentLinksList = document.getElementById('recent-links-list');

        data.topLinks.forEach(link => {
            const li = document.createElement('li');
            li.innerText = link.title;
            topLinksList.appendChild(li);
        });

        data.recentLinks.forEach(link => {
            const li = document.createElement('li');
            li.innerText = link.title;
            recentLinksList.appendChild(li);
        });
    });
</script>


This code snippet sets up the greeting based on local time, creates a chart from the API response using Chart.js, and adds tabs to display lists of top and recent links from the API response. Ensure you include necessary libraries and styles in your project





