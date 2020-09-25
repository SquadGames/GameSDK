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

### `tokenReserveValue`
`tokenReserveValue(contributionId, buySellAmount) => value in reserve tokens`

Gets the supply of the contribution token, then calls `price` on the curve used in the Squad contract. Adds a standard buffer amount to the price estimate to account for gaps between estimate and actual price (positive buffer for positive buySell, negative for negative).

### `mintLicensePrice`
`mintLicensePrice(contributionId) => price in reserve tokens`

Returns the price in reserve tokens of minting a license for a contribution.

### `licenseTokenValue`
`licenseTokenValue(licenseId) => value in contribution tokens`

Returns the number of contribution tokens locked in the license. (contract function not written yet?)

### `licenseReserveValue`
`licenseReserveValue(licenseId) => value in reserve tokens`

Calls `tokenReserveValue` on the result of `licenseTokenValue`. Returns an estimated number of reserve tokens the license can be sold for.

### `buyTokens`
`buyTokens(contributionId, buyAmount, maxPrice)`

Calls `buyBond` in the Squad contract. Transfers the price in reserve tokens (but reverts if it's > maxPrice) from the caller to Squad. Transfers the buy amount of contribution bond tokens to the caller.

### `mintLicense`
`mintLicense(contributionId)`

Calls `buyAndMint` in the Squad contract. Transfers the purchase price in reserve tokens from the caller to Squad. Mints and transfers an NFT license to the caller.

### `sellTokens`
`sellTokens(contributionId, amount, minValue)`

Calls `sellBond` in the Squad contract. Transfers an amount of contribution tokens from the caller to Squad. Transfers the equivalent number of reserve tokens to the caller (but reverts if it's < minValue).

### `sellLicenseForTokens`
`sellLicenseForTokens(licenseId)`

Calls `returnLicense` in the Squad contract. Destroys the license and transfers the contribution tokens it represents to the caller.

### `sellLicenseForReserve`
`sellLicenseForReserve(licenseId, minValue)`

Calls `returnAndSell` in the Squad contract. Destroys the license, sells the resulting tokens for reserve, and transfers the reserve to the caller (reverts if sell price is < minValue).

TODO: possible that Squad doesn't need `returnAndSell` because we can call the functions atomically here?

### `refinanceLicense`
`refinanceLicense(licenseId)`

Checks that `licenseReserveValue` > `licensePrice`. If it is, calls `returnAndSell` followed by `buyLicense` in the Squad contract, leaving the caller with the extra reserve tokens and a newly minted license.

TODO: see above

## Withdrawing Funds

### `withdrawFor`
`withdrawFor(benefactor)`

Calls `withdrawFor(address)` in the Squad contract, withdrawing any reserve tokens that have accumulated for the benefactor (minus network fees).

TODO: these should be called 'beneficiaries' not 'benefactors'

## Curating Contributions

TODO: what events do we need to record in a subgraph to enable these methods?

### `getTopContributions`
`getTopContributions([tags], num)`

Fetches the top `num` contributions in terms of market capitalization that share all `[tags]`.

### `getHotContributions`
`getHotContributions([tags], num)`

Fetches the top `num` contributions in terms of acceleration of market capitalization that share all `[tags]`.

### `getNewContributions`
`getNewContributions([tags], num)`

Fetches the newest `num` contributions in terms of creation date that share all `[tags]`.

# Squad Games Client API

## Submitting and validating Game-specific Contribution Types

### `newGame`
`newGame(gameContribution, [tags], licenseConfiguration)`

Data in a game contribution should contain the information needed to launch the game. A standard "squad game" tag is added to all games.

### `newComponent`
`newComponent(componentContribution, [tags], licenseConfiguration)`

Component contributions have no special requirements, but `tags` are expected to include the game contributions the components are intended for.

### `newFormat`
`newFormat(formatContribution, [tags], licenseConfiguration)`

Formats are like components, except their contribution `data` must include a list of components, which the API will verify are valid components before submitting.
