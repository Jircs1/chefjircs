# ABI Chef

This abi-chef repo contains JSON-LD ABIs of Web3 projects (at present, EVM-centric) empowering Colorful Notion's Chefs to programmatically index Web3 projects.

The JSON-LD ABIs enable us to:
* generate project datasets for hundreds of Web3 projects ([Uniswap](/defi/uniswap), [Curve](/defi/dex/curve), [ENS](/naming/ens)) 
* aggregate projects with similar data types following recipes 
* visualize public Web3 visualizations 

JSON-LD files are organized in 2 levels (e.g `defi/dex`) with a file naming convention of:
* `config.jsonc` holds "seeds" for the Chef process, curated by data engineers
* `config.jsonld` holds JSON-LD ABI, programmatically generated
* `logs.json` holds recent tallies of observed calls/logs, programmatically generated

At present, the output of the Chefs is in POC concept in a "awesome-web3" [Google BigQuery Public Dataset](https://cloud.google.com/bigquery/public-data) and contains the following datasets:
 * `caladan_evm` - full tables -- similar to "crypto_ethereum", except a SET of tables, one for each chain, e.g. Base being chain 8453 has `awesome-web3.caladan_evm.{blocks8453, transactions8453, logs8453, ...}`
 * `caladan_traces` - partitioned { hourly, daily } datasets of call data 
 * `caladan_logs` - partitioned { hourly, daily } datasets of log data
 * `{project}` -- _project-specific_ datasets built from the above partitioned tables **based on `config.jsonc` in this repo**
   - `naming_ens` holds project tables for [ENS](https://ens.domains/) based on [`/naming/ens/config.jsonc`](/naming/ens/config.jsonc)
   - `ethereum_optimism`  holds tables for [Optimism](https://www.optimism.io/)  based on [`/ethereum/optimism/config.jsonc`](/naming/ens/config.jsonc)
   - `defi_uniswap`  holds tables for [Uniswap](https://app.uniswap.org/) based on [`/defi/dex/uniswap/swapv2/config.jsonc`](/defi/dex/uniswap/swapv2/config.jsonc)
   - `defi_curve`  holds tables for [Curve](https://curve.fi/) based on [`/defi/dex/curve/config.jsonc`](/defi/dex/curve/config.jsonc)
   - `gitcoin_allo`  holds tables for [GitCoin Allo](https://allo.gitcoin.co/) across multiple chains

The JSON-LD ABIs contain "web3 semantics" features to:
1. power Colorful Notion's [evm-etl](https://github.com/colorfulnotion/evm-etl) indexer, which indexes EVM Chains into `caladan_{evm/traces/logs}{_hourly,daily}`, containing decoded data (ethers.js) and decorated data (pricing, labels)
2. power project aggregation following JSON-LD recipes

The above design is intended to scale to any project in the Ethereum/EVM ecosystem and will be extended to other ecosystems (e.g Polkadot/Substrate, WASM Contracts) in the future.

## Chain Support

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
a "config.jsonc" (with comments).  The goal is to have addition of new
config.jsonc programmatically generate new datasets within minutes of
addition to this repo via Github Actions.

A ChefTime DAO to build and project models is under design consideration for Fall 2023:
 * Buying [ChefTime NFT](/cheftime) enhance speed and quality of abi-chef generated datasets: inclusion of real-time data, increased frequency of dataset generation, appended labels
 * Revenue from [ChefTime NFTs](/cheftime) flow to chefs who create and maintain recipes models and a Treasury, augmented by Gitcoin Allo

## License

This repo is under a [Fair Source License](LICENSE).

## Support / Acknowledgements

* The "awesome-web3" is generously supported by the [Google Cloud Web3](https://cloud.google.com/web3)
* [Colorful Notion](https://colorfulnotion.com) is supported in part by Polkadot Treasury for its [substrate-etl](https://github.com/colorfulnotion/substrate-etl), a sister of the evm-etl indexer used in this project
* Raw Signatures database is from the amazingly useful [openchain.xyz](https://openchain.xyz)






