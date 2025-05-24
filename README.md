# Bitwavie OpenAI Tool for GPT

This repository contains the OpenAPI specification for integrating the Bitwavie crypto transaction processing platform with OpenAI's GPT tools functionality.

## Contents

- `openapi.yaml` - OpenAPI 3.0.1 specification for the Bitwavie API endpoints

## Endpoints

The specification defines three main endpoints:

1. **GET /price/** - Retrieve historical cryptocurrency prices
   - Required parameters: `fromSym` (asset symbol), `timestampSEC` (Unix timestamp)
   - Optional parameters: `toFiat`, `service`, `resolution`, `timezone`

2. **POST /fifo/universal** - Process FIFO calculations across all wallets
   - Accepts a CSV file with transaction data
   - Returns cost basis and realized gain/loss calculations

3. **POST /fifo/per_wallet** - Process FIFO calculations on a per-wallet basis
   - Accepts a CSV file with transaction data including wallet IDs
   - Returns cost basis and realized gain/loss calculations per wallet

## Usage with OpenAI GPT

1. Create a custom GPT in the OpenAI platform
2. In the configuration, add an "Action" and upload this OpenAPI specification
3. Configure authentication if needed (currently no authentication is required)
4. Your GPT will now be able to make API calls to the Bitwavie services

## Service URL

All endpoints are accessible through the base URL:
```
https://bitwavie-orchestrator-455488113475.us-central1.run.app
```

## Sample CSV Formats

### Universal FIFO CSV Format
```
dateTime,operation,type,assetTicker,assetAmount,assetvalueInBaseCurrency,feeAmount,feeAsset
2023-01-01T10:00:00Z,DEPOSIT,purchase,BTC,1.5,60000,,
2023-01-15T14:30:00Z,WITHDRAW,sale,BTC,0.5,25000,,
```

### Per-wallet FIFO CSV Format
```
dateTime,walletId,operation,type,transactionId,assetTicker,assetAmount,assetvalueInBaseCurrency,feeAmount,feeAsset
2023-01-01T10:00:00Z,wallet1,DEPOSIT,purchase,tx1,BTC,1.5,60000,,
2023-01-15T14:30:00Z,wallet1,WITHDRAW,sale,tx2,BTC,0.5,25000,,
```
