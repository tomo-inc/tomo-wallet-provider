# tomo-wallet-provider

## Chain
```typescript
type TomoChain = {
  network: string
  backendUrls?: {
    rpcRrl?: string
    // only BTC
    mempoolUrl?: string
    inscriptionUrl?: string
  }
}
```
### inscriptionUrl
`GET ${inscriptionUrl}/openapi/bitcoin/inscriptions`

**request params**
```typescript
{
  address: string
  networkType: "MAINNET" | "SIGNET" | "TESTNET"
  cursor?: number
  size?: number
}
```
**response**
```typescript
{
  list: {
    output: string
    inscriptionId: string
    address: string
    offset: number
    outputValue: number
    location: string
    contentType: string
    contentLength: number
    inscriptionNumber: number
    timestamp: number
    genesisTransaction: string
  }[]
  total: number
}
```

## Release process

1. Update the `version` field in `package.json`.
2. Commit and push the change to the `main` branch.
3. Create and push a git tag:

```bash
git tag vX.Y.Z
git push origin vX.Y.Z
```

4. GitHub Actions will run the CI workflow and:
   - for tags like `vX.Y.Z`, publish `@tomo-inc/tomo-wallet-provider` as a stable release
   - for tags like `vX.Y.Z-beta.N`, publish it as a prerelease with the corresponding npm dist-tag.