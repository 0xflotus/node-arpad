# Arpad: ELO Rating System for Node.js

![Build Status](https://travis-ci.org/PhobosRising/node-arpad.svg?branch=master)

This is an implementation of [ELO](http://en.wikipedia.org/wiki/Elo_rating_system) for Node.js (ELO is named after Arpad Elo, hence the package name).
This module is heavily tested and has many features used in real-world ELO situations.

## Installation

```
npm install arpad
```

## Simple Usage

This is a fairly simple example showing the most common usage for Arpad:

```js
var Elo = require('arpad');

var elo = new Elo();

var alice = 1600;
var bob = 1300;

var new_alice = elo.newRatingIfWon(alice, bob);
console.log("Alice's new rating if she won:", new_alice); // 1605

var new_bob = elo.newRatingIfWon(bob, alice);
console.log("Bob's new rating if he won:", new_bob); // 1327
```

## Complex Usage

This is a more complex example, making use of K-factor tables and score values:

```js
var Elo = require('arpad');

var uscf = {
  default: 32,
  2100: 24,
  2400: 16
};

var min_score = 100;
var max_score = 10000;

var elo = new Elo(uscf, min_score, max_score);

var alice = 2090;
var bob = 2700;

var odds_alice_wins = elo.expectedScore(alice, bob);
console.log("The odds of Alice winning are about:", odds_alice_wins); // ~2.9%
alice = elo.newRating(odds_alice_wins, 1.0, alice);
console.log("Alice's new rating after she won:", alice); // 2121

odds_alice_wins = elo.expectedScore(alice, bob);
console.log("The odds of Alice winning again are about:", odds_alice_wins); // ~3.4%
alice = elo.newRating(odds_alice_wins, 1.0, alice);
console.log("Alice's new rating if she won again:", alice); // 2144
```

## Running Tests

If you'd like to contribute be sure to run `npm install` to get the required packages and then make changes.
Afterwards simply run the tests.
If everything passes your should be Pull Request ready.

```
npm test
```

## License

MIT
