# Squad Client Base API

## Submitting Contributions

### `newContribution`
`newContribution(contribution, [tags], benefactor, network) => id`

`Contribution { data, license }`

## Buying and Selling Contribution Bonds and Usage Rights

### `tokenPriceEstimate`
`tokenPriceEstimate(contributionId, buySellAmount)`

### `licensePriceEstimate`
`licensePriceEstimate(contributionId)`

### `buyTokens`
`buyTokens(contributionId, buyAmount, buyPrice)`
Automatically set maxPrice

### `buyLicense`

### `sellTokens`

### `sellLicenseForTokens`

### `sellLicenseForReserve`

## Curating Contributions

### `getTopContributions`

### `getHotContributions`

### `getNewContributions`

# Squad Games Client API

## Submitting and validating Game-specific Contribution Types

### `newGame`

### `newComponent`

### `newFormat`
