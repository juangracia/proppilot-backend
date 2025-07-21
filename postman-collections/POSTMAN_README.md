# PropPilot API - Postman Collection

This directory contains a comprehensive Postman collection for testing the PropPilot API with real sample data from the PostgreSQL database.

## Files Included

- `PropPilot-API.postman_collection.json` - Complete API collection with all endpoints
- `PropPilot-Environment.postman_environment.json` - Environment variables for development
- `POSTMAN_README.md` - This documentation file

## Setup Instructions

### 1. Import Collection and Environment

1. Open Postman
2. Click **Import** button
3. Import both files:
   - `PropPilot-API.postman_collection.json`
   - `PropPilot-Environment.postman_environment.json`

### 2. Set Environment

1. Select "PropPilot Development" environment from the dropdown
2. Verify the `baseUrl` is set to `http://localhost:8080`

### 3. Start the Application

Before testing, ensure your application is running:

```bash
# Start the database
docker-compose up -d

# Populate with sample data
./populate_database.sh

# Start the Spring Boot application
./start-backend.sh
```

## Collection Structure

### Property Units Endpoints

- **POST** `/api/property-units` - Create new property unit
- **GET** `/api/property-units` - Get all property units  
- **GET** `/api/property-units/{id}` - Get property unit by ID
- **GET** `/api/property-units/search` - Search property units by address
- **PUT** `/api/property-units/{id}` - Update property unit
- **DELETE** `/api/property-units/{id}` - Delete property unit

### Payments Endpoints

- **POST** `/api/payments` - Create new payment
- **GET** `/api/payments` - Get all payments
- **GET** `/api/payments/{id}` - Get payment by ID
- **GET** `/api/payments/property-unit/{id}` - Get payments by property unit
- **PUT** `/api/payments/{id}` - Update payment
- **DELETE** `/api/payments/{id}` - Delete payment

### Advanced Payment Calculations

- **GET** `/api/payments/property-unit/{id}/adjusted-rent` - Calculate adjusted rent
- **GET** `/api/payments/property-unit/{id}/outstanding` - Get outstanding payments
- **GET** `/api/payments/property-unit/{id}/outstanding-amount` - Calculate outstanding amount
- **GET** `/api/payments/property-unit/{id}/total-paid` - Get total paid by payment type
- **GET** `/api/payments/property-unit/{id}/history` - Get payment history

## Sample Data Available

The collection uses real data from your PostgreSQL database:

### Property Units
- **ID 1**: 123 Oak Street, Apt 2A (Apartment, $1,850/month)
- **ID 2**: 456 Pine Avenue (House, $2,100/month)  
- **ID 3**: 789 Maple Drive (House, $2,850/month)
- **ID 4**: 321 Elm Street, Unit 5 (Apartment, $1,650/month)
- **ID 5**: 654 Cedar Lane (Townhouse, $1,950/month)

### Sample Payments
- Property Unit 1 has deposit ($2,500) and monthly rent payments from Aug 2023
- Property Unit 2 has deposit ($3,000) and monthly rent payments from Sep 2023
- All payments are marked as "PAID" status

## Environment Variables

| Variable | Value | Description |
|----------|-------|-------------|
| `baseUrl` | `http://localhost:8080` | API base URL |
| `propertyUnitId` | `1` | Sample property unit ID for testing |
| `paymentId` | `1` | Sample payment ID for testing |
| `currentDate` | `2024-07-21` | Current date for calculations |
| `sampleAddress` | `123 Oak Street, Apt 2A` | Sample address for search |
| `sampleRentAmount` | `1850.00` | Sample rent amount |

## Testing Workflow

### 1. Basic CRUD Operations

1. **Create Property Unit**: Use the POST endpoint with sample data
2. **List All Units**: GET all property units to see the created unit
3. **Get Specific Unit**: GET by ID to see details with payments
4. **Update Unit**: PUT to modify the unit details
5. **Search Units**: Use the search endpoint with address parameter

### 2. Payment Management

1. **Create Payment**: POST a new rent or deposit payment
2. **List Payments**: GET all payments or filter by property unit
3. **Payment History**: GET payment history with date range
4. **Update Payment**: PUT to modify payment details

### 3. Advanced Calculations

1. **Adjusted Rent**: Calculate rent with inflation adjustments
2. **Outstanding Amount**: Check how much rent is owed
3. **Total Paid**: Sum payments by type (RENT, DEPOSIT, etc.)
4. **Outstanding Payments**: List pending payments

## Response Examples

All endpoints return JSON responses with real data. Check the collection's example responses to see the expected format.

## Troubleshooting

### Common Issues

1. **Connection Refused**: Ensure the Spring Boot app is running on port 8080
2. **Database Errors**: Verify PostgreSQL is running with `docker ps`
3. **No Data**: Run `./populate_database.sh` to add sample data
4. **404 Errors**: Check that the property unit or payment ID exists

### Verify Setup

Test the basic endpoint to ensure everything is working:

```
GET {{baseUrl}}/api/property-units
```

This should return a list of property units with real data.

## API Documentation

For detailed API documentation, visit the Swagger UI when the application is running:

**Swagger UI**: http://localhost:8080/swagger-ui.html

The Swagger documentation now includes real examples that match the Postman collection data.
