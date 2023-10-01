# ABI Chef

This abi-chef repo contains (a) JSON-LD EVM ABIs (b) seed contract
addresses empowering Colorful Notion's Chefs to programmatically index
Web3 projects.

The JSON-LD ABIs enable the evm-etl indexer to:
* generate project datasets for hundreds of Web3 projects ([Uniswap](/defi/uniswap), [Curve](/defi/curve), [ENS](/naming/ens)) 
* aggregate projects with recipes to put similar projects together
* visualize projects in dashboard

A single JSON-LD file `seed.jsonc` holds "seeds" for the EVM-ETL indexer to take transaction call and log events activity and aggregate them into projects.   The current output is in an "awesome-web3" [Google BigQuery Public Dataset](https://cloud.google.com/bigquery/public-data) and contains the following datasets:
 * `caladan_evm` - full tables -- similar to "crypto_ethereum", except a SET of tables, one for each chain, e.g. Base being chain 8453 has `awesome-web3.caladan_evm.{blocks8453, transactions8453, logs8453, ...}`
 * `caladan_traces` - partitioned { hourly, daily } datasets of call data 
 * `caladan_logs` - partitioned { hourly, daily } datasets of log data
 * `{project}` -- _project-specific_ datasets built from the above partitioned tables **based on `seed.jsonc` in this repo**
   - `naming_ens` holds project tables for [ENS](https://ens.domains/) based on [`/naming/ens/seed.jsonc`](/naming/ens/seed.jsonc)
   - `ethereum_optimism`  holds tables for [Optimism](https://www.optimism.io/)  based on [`/ethereum/optimism/seed.jsonc`](/naming/ens/seed.jsonc)
   - `defi_uniswap`  holds tables for [Uniswap](https://app.uniswap.org/) based on [`/defi/uniswap/seed.jsonc`](/defi/uniswap/seed.jsonc)
   - `defi_curve`  holds tables for [Curve](https://curve.fi/) based on [`/defi/curve/seed.jsonc`](/defi/curve/seed.jsonc)
   - `gitcoin_allo`  holds tables for [GitCoin Allo](https://allo.gitcoin.co/) across multiple chains

The above design is intended to scale to any project in the Ethereum/EVM ecosystem and others in the fture


* Ethereum (1) - in progress as of September 2023
* Public Goods (424) - in progress as of September 2023
* Base (8453) - in progress as of September 2023
* Optimism (10) - in progress as of September 2023
* Arbitrum (42161) - in progress as of September 2023
* Moonbeam (1284) - in progress as of September 2023
* Astar (592) - in progress as of September 2023
* Moonriver (1285) - planned Q4 2023
* Solana - planned Q4 2023
* Polygon - planned Q4 2023
* Polkadot/Kusama - planned Q1 2024

## Contributions

New projects may be added via pull request by adding a directory with
a "seed.jsonc" (jsonc=with comments) containing:

* `seeds` - an array of seed deployment + factory addresses
* `recipes` - an array of  ABI functions/event names that will have 1 or more tables generated

The goal is to have chefs be able to quick and _programmatically_ generate new datasets within minutes of
addition to this repo via Github Actions.

A ChefTime DAO to build and project models is under design consideration for Fall 2023:
 * Buying [ChefTime NFT](/cheftime) enhance speed and quality of abi-chef generated datasets: inclusion of real-time data, increased frequency of dataset generation, appended labels
 * Revenue from [ChefTime NFTs](/cheftime) flow to chefs who create and maintain recipes models and a Treasury, augmented by Gitcoin Allo

## License

This repo is under a [Fair Source License](LICENSE).

## Support / Acknowledgements

* The "awesome-web3" is generously supported by the [Google Cloud Web3](https://cloud.google.com/web3) team
* [Colorful Notion](https://colorfulnotion.com) is supported in part by Polkadot Treasury for its [substrate-etl](https://github.com/colorfulnotion/substrate-etl), a sister of the evm-etl indexer used in this project
* Raw Signatures database is powered by the amazingly useful [openchain.xyz](https://openchain.xyz)






