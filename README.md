# DiaBuddy USSD Application Documentation

Authors: Myles Ngicu, Delbert Kipyegon, Barrack Ouma, Immanuel Kibet

## Overview
This is a bilingual (English and Kiswahili) USSD application that provides information on Diabetes. It leverages the Africastalking USSD API for the USSD services and OpenAI's GPT-3 model to answer the questions on Diabetes.

## Dependencies
The application uses several Node.js modules including:

- express: A fast, unopinionated, and minimalist web framework for Node.js
- cors: A Node.js package for providing a Connect/Express middleware that can be used to enable CORS with various options.
- dotenv: This module loads environment variables from a .env file into process.env
- openai: The module that contains the utility functions to interact with OpenAI's GPT-3 model
- axios

## Application Structure
The main file of the application is the server.js file.

At the top of the server.js file, the required modules are imported, and instances of the express application (app) and the PORT are created.

Middleware is then set up to allow the server to handle JSON data, handle urlencoded data, and use CORS.

The application's main route is set up with a GET request to the root ('/') of the app that responds with a welcome message.

The main logic of the app lies within the POST route to '/ussd'. This is the endpoint that Africastalking USSD API hits with a POST request whenever a USSD session is initiated.

Depending on the text parameter from the body of the request, the application responds with a relevant USSD message.

For example, if the text parameter is empty, the application responds with a welcome message asking the user to select a language. If the text parameter indicates that the user has selected English (by being equal to '1'), the application prompts the user to ask a question. If the user has already asked a question, the application uses the OpenAI's GPT-3 model to answer the question.

The app also handles other user selections such as choosing Kiswahili as the preferred language and exiting the service.

Finally, the app has a catch-all route that sends an error message for any requests made to routes that are not defined.

The application starts listening on the defined PORT after setting up all the routes.

## Running The Application
To run the application, use the command `node server.js` in the terminal. The application will start and listen on the port defined in the .env file or port 3000 if the .env file does not define a port.
