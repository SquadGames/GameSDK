# Squad Client Base API

## Submitting Contributions

### `newContribution`
`newContribution(contribution, [tags], benefactor, network) => id`

`Contribution { data, license }`

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
