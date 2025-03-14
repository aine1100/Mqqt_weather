

# Weather Monitoring Dashboard

*A real-time weather monitoring system using MQTT, Chart.js, and a sleek web interface.*

This project is a **Weather Monitoring Dashboard** designed to display real-time temperature and humidity data. It uses MQTT to receive sensor data, Chart.js to visualize trends over time, and a modern web interface for an intuitive user experience. The system is built for IoT applications, such as embedded weather stations.

## Features
- Real-time temperature and humidity updates via MQTT.
- Interactive line chart showing trends over time.
- Responsive and modern UI with a gradient design.
- Data averaging every 5 seconds (configurable to 5 minutes).
- Backend API integration to store weather data.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Configuration](#configuration)
- [Contributing](#contributing)
- [License](#license)

## Prerequisites
- **Node.js** (optional, if running a local backend server).
- **Git** for cloning the repository.
- A web browser (Chrome, Firefox, etc.).
- Access to an MQTT broker (e.g., `ws://157.173.101.159:9001`).
- A backend server (e.g., running on `http://localhost:5000/weather_api`) if storing data.

## Installation
1. **Clone the Repository**:
   ```bash
   git clone git@github.com:aine1100/Mqqt_weather.git
   cd Mqqt_weather
   ```

2. **Open the Project**:
   - Since this is a static HTML file, no build step is required. Simply open `index.html` in a web browser:
     ```bash
     open index.html  # macOS
     start index.html # Windows
     ```

3. **Set Up the MQTT Broker**:
   - Ensure the MQTT broker at `ws://157.173.101.159:9001` is running and accessible.
   - Subscribe to topics: `/work_group_01/room_temp/temperature` and `/work_group_01/room_temp/humidity`.

4. **Optional Backend Setup**:
   - If using the POST request to `http://localhost:5000/weather_api`, set up a simple server (e.g., with Flask or Node.js). Example Flask server:
     ```python
     from flask import Flask, request, jsonify
     app = Flask(__name__)

     @app.route('/weather_api', methods=['POST'])
     def weather_api():
         data = request.get_json()
         print(f"Received: {data}")
         return jsonify({"message": "Data received"}), 200

     if __name__ == "__main__":
         app.run(port=5000)
     ```

## Usage
1. Open `index.html` in your browser.
2. The dashboard will connect to the MQTT broker and start displaying temperature and humidity data.
3. The chart updates every 5 seconds with averaged values (configurable in the code).
4. Data is sent to the backend API (if configured) at the same interval.

To change the update interval to 5 minutes, modify the `setInterval` calls in `index.html`:
```javascript
setInterval(updateAverages, 300000); // 5 minutes
setInterval(sendData, 300000);       // 5 minutes
```

## Project Structure
```
Mqqt_weather/
├── index.html       # Main dashboard file (HTML, CSS, JS)
├── README.md        # Project documentation (this file)
└── (optional backend files, e.g., server.py)
```

- **`index.html`**: Contains the HTML structure, CSS styles, and JavaScript logic for MQTT, Chart.js, and AJAX.

## Configuration
- **MQTT Broker**: Update the broker URL in `index.html` if needed:
  ```javascript
  const client = mqtt.connect('ws://your-broker-url:port');
  ```
- **Topics**: Modify the subscribed topics if your sensors use different ones:
  ```javascript
  client.subscribe('/your/temperature/topic');
  client.subscribe('/your/humidity/topic');
  ```
- **Backend URL**: Adjust the AJAX URL to match your server:
  ```javascript
  url: 'http://your-backend-url:port/weather_api',
  ```

## Contributing
Contributions are welcome! To contribute:
1. Fork the repository.
2. Create a new branch (`git checkout -b feature/your-feature`).
3. Make your changes and commit (`git commit -m "Add your feature"`).
4. Push to your fork (`git push origin feature/your-feature`).
5. Open a Pull Request.

Please ensure your code follows the existing style and includes comments where necessary.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details (you can add one if needed).

---

### Notes:
- Replace the placeholder image URL (`https://via.placeholder.com/...`) with a screenshot of your dashboard once you have one.
- If you’re using this with specific hardware (e.g., an embedded IoT device), consider adding a section about the hardware setup.
- Let me know if you’d like to tweak this further (e.g., add badges, specific hardware details, or a different tone)!
