# Currency Converter using Node-RED and ExchangeRate-API

This project is a currency converter built with [Node-RED](https://nodered.org/) using the [ExchangeRate-API](https://www.exchangerate-api.com/) for real-time exchange rate data. The flow retrieves exchange rates for a specified currency pair and displays the conversion rate.

## Features
- Fetches real-time exchange rates using the ExchangeRate-API.
- Easily configurable for different base and target currencies.
- Node-RED flow with HTTP request, Function, and Debug nodes.
  
## Prerequisites
- [Node-RED](https://nodered.org/) installed and running.
- An API key from [ExchangeRate-API](https://www.exchangerate-api.com/).
- Basic knowledge of Node-RED flows.

## Installation

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/your-username/currency-converter-node-red.git
   cd currency-converter-node-red
   ```

2. **Install Node-RED Dependencies:**
   If you don't have Node-RED installed, follow the [official installation guide](https://nodered.org/docs/getting-started/).

3. **Get an API Key:**
   Sign up for an account at [ExchangeRate-API](https://www.exchangerate-api.com/) and obtain your free API key.

4. **Import the Flow into Node-RED:**
   - Copy the flow from the `currency_converter_flow.json` file (or from the instructions below).
   - Open Node-RED and import the flow by pasting the JSON into the editor.

5. **Configure API Key:**
   - Replace `YOUR_API_KEY` in the flow with your actual ExchangeRate-API key.

## How to Use

1. **Open Node-RED**: Start Node-RED by running:
   ```bash
   node-red
   ```
   Navigate to `http://localhost:1880` in your browser.

2. **Configure Currencies**: 
   In the "Set Request Parameters" function node, configure the `baseCurrency` and `targetCurrency` variables to the currencies you want to convert (e.g., USD to EUR).

3. **Deploy the Flow**: 
   Click the deploy button in the top right of the Node-RED editor to save and activate the flow.

4. **Test the Flow**: 
   Use the inject node to trigger the flow and check the exchange rate in the debug panel.

## Example Flow

Below is the Node-RED flow JSON for the currency converter. You can copy and import this directly into your Node-RED editor.

```json
[
    {
        "id": "inject1",
        "type": "inject",
        "z": "flow_id",
        "name": "Trigger Currency Conversion",
        "props": [],
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "",
        "payloadType": "date",
        "x": 150,
        "y": 100,
        "wires": [["function1"]]
    },
    {
        "id": "function1",
        "type": "function",
        "z": "flow_id",
        "name": "Set Request Parameters",
        "func": "// Set the base and target currencies\nlet baseCurrency = \"USD\";\nlet targetCurrency = \"EUR\";\n\n// Build the API URL with your API key\nconst apiKey = \"YOUR_API_KEY\";\nconst url = `https://v6.exchangerate-api.com/v6/${apiKey}/pair/${baseCurrency}/${targetCurrency}`;\n\nmsg.url = url;\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 400,
        "y": 100,
        "wires": [["http1"]]
    },
    {
        "id": "http1",
        "type": "http request",
        "z": "flow_id",
        "name": "Fetch Exchange Rate",
        "method": "GET",
        "ret": "obj",
        "paytoqs": "ignore",
        "url": "",
        "tls": "",
        "persist": false,
        "proxy": "",
        "authType": "",
        "x": 650,
        "y": 100,
        "wires": [["function2"]]
    },
    {
        "id": "function2",
        "type": "function",
        "z": "flow_id",
        "name": "Process Response",
        "func": "if (msg.payload.result === \"success\") {\n    let rate = msg.payload.conversion_rate;\n    msg.payload = `1 ${msg.payload.base_code} = ${rate} ${msg.payload.target_code}`;\n} else {\n    msg.payload = \"Error retrieving exchange rate.\";\n}\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 900,
        "y": 100,
        "wires": [["debug1"]]
    },
    {
        "id": "debug1",
        "type": "debug",
        "z": "flow_id",
        "name": "Show Exchange Rate",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "payload",
        "targetType": "msg",
        "statusVal": "",
        "statusType": "auto",
        "x": 1150,
        "y": 100,
        "wires": []
    }
]
```

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

Feel free to contribute by opening issues or submitting pull requests!

## Contact
For any questions or feedback, you can reach me at:

- GitHub: [Naveen kumar](https://github.com/naveenkumarpinagani)
- Email: [Gmail.com](pinaganinaveenkumar@gmail.com)
---

