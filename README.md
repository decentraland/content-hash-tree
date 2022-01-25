# @dcl/content-hash-tree

[![NPM version](https://badge.fury.io/js/@dcl%2Fcontent-hash-tree.svg)](https://npmjs.org/package/@dcl/content-hash-tree)
[![Install Size](https://packagephobia.now.sh/badge?p=@dcl/content-hash-tree@latest)](https://packagephobia.now.sh/result?p=@dcl/content-hash-tree@latest)

_Idea from @uniswap/merkle-distributor_

## Local Development

The following assumes the use of `node@>=10`.

### Install Dependencies

`npm ci`

#### Lib

### Generate a tree

```typescript
import { generateTree } from '@dcl/content-hash-tree'

const items = [
  { urn: 'urn:item:1', contentHash: 'hash1' },
  { urn: 'urn:item:2', contentHash: 'hash2' },
  { urn: 'urn:item:3', contentHash: 'hash3' }
]

const tree = generateTree(items)
```

### Verify whether a contnet hash is part of the tree or not

```typescript
import { verifyProof } from '@dcl/content-hash-tree'

const items = [
  { urn: 'urn:item:1', contentHash: 'hash1' },
  { urn: 'urn:item:2', contentHash: 'hash2' },
  { urn: 'urn:item:3', contentHash: 'hash3' }
]
const proof = tree.getProof(0, items[0].urn, items[0].contentHash)
const root = tree.getHexRoot()

const isPartOfTheTree = verifyProof(
  0,
  items[0].urn,
  items[0].contentHash,
  proof,
  root
)
```

#### CLI (Benchmark)

### Generate a tree

`npm run generate-merkle-root:data`

_~10k items: time to completion 1.049s. Json size: 18mb_
_~100k items: time to completion 10.049s. Json size: 155mb_

This will generate a `proofs.json` file in the root of the project.

### Verify a single proof of a tree with ~100k leafs

`npm run verify-merkle-root:proof`

Time to completion 9.294ms. Json size: 4kb
