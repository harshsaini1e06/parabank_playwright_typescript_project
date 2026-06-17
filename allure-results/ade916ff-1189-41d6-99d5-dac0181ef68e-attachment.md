# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: API\accountCreation.spec.ts >> Create New Account API
- Location: tests\API\accountCreation.spec.ts:5:5

# Error details

```
Error: expect(received).toBe(expected) // Object.is equality

Expected: 200
Received: 400
```

# Test source

```ts
  1  | import {test,expect}from'@playwright/test'
  2  | import * as fs from'fs'
  3  | import * as path from'path'
  4  | 
  5  | test('Create New Account API', async ({ request }) => {
  6  |     const checkingData = JSON.parse(
  7  |         fs.readFileSync(path.join(__dirname, '../Utils/checkingAcc.json'),
  8  |     'utf-8'
  9  |         )
  10 |     )
  11 |     const customerId=checkingData.customerId
  12 |     const fromAccountId=checkingData.accountId
  13 | 
  14 |     console.log('customerId =', customerId)
  15 |     console.log('fromAccountId =', fromAccountId)
  16 | 
  17 |     const response = await request.post(`https://parabank.parasoft.com/parabank/services/bank/createAccount?customerId=${customerId}&newAccountType=1&fromAccountId=${fromAccountId}`
  18 |     )
  19 | 
  20 |     console.log('Status =', response.status())
  21 |     const body = await response.text()
  22 |     console.log(body)
> 23 |     expect(response.status()).toBe(200)
     |                               ^ Error: expect(received).toBe(expected) // Object.is equality
  24 |     
  25 |     expect(body).toContain('<id>')
  26 | })
```