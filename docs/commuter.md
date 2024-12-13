## <strong>Commuter Api's Collection</strong>
### Marketing - analytics.apnibus.com

<details>
    <summary><strong>Endpoint:</strong> https://analytics.apnibus.com/analytics/record-event/</summary>
    <p><strong>Method:</strong> POST</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Token 912512e9e3f8fe22153f06403050b9e313b1d0bf</td>
                </tr>
            </table>
        </details>
    </details>
    <details>
    <summary><strong>Request</strong></summary>
    <pre>
    {
        "event_type": "generate_otp",
        "data": {
            "number": "9685338171",
            "from": "App",
            "timestamp": "2024-12-13T12:59:21.000Z",
            "session_id": "9a6f64a2-2624-4cf7-887a-915c815f0a07",
            "mobile": "9685338171"
        },
        "session_id": "9a6f64a2-2624-4cf7-887a-915c815f0a07"
    }
    </pre>
    </details>
    <details>
    <summary><strong>Response</strong></summary>
    <pre>
    {
    "message": "event recorded!",
    "token": "a054bdbfaed8eb3ff75b36bc78c9fed1b270c108"
    }
    </pre>
    </details>
</details>


### Commuter - commuter.apis.apnibus.com

<details>
    <summary><strong>Endpoint:</strong> https://commuter.apis.apnibus.com/auth/generate-otp</summary>
    <p><strong>Method:</strong> POST</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
    </details>
    <details>
        <summary><strong>Request</strong></summary>
        <pre>
        {
            "userContact": "9685338171",
            "userLanguage": "1"
        }
        </pre>
    </details>
    <details>
        <summary><strong>Response</strong></summary>
        <pre>
        {
            "success": true,
            "code": 200,
            "data": {
                "isExistingUser": true
        },
            "message": "OTP sent successfully"
        }
        </pre>
    </details>
</details>

<details>
    <summary><strong>Endpoint:</strong> https://commuter.apis.apnibus.com/auth/verify-otp</summary>
    <p><strong>Method:</strong> POST</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
    </details>
    <details>
        <summary><strong>Request</strong></summary>
        <pre>
        {
            "userContact": "9685338171",
            "otp": 2611
        }
        </pre>
    </details>
</details>

<details>
    <summary><strong>Endpoint:</strong> https://commuter.apis.apnibus.com/user/{{param1}}</summary>
    <p><strong>Method:</strong> GET</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxNDVjZTdmMy0zMjNhLTRmOTctOTRlMi1kM2YzNDI0OTU5ZmEiLCJpYXQiOjE3MzQwOTQ3NjMsImV4cCI6MTc2NTYzMDc2M30.u-_dO0w0d3L25caq5Ty20N1emHIIi5LquVZLNxR5MxFVIczpODCmd3-AiWJRZaAqMFhROgeBc6aGkqgVzFOzOQ</td>
                </tr>
            </table>
        </details>
    </details>
</details>

<details>
    <summary><strong>Endpoint:</strong> https://commuter.apis.apnibus.com/ticket/v2</summary>
    <p><strong>Method:</strong> GET</p>
    <p><strong>URL:</strong> https://commuter.apis.apnibus.com/ticket/v2?perPage=100</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxNDVjZTdmMy0zMjNhLTRmOTctOTRlMi1kM2YzNDI0OTU5ZmEiLCJpYXQiOjE3MzQwOTQ3NjMsImV4cCI6MTc2NTYzMDc2M30.u-_dO0w0d3L25caq5Ty20N1emHIIi5LquVZLNxR5MxFVIczpODCmd3-AiWJRZaAqMFhROgeBc6aGkqgVzFOzOQ</td>
                </tr>
            </table>
        </details>
    </details>
    <details>
        <summary><strong>Query Params:</strong></summary>
        <table>
            <tr>
                <th>Param</th>
                <th>Value</th>
            </tr>
            <tr>
                <td>perPage</td>
                <td>100</td>
            </tr>
        </table>
    </details>
</details>

<details>
    <summary><strong>Endpoint:</strong> https://commuter.apis.apnibus.com/ticket/upcoming-ticket</summary>
    <p><strong>Method:</strong> GET</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxNDVjZTdmMy0zMjNhLTRmOTctOTRlMi1kM2YzNDI0OTU5ZmEiLCJpYXQiOjE3MzQwOTQ3NjMsImV4cCI6MTc2NTYzMDc2M30.u-_dO0w0d3L25caq5Ty20N1emHIIi5LquVZLNxR5MxFVIczpODCmd3-AiWJRZaAqMFhROgeBc6aGkqgVzFOzOQ</td>
                </tr>
            </table>
        </details>
    </details>
</details>

<details>
    <summary><strong>Endpoint:</strong> https://commuter.apis.apnibus.com/user/user-ticket-saving</summary>
    <p><strong>Method:</strong> GET</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxNDVjZTdmMy0zMjNhLTRmOTctOTRlMi1kM2YzNDI0OTU5ZmEiLCJpYXQiOjE3MzQwOTQ3NjMsImV4cCI6MTc2NTYzMDc2M30.u-_dO0w0d3L25caq5Ty20N1emHIIi5LquVZLNxR5MxFVIczpODCmd3-AiWJRZaAqMFhROgeBc6aGkqgVzFOzOQ</td>
                </tr>
            </table>
        </details>
    </details>
</details>

<details>
    <summary><strong>Endpoint:</strong> https://commuter.apis.apnibus.com/history/recommended-journey</summary>
    <p><strong>Method:</strong> GET</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxNDVjZTdmMy0zMjNhLTRmOTctOTRlMi1kM2YzNDI0OTU5ZmEiLCJpYXQiOjE3MzQwOTQ3NjMsImV4cCI6MTc2NTYzMDc2M30.u-_dO0w0d3L25caq5Ty20N1emHIIi5LquVZLNxR5MxFVIczpODCmd3-AiWJRZaAqMFhROgeBc6aGkqgVzFOzOQ</td>
                </tr>
            </table>
        </details>
    </details>
</details>

<details>
    <summary><strong>Endpoint:</strong> https://commuter.apis.apnibus.com/bus-search/user-bus-search</summary>
    <p><strong>Method:</strong> GET</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxNDVjZTdmMy0zMjNhLTRmOTctOTRlMi1kM2YzNDI0OTU5ZmEiLCJpYXQiOjE3MzQwOTQ3NjMsImV4cCI6MTc2NTYzMDc2M30.u-_dO0w0d3L25caq5Ty20N1emHIIi5LquVZLNxR5MxFVIczpODCmd3-AiWJRZaAqMFhROgeBc6aGkqgVzFOzOQ</td>
                </tr>
            </table>
        </details>
    </details>
</details>

<details>
    <summary><strong>Endpoint:</strong> https://commuter.apis.apnibus.com/bus-search/v2</summary>
    <p><strong>Method:</strong> GET</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxNDVjZTdmMy0zMjNhLTRmOTctOTRlMi1kM2YzNDI0OTU5ZmEiLCJpYXQiOjE3MzQwOTQ3NjMsImV4cCI6MTc2NTYzMDc2M30.u-_dO0w0d3L25caq5Ty20N1emHIIi5LquVZLNxR5MxFVIczpODCmd3-AiWJRZaAqMFhROgeBc6aGkqgVzFOzOQ</td>
                </tr>
            </table>
        </details>
    </details>
    <details>
        <summary><strong>Query Params</strong></summary>
        <table>
            <tr>
                <th>Param</th>
                <th>Value</th>
            </tr>
            <tr>
                <td>fromTownId</td>
                <td>a5a24f6e-cde3-11ec-a96e-e71112ec6aeb</td>
            </tr>
            <tr>
                <td>toTownId</td>
                <td>14e6e936-cd33-11ec-a96e-e71112ec6aeb</td>
            </tr>
            <tr>
                <td>journeyDate</td>
                <td>2024-12-14</td>
            </tr>
            <tr>
                <td>fromDb</td>
                <td>false</td>
            </tr>
        </table>
    </details>
</details>

<details>
    <summary><strong>Endpoint:</strong> https://commuter.apis.apnibus.com/bus-search/v2/layout</summary>
    <p><strong>Method:</strong> POST</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxNDVjZTdmMy0zMjNhLTRmOTctOTRlMi1kM2YzNDI0OTU5ZmEiLCJpYXQiOjE3MzQwOTQ3NjMsImV4cCI6MTc2NTYzMDc2M30.u-_dO0w0d3L25caq5Ty20N1emHIIi5LquVZLNxR5MxFVIczpODCmd3-AiWJRZaAqMFhROgeBc6aGkqgVzFOzOQ</td>
                </tr>
            </table>
        </details>
    </details>
    <details>
        <summary><strong>Body (raw)</strong></summary>
        <pre>
        {
            "source": 10,
            "commuterId": "145ce7f3-323a-4f97-94e2-d3f3424959fa",
            "serviceId": "abdf164a-be27-4878-88c7-7c7486c65ec7",
            "busFormat": "2+1",
            "fromTownId": "a5a24f6e-cde3-11ec-a96e-e71112ec6aeb",
            "toTownId": "14e6e936-cd33-11ec-a96e-e71112ec6aeb",
            "journeyDate": "2024-12-14",
            "fromStationCode": "528",
            "toStationCode": "1353"
        }
        </pre>
    </details>
</details>

<details>
    <summary><strong>Endpoint:</strong> https://commuter.apis.apnibus.com/towns/get-stops</summary>
    <p><strong>Method:</strong> GET</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxNDVjZTdmMy0zMjNhLTRmOTctOTRlMi1kM2YzNDI0OTU5ZmEiLCJpYXQiOjE3MzQwOTQ3NjMsImV4cCI6MTc2NTYzMDc2M30.u-_dO0w0d3L25caq5Ty20N1emHIIi5LquVZLNxR5MxFVIczpODCmd3-AiWJRZaAqMFhROgeBc6aGkqgVzFOzOQ</td>
                </tr>
            </table>
        </details>
    </details>
    <details>
        <summary><strong>Query Params</strong></summary>
        <table>
            <tr>
                <th>Param</th>
                <th>Value</th>
            </tr>
            <tr>
                <td>fromTownId</td>
                <td>a5a24f6e-cde3-11ec-a96e-e71112ec6aeb</td>
            </tr>
            <tr>
                <td>toTownId</td>
                <td>14e6e936-cd33-11ec-a96e-e71112ec6aeb</td>
            </tr>
            <tr>
                <td>journeyDate</td>
                <td>2024-12-14</td>
            </tr>
            <tr>
                <td>serviceId</td>
                <td>abdf164a-be27-4878-88c7-7c7486c65ec7</td>
            </tr>
            <tr>
                <td>source</td>
                <td>10</td>
            </tr>
            <tr>
                <td>tripNumber</td>
                <td>null</td>
            </tr>
            <tr>
                <td>busType</td>
                <td>2+1</td>
            </tr>
            <tr>
                <td>fromStationCode</td>
                <td>528</td>
            </tr>
            <tr>
                <td>toStationCode</td>
                <td>1353</td>
            </tr>
        </table>
    </details>
</details>

<details>
    <summary><strong>Endpoint:</strong> https://commuter.apis.apnibus.com/coupon</summary>
    <p><strong>Method:</strong> POST</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxNDVjZTdmMy0zMjNhLTRmOTctOTRlMi1kM2YzNDI0OTU5ZmEiLCJpYXQiOjE3MzQwOTQ3NjMsImV4cCI6MTc2NTYzMDc2M30.u-_dO0w0d3L25caq5Ty20N1emHIIi5LquVZLNxR5MxFVIczpODCmd3-AiWJRZaAqMFhROgeBc6aGkqgVzFOzOQ</td>
                </tr>
            </table>
        </details>
    </details>
    <details>
        <summary><strong>Body (raw)</strong></summary>
        <pre>
        {
            "amountWithoutDiscount": "350.00",
            "rewardId": null,
            "rescheduleTicketId": "null",
            "onBookingReward": false,
            "isReschedule": false,
            "passId": null,
            "ticketSourcing": 2,
            "seatBooked": [
                {
                    "seatPrice": 350,
                    "serviceTax": 17
                }
            ],
            "sourcePassDiscount": 10
        }
        </pre>
    </details>
</details>

<details>
    <summary><strong>Endpoint:</strong> https://commuter.apis.apnibus.com/ticket/passenger-data</summary>
    <p><strong>Method:</strong> GET</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxNDVjZTdmMy0zMjNhLTRmOTctOTRlMi1kM2YzNDI0OTU5ZmEiLCJpYXQiOjE3MzQwOTQ3NjMsImV4cCI6MTc2NTYzMDc2M30.u-_dO0w0d3L25caq5Ty20N1emHIIi5LquVZLNxR5MxFVIczpODCmd3-AiWJRZaAqMFhROgeBc6aGkqgVzFOzOQ</td>
                </tr>
            </table>
        </details>
    </details>
</details>

<details>
    <summary><strong>Endpoint:</strong> https://commuter.apis.apnibus.com/ticket/v2</summary>
    <p><strong>Method:</strong> POST</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxNDVjZTdmMy0zMjNhLTRmOTctOTRlMi1kM2YzNDI0OTU5ZmEiLCJpYXQiOjE3MzQwOTQ3NjMsImV4cCI6MTc2NTYzMDc2M30.u-_dO0w0d3L25caq5Ty20N1emHIIi5LquVZLNxR5MxFVIczpODCmd3-AiWJRZaAqMFhROgeBc6aGkqgVzFOzOQ</td>
                </tr>
            </table>
        </details>
    </details>
    <details>
        <summary><strong>Body (raw)</strong></summary>
        <pre>
        {
            "ticketServiceId": "abdf164a-be27-4878-88c7-7c7486c65ec7",
            "ticketSeatBooked": [
                {
                    "seatType": "Seater",
                    "seatTypeCode": 1,
                    "seatPrice": 350,
                    "seatNumber": "2",
                    "passengerName": "sambhav ",
                    "passengerContact": "9685338171",
                    "passengerAge": 25,
                    "passengerGender": "Male",
                    "passengerGenderCode": 1,
                    "serviceTax": 17
                }
            ],
            "ticketStatus": 1,
            "ticketTotalAmount": 367,
            "fromTownId": "a5a24f6e-cde3-11ec-a96e-e71112ec6aeb",
            "toTownId": "14e6e936-cd33-11ec-a96e-e71112ec6aeb",
            "payableAmount": 367,
            "boardingPointId": "f1faed5c-86e5-4924-9004-ae65dce307fc",
            "droppingPointId": "cf65d978-c73e-4caa-ad5a-873ea994387d",
            "ticketJourneyDate": "2024-12-14 04:00:00",
            "ticketSource": 10,
            "tripNumber": null,
            "ticketTax": {
                "gst": 17,
                "discount": 0,
                "fare": 350,
                "serviceCharge": 0
            },
            "bookingId": 155327,
            "ticketId": null,
            "ticketRewardId": null,
            "ticketPassRewardId": null,
            "ticketSourcing": 2,
            "ticketWithPass": false
        }
        </pre>
    </details>
</details>

<details>
    <summary><strong>Endpoint:</strong> https://commuter.apis.apnibus.com/ticket/passenger-data</summary>
    <p><strong>Method:</strong> POST</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxNDVjZTdmMy0zMjNhLTRmOTctOTRlMi1kM2YzNDI0OTU5ZmEiLCJpYXQiOjE3MzQwOTQ3NjMsImV4cCI6MTc2NTYzMDc2M30.u-_dO0w0d3L25caq5Ty20N1emHIIi5LquVZLNxR5MxFVIczpODCmd3-AiWJRZaAqMFhROgeBc6aGkqgVzFOzOQ</td>
                </tr>
            </table>
        </details>
    </details>
    <details>
        <summary><strong>Body (raw)</strong></summary>
        <pre>
        {
            "passengerData": [
                {
                    "passengerName": "sambhav ",
                    "passengerAge": 25,
                    "passengerGenderCode": 1
                }
            ]
        }
        </pre>
    </details>
</details>

### Gamification - gamification.apnibus.com

<details>
    <summary><strong>Endpoint:</strong> https://gamification.apnibus.com/profile/utilized-points</summary>
    <p><strong>Method:</strong> GET</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxNDVjZTdmMy0zMjNhLTRmOTctOTRlMi1kM2YzNDI0OTU5ZmEiLCJpYXQiOjE3MzQwOTQ3NjMsImV4cCI6MTc2NTYzMDc2M30.u-_dO0w0d3L25caq5Ty20N1emHIIi5LquVZLNxR5MxFVIczpODCmd3-AiWJRZaAqMFhROgeBc6aGkqgVzFOzOQ</td>
                </tr>
            </table>
        </details>
    </details>
</details>

<details>
    <summary><strong>Endpoint:</strong> https://gamification.apnibus.com/profile/{{param1}}</summary>
    <p><strong>Method:</strong> GET</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxNDVjZTdmMy0zMjNhLTRmOTctOTRlMi1kM2YzNDI0OTU5ZmEiLCJpYXQiOjE3MzQwOTQ3NjMsImV4cCI6MTc2NTYzMDc2M30.u-_dO0w0d3L25caq5Ty20N1emHIIi5LquVZLNxR5MxFVIczpODCmd3-AiWJRZaAqMFhROgeBc6aGkqgVzFOzOQ</td>
                </tr>
            </table>
        </details>
    </details>
</details>

<details>
    <summary><strong>Endpoint:</strong> https://gamification.apnibus.com/rewards/best-V2</summary>
    <p><strong>Method:</strong> GET</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxNDVjZTdmMy0zMjNhLTRmOTctOTRlMi1kM2YzNDI0OTU5ZmEiLCJpYXQiOjE3MzQwOTQ3NjMsImV4cCI6MTc2NTYzMDc2M30.u-_dO0w0d3L25caq5Ty20N1emHIIi5LquVZLNxR5MxFVIczpODCmd3-AiWJRZaAqMFhROgeBc6aGkqgVzFOzOQ</td>
                </tr>
            </table>
        </details>
    </details>
    <details>
        <summary><strong>Query Params</strong></summary>
        <table>
            <tr>
                <th>Param</th>
                <th>Value</th>
            </tr>
            <tr>
                <td>ticketAmount</td>
                <td>5000</td>
            </tr>
            <tr>
                <td>ticketCount</td>
                <td>16</td>
            </tr>
        </table>
    </details>
</details>

<details>
    <summary><strong>Endpoint:</strong> https://gamification.apnibus.com/profile/my-rewards-V2</summary>
    <p><strong>Method:</strong> GET</p>
    <details>
        <summary><strong>Headers:</strong></summary>
        <details>
            <summary><strong>Content-Type</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Content-Type</td>
                    <td>application/json</td>
                </tr>
            </table>
        </details>
        <details>
            <summary><strong>Authorization</strong></summary>
            <table>
                <tr>
                    <th>Header</th>
                    <th>Value</th>
                </tr>
                <tr>
                    <td>Authorization</td>
                    <td>Bearer eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxNDVjZTdmMy0zMjNhLTRmOTctOTRlMi1kM2YzNDI0OTU5ZmEiLCJpYXQiOjE3MzQwOTQ3NjMsImV4cCI6MTc2NTYzMDc2M30.u-_dO0w0d3L25caq5Ty20N1emHIIi5LquVZLNxR5MxFVIczpODCmd3-AiWJRZaAqMFhROgeBc6aGkqgVzFOzOQ</td>
                </tr>
            </table>
        </details>
    </details>
    <details>
        <summary><strong>Query Params</strong></summary>
        <table>
            <tr>
                <th>Param</th>
                <th>Value</th>
            </tr>
            <tr>
                <td>ticketCount</td>
                <td>16</td>
            </tr>
            <tr>
                <td>ticketSource</td>
                <td>10</td>
            </tr>
            <tr>
                <td>isAc</td>
                <td>true</td>
            </tr>
            <tr>
                <td>ticketAmount</td>
                <td>0</td>
            </tr>
        </table>
    </details>
</details>
