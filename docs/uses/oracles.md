# Oracles

Oracles are the backbone of a decentralized financial system. It connects off-chain data with the on-chain world. Normally, ETH has no info about the current market price. During a swap order in a decentralized exchange, a swap contract needs to call the data from various sources to obtain market price. Thus, oracles are the messengers of the crypto ecosystem. Not only in atomic swaps but also more complex interactions such as lending/borrowing assets or dynamic market-making need the data feeds provided by oracles. DeFi ecosystem suffered from Flash Loan attacks caused by [misinformation from centralized price oracles](https://insights.glassnode.com/defi-attacks-flash-loans-centralized-price-oracles/).

## Oracle Pools

Ergo developed [Oracle Pools](https://ergoplatform.org/en/blog/2020-08-31-ergos-oracle-pools-and-what-they-mean-for-the-ecosystem/) to maintain a robust DeFi ecosystem. Because of the eUTXO design and its rich programming language, ErgoScript, oracle networks can be more decentralized. In the extended UTXO model, we have a lot of flexibility and power available to build new protocols. This can be utilized to construct oracle datapoint hierarchies of confidence. In short, they are an abstraction above oracle pools, allowing us to scale the benefits of oracle pools as much as we desire at the cost of price and speed. [ERG/USD oracle pool](https://explorer.ergoplatform.com/en/oracle-pools-list) is running on Ergo Blockchain.

When external oracle data is posted on-chain, it needs to be encoded in a very precise way within a transaction. Furthermore, oracle pools have a bunch of different moving parts which require transactions to be issued to move between the different stages of the pool protocol. [Oracle Core](https://github.com/ergoplatform/oracle-core) creates all of the complex transactions which post the data on-chain & run the oracle pool protocol on-chain (such as averaging data points). This comes bundled with [Oracle Pool Bootstrap](https://github.com/ergoplatform/oracle-core/tree/master/oracle-pool-bootstrap) and a [Connector Library](https://github.com/ergoplatform/oracle-core/tree/master/connectors/connector-lib). The [ada-usd-oracle](https://github.com/ergoplatform/oracle-core/blob/master/scripts/ada-usd-oracle/oracle-config.yaml) source can be seen here. 
See this [overview](https://github.com/Emurgo/Emurgo-Research/blob/master/oracles/Oracle-Pools.md) by Robert Kornacki.

See [Oracles-V2](oracles-v2.md) for more information. 


## Resources

### Forum Posts

- [Trustless Oracle Contracts](https://www.ergoforum.org/t/trustless-oracle-contracts/3793)
- [Shrimpcoin - The first shrimp-pinned stablecoin on Ergo](https://www.ergoforum.org/t/shrimpcoin-the-first-shrimp-pinned-stablecoin-on-ergo/1381) (Inactive)


### GitHub

- [eth/usd connector](https://github.com/Luivatra/oracle-core/tree/eth-connector)
- [Ergo oracles](https://github.com/sininen-taivas/ergo-oracle) | simple command-line tool to launch oracles. Inbuilt implementations for USD/ERG, EUR/ERG, BTC/ERG, AUG/ERG (gold) prices delivery. 
  - See also a [forum topic with example](https://www.ergoforum.org/t/erg-usd-oracle-on-top-of-ergo/119)



### Articles

- [Chainlink Oracles vs. Ergo Oracle Pools](https://ergoplatform.org/en/blog/2021-04-27-chainlink-oracles-vs-ergo-oracle-pools/)
- [Oracle Pools - A New Oracle Model](https://www.ergoforum.org/t/oracle-pools-a-new-oracle-model/263)
- [First steps towards interoperability with Cardano oracles](https://ergoplatform.org/en/blog/2020-11-09-first-steps-towards-interoperability-with-cardano-oracles/)
- [Ergo Blockchain: Oracle Pool Governance Update](https://curiaregiscrypto.medium.com/ergo-blockchain-oracle-pool-governance-update-d078d58571b0)
- [The role of Ergo Oracles](https://veriumfellow.medium.com/oracle-special-4e36cfa6a852)

### The Delphi Project (Inactive)

The Delphi Project aims to help anyone explore, run, and launch decentralized oracles on the Ergo blockchain. 

- [Website](https://delphiproject.org/#)
- [Final Report](https://hackmd.io/@abchris/S1dHZcwyc)

