<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Expense Tracker Application</title>
</head>
<body>
    <h1>Expense Tracker Application</h1>

    <h2>Project Overview</h2>
    <p>
        The application is designed as an expense management tool. Its primary feature is an AI-powered system that identifies items, their costs, and categories from grocery store receipts. 
        Users can upload a receipt image through the app or capture one directly using their device's camera.
    </p>
    <p>
        It includes a section where users can get chatbot recommendations about the expenses.
    </p>
    <p>
        The app includes a data visualization module with graphs and charts to help users analyze spending patterns, track expenses by category, view trends, alongside predictions.
    </p>

    <hr>

    <h2>Folder Structure</h2>

    <h3>1. Demo</h3>
    <p>The <code>demo</code> folder contains the <strong>front-end</strong> implementation of the application, built with <strong>Expo</strong> for mobile compatibility using <strong>React Native</strong>.</p>
    <h4>Key Features:</h4>
    <ul>
        <li><strong>Dashboard:</strong> The home screen is designed as a dashboard providing users with an overview of their expenses.
            <ul>
                <li><strong>Visual Representations:</strong> Includes a <strong>pie chart</strong> for expense categories and a <strong>line chart</strong> for expense trends over time.</li>
                <li><strong>Filter by Period:</strong> Allows users to filter expenses for a specific time period.</li>
            </ul>
        </li>
        <li><strong>Receipt Management:</strong>
            <ul>
                <li><strong>Scan Receipts:</strong> Use the device's native camera to scan receipts directly.</li>
                <li><strong>Upload Receipts:</strong> Upload receipt images from the device's storage.</li>
                <li><strong>Manual Input:</strong> Enter expense details manually for complete control.</li>
            </ul>
        </li>
    </ul>

    <h3>2. Backend</h3>
    <p>The <code>backend</code> folder contains the server-side logic, managing the application's data and functionality.</p>
    <h4>Key Features:</h4>
    <ul>
        <li><strong>Models:</strong> Defines data models using <strong>MongoDB</strong> to store user data, expenses, and other application-specific information.</li>
        <li><strong>Routing:</strong> Handles all API endpoints to support the functionalities of the front-end, including:
            <ul>
                <li>Receipt processing.</li>
                <li>Expense filtering and categorization.</li>
                <li>User data management.</li>
            </ul>
        </li>
    </ul>

    <h3>3. Service</h3>
    <p>The <code>service</code> folder is responsible for handling image processing, enabling the automatic classification of expenses from scanned or uploaded receipts.</p>
    <h4>Key Features:</h4>
    <ul>
        <li><strong>Image Processing:</strong> Extracts relevant data from receipts using advanced algorithms.</li>
        <li><strong>Expense Classification:</strong> Processes images to categorize expenses and outputs the results as a <strong>JSON</strong> format.</li>
        <li><strong>Integration:</strong> Seamlessly integrates with the backend to update the user's expense data.</li>
    </ul>

    <hr>

    <h2>Technologies Used</h2>
    <ul>
        <li><strong>Front-End:</strong> React Native (Expo)</li>
        <li><strong>Back-End:</strong> Node.js with Express.js</li>
        <li><strong>Database:</strong> MongoDB</li>
        <li><strong>Image Processing:</strong> Custom services for expense classification from images</li>
        <li><strong>Server:</strong> Flask for Python-based services</li>
    </ul>

    <hr>

    <h2>Setup Instructions</h2>

    <h3>Prerequisites</h3>
    <ul>
        <li>Python 3.8+</li>
        <li>Flask Framework</li>
        <li>MongoDB</li>
        <li>Node 18.12.1</li>
    </ul>

    <h3>Installation</h3>
    <ol>
    <li>
        Clone the Repository:
        <pre><code>
git clone https://github.com/aBenbou/2024-InnovAI-Hackathon.git
cd team-51 
cd service
        </code></pre>
    </li>
    <li>
        Install Dependencies:
        <pre><code>
pip install -r requirements.txt
        </code></pre>
    </li>
    <li>
        Seed the Database:
        <pre><code>
python seed.py
        </code></pre>
    </li>
    <li>
        Start the Flask Server:
        <pre><code>
python app.py
        </code></pre>
    </li>
    <li>
        Start the Backend:
        <pre><code>
cd backend 
npm start
        </code></pre>
    </li>
    <li>
        Start the React Native App:
        <pre><code>
cd demo
npm install 
npm start
        </code></pre>
    </li>
</ol>


    <hr>

    <h2>API Endpoints</h2>

    <h3>1. Budget Recommendations</h3>
    <p><strong>Endpoint:</strong> <code>GET /recommend</code></p>
    <p><strong>Description:</strong> Provides budget-saving recommendations based on user purchase history and current offers.</p>
    <p><strong>Request Example:</strong></p>
    <pre><code>curl -G "http://127.0.0.1:5000/recommend" \
--data-urlencode "user_id=12345" \
--data-urlencode "days=7"</code></pre>
    <p><strong>Success Response:</strong></p>
    <pre><code>{
  "status": "success",
  "recommendation": "بالنظر للمشتريات ديالك، هنا بعض النصائح لتوفير الميزانية...\n..."
}</code></pre>

    <h3>2. Receipt Parsing</h3>
    <p><strong>Endpoint:</strong> <code>POST /receipt</code></p>
    <p><strong>Description:</strong> Processes a base64-encoded receipt image and returns structured item data.</p>
    <p><strong>Request Example:</strong></p>
    <pre><code>curl -X POST http://127.0.0.1:5000/receipt \
-H "Content-Type: application/json" \
-d '{
    "image": "'"$(cat /path/to/receipt_base64.txt)"'"
}'</code></pre>
    <p><strong>Success Response:</strong></p>
    <pre><code>{
  "status": "success",
  "data": {
    "currency": "MAD",
    "items": [
      {"category": "dairy", "cost": 0.89, "name": "Fresh Milk", "quantity": 1},
      {"category": "breakfast", "cost": 2.29, "name": "Muesli", "quantity": 1},
      {"category": "sweets", "cost": 0.95, "name": "Dark Chocolate", "quantity": 2}
    ],
    "purchase_date": "Mon, 23 Apr 2012 19:51:00 GMT",
    "receipt_id": "5.08_20120423_195100",
    "total_amount": 5.08,
    "user_id": "12345",
    "user_location": "Casablanca"
  }
}</code></pre>

    <hr>

    <h2>MongoDB Database Initialization</h2>
    <p>The <code>seed.py</code> script populates the following collections with dummy data:</p>
    <ul>
        <li><strong>products:</strong> List of Moroccan products and their prices.</li>
        <li><strong>offers:</strong> Active offers and discounts.</li>
        <li><strong>purchases:</strong> User purchase history.</li>
        <li><strong>receipts:</strong> Receipt metadata and details.</li>
        <li><strong>users:</strong> User profile data.</li>
    </ul>

    <hr>

    <h2>Notes</h2>
    <p>Ensure MongoDB is running locally or on the specified host. All responses are in Arabic where applicable for localization.</p>

    <hr>

    <h2>License</h2>
    <p>This project is licensed under the MIT License.</p>
</body>
</html>
