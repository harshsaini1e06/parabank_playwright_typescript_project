# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: API\accountDetailValidation.spec.ts >> Validate Account Details
- Location: tests\API\accountDetailValidation.spec.ts:5:5

# Error details

```
Error: expect(received).toBe(expected) // Object.is equality

Expected: 200
Received: 400
```

# Test source

```ts
  1  | import {test,expect} from'@playwright/test'
  2  | import * as fs from'fs'
  3  | import * as path from'path'
  4  | 
  5  | test('Validate Account Details',async({request})=>{
  6  |     const savingAcc = JSON.parse(fs.readFileSync(path.join(__dirname, '../Utils/savingAcc.json'),
  7  |             'utf-8'
  8  |         )
  9  |     )
  10 | 
  11 |     console.log('Account ID =', savingAcc.accountId)
  12 |     const response = await request.get(`https://parabank.parasoft.com/parabank/services/bank/accounts/${savingAcc.accountId}`
  13 |     )
  14 |     console.log('Status =', response.status())
> 15 |     expect(response.status()).toBe(200)
     |                               ^ Error: expect(received).toBe(expected) // Object.is equality
  16 |     const responseText = await response.text()
  17 | 
  18 |     console.log('Response =', responseText)
  19 |     expect(responseText).toContain(`<id>${savingAcc.accountId}</id>`)
  20 |     expect(responseText).toContain('<balance>')
  21 | })
```