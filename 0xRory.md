---
timezone: Asia/Taipei
---

---

# 0xRory

1. 自我介绍

  hi~ 我是 0xRory 打好基礎功，學習再學習！

2. 你认为你会完成本次残酷学习吗？
  一定會的！

## Notes

<!-- Content_START -->

### 2024.09.23

學習內容: 
- A 系列的 Ethernaut CTF, 之前做了差不多了. POC: [ethernaut-foundry-solutions](https://github.com/SunWeb3Sec/ethernaut-foundry-solutions)
- A 系列的 QuillAudit CTF 題目的網站關掉了, 幫大家收集了[題目](./Writeup/SunSec/src/QuillCTF/), 不過還是有幾題沒找到. 有找到題目的人可以在發出來.
- A 系列的 DamnVulnerableDeFi 有持續更新, 題目也不錯. [Damn Vulnerable DeFi](https://github.com/theredguild/damn-vulnerable-defi/tree/v4.0.0).
- 使用 [Foundry](https://book.getfoundry.sh/) 在本地解題目, 可以參考下面 RoadClosed 為例子
- ``forge test --match-teat testRoadClosedExploit -vvvv``
#### [QuillAudit CTF - RoadClosed](./Writeup/SunSec/src/QuillCTF/RoadClosed.sol)
```
  function addToWhitelist(address addr) public {
    require(!isContract(addr), "Contracts are not allowed");
    whitelistedMinters[addr] = true;
  }

  function changeOwner(address addr) public {
    require(whitelistedMinters[addr], "You are not whitelisted");
    require(msg.sender == addr, "address must be msg.sender");
    require(addr != address(0), "Zero address");
    owner = addr;
  }

  function pwn(address addr) external payable {
    require(!isContract(msg.sender), "Contracts are not allowed");
    require(msg.sender == addr, "address must be msg.sender");
    require(msg.sender == owner, "Must be owner");
    hacked = true;
  }

  function pwn() external payable {
    require(msg.sender == pwner);
    hacked = true;
  }
```
- 解決這個題目需要成為合約的 owner 和 hacked = true.
- On-chain: 可以透過 ``cast send`` 或是 forge script 來解.
- Local: 透過 forge test 通常是在local解題, 方便 debug.
- RoadClosed 為例子我寫了2個解題方式. testRoadClosedExploit 和 testRoadClosedContractExploit (因為題目有檢查msg.sender是不是合約, 所以可以透過constructor來繞過 isContract)
- [POC](./Writeup/SunSec/test/QuillCTF/RoadClosed.t.sol) 

### 

<!-- Content_END -->
