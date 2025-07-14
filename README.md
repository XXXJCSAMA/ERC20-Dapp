# Sample Hardhat Project

This project demonstrates a basic Hardhat use case. It comes with a sample contract, a test for that contract, and a Hardhat Ignition module that deploys that contract.

Try running some of the following tasks:

```shell
npx hardhat help
npx hardhat test
REPORT_GAS=true npx hardhat test
npx hardhat node
npx hardhat ignition deploy ./ignition/modules/Lock.js
```<img width="1607" height="1030" alt="image" src="https://github.com/user-attachments/assets/f6687bc3-df33-42a7-a17c-19c86b1a1f21" />

代币合约 (ERC-20) 项目需求文档
项目概述
开发一个基于 Solidity 的 ERC-20 代币合约，并配合 Hardhat 进行测试和部署。该代币应具备基本的转账、余额查询、铸造（增发）和销毁（减少供应量）功能。

功能需求
对应 contracts/MyErc20Token.sol 文件

执行：npx hardhat compile
代币基本属性
合约部署的时候输入下边的内容进行初始化

名称 (Name): MyErc20Token
符号 (Symbol): MET
小数位数 (Decimals): 18 (先不考虑)
初始供应量 (Initial Supply): 1,000,000 MET
核心功能
_ownerMint：owner铸造

仅合约所有者可用
增发代币到指定地址。
_userrMint：user铸造

仅 被授权的user 可用
user可以铸造的数量为被授权的数量
_balanceOfUser：余额查询

查询任意地址的代币余额。
_balanceOfApprove：授权额度查询

查询任意地址的可以铸造代币的额度。
_transfer：转账

用户向其他地址转账代币
_burn：销毁

允许用户销毁自己持有的代币，减少总供应量。
_approveMint：授权

owner授权给某个地址允许他去自行mint
onlyOwner：宏定义——仅所有者可操作

balanceEnough：宏定义——某个地址的余额大余指定数量

项目部署
本地部署脚本（测试环境）
对应 deploy/deploy_MyErc20Token.js 文件

执行：npx hardhat deploy
测试脚本
对应 test/uint.test.js 文件

执行：npx hardhat test
测试内容

_ownerMint：仅 owner 可以调用
_ownerMint：mint总量达到
_ownerMint：正常mint（owner给自己mint）
_ownerMint：正常mint正常mint（owner给别人mint）
_approveMintBal：仅 owner 可以调用
_approveMintBal：正常 approve
_userrMint：没有给账户 secondAccount 授权任何余额
_userrMint：mint超过approve余额
_userrMint：正常 _userrMint
_transfer：sender balance is not enough
_transfer：transfer success
_burn：燃烧成功
线上部署脚本（生产环境）
对应 deploy/deploy_MyErc20Token.js 文件

执行：npx hardhat deploy --network sepolia
输出部署合约地址：0x6c9bd512183c8829e749f886556eaf100b66dc44
sepolia查看验证的代码： https://sepolia.etherscan.io/address/0x3CA742d5FE996133917C714D032CF1c04FE70a17#code
