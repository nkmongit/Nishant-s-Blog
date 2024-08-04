---
date created: Saturday, August 3rd 2024, 4:35:58 pm
date modified: Sunday, August 4th 2024, 11:49:36 pm
tags:
  - 100xdevs
  - moc/web3
  - orientation
---

# Cohort 3.0 Exclusive Hackathon
Link - [https://earn.superteam.fun/listings/project/100xdevs-solana-mini-hackathon-1/](https://earn.superteam.fun/listings/project/100xdevs-solana-mini-hackathon-1/)

### Project ideas
1. **Web3 Zapier** -> [https://build.superteam.fun/ideas/automated-workflows](https://build.superteam.fun/ideas/automated-workflows)

2. **Whale Alert** -> [https://x.com/cyversalerts/status/1813834131165286464](https://x.com/cyversalerts/status/1813834131165286464)

3. **Liquidating an NFT to a token** -> [https://build.superteam.fun/ideas/liquidating-an-nft-to-any-token](https://build.superteam.fun/ideas/liquidating-an-nft-to-any-token)

4. **NFT** viewing gallery (maybe in 3D) 

5. **Decentralized Fiver** -> End to End job portal to hire solana devs, pay them, **escrow money** from the job provider.

6. **RPC Aggregator** -> Let a user put in a bunch of RPCs from various providers (Helius, Alchemy, QuickNode) and you should figure out which one to forward requests to (Similar to [https://www.ironforge.cloud/](https://www.ironforge.cloud/) )

7. Wallet adapter for a web based wallet.

8. **Youtube Channel Opinions Market** -> Let people trade on a coin associated to a Youtube channel. Creator can come and collect royalties by connecting their YT account. [https://www.youtube.com/watch?v=PZNgcH2Jtac](https://www.youtube.com/watch?v=PZNgcH2Jtac)

9. **Tiplink** -> (even tho we’re building it separately, if you want to build a better version with a twist, you should do it), it's a wallet as a service.

10. **Github Bounty Dispenser** -> Make users give their Aadhar/Pan. Make users link their github with their wallet address. Allow maintainers to approve bounties. Create a dashboard where you can track profiles of users/companies and a leader-board of contributors based on bounty earned. [Algora.io](console.algora.io) it lets you dispense bounty from github.

12. **UI Library for Solana** -> NFTCard, TokenCard, SwapCard

 Companies like [Helius - Solana's Leading RPC & API Platform](https://www.helius.dev/) has web-hooks to make call on Solana.

# Why Blockchains?
### Inflating currencies
Government has been printing currencies left right and center. This leads to increasing inflation, price of everything goes up.

Holding on to cash is a losers bet in the long run. Holding on to any asset (Gold, Stock, real estate) is better compared to currencies like USD, INR.

### Fractional Reserve Banking

Banks don't have your money. They lend out most of it.
If there is a bank run (everyone goes to the bank to withdraw their money), banks wont be able to pay everyone.
Silicon valley collapsed in 2022. I was in the US when it happened. Most YC companies had their funds in SVB. They were bailed out, but if not, you would’ve seen a lot of startups die.
### Bailouts
The 2008 Financial crisis was triggered by a financial instrument called mortgage-backed securities.
Even though the banks at Wall Street were at fault, the government ended up bailing them out using Taxpayer money.


A great movie to look at is **Big Short.** 
![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F085e8ad8-528e-47d7-8922-a23dc4016453%2F37d3740e-ab52-497f-99e6-cdd9f722cc79%2Fscale.webp?table=block&id=2d1e0bad-402b-473b-8951-025296f8fb14&cache=v2)

# How to create a new currency?
Right now, currencies can only be issued by central governments. You can’t create your own `Nishant coin` and ask users to use it.

Even if I do issue a `Nishant coin` , no one would use it, and for good reasons -
1. I can print any number of Nishant coins, making myself richer.
2. I become the central mint and verification authority for the coin.
3. No one would (or should) trust me.

# Intro to Hashing

![[hashing.png]]

**Hashing** is a process that transforms input data (of any size) into a fixed-size string of characters.

Hash functions have several important properties:

1. **Deterministic**: The same input will always produce the same output.
2. **Fast computation**: The hash value can be quickly computed for any given data.
3. **Pre-image resistance**: It should be computationally infeasible to reverse the hash function (i.e., find the original input given its hash output).
4. **Small changes in input produce large changes in output**: Even a tiny change in the input should drastically change the hash output.
5. **Collision resistance**: It should be computationally infeasible to find two different inputs that produce the same hash output.

### Is this a hashing algorithm?

What if I try “hashing” a string by increasing each alphabet’s value by one. Do you think this follows all the rules we’ve written above?
![[hashing2.png]]

### SHA-256

Lets try out a famous hash function, SHA-256 here - [https://emn178.github.io/online-tools/sha256.html](https://emn178.github.io/online-tools/sha256.html)

#### Node.js code for generating SHA-256

```javascript
const crypto = require('crypto');

const input = "100xdevs";
const hash = crypto.createHash('sha256').update(input).digest('hex');

console.log(hash)
```

![[sha256.png]]


# Intro to Proof of Work
### Assignment #1

What if I ask you the following question — Give me an input string that outputs a SHA-256 hash that starts with `00000` . **How will you do it?**

**A: You will have to brute force until you find a value that starts with** `**00000**`
Node.js code


```javascript
const crypto = require("crypto");
let input = "100xDevs";
let hash = crypto.createHash("sha256").update(input).digest("hex");
let stopComputation = 0;

while (!String(hash).startsWith("00000")) {
	let randomValue = (Math.random() + 1).toString(36).substring(7);
	input = randomValue;
	hash = crypto.createHash("sha256").update(randomValue).digest("hex");
}
console.log(hash);
```

![[pic1.png]]

`This is what mostly miners do "kind of" mining that certain hash for the bitcoin, that's a rason they need heavy GPUs, because that GPU is running that heavy computation.`
`Solving this problem is called "Proof of Work"`
#### What miners do?
- Let's assume that you have found a string which gives '0000000' to you as starting hash values, now you have done "<font color="#4bacc6">proof of work</font>". but here bitcoin needs to constantly mine.
- Miners are constantly solving a problem, which is why the miners have to do this.
- Like every time they are mining, we can keep giving them "**prefixes**".
- They have to find a string but their input string should have "**prefix**" that was provided.
- So the miners are doing like they have given a "**prefix**", and this "**prefix**" keeps changing every time, they have to find what's called a **nonce**.

![[pic2.png]]