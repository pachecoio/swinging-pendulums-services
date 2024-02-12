# Simple Pendulum Application

This application simulates a simple pendulum in one dimension using Node.js. It provides a REST interface to configure the pendulum's initial parameters such as angular offset, mass, string length, etc. Additionally, it supports multiple instances of the pendulum, each running on its own TCP port and communicating with their immediate neighbors.

The application consists of two main components: the backend server and the web application.

## Backend Server

The backend server, implemented in Node.js, provides the REST API for configuring the pendulum instances and managing their interactions. It also utilizes MQTT for communication between the pendulum instances.

## Web Application

The web application provides a user-friendly interface to configure and visualize the pendulum instances. It allows users to drag and drop the pendulum to set its initial position and provides controls to start, pause, and stop the simulation.


### Setup

1. Clone the repository.
2. Fetch and update the submodules
    ```
    git submodule update
    ```
3. Run the application with Docker
    ```
    docker compose up --build
    ```

## MQTT Communication

The backend server uses MQTT for communication between pendulum instances. When pendulum instances detect that they are too close to their immediate neighbors, they send a STOP message via MQTT. Upon receiving a STOP message, each instance stops moving immediately and waits for 5 seconds before sending a RESTART message. Once all instances have received all distinct RESTART messages, they restart moving.

For detailed documentation on the REST API and the web application, please refer to the `backend/readme.md` and `webapp/readme.md` files respectively.
