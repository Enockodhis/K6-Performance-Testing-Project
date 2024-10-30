# K6-Performance-Testing-Project
This project demonstrates a performance test using [k6](https://k6.io/), a load testing tool for testing the reliability and performance of web applications. The script sends HTTP GET requests to a sample endpoint (`https://test.k6.io`) and generates a detailed HTML summary report using the [k6-reporter](https://github.com/benc-uk/k6-reporter) library.

![image](https://github.com/user-attachments/assets/0551c727-eedb-4c3b-adeb-a21a7092ffd4)

## Prerequisites
- [k6](https://k6.io/docs/getting-started/installation/) must be installed.
- Internet access to fetch the k6-reporter module and access the tested URL.

## Script Explanation

The main components of the script are:
1. **HTTP Request**: A GET request is sent to the endpoint.
2. **Pause**: A 1-second sleep after each request to simulate real user wait times.
3. **HTML Summary Report**: After the test run, an HTML report (`summary.html`) is generated with k6-reporter.

### Script Code

```javascript
import http from 'k6/http';
import { sleep } from 'k6';
import { htmlReport } from 'https://raw.githubusercontent.com/benc-uk/k6-reporter/main/dist/bundle.js';

export default function () {
  http.get('https://test.k6.io');
  sleep(1);
}

export function handleSummary(data) {
  return {
    'summary.html': htmlReport(data),
  };
}

Running the Test
Use the following command to run the test with 10 virtual users (VUs) for a duration of 30 seconds:

k6 run --vus 10 --duration 30s script.js

Example Output
Below is an example of the command output you may see in the console:

         /\      Grafana   /‾‾/
    /\  /  \     |\  __   /  /
   /  \/    \    | |/ /  /   ‾‾\
  /          \   |   (  |  (‾)  |
 / __________ \  |_|\_\  \_____/

     execution: local
        script: script.js
        output: -

     scenarios: (100.00%) 1 scenario, 10 max VUs, 1m0s max duration (incl. graceful stop):
              * default: 10 looping VUs for 30s (gracefulStop: 30s)

INFO[0031] [k6-reporter v2.3.0] Generating HTML summary report  source=console

running (0m31.0s), 00/10 VUs, 217 complete and 0 interrupted iterations
default ✓ [======================================] 10 VUs  30s

