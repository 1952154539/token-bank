# TokenBank

A Solidity smart contract for depositing and withdrawing ERC20 tokens, with a focus on security and compatibility.

## Contract

**TokenBank** manages user token deposits with two core functions:

- **`deposit(uint256 amount)`** — Transfers ERC20 tokens from the caller to the contract and records the balance.
- **`withdraw(uint256 amount)`** — Transfers a specific amount of tokens back to the caller.
- **`withdrawAll()`** — Transfers the caller's entire balance in one call.

### State

- `token` — The ERC20 token address set at deployment (immutable).
- `balances` — Mapping from user address to deposited amount.
- `totalDeposits` — Total tokens held by the contract.

### Events

- `Deposited(address indexed user, uint256 amount)`
- `Withdrawn(address indexed user, uint256 amount)`

## Security Features

- **Zero-address check** — Constructor reverts if `_token` is `address(0)`.
- **Non-standard ERC20 compatibility** — Uses low-level `call` for `transfer`/`transferFrom` to support tokens like USDT that do not return a bool.
- **Checks-Effects-Interactions** — Balances are updated before external calls to prevent reentrancy.
- **ETH rejection** — The `receive()` function reverts to prevent accidental ETH transfers.
- **Custom errors** — `TokenBank__ZeroAddress`, `TokenBank__ZeroAmount`, `TokenBank__InsufficientBalance`, `TokenBank__TransferFailed` — more gas-efficient than `require` with strings.

## Usage

1. Deploy `TokenBank` with the ERC20 token address.
2. Call `token.approve(tokenBankAddress, amount)` on the ERC20 token.
3. Call `tokenBank.deposit(amount)` to deposit.
4. Call `tokenBank.withdraw(amount)` or `tokenBank.withdrawAll()` to withdraw.

## License

MIT
