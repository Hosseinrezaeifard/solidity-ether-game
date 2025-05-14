# solidity-ether-game
# 🧨 EtherGame Exploit Demo

This repository demonstrates a smart contract vulnerability scenario using `selfdestruct()` and shows how it can be used to **break a game** without violating any business logic — just by force-sending ETH.

---

## 📁 Files Included

- `EtherGame_Bad.sol` – vulnerable version of the game
- `EtherGame_Good.sol` – safe version with hardened logic
- `Attack.sol` – malicious contract used to exploit the vulnerability

---

## 🎮 EtherGame Rules

- Players must deposit **exactly 1 ETH**.
- The **7th depositor** becomes the `winner`.
- The winner can then `claimReward()` to receive all accumulated ETH.

---

## 💥 The Exploit

The `Attack` contract forcefully sends ETH to the `EtherGame` using `selfdestruct`, bypassing the `deposit()` function logic.

> This pushes the contract’s balance over 7 ETH, making it **impossible for anyone to win** — the game is stuck.

---

## 🛡️ The Fix

In `EtherGame_Good.sol`, we fix the logic by tracking a separate `uint depositedAmount` instead of relying on `address(this).balance`.  
This prevents external ETH transfers from interfering with game mechanics.

---

## 🧪 How to Use

1. Deploy `EtherGame_Bad.sol`
2. Send 1 ETH per deposit, up to 6 deposits.
3. Deploy `Attack.sol` and pass in the EtherGame address.
4. Call `attack()` with 5 ETH.
5. Notice the game is now broken — no one can win.

Try the same flow with `EtherGame_Good.sol` — it resists the exploit 💪

---

## 📚 Learnings

- 🔥 `selfdestruct()` can **force ETH** into a contract, ignoring logic
- ⚠️ Avoid using `address(this).balance` as a logic check
- 💡 Always separate **game state** from **ETH balance**

---

