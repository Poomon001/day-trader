# Nightrader [![test](https://github.com/bhavanvir/day-trader/actions/workflows/main.yml/badge.svg?branch=main)](https://github.com/bhavanvir/day-trader/actions/workflows/main.yml)

Nightrader is a robust stock trading platform built on microservices architecture. We leverage Docker for orchestration, Go and Gin-Gonic for the backend API, PostgreSQL for our database, and React with Daisy UI and TailwindCSS for the frontend.

## Services

- **Engine** (Port `8585`): Implements the matching engine, which processes buy and sell orders using a Pro Rata algorithm.
- **Setup** (Port `8080`): Initializes Nightrader by adding and creating stocks for market use.
- **Database** (Port `5432`): Handles table creation and data preprocessing, including password encryption.
- **Authentication** (Port `8888`): Verifies user credentials against the database and generates session tokens that expire after a fixed time.
- **Transaction** (Port `5433`): Manages client-exchange interactions, such as fetching current market prices and funding user balances.
- **Frontend** (Port `3000`): The user-facing application that facilitates interactions with the exchange.

## Endpoints

| Category       | Method | Endpoint                | Parameters                                                                                                                                                                                                                                                       |
| -------------- | ------ | ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Authentication | POST   | /register               | { <br/> &nbsp;&nbsp;&nbsp;&nbsp;"username": string, <br/> &nbsp;&nbsp;&nbsp;&nbsp;"password": string, <br/> &nbsp;&nbsp;&nbsp;&nbsp;"name": string <br/> }                                                                                                       |
|                | POST   | /login                  | { <br/> &nbsp;&nbsp;&nbsp;&nbsp;"user_name": string, <br/> &nbsp;&nbsp;&nbsp;&nbsp;"password": string <br/> }                                                                                                                                                    |
| Transaction    | GET    | /getStockPrices         | -                                                                                                                                                                                                                                                                |
|                | GET    | /getWalletBalance       | -                                                                                                                                                                                                                                                                |
|                | GET    | /getStockPortfolio      | -                                                                                                                                                                                                                                                                |
|                | GET    | /getWalletTransactions  | -                                                                                                                                                                                                                                                                |
|                | GET    | /getStockTransactions   | -                                                                                                                                                                                                                                                                |
|                | POST   | /addMoneyToWallet       | { <br/> &nbsp;&nbsp;&nbsp;&nbsp;"amount": number <br/> }                                                                                                                                                                                                         |
|                | POST   | /placeStockOrder        | { <br/> &nbsp;&nbsp;&nbsp;&nbsp;"stock_id": number, <br/> &nbsp;&nbsp;&nbsp;&nbsp;"is_buy": boolean, <br/> &nbsp;&nbsp;&nbsp;&nbsp;"order_type": string, <br/> &nbsp;&nbsp;&nbsp;&nbsp;"quantity": number, <br/> &nbsp;&nbsp;&nbsp;&nbsp;"price": number <br/> } |
|                | POST   | /cancelStockTransaction | { <br/> &nbsp;&nbsp;&nbsp;&nbsp;"stock_tx_id": string <br/> }                                                                                                                                                                                                    |
| Setup          | POST   | /createStock            | { <br/> &nbsp;&nbsp;&nbsp;&nbsp;"stock_name": string <br/> }                                                                                                                                                                                                     |
|                | POST   | /addStockToUser         | { <br/> &nbsp;&nbsp;&nbsp;&nbsp;"stock_id": string, <br/> &nbsp;&nbsp;&nbsp;&nbsp;"quantity": number <br/> }                                                                                                                                                     |

## Installation

1. **Prerequisites**: Ensure Docker is installed and configured on your system.
2. **Clone the repository**:

   ```bash
   git clone https://github.com/bhavanvir/day-trader.git
   ```

3. **Navigate to the project directory**:

   ```bash
   cd day-trader
   ```

4. **Start up all microservices**:

   ```bash
   docker compose up --build -d
   ```

5. **Access the frontend**:
   Open a web browser and go to `localhost:3000` to start trading.

6. **Setup RabbitMQ**:
   download: https://www.rabbitmq.com/docs/download

   Under Dependencies: Install Erlang (v26.0+)

   Install rabbitmq-server-3131.exe.asc

   Open RabbitMQ Command Prompt - from Window search

   In the command: enter rabbitmq-plugins enable rabbitmq_management

   In Window search type: rabbitMQ -> there will be rabbitMQ - start/stop

   See UI details:

   go to: http://localhost:15672/

   Start:

   docker compose up rabbitMQ3

7. **Test Frontend**:

   ```bash
   make start
   jmeter -n -t tests/Seng468_Report1_No_Delay.jmx
   ```

   Navigate to localhost in your browser then you can login with FinanceGuru with password Fguru@2024

8. **Load Tets**:
   Download JMeter
   ```bash
   cd <PATH>\JMeter\apache-jmeter-5.6.3\apache-jmeter-5.6.3\bin
   jmeter -n -t "C:\Users<PATH>\tests\TestRun3\InitialSetup.jmx" -l "C:\Users<PATH>\tests\TestRun3\result\testresults1.jtl"
   jmeter -n -t "C:\Users<PATH>\tests\TestRun3\UserThreadTest.jmx" -l "C:\Users<PATH>\tests\TestRun3\result\testresults2.jtl"
   ```

Feel free to reach out if you have any questions or need further assistance. Happy trading!
