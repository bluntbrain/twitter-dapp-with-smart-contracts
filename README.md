# Twitter DApp

[View the Smart Contract on Etherscan](https://sepolia.etherscan.io/address/0x26fd42F1566618616b16b72def09d0940174206c#readContract)

![Video](demo.mp4)

This is a decentralized application (DApp) built on the Ethereum blockchain that mimics basic functionalities of Twitter. Users can connect their wallets, post tweets, and like tweets. The smart contract handles the tweet creation and liking functionalities.

## Table of Contents

- [Concepts Used](#concepts-used)
- [Setup and Installation](#setup-and-installation)
- [Smart Contract Explanation](#smart-contract-explanation)
- [Frontend Overview](#frontend-overview)

## Concepts Used

### Web3.js

Web3.js is a JavaScript library that allows interaction with the Ethereum blockchain. It's used to connect the frontend of the DApp to the smart contract deployed on the Ethereum network.

### MetaMask

MetaMask is a browser extension that acts as a wallet for Ethereum. It allows users to connect to the DApp, manage their accounts, and interact with the smart contract.

### Solidity

Solidity is the programming language used for writing smart contracts on the Ethereum blockchain. It ensures the decentralized logic for the application's functionalities.

## Setup and Installation

1. Clone the repository.
2. Ensure you have MetaMask installed in your browser.
3. Run a local server to serve the HTML file or open `index.html` directly in your browser.
4. Deploy the smart contract on the Ethereum network and update the contract address in `index.js`.

## Smart Contract Explanation

The smart contract `twitter.sol` is the core of this DApp. Below is a detailed explanation of its components:

### Variables

- `uint16 public MAX_TWEET_LENGTH = 280;`: The maximum length allowed for a tweet.
- `mapping(address => Tweet[]) public tweets;`: A mapping from user addresses to their tweets.
- `address public owner;`: The owner of the contract.

### Structs

- `struct Tweet`: Represents a tweet with the following fields:
  - `uint256 id`: The ID of the tweet.
  - `address author`: The address of the tweet's author.
  - `string content`: The content of the tweet.
  - `uint256 timestamp`: The timestamp when the tweet was created.
  - `uint256 likes`: The number of likes the tweet has received.

### Events

- `event TweetCreated(uint256 id, address author, string content, uint256 timestamp);`: Emitted when a new tweet is created.
- `event TweetLiked(address liker, address tweerAuthor, uint256 tweetId, uint256 newLikeCount);`: Emitted when a tweet is liked.
- `event TweetUnLiked(address unliker, address tweerAuthor, uint256 tweetId, uint256 newLikeCount);`: Emitted when a tweet is unliked.

### Modifiers

- `modifier onlyOwner()`: Restricts certain functions to be called only by the contract owner.

### Functions

- `constructor()`: Sets the contract deployer as the owner.
- `createTweet(string memory _tweet) public`: Allows a user to create a tweet. It takes the tweet content as input, creates a new tweet object, and stores it in the `tweets` array. Emits `TweetCreated` event.
- `getTweet(uint _i) public view returns (Tweet memory)`: Returns a specific tweet by index for the caller.
- `getAllTweets(address _owner) public view returns (Tweet[] memory)`: Returns all tweets created by a specific user.
- `changeTweetLength(uint16 newTweetLength) public onlyOwner`: Allows the contract owner to change the maximum tweet length.
- `likeTweet(address author, uint256 id) external`: Allows a user to like a specific tweet. Emits `TweetLiked` event.
- `unLikeTweet(address author, uint256 id) external`: Allows a user to unlike a specific tweet. Emits `TweetUnLiked` event.

## Frontend Overview

### index.html

The HTML file contains the basic structure and elements required for the DApp. It includes a container for displaying tweets, a form for submitting new tweets, and buttons for wallet connection.

### index.js

This JavaScript file handles the interaction between the frontend and the smart contract.

#### Key Functions:

- `connectWallet()`: Connects the user's MetaMask wallet to the DApp.
- `createTweet(content)`: Calls the smart contract function to create a new tweet.
- `displayTweets(userAddress)`: Fetches and displays all tweets from a specific user.
- `likeTweet(author, id)`: Calls the smart contract function to like a tweet.
- `setConnected(address)`: Updates the UI to show the connected user's address and displays their tweets.

## Usage

1. Open the DApp in your browser.
2. Connect your MetaMask wallet by clicking on the "Connect Wallet" button.
3. Post tweets using the provided form.
4. Like tweets by clicking on the heart icon next to each tweet.
