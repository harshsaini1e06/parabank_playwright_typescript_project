# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: API\accountList.spec.ts >> Get Accounts List
- Location: tests\API\accountList.spec.ts:5:5

# Error details

```
Error: API failed. Response: Could not find customer #16652

expect(received).toBe(expected) // Object.is equality

Expected: 200
Received: 400
```

# Test source

```ts
  1  | import { test, expect } from'@playwright/test'
  2  | import * as fs from'fs'
  3  | import * as path from'path'
  4  | 
  5  | test('Get Accounts List',async({request})=>{
  6  |     const checkingData = JSON.parse(
  7  |         fs.readFileSync(path.join(__dirname, '../Utils/checkingAcc.json'),
  8  |     'utf-8'
  9  |         )
  10 |     )
  11 |     const customerId = checkingData.customerId
  12 |     console.log('Customer ID =', customerId)
  13 | 
  14 |     const response = await request.get(`https://parabank.parasoft.com/parabank/services/bank/customers/${customerId}/accounts`
  15 |     )
  16 | const body = await response.text()
  17 |     console.log('Status =', response.status())
  18 |     console.log('Response =')
  19 |     console.log(body)
  20 | 
  21 |     expect(
> 22 |         response.status(),`API failed. Response: ${body}`).toBe(200)
     |                                                            ^ Error: API failed. Response: Could not find customer #16652
  23 |     expect(body).toContain('<account>')
  24 | })
```