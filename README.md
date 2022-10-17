# Algorand School Project Proposal

## Group G4: 
1. Uroš Hudomalj - https://github.com/uhudo
2. Fadi Barbara - https://gihub.com/disnocen
3. Akshay Kant - https://github.com/akshaykant

*Project Name: Decentralized Auction marketplace*

## Goal 

The end-goal of the project is to create a NFT auction manager (NAM) based on the contracts presented [at the school](https://github.com/algorand-school/handson-contract). NFT sellers deploy and manage auctions through the NAM, while bidders can interact with the currently-active auction by sending specific bids through the NAM.

Of course, the management of auctions is part of some solutions already deployed (see the [State of the art](#state-of-the-art) section). On the other hand, those are *ad hoc* solutions and it is not easy to deploy them separately from the market itself. This creates a network effect that *de facto* increases the centralization of the markets to a handful of competitors that can easily create a monopoly (or oligopoly) and [threat the opennes of the environment](https://www.fon.hum.uva.nl/rob/Courses/InformationInSpeech/CDROM/Literature/LOTwinterschool2006/szabo.best.vwh.net/ttps.html). We argue that this scenario would hinder blockchain's potential at the detriment of the end-users.

To mitigate this problem, we aim to create a service that specifically addresses *only* the management of auctions. We believe that this service could be an important tool in the decentralization of markets (at least of those related to NFTs): it simplifies the sale of assets, from the seller's point of view, removing friction and opening the creation of many (possibly smaller) online markets.

## State of the art
Auctions have been around for [more than 2500 years](https://www.econport.org/content/handbook/auctions/historyofauctions.html). Through the course of history many things have changed, of course, but since the practice is so ingrained into the human history it is no surprise that auctions are also a conspicuous part of the blockchain ecosystem.

Many examples can be made, from the [Maker Protocol's auctions](https://docs.makerdao.com/keepers/the-auctions-of-the-maker-protocol#auctions) for *surplus* and *collateral* of (fungible) tokens, to the [Flashbots' auctions](https://docs.flashbots.net/Flashbots-auction/overview/) for a fairer Miner Extractable Value (MEV).

Non Fungible Tokens are currently widely exchanged and make up for a lot of volume in transactions. While ....
## Smart Contract Specifications



## Modifications
We improved upon the NFT auction smart contract (https://github.com/algorand-school/handson-contract) by improving some functions and creating new ones. In particular, we maintained two contracts: one which supports sealed bids and one without.

In the following we list the specific changes we made to the contract

### Improvements

This is a list of improvement with respect the original contract. For both the ordinary and sealed-type, we:

- modified the tracking of time from timestamp to rounds: this way we use the blockchain inner clocking mechanism and we are not subject to subjective changes in the participants' watches
- individual claiming - explain why `please explain`
- check of dynamic datatypes according to ABI guideline recommendations

For sealed-type we made some specific improvements too:
- improved obfuscation with a `nonce`: the goal is to avoid a [rainbow attack](https://en.wikipedia.org/wiki/Rainbow_table)
- code optimization - removing unnecessary check (`start<commit` and `commit<end`, where it was unnecessary to check `start<end`, etc.)

### New features

- Service fees 
- Overcollateralization 
- Vickrey auction 

### Future features
- Marketplace 
- Dutch auction 

## Decentralized Auction Marketplace Mechanics: 

- Auction Contract which will act as the parent/entry point to smart contracts.
- List Function: take the NFT along with arguments like reserve price and duration of the auction along with the choice of auction mechanism (sealed auction). This will deploy a unique contract along with all the parameters for that auction and transfer NFT into the custody of that `app_id`. Also, store the `app_id` in the global storage.
- Send Sealed Bid
hash(nonce, amount) - represent the sealed bid along with `app_id` of the auction. The auction marketplace can check the global storage if `app_id` exists and send the sealed bid. Auction with `app_id` will store the sealed bin in global storage and replace it if there was already sent.
- Send Opening Bid
Send `nonce`, the amount along with payment and `app_id`. Auction contract checks if openings could be received and accept payment transaction only if it reaches the reserve price. If the auction holds the previous highest bid and the recent one is higher, accept the new one and return funds to the previous higher bid.

## Economics of protocol
Fees from the seller to make the decentralized protocol running which included Service fees - 2% fees of winning bid




## Open Questions

- For project initiation which features should we implement?

- How does global storage work? Who pays for the allocated space?
  Here is the open question - https://forum.algorand.org/t/global-storage-fees/7996

- Complexity of building an auction marketplace that supports multiple auction types?

- Current Algorand smart contract architecture has a limitation for global storage which will be resolved with the introduction of Box storage. So we could consider Box storage as an upgrade for a more involved and scalable application?
