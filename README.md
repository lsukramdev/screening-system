# Screening System

LHV needs to build transaction screening system to identify transactions that may be related to sanctioned entities or activities.

## Screening Flow

1) Payment service want to commit a transaction. Before doing so they send a request to Screening System.
2) Screening System checks the transaction details against various sanction lists and rules.
3) If a match is found, the transaction is flagged for further review. If no match is found, the transaction is approved.
4) The result Screening System returns response to Payment service with either "approved" or "flagged".

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

## TODO List:
1) Set up new Spring Boot project for Screening System. Use Gradle or Maven as build tool.
2) Implement REST API endpoint for screening requests.
3) For PoC phase this repository contains hardcoded sanctioned entities.
4) Implement simple equals based screening check for our PoC phase. Building complex validation is not part of this PoC.