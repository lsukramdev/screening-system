# Screening System

LHV needs to build a transaction-screening system to identify payments that may be related to sanctioned entities or activities.

## Screening Flow

1) The payment service intends to commit a transaction. Before doing so, it sends a request to the Screening System. 
2) The Screening System checks the transaction details against relevant sanction lists and screening rules. 
3) If a match is detected, the transaction is flagged for further review; if no match is found, the transaction is approved. 
4) The Screening System returns a response to the payment service indicating whether the transaction is approved or flagged.

### Screening API example

**Request:**

```json
POST /screening
Content-Type: application/json
{
  "transactionId": "123456",
  "senderName": "John Doe",
  "senderAccount": "LT123456789012345678",
  "receiverName": "Jane Smith",
  "receiverAccount": "LT987654321098765432",
  "amount": 1000.00,
  "currency": "EUR",
  "transaction_date": "2024-01-01T12:00:00Z"
}
```

**Response (approved):**

```json
200 OK
Content-Type: application/json
{
  "transactionId": "123456",
  "status": "approved"
}
```
**Response (flagged):**

```json
200 OK
Content-Type: application/json
{
  "transactionId": "123456",
  "status": "flagged"
}
```

### Example curl requests

**Test a flagged transaction (with sanctioned entity):**

```bash
curl -X POST http://localhost:8080/screening \
  -H "Content-Type: application/json" \
  -d '{
    "transactionId": "789012",
    "senderName": "Ivan Popov",
    "senderAccount": "AF123456789012345678",
    "receiverName": "Jane Smith",
    "receiverAccount": "LT987654321098765432",
    "amount": 5000.00,
    "currency": "USD",
    "transaction_date": "2024-01-15T10:30:00Z"
  }'
```

## TODO List:
1) Set up a new Spring Boot project for the Screening System using either Gradle or Maven as the build tool. 
2) Implement a REST API endpoint for screening requests. 
3) For the PoC phase, use the hardcoded sanctioned entities provided in this repository. 
4) Implement a simple equality-based screening check for the PoC phase. Building more complex validation logic is out of scope for this PoC.
