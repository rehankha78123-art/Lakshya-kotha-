// Define time zones with their UTC offsets
const timeZones = {
    nyc: { name: 'America/New_York', offset: -5 },
    london: { name: 'Europe/London', offset: 0 },
    tokyo: { name: 'Asia/Tokyo', offset: 9 },
    sydney: { name: 'Australia/Sydney', offset: 11 },
    dubai: { name: 'Asia/Dubai', offset: 4 },
    la: { name: 'America/Los_Angeles', offset: -8 },
    singapore: { name: 'Asia/Singapore', offset: 8 },
    india: { name: 'Asia/Kolkata', offset: 5.5 }
};

/**
 * Update all clocks with current time in their respective time zones
 */
function updateClocks() {
    const now = new Date();

    for (const [id, timezone] of Object.entries(timeZones)) {
        // Get current UTC time
        const utcTime = new Date(now.getTime() + now.getTimezoneOffset() * 60000);
        
        // Apply timezone offset
        const offset = timezone.offset;
        const tzTime = new Date(utcTime.getTime() + offset * 60 * 60 * 1000);

        // Format time as HH:MM:SS
        const hours = String(tzTime.getHours()).padStart(2, '0');
        const minutes = String(tzTime.getMinutes()).padStart(2, '0');
        const seconds = String(tzTime.getSeconds()).padStart(2, '0');

        const timeString = `${hours}:${minutes}:${seconds}`;

        // Update the clock display
        const clockElement = document.getElementById(id);
        if (clockElement) {
            clockElement.textContent = timeString;
        }
    }
}

// Update clocks immediately on page load
updateClocks();

// Update clocks every second
setInterval(updateClocks, 1000);

// Optional: Add keyboard shortcut to refresh
document.addEventListener('keydown', (event) => {
    if (event.key === 'r' || event.key === 'R') {
        updateClocks();
    }
});
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Digital Clock - Multiple Time Zones</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Digital Clock - Multiple Time Zones</h1>
        
        <div class="clocks-grid">
            <!-- New York -->
            <div class="clock-card">
                <h2>New York (EST)</h2>
                <div class="clock" id="nyc">00:00:00</div>
                <p class="timezone">UTC -5</p>
            </div>

            <!-- London -->
            <div class="clock-card">
                <h2>London (GMT)</h2>
                <div class="clock" id="london">00:00:00</div>
                <p class="timezone">UTC +0</p>
            </div>

            <!-- Tokyo -->
            <div class="clock-card">
                <h2>Tokyo (JST)</h2>
                <div class="clock" id="tokyo">00:00:00</div>
                <p class="timezone">UTC +9</p>
            </div>

            <!-- Sydney -->
            <div class="clock-card">
                <h2>Sydney (AEDT)</h2>
                <div class="clock" id="sydney">00:00:00</div>
                <p class="timezone">UTC +11</p>
            </div>

            <!-- Dubai -->
            <div class="clock-card">
                <h2>Dubai (GST)</h2>
                <div class="clock" id="dubai">00:00:00</div>
                <p class="timezone">UTC +4</p>
            </div>

            <!-- Los Angeles -->
            <div class="clock-card">
                <h2>Los Angeles (PST)</h2>
                <div class="clock" id="la">00:00:00</div>
                <p class="timezone">UTC -8</p>
            </div>

            <!-- Singapore -->
            <div class="clock-card">
                <h2>Singapore (SGT)</h2>
                <div class="clock" id="singapore">00:00:00</div>
                <p class="timezone">UTC +8</p>
            </div>

            <!-- India -->
            <div class="clock-card">
                <h2>India (IST)</h2>
                <div class="clock" id="india">00:00:00</div>
                <p class="timezone">UTC +5:30</p>
            </div>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Arial', sans-serif;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
}

.container {
    width: 100%;
    max-width: 1200px;
}

h1 {
    text-align: center;
    color: white;
    margin-bottom: 40px;
    font-size: 2.5rem;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}

.clocks-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    margin-bottom: 40px;
}

.clock-card {
    background: white;
    border-radius: 15px;
    padding: 30px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
    text-align: center;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.clock-card:hover {
    transform: translateY(-10px);
    box-shadow: 0 15px 40px rgba(0, 0, 0, 0.4);
}

.clock-card h2 {
    color: #333;
    margin-bottom: 15px;
    font-size: 1.3rem;
}

.clock {
    font-size: 3rem;
    font-weight: bold;
    color: #667eea;
    font-family: 'Courier New', monospace;
    margin: 20px 0;
    letter-spacing: 2px;
    background: #f0f0f0;
    padding: 20px;
    border-radius: 10px;
    box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.1);
}

.timezone {
    color: #666;
    font-size: 0.9rem;
    margin-top: 10px;
}

/* Responsive Design */
@media (max-width: 768px) {
    h1 {
        font-size: 1.8rem;
        margin-bottom: 25px;
    }

    .clocks-grid {
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
        gap: 15px;
    }

    .clock {
        font-size: 2rem;
    }

    .clock-card {
        padding: 20px;
    }
}

@media (max-width: 480px) {
    h1 {
        font-size: 1.4rem;
    }

    .clocks-grid {
        grid-template-columns: 1fr;
    }

    .clock {
        font-size: 1.8rem;
    }
}
