# Squad Client Base API

## Submitting Contributions

### `newContribution`
`newContribution(contribution, [tags], licenseConfiguration) => id`

Contributions are of the type `{ data, license }`.

Tags are strings used for querying contributions. 

The data signature of the license configuration depends on the license. For the Squad beta contract, license configuration should be `{ benefactor, basisPoints, purchasePrice }`, where:

- The benefactor is the address that can redeem profit from the Squad contract. This version of the API can only support licenses with a single benefactor.

- Basis points (1/100s of a percent) represent the portion of incoming contribution revenue that goes to the benefactor, minus the network fee.

- Purchase price is the amount, in reserve tokens, one must pay for rights to use the contribution

## Buying and Selling Contribution Bonds and Usage Rights

### `tokenPriceEstimate`
`tokenPriceEstimate(contributionId, buySellAmount)`
Should price estimate's automatically give a little wiggle room in case of simultaneous purchases?

### `licensePriceEstimate`
`licensePriceEstimate(contributionId)`

### `buyTokens`
`buyTokens(contributionId, buyAmount, maxPrice)`

### `buyLicense`
`buyLicense(contributionId)`

### `sellTokens`

### `sellLicenseForTokens`

### `sellLicenseForReserve`

## Withdrawing Funds

### `withdraw`
`withdraw(benefactor)`

## Curating Contributions

### `getTopContributions`

### `getHotContributions`

### `getNewContributions`

# Squad Games Client API

## Submitting and validating Game-specific Contribution Types

### `newGame`

### `newComponent`

### `newFormat`
