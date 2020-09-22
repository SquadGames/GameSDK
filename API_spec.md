# Squad Client Base API

## Submitting Contributions

### `newContribution`
`newContribution(contribution, [tags], licenseConfiguration) => id`

Contributions are of the type `{ data, license }`.

Tags are strings used for querying contributions. 

The data signature of the license configuration depends on the license. For the Squad beta contract, license configuration should be `{ benefactor, basisPoints, purchasePrice }`, where:

- The benefactor is the address that can redeem profit from the Squad contract. This version of the API can only support licenses with a single benefactor.

- Basis points are the portion of incoming contribution revenue that goes to the benefactor, minus the network fee, where 1 BP = 1/10,000.

- Purchase price is the amount, in reserve tokens, one must pay for rights to use the contribution

Stores the contribution in a database under a unique ID (TODO: events and subgraph? IPFS pin?). 

Uses the ID, license, and license configuration to call `createBond` in the Squad contract.

## Buying and Selling Contribution Bonds and Usage Rights

### `tokenPriceEstimate`
`tokenPriceEstimate(contributionId, buySellAmount) => price`
Gets the supply of the contribution token, then calls `price` on the curve used in the Squad contract. Adds a standard buffer amount to the price estimate to account for gaps between estimate and actual price.

### `licensePrice`
`licensePrice(contributionId) => price`
Returns the price of minting a license for a contribution.

### `buyTokens`
`buyTokens(contributionId, buyAmount, maxPrice)`


### `buyLicense`
`buyLicense(contributionId)`
Mints a license

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
