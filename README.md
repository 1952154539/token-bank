# TokenBank

A Solidity smart contract for depositing and withdrawing ERC20 tokens.

## Contract

**TokenBank** manages user token deposits with two core functions:

- **`deposit(uint256 amount)`** — Transfers ERC20 tokens from the caller to the contract and records the balance.
- **`withdraw(uint256 amount)`** — Transfers tokens back to the caller if they have sufficient balance, following the Checks-Effects-Interactions pattern.

### State

- `token` — The ERC20 token address set at deployment.
- `balances` — Mapping from user address to deposited amount.
- `totalDeposits` — Total tokens held by the contract.

### Events

- `Deposited(address indexed user, uint256 amount)`
- `Withdrawn(address indexed user, uint256 amount)`

## Usage

1. Deploy `TokenBank` with the ERC20 token address.
2. Call `token.approve(tokenBankAddress, amount)` on the ERC20 token.
3. Call `tokenBank.deposit(amount)` to deposit.
4. Call `tokenBank.withdraw(amount)` to withdraw.

## License

MIT
