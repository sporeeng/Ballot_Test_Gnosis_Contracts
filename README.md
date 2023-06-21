# Ballot Gnosis Contracts

## WhitelistSoulbound1155NFT.sol
ERC1155 Soulbound NFT implementation to serve as whitelist and KYC mechanism for participants.
- **Contract:** https://gnosisscan.io/address/0x77f6A5f1B7a2b6D6C322Af8581317D6Bb0a52689

| Function | Visibility | Restricted | Description |
| ------------- | :-------------: | :-----: | :----- |
| burn | public | yes | Used to burn tokens from members. |
| mint | public | yes | Used to mint tokens to members. |
| setSoulbound | public | yes | Used to restrict token ID transfers. |
| totalSupply | public | no | Used to track token ID supply and overall supply. |

## BallotContract.sol
Voting contract with a custom whitelist and KYC criteria determined by holdgin NFTs.
- **Contract:** https://gnosisscan.io/address/0x84Da107541eCda5B1dd16B322938A9629162512E

| Function | Visibility | Restricted | Description |
| ------------- | :-------------: | :-----: | :----- |
| setEndTime | public | yes | Used to set the voting end time. |
| setKYCID | public | yes | Used to set the NFT ID corresponding to the KYC, default=0. |
| setVOTEID | public | yes | Used to set the NFT ID corresponding to the whitelisted voting campaign, default=1. |
| setNFT | public | yes | Used to set the NFT address contract. |
| setVotingProposalTitle | public | yes | Used to set the main voting title. |
| vote | public | no | Used for users to vote, users should hold NFT ID 0 and the NFT ID corresponding to the voting campaign to be able to vote. |
| END_TIME | public | no | Returns the end time of the voting initiative. |
| KYC_NFT_ID | public | no | Returns the NFT ID corresponding to the user KYC. |
| VOTE_NFT_ID | public | no | Returns the NFT ID corresponding to the user whitelisting. |
| NFT | public | no | Returns the contract NFT address. |
| participants | public | no | Array of addresses corresponding to the voters. |
| participantsAmount | public | no | Returns the amount of voters as integer, used to parse participants array. |
| proposals | public | no | Array of options/choices for the given ballot. |
| proposalsAmount | public | no | Returns the amount of options/choices as integer, used to parse proposals array. |
| voters | public | no | Mapping with voter's information. |
| winnerProposal | public | no | Returns the name of the winner option/choice. |
 
## Whitelist & KYC Mechanism

The NFT ID 0 from the ERC1155 implementation should be a representation of the user's KYC completition, meaning that, if user holds this NFT, platforms and business logic inside contracts should understand that the user have a valid and active KYC.

The subsecuent NFTs represents if the user is whitelisted for the voting contracts or not, as requested, every new voting initiative is a new contract, which means that, if users want to vote on the current deployed voting initiative, they must hold NFT ID 0 for KYC along with NFT ID 1 for the voting contract, but if a new voting contract is deployed, users should hold NFT ID 0 and NFT ID 2 for the respective voring contract, and so on (only if needed, by design whitelisted NFTs can be reused on more than 1 voting contract).

- NFT ID 0 represents the user KYC compliance.
- NFT ID 1~N represents the user whitelist for the voting contracts.

## Why The NFT Approach?

- **Costs:** Some times the process of upload big lists of whitelisted addresses could be costly in gas.
- **Efficiency:** Once NFTs are minted, contracts can perform automatic business logic based on many custom scenarios.
- **Flexibility:** Users can been fidelized and unlock more incentives by holding an unique key for many products.

## Improvements & Known Issues

- The **safeBatchTransferFrom** function from the ERC1155 contract is not soulbound enabled, users could transfer their NFTs using this method.
- If a votation is deuce, there's no way to break the even.
- Using Merkle Tree signatures for whitelisting users instead of NFTs.
- Mint ERC20 tokens once users vote to serve as some kind of voting power for upcoming initiatives or reward systems to fidelize.

## How To Use

