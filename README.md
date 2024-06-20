This Repo Is Use For The Backend Of Tanamin AI App So It Can Communicate With Sensor And Stored The Data To Firebase Realtime Database

## Technologies Used

- **Firebase Realtime Database**: For storing soil condition data.
- **Express.js**: For building RESTful APIs.
- **Docker**: For containerization and easy deployment.
- **Google Cloud Platform (GCP)**: For hosting the application.
- **Node.js**: The runtime environment.

## How to Try It

 Prerequisites:

- Docker installed
- Google Cloud SDK installed and configured
- Firebase project set up with a Realtime Database

### Steps

1. **Clone the repository**

   ```sh
   git clone https://github.com/your-username/tanamin-ai-backend.git
   cd tanamin-ai-backend
   1. **Set up Firebase**
    
    Create a `firebase.js` file in the root directory with your Firebase configuration:
    
    ```jsx
    javascriptCopy code
    const firebase = require('firebase/app');
    require('firebase/database');
    
    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
      databaseURL: "https://YOUR_PROJECT_ID.firebaseio.com",
      projectId: "YOUR_PROJECT_ID",
      storageBucket: "YOUR_PROJECT_ID.appspot.com",
      messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
      appId: "YOUR_APP_ID"
    };
    
    const db = firebase.initializeApp(firebaseConfig).database();
    
    module.exports = { db };
    
    ```
    
2. **Build and run the Docker container locally**
    
    ```
    shCopy code
    docker build -t soil-condition-monitoring .
    docker run -p 8080:8080 soil-condition-monitoring
    
    ```
    
3. **Access the API locally**
    - Save soil condition data:
        
        ```
        shCopy code
        curl -X POST \
          http://localhost:8080/save-soil-condition \
          -H 'Content-Type: application/json' \
          -d '{
            "temp": 25,
            "hum": 60,
            "ph": 7,
            "N": 10,
            "P": 5,
            "K": 15
          }'
        
        ```
        
    - Get the latest soil condition data:
        
        ```
        shCopy code
        curl http://localhost:8080/get-latest-soil-condition
        
        ```
        
4. **Deploy to Google Cloud Platform**
    
    Authenticate and set the project:
    
    ```
    shCopy code
    gcloud auth login
    gcloud config set project YOUR_PROJECT_ID
    
    ```
    
    Push the Docker image to Google Container Registry (GCR):
    
    ```
    shCopy code
    docker tag soil-condition-monitoring gcr.io/YOUR_PROJECT_ID/soil-condition-monitoring
    docker push gcr.io/YOUR_PROJECT_ID/soil-condition-monitoring
    
    ```
    
    Deploy to Google Cloud Run:
    
    ```
    shCopy code
    gcloud run deploy soil-condition-monitoring \
      --image gcr.io/YOUR_PROJECT_ID/soil-condition-monitoring \
      --platform managed \
      --region YOUR_PREFERRED_REGION \
      --allow-unauthenticated
    
    ```
    
    Access the provided URL for your service to use the API.
    

## License

This project is licensed under the MIT License.

This version provides a brief overview of the project, lists the technologies used, and gives straightforward steps for trying out the project locally and deploying it to Google Cloud Platform.

