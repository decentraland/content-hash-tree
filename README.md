# @dcl/content-hash-tree

[![NPM version](https://badge.fury.io/js/@dcl%2Fcontent-hash-tree.svg)](https://npmjs.org/package/@dcl/content-hash-tree)
[![Install Size](https://packagephobia.now.sh/badge?p=@dcl/content-hash-tree@latest)](https://packagephobia.now.sh/result?p=@dcl/content-hash-tree@latest)

## Forked from @uniswap/merkle-distributor

## Local Development

The following assumes the use of `node@>=10`.

### Install Dependencies

`npm ci`

#### Lib

### Generate a tree

```typescript
import { generateTree } from '@dcl/content-hash-tree'

const contentHashes = ['hash1', 'hash2', 'hash3']

const tree = generateTree(contentHashes)
```

### Verify whether a contnet hash is part of the tree or not

```typescript
import { verifyProof } from '@dcl/content-hash-tree'

const contentHashes = ['hash1', 'hash2', 'hash3']
const proof = tree.getProof(0, contentHashes[0])
const root = tree.getHexRoot()

const isPartOfTheTree = verifyProof(0, contentHashes[0], proof, root)
```

#### CLI (Benchmark)

### Generate a tree with ~10k content hashes

`npm run generate-merkle-root:data`

Time to completion 1.049s. Json size: 18mb

This will generate a `proofs.json` file in the root of the project.

### Verify a single proof of a tree with ~10k leafs

`npm run verify-merkle-root:proof`

Time to completion 9.294ms. Json size: 4kb
