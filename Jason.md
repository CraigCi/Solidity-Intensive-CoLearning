---
timezone: Asia/Shanghai

---

# Jason

1. 自我介绍 - Web3 lawyer

2. 你认为你会完成本次残酷学习吗？ 會
   
## Notes

<!-- Content_START -->
### 2024.09.23
1. 複習Solidity 101
2. 資源筆記：（a） Solidity中文文档（[官方文档的中文翻译](https://docs.soliditylang.org/zh/v0.8.19/index.html)）(b) [崔棉大师solidity教程](https://space.bilibili.com/286084162) (c) [Solidity 入門走到飛](https://www.youtube.com/watch?v=X135KO-8OTg)
3. structure
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.21;
contract HelloWeb3{
    string public _string = "Hello Web3!";
}
```
4. Variables
   (a) 值类型(Value Type)： These variables directly pass values when assigned

   ■ Boolean: A binary variable with values of true or false.

   ■ Integers: Signed (int) and unsigned (uint) integers, storing up to 256-bit integers.
   
         ■ Addresses: Holds a 20-byte Ethereum address, with address payable allowing ETH transfers.
         ■ Fixed-size byte arrays: byte, bytes8, bytes32, etc., with a fixed length declared at initialization.
         ■ Enumeration (enum): User-defined data types that assign names to uint values for readability
   
   (b) 引用类型(Reference Type)： These variables store the address of data and can be modified with different variable names:

         ■ Arrays: Used to store a set of data. Can be fixed-size (T[k]) or dynamically-sized (T[]).
         ■ Structs: User-defined data types that group together variables of different types.
         ■ Variable-length byte arrays: bytes, with a length that can be modified after declaration
   
   (c) 映射类型(Mapping Type): Solidity中存储键值对的数据结构，可以理解为哈希表

### 

### 2024.09.24
在以太坊區塊鏈中,合約和帳號是兩種不同類型的實體,它們有以下主要區別:
一、函數
1. 函數類型與形式
   - 形式：
   ```
   function <function name>(<parameter types>) {internal|external|public|private} [pure|view|payable] [returns (<return types>)]
   ```
   - 類型
      - (1) 可見性類型:
         public: 內部和外部都可以調用
         private: 只能在當前合約內部調用
         internal: 只能在當前合約及其子合約內部調用
         external: 只能從合約外部調用
      - (2) 狀態可變性: view: 不修改狀態,只讀取狀態; pure: 不讀取也不修改狀態; payable: 可以接收以太幣
      - (3) 特殊函數: constructor: 構造函數,部署合約時執行; fallback: 回退函數,在調用不存在的函數時執行; receive: 接收以太幣的函數
      - (4) 修飾器函數: 使用 modifier 關鍵字定義,用於修改其他函數的行為
      - (5) 虛擬函數和重寫函數: virtual: 可以被子合約重寫的函數; override: 重寫父合約的函數
   
3. 函數輸出
在 Solidity 中,函數的輸出主要通過返回值(return value)來實現。以下是關於函數輸出的一些重要概念:

#### 返回值聲明

1. 使用 `returns` 關鍵字在函數聲明中指定返回值類型:

```solidity
function myFunction() public returns (uint) {
  return 123;
}
```

2. 可以返回多個值:

```solidity
function multipleReturns() public returns (uint, bool, uint) {
  return (1, true, 2);
}
```

#### 返回方式

1. 使用 `return` 語句直接返回值:

```solidity
function returnValue() public returns (uint) {
  return 100;
}
```

2. 命名式返回:在 `returns` 中聲明變量名,函數體中給這些變量賦值,最後自動返回[1]:

```solidity
function namedReturn() public returns (uint _number, bool _bool) {
  _number = 2;
  _bool = true;
}
```

## 接收返回值

1. 可以使用解構賦值接收全部或部分返回值[1]:

```solidity
(uint x, bool b, ) = multipleReturns();
```

2. 單個返回值可直接賦值:

```solidity
uint result = returnValue();
```

## 注意事項

1. `view` 和 `pure` 函數可以有返回值,但不修改狀態[5]。

2. 返回值類型可以是基本類型,也可以是複雜類型如數組、結構體等[4]。

3. 如果函數聲明了返回值但沒有顯式返回,將返回該類型的默認值[3]。

4. 返回值可以用於函數內部計算,也可以供外部調用者使用[6]。

總之,合理使用函數返回值可以使合約邏輯更清晰,提高代碼的可讀性和可維護性。在設計函數時,應根據實際需求選擇合適的返回方式。
References:
[1] https://blog.csdn.net/wo541075754/article/details/104354721
[2] https://www.cnblogs.com/zhanchenjin/p/18218201
[3] https://hackmd.io/%40rogerwutw/BJ3CoxkTK
[4] https://mirror.xyz/wtfacademy.eth/FIGf9tF7wiBlLnQGXfEjVkJ0efzKBNltJS1fRxPKYTk
[5] https://u.naturaldao.io/solidity/1.6-solidity-yu-yan-jiao-cheng/structure
[6] https://metana.io/blog/solidity-functions-types-and-use-cases/
   
二、自問自答：
## 帳號(Account)
1. 外部擁有帳戶(EOA):
   - 由私鑰控制
   - 可以發起交易
   - 沒有相關程式碼
   - 有以太幣餘額
2. 合約帳戶:
   - 由智能合約程式碼控制
   - 不能主動發起交易,只能被觸發執行
   - 包含智能合約程式碼
   - 有以太幣餘額

## 智能合約(Smart Contract)
- 是一種特殊的合約帳戶
- 包含可執行的程式碼
- 在區塊鏈上自動執行預定義的操作
- 可以持有資產和狀態
- 由交易或其他合約調用來執行

## 主要差異
1. 控制方式:帳號由私鑰控制,合約由程式碼控制
2. 功能:帳號用於持有資產,合約用於執行邏輯
3. 交易發起:帳號可主動發起交易,合約只能被動執行
4. 程式碼:帳號沒有程式碼,合約包含可執行程式碼
5. 創建方式:帳號可直接創建,合約需要通過交易部署
6. 靈活性:帳號操作簡單,合約可實現複雜邏輯
總之,帳號主要用於管理資產,而智能合約則用於在區塊鏈上執行自動化的業務邏輯。兩者在以太坊生態系統中扮演不同但互補的角色。


### 2024.09.26
1. 引用：引用类型(Reference Type)：包括数组（array）和结构体（struct），由于这类变量比较复杂，占用存储空间大，我们在使用时必须要声明数据存储的位置。

2. 数据位置: Solidity数据存储位置有三类：storage，memory和calldata。不同存储位置的gas成本不同。storage类型的数据存在链上，类似计算机的硬盘，消耗gas多；memory和calldata类型的临时存在内存里，消耗gas少。大致用法：

(1) storage：合约里的状态变量默认都是storage，存储在链上。
(2) memory：函数里的参数和临时变量一般用memory，存储在内存中，不上链。尤其是如果返回数据类型是变长的情况下，必须加memory修饰，例如：string, bytes, array和自定义结构。
(3) calldata：和memory类似，存储在内存中，不上链。与memory的不同点在于calldata变量不能修改（immutable），一般用于函数的参数

3. 变量的作用域: 作用域划分有三种: 状态变量（state variable）、局部变量（local variable）和全局变量(global variable)

4. 以太单位:
   wei: 1
   gwei: 1e9 = 1000000000
   ether: 1e18 = 1000000000000000000
   
6. 时间单位
   seconds: 1
   minutes: 60 seconds = 60
   hours: 60 minutes = 3600
   days: 24 hours = 86400
   weeks: 7 days = 604800

7. 数组（Array）是Solidity常用的一种变量类型，用来存储一组数据（整数，字节，地址等等）。数组分为固定长度数组和可变长度数组两种：
   注意：bytes比较特殊，是数组，但是不用加[]。另外，不能用byte[]声明单字节数组，可以使用bytes或bytes1[]。bytes 比 bytes1[] 省gas。

8. 创建数组的规则:
   (1) 对于memory修饰的动态数组，可以用new操作符来创建，但是必须声明长度，并且声明后长度不能改变。

   (2) 数组字面常数(Array Literals)是写作表达式形式的数组，用方括号包着来初始化array的一种方式，并且里面每一个元素的type是以第一个元素为准的，例如[1,2,3]里面所有的元素都是uint8类型，因为在Solidity中，如果一个值没有指定type的话，会根据上下文推断出元素的类型，默认就是最小单位的type，这里默认最小单位类型是uint8。而[uint(1),2,3]里面的元素都是uint类型，因为第一个元素指定了是uint类型了，里面每一个元素的type都以第一个元素为准。

   (3) 数组成员
length: 数组有一个包含元素数量的length成员，memory数组的长度在创建后是固定的。
push(): 动态数组拥有push()成员，可以在数组最后添加一个0元素，并返回该元素的引用。
push(x): 动态数组拥有push(x)成员，可以在数组最后添加一个x元素。
pop(): 动态数组拥有pop()成员，可以移除数组最后一个元素。

   (4) 结构体 struct
Solidity支持通过构造结构体的形式定义新的类型。结构体中的元素可以是原始类型，也可以是引用类型；结构体可以作为数组或映射的元素。

### 2024.09.27
1. 映射
(1）語法: mapping(KeyType => ValueType) mappingName;
(2) 特點:所有可能的鍵都存在,未賦值的鍵對應的值為該類型的默認值
(3) 無法獲取映射的大小或遍歷所有鍵
(4) 只能用作狀態變量
(5) 規則1: 映射的_KeyType只能选择Solidity内置的值类型，比如uint，address等，不能用自定义的结构体。而_ValueType可以使用自定义的类型。
(6) 规则2：映射的存储位置必须是storage，因此可以用于合约的状态变量，函数中的storage变量和library函数的参数（见例子）。不能用于public函数的参数或返回结果中，因为mapping记录的是一种关系 (key - value pair)。
(7) 规则3：如果映射声明为public，那么Solidity会自动给你创建一个getter函数，可以通过Key来查询对应的Value。
(8) 规则4：给映射新增的键值对的语法为_Var[_Key] = _Value，其中_Var是映射变量名，_Key和_Value对应新增的键值对。

4. 變量初始值
   ■ Value Types:
      ● boolean: false
      ● string: "" (an empty string)
      ● int: 0
      ● uint: 0
      ● enum: The first element listed in the enum definition
      ● address: 0x0000000000000000000000000000000000000000 (or address(0))
   ■ Reference Types:
      ● mapping: All members are set to their respective default values.
      ● struct: All members are set to their respective default values.
      ● array (dynamic): [] (an empty array)
      ● array (static/fixed-length): All members are set to their respective default values.

### 2024.09.28
// 昨天的提交被覆蓋了
常量(constant)和不變量(immutable)的概念及其在Solidity中的使用:

## 常量 (constant)
常量是在合約中不可更改的值,必須在聲明時就給予初始值。

### 特點:
1. **立即初始化**: 必須在變量聲明的同時賦予初值。
2. **不可修改**: 一旦初始化後,在合約的整個生命週期內都不能被改變。
3. **適用範圍廣**: 可用於數值類型(如uint、int)、字符串(string)和字節(bytes)。

### 示例:

```solidity
uint256 constant MAX_UINT = 2**256 - 1;
string constant GREETING = "Hello, World!";
bytes32 constant HASH = keccak256("example");
```

### 使用場景:

- 定義數學常數(如π)
- 設置系統限制(如最大用戶數)
- 存儲不變的配置信息(如合約名稱)

## 不變量 (immutable)
不變量提供了比常量更大的靈活性,允許在構造函數中進行初始化。

### 特點:

1. **靈活初始化**: 可以在聲明時或在構造函數中初始化。
2. **運行時不可變**: 一旦構造函數執行完畢,值就不能再被改變。
3. **僅適用於值類型**: 主要用於數值、地址等值類型,不能用於引用類型如數組或映射。

### 示例:

```solidity
contract Example {
    uint256 public immutable CREATION_TIMESTAMP;
    address public immutable OWNER;

    constructor() {
        CREATION_TIMESTAMP = block.timestamp;
        OWNER = msg.sender;
    }
}
```

### 使用場景:
- 存儲部署時的狀態(如部署時間戳)
- 記錄初始設置(如合約擁有者地址)
- 需要在部署時動態設置的不變值

## 對比與選擇

1. **初始化時機**: constant必須在編譯時知道值,immutable可以在運行時(構造函數中)設置。
2. **靈活性**: immutable允許使用構造函數參數或其他運行時信息進行初始化。
3. **gas成本**: 兩者都比普通狀態變量更節省gas,因為它們直接嵌入到合約字節碼中。
4. **安全性**: 兩者都提高了合約的安全性,防止關鍵值被意外或惡意修改。

選擇使用constant還是immutable主要取決於您是否需要在部署時動態設置值。如果值在編譯時就已知,使用constant;如果需要在部署時根據參數或環境設置,則使用immutable。

### 2024.09.29
這個章節主要介紹了Solidity中的控制流和一個實際的應用案例——插入排序算法的實現，重點如下：

## Solidity控制流概述
Solidity提供了與其他程式語言類似的控制流結構，包括：
1. if-else條件語句
2. for循環
3. while循環
4. do-while循環
5. 三元運算符

當然,我會為您詳細解釋這些Solidity中的控制流結構:

1. if-else條件語句

if-else語句用於根據條件執行不同的代碼塊。它的基本結構如下:

```solidity
if (條件) {
    // 如果條件為真,執行這裡的代碼
} else {
    // 如果條件為假,執行這裡的代碼
}
```

還可以使用else if來檢查多個條件:

```solidity
if (條件1) {
    // 代碼塊1
} else if (條件2) {
    // 代碼塊2
} else {
    // 如果以上條件都不滿足,執行這裡的代碼
}
```

2. for循環

for循環用於重複執行一段代碼特定次數。基本語法為:

```solidity
for (初始化; 條件; 更新) {
    // 循環體
}
```

例如:
```solidity
for (uint i = 0; i < 10; i++) {
    // 這段代碼會執行10次
}
```

3. while循環

while循環在條件為真時重複執行代碼塊:

```solidity
while (條件) {
    // 循環體
}
```

4. do-while循環

do-while循環類似於while循環,但保證至少執行一次循環體:

```solidity
do {
    // 循環體
} while (條件);
```

5. 三元運算符

三元運算符是一種簡潔的條件表達式,格式為:

```solidity
條件 ? 表達式1 : 表達式2
```

如果條件為真,返回表達式1的結果;否則返回表達式2的結果。例如:

```solidity
uint result = x > y ? x : y; // 返回x和y中的較大值
```

這些控制結構在Solidity中的使用需要特別注意:

- 在循環中要避免無限循環,因為這可能導致合約執行超出gas限制。
- 使用uint類型時,要注意避免下溢(如在0上減1)。
- 在編寫複雜邏輯時,要確保所有可能的路徑都被考慮到,以避免意外行為。
- 三元運算符雖然簡潔,但在複雜情況下可能降低代碼可讀性,應謹慎使用。


這些控制結構允許開發者實現複雜的邏輯和算法。

## 插入排序案例研究

章節後半部分通過實現插入排序算法來展示Solidity的應用和潛在陷阱：

1. **算法簡介**：插入排序是一種簡單但效率不高的排序算法，適合小規模數據。

2. **從Python到Solidity的轉換**：展示了如何將Python版本的插入排序轉換為Solidity。

3. **錯誤版本分析**：直接轉換的版本存在bug，主要是由於Solidity中uint類型不能取負值造成的。

4. **正確實現**：通過調整索引邏輯，避免了負值問題，成功實現了插入排序。

## 核心洞察

1. **Solidity的特殊性**：雖然Solidity的語法與其他語言相似，但它有其獨特的特性和限制，如uint類型不能為負。

2. **細節的重要性**：在區塊鏈環境中，即使是小的編程錯誤也可能導致嚴重的後果，如大額資金損失。

3. **持續學習和練習的必要性**：掌握Solidity需要深入理解其特性，並通過不斷練習來避免常見陷阱。

4. **安全意識**：強調了在開發智能合約時必須格外謹慎，因為錯誤可能造成巨大的經濟損失。

總的來說，這個章節不僅介紹了基本的編程概念，還通過一個實際的例子展示了Solidity編程的複雜性和重要性，強調了在區塊鏈開發中對細節的關注和安全意識的重要性。

### 2024.09.30
# 一、構造函數

## Solidity中的構造函數和修飾器

本章節介紹了Solidity中兩個重要的概念：構造函數（constructor）和修飾器（modifier），並以權限控制（Ownable）為例說明其應用。

### 構造函數（Constructor）

構造函數是一種特殊的函數，在合約部署時自動執行一次，用於初始化合約狀態。

**關鍵點：**
- 每個合約只能有一個構造函數
- 用於設置初始狀態，如合約擁有者地址
- Solidity 0.4.22版本後使用`constructor`關鍵字

**示例：**
```solidity
constructor(address initialOwner) {
    owner = initialOwner;
}
```

### 修飾器（Modifier）

修飾器是Solidity特有的語法，用於在函數執行前進行條件檢查，增強代碼的可重用性和安全性。

**關鍵點：**
- 類似於其他語言中的裝飾器（decorator）
- 主要用於函數執行前的條件檢查
- 使用`_`符號表示被修飾函數的執行點

**示例：**
```solidity
modifier onlyOwner {
   require(msg.sender == owner);
   _;
}
```

### Ownable合約示例

通過結合構造函數和修飾器，可以實現簡單的合約權限控制：

```solidity
contract Ownable {
    address public owner;

    constructor(address initialOwner) {
        owner = initialOwner;
    }

    modifier onlyOwner {
        require(msg.sender == owner);
        _;
    }

    function changeOwner(address newOwner) external onlyOwner {
        owner = newOwner;
    }
}
```

### 補充說明

1. **構造函數的演變**：Solidity早期版本使用與合約同名的函數作為構造函數，新版本改為使用`constructor`關鍵字，提高了安全性和可讀性。

2. **修飾器的靈活性**：修飾器可以接受參數，允許更靈活的條件檢查。

3. **OpenZeppelin標準**：提到了OpenZeppelin的Ownable實現，這是業界廣泛採用的標準實現，值得進一步學習。

4. **安全考慮**：使用修飾器進行權限控制是智能合約安全的基礎，但需要謹慎設計和實現。

5. **gas消耗**：雖然修飾器提高了代碼的可讀性和可維護性，但過度使用可能增加gas消耗。

總的來說，構造函數和修飾器是Solidity中實現合約初始化和訪問控制的關鍵工具，掌握這些概念對於編寫安全、高效的智能合約至關重要。

# 二、事件
這個章節主要介紹了Solidity中的事件（Event）概念及其應用。以下是摘要、改寫和補充：

## Solidity事件概述

事件是Solidity中用於記錄合約狀態變化的機制，它在以太坊虛擬機（EVM）上以日誌的形式存儲。

### 關鍵特點

1. **響應性**：允許應用程序通過RPC接口訂閱和監聽。

您提到的是關於Solidity事件的響應性特點的補充說明。我可以為您進一步解釋和擴展這個概念：

## 事件的響應性

事件的響應性是指應用程序能夠實時地監聽和反應智能合約中發生的特定事件。這個特性對於構建互動性強的去中心化應用（DApps）至關重要。

### 具體實現方式

1. **RPC (Remote Procedure Call) 接口**
   - 應用程序通過RPC接口與以太坊節點通信。
   - 常見的RPC提供者包括Infura、Alchemy等。

2. **訂閱機制**
   - 使用WebSocket連接來實現實時訂閱。
   - 應用可以訂閱特定合約地址或特定事件類型。

3. **事件監聽**
   - 使用諸如Web3.js或ethers.js等庫來簡化事件監聽過程。

### 應用場景

1. **實時更新UI**
   - 例如，在代幣轉賬後立即更新用戶餘額。

2. **交易確認通知**
   - 當交易被確認時，立即通知用戶。

3. **複雜業務邏輯觸發**
   - 某些事件可能觸發應用程序中的其他操作。

4. **數據分析和監控**
   - 實時追蹤合約活動，用於分析或監控目的。

### 代碼示例（使用ethers.js）

```javascript
const ethers = require('ethers');

// 連接到以太坊網絡
const provider = new ethers.providers.WebSocketProvider('wss://mainnet.infura.io/ws/v3/YOUR-PROJECT-ID');

// 合約地址和ABI
const contractAddress = '0x...';
const contractABI = [...];

// 創建合約實例
const contract = new ethers.Contract(contractAddress, contractABI, provider);

// 監聽Transfer事件
contract.on('Transfer', (from, to, amount, event) => {
    console.log(`Transfer from ${from} to ${to} of ${amount} tokens`);
    // 在這裡更新UI或觸發其他操作
});
```

### 注意事項
1. **網絡穩定性**：使用WebSocket連接時需考慮網絡穩定性問題。
2. **錯誤處理**：應妥善處理連接中斷等異常情況。
3. **擴展性考慮**：在大規模應用中，可能需要考慮負載均衡和事件過濾。
通過有效利用事件的響應性，開發者可以創建更加動態和互動的區塊鏈應用，提升用戶體驗並實現更複雜的業務邏輯。
   
3. **經濟性**：比鏈上存儲更節省gas。

### 事件結構

- **聲明**：使用`event`關鍵字。
- **主題（Topics）**：包含事件簽名和最多3個帶`indexed`標記的參數。
- **數據（Data）**：存儲不帶`indexed`的參數。

### 使用示例

```solidity
event Transfer(address indexed from, address indexed to, uint256 value);

function _transfer(address from, address to, uint256 amount) external {
    // 轉賬邏輯
    emit Transfer(from, to, amount);
}
```

### 事件查詢

可以通過Etherscan等區塊鏈瀏覽器查看事件詳情。

## 補充和延伸思考

1. **索引參數的選擇**
   - 問題：如何決定哪些參數應該被標記為`indexed`？
   - 思考：考慮查詢需求和gas成本的平衡。

2. **事件vs狀態變量**
   - 問題：在哪些情況下應該使用事件而不是狀態變量？
   - 思考：考慮數據的用途、存儲成本和訪問頻率。

3. **事件在DApp開發中的角色**
   - 問題：如何有效利用事件來改善DApp的用戶體驗？
   - 思考：考慮實時通知、歷史記錄查詢等應用場景。

4. **事件的安全性考慮**
   - 問題：事件可能帶來哪些安全風險？如何緩解？
   - 思考：考慮隱私問題、前端依賴事件的潛在風險。

5. **跨鏈應用中的事件處理**
   - 問題：在跨鏈應用中，如何處理和同步來自不同鏈的事件？
   - 思考：考慮事件的標準化、跨鏈橋接等技術。

6. **事件在鏈上分析中的應用**
   - 問題：如何利用事件數據進行有效的鏈上分析？
   - 思考：考慮數據聚合、模式識別等高級應用。

通過深入理解和靈活運用事件，開發者可以構建更具互動性和可追溯性的智能合約，同時為鏈上分析提供寶貴的數據來源。

# 三、繼承

這個章節主要介紹了Solidity中的繼承概念及其各種應用。以下是摘要、改寫和補充：

## Solidity繼承概述

繼承是Solidity中重要的面向對象特性，允許合約重用代碼並建立層次結構。

### 主要概念

1. **簡單繼承**：使用`is`關鍵字實現單一繼承。
2. **多重繼承**：Solidity支持多重繼承，需要注意繼承順序。
3. **虛擬函數和重寫**：使用`virtual`和`override`關鍵字。
4. **修飾器繼承**：修飾器也可以被繼承和重寫。
5. **構造函數繼承**：有兩種方式繼承父合約的構造函數。
6. **調用父合約函數**：可以直接調用或使用`super`關鍵字。
7. **鑽石繼承**：處理多重繼承中的複雜情況。

### 關鍵點

- 繼承順序很重要，特別是在多重繼承中。
- 重寫函數時需要使用正確的關鍵字。
- `super`關鍵字在多重繼承中的行為需要特別注意。

## 補充和延伸思考

1. **繼承vs組合**
   - 問題：在什麼情況下應該選擇繼承而不是組合？
   - 思考：考慮代碼重用、靈活性和合約間關係的緊密程度。

2. **繼承對gas消耗的影響**
   - 問題：繼承如何影響合約的gas消耗？
   - 思考：考慮合約大小、函數調用成本等因素。

3. **安全性考慮**
   - 問題：繼承可能帶來哪些安全風險？如何緩解？
   - 思考：考慮函數可見性、狀態變量訪問等問題。

4. **接口vs抽象合約vs繼承**
   - 問題：在設計合約時，如何選擇使用接口、抽象合約或繼承？
   - 思考：考慮設計的靈活性、代碼重用和標準化需求。

5. **版本兼容性**
   - 問題：在升級合約時，如何處理繼承關係中的版本兼容性問題？
   - 思考：考慮向後兼容性、升級策略等。

6. **測試策略**
   - 問題：如何有效地測試包含複雜繼承關係的合約？
   - 思考：考慮單元測試、集成測試的策略。

7. **設計模式的應用**
   - 問題：如何將常見的面向對象設計模式應用到Solidity的繼承中？
   - 思考：考慮工廠模式、策略模式等在智能合約中的應用。

通過深入理解和靈活運用繼承，開發者可以創建更模塊化、可維護和可擴展的智能合約。同時，合理使用繼承可以提高代碼的重用性和可讀性，但也需要注意潛在的複雜性和安全風險。


### 2024.10.01
## 一、抽象合约和接口

## 抽象合約與接口:ERC721標準的骨架

本章節將深入探討Solidity中的抽象合約(abstract)和接口(interface)概念,以ERC721標準為例,幫助讀者更好地理解這些重要的合約結構。

### 抽象合約:未完成的藍圖

抽象合約是一種特殊的合約,它至少包含一個未實現的函數。這種合約為其他合約提供了一個基礎框架,允許開發者在後續實現中填充細節。

**關鍵特點:**
- 至少有一個未實現的函數(沒有函數體)
- 必須使用`abstract`關鍵字聲明
- 未實現的函數需要加`virtual`關鍵字

**思考問題:** 
1. 抽象合約在大型項目開發中有什麼優勢?
2. 如何決定某個函數應該在抽象合約中保留為未實現狀態?

### 接口:合約的純粹骨架

接口更進一步,它只定義了合約應該具有的功能,而不提供任何實現。接口是智能合約間互操作性的關鍵。

**接口的規則:**
- 不能包含狀態變量
- 不能包含構造函數
- 不能繼承除接口外的其他合約
- 所有函數必須是`external`且沒有函數體
- 實現接口的非抽象合約必須實現所有定義的功能

**接口的重要性:**
1. 定義合約功能和觸發方式
2. 提供函數選擇器和簽名信息
3. 提供接口ID(EIP165)

**思考問題:**
1. 為什麼接口對於區塊鏈生態系統的互操作性如此重要?
2. 接口與ABI(Application Binary Interface)之間有什麼關係?

### ERC721接口深度解析

以ERC721接口為例,我們可以看到它定義了NFT標準的核心功能。

**主要組成:**
- 3個事件(Transfer, Approval, ApprovalForAll)
- 9個函數(包括餘額查詢、所有權轉移、授權等)

**代碼示例:**
```solidity
interface IERC721 {
    function balanceOf(address owner) external view returns (uint256 balance);
    function ownerOf(uint256 tokenId) external view returns (address owner);
    // ... 其他函數
}
```

**思考問題:**
1. ERC721標準為什麼選擇這些特定的函數和事件?
2. 如何擴展ERC721接口以添加新功能,同時保持向後兼容性?

### 實際應用:與知名NFT項目交互

通過接口,我們可以輕鬆與實現了該接口的任何合約進行交互,而無需了解其內部實現細節。

**示例:與BAYC交互**
```solidity
contract InteractWithBAYC {
    IERC721 BAYC = IERC721(0xBC4CA0EdA7647A8aB7C2061c2E118A18a936f13D);
    
    function checkBalance(address owner) external view returns (uint256) {
        return BAYC.balanceOf(owner);
    }
}
```

**延伸思考:**
1. 如何設計一個通用的NFT交互合約,使其能與任何ERC721代幣進行交互?
2. 在處理不同標準(如ERC721, ERC1155)的NFT時,接口如何幫助簡化開發過程?

### 總結與展望
抽象合約和接口是Solidity中強大的工具,它們不僅提供了代碼重用和標準化的方法,還為智能合約的互操作性奠定了基礎。隨著區塊鏈技術的發展,理解和靈活運用這些概念將變得越來越重要。

**未來展望:**
- 探索更複雜的接口設計模式
- 研究如何在不同區塊鏈間實現標準化的接口

通過深入理解抽象合約和接口,開發者可以創建更加模塊化、可擴展和互操作的智能合約系統。


## 二、 異常

## Solidity中的異常處理:Error、Require和Assert

本章節深入探討Solidity中三種主要的異常處理機制:Error、Require和Assert。我們將分析它們的使用場景、語法特點以及gas消耗情況,幫助開發者做出最優的選擇。

### Error:高效且信息豐富的異常處理

Error是Solidity 0.8.4版本引入的新特性,旨在提供更高效和信息豐富的異常處理方式。

**特點:**
- 可自定義錯誤類型
- 支持攜帶參數
- 必須與revert配合使用
- gas消耗最低

**代碼示例:**
```solidity
error TransferNotOwner(address sender);

function transferOwner1(uint256 tokenId, address newOwner) public {
    if(_owners[tokenId] != msg.sender){
        revert TransferNotOwner(msg.sender);
    }
    _owners[tokenId] = newOwner;
}
```

**思考問題:**
1. 在什麼情況下使用帶參數的Error更有優勢?
2. Error如何影響合約的可讀性和可維護性?

### Require:傳統且直觀的條件檢查

Require是Solidity早期版本就存在的異常處理方法,因其直觀性仍被廣泛使用。

**特點:**
- 語法簡單:require(條件, "錯誤信息")
- 可提供錯誤描述字符串
- gas消耗隨錯誤信息長度增加

**代碼示例:**
```solidity
function transferOwner2(uint256 tokenId, address newOwner) public {
    require(_owners[tokenId] == msg.sender, "Transfer Not Owner");
    _owners[tokenId] = newOwner;
}
```

**思考問題:**
1. 在大型項目中,如何平衡require的使用頻率和gas成本?
2. 相比Error,require在哪些場景下可能更適合使用?

### Assert:開發階段的嚴格檢查

Assert主要用於開發階段的調試和嚴格的不變量檢查。
**特點:**
- 語法最簡單:assert(條件)
- 不提供錯誤信息
- 用於檢查不應該發生的情況

**代碼示例:**
```solidity
function transferOwner3(uint256 tokenId, address newOwner) public {
    assert(_owners[tokenId] == msg.sender);
    _owners[tokenId] = newOwner;
}
```

**思考問題:**
1. 在生產環境中,應該如何使用assert以確保合約安全?
2. assert和require在合約邏輯驗證中的角色有何不同?

### Gas消耗比較與最佳實踐
通過實際測試,我們發現三種方法的gas消耗存在明顯差異:
1. Error: 24457 gas (帶參數時24660 gas)
2. Require: 24755 gas
3. Assert: 24473 gas

**延伸思考:**
1. 如何在複雜的智能合約中優化異常處理以降低整體gas成本?
2. 不同的異常處理方法如何影響合約的安全性和可審計性?

### 總結與未來展望

Solidity的異常處理機制為開發者提供了多樣化的選擇。Error作為新引入的特性,在效率和信息豐富度上都有優勢。然而,require和assert在特定場景下仍有其獨特價值。

**未來發展方向:**
- 探索更智能的異常處理機制,如自動化的錯誤診斷和修復建議
- 研究如何在合約升級過程中優雅地處理異常情況
- 開發工具以幫助分析和優化合約中的異常處理邏輯

通過深入理解和靈活運用這些異常處理機制,開發者可以創建更加健壯、高效且用戶友好的智能合約。

### 2024.10.02

## WTF 102: 函數重載在Solidity中的應用

函數重載是Solidity中一個強大而靈活的特性，允許開發者使用相同的函數名但不同的參數列表來定義多個函數。這種機制大大增加了代碼的可讀性和可維護性。

### 基本概念

函數重載允許在同一作用域內定義多個具有相同名稱但參數列表不同的函數。Solidity編譯器會根據調用時提供的參數類型和數量來決定調用哪個函數。

```solidity
function saySomething() public pure returns(string memory) {
    return "Nothing";
}

function saySomething(string memory something) public pure returns(string memory) {
    return something;
}
```

在這個例子中，`saySomething()`函數被重載了。第一個版本不接受任何參數，而第二個版本接受一個字符串參數。

### 函數選擇器

重載函數在編譯過程中會生成不同的函數選擇器。函數選擇器是函數簽名的Keccak-256哈希的前4個字節，用於在合約調用時識別特定函數。

### 實參匹配

當調用重載函數時，Solidity會嘗試將提供的參數與可用的函數簽名進行匹配。如果存在多個可能的匹配，編譯器將報錯。

```solidity
function f(uint8 _in) public pure returns (uint8 out) {
    out = _in;
}

function f(uint256 _in) public pure returns (uint256 out) {
    out = _in;
}
```

在這個例子中，調用`f(50)`會導致編譯錯誤，因為50可以被解釋為`uint8`或`uint256`。

### 重載的優勢

1. **代碼可讀性**：允許使用直觀的函數名，而不是為類似的操作創建多個不同名稱的函數。
2. **靈活性**：可以根據不同的輸入參數處理不同的邏輯。
3. **向後兼容性**：可以在不破壞現有代碼的情況下添加新的函數版本。

### 注意事項

- 修飾器（modifier）不能被重載。
- 返回類型不同但參數相同的函數不能被視為重載。
- 在使用重載時要小心避免歧義，確保每個重載函數的用途清晰明確。

### 最佳實踐

- 謹慎使用重載，確保每個重載函數都有明確的用途。
- 在文檔中清楚說明每個重載函數的預期行為。
- 避免過度重載，這可能會導致代碼難以理解和維護。

函數重載是Solidity中一個強大的特性，能夠大大提高代碼的表達能力和靈活性。然而，它也需要謹慎使用，以確保代碼的清晰度和可維護性。通過合理運用函數重載，開發者可以編寫出更加優雅和高效的智能合約.

### 2024.10.03

## 庫合約(Library)簡介
庫合約是 Solidity 中一種特殊的合約,主要用於提高代碼重用性和降低 gas 消耗。它本質上是一系列函數的集合,由經驗豐富的開發者創建,我們可以直接使用這些現成的功能。

庫合約與普通合約的主要區別:

1. 不能有狀態變量
2. 不能繼承或被繼承  
3. 不能接收以太幣
4. 不能被銷毀

使用庫合約的好處是"站在巨人的肩膀上",我們可以利用前人的智慧,無需重複造輪子。
我們只需要知道什麼情況該用什麼庫合約。常用的有：
Strings：將uint256轉換為String
Address：判斷某個地址是否為合約地址
Create2：更安全的使用Create2 EVM opcode
Arrays：跟數組相關的庫合約

## Strings 庫合約示例

Strings 庫提供了將 uint256 轉換為 string 的功能。主要包含兩個函數:

1. `toString()`: 將 uint256 轉為十進制 string
2. `toHexString()`: 將 uint256 轉為十六進制 string

## 如何使用庫合約

有兩種主要方法使用庫合約:

1. 使用 `using for` 指令:

```solidity
using Strings for uint256;

function getString1(uint256 _number) public pure returns(string memory){
    return _number.toHexString();
}
```

2. 直接通過庫合約名稱調用:

```solidity
function getString2(uint256 _number) public pure returns(string memory){
    return Strings.toHexString(_number);
}
```

## 補充思考
1. **性能考量**: 庫合約可以提高代碼重用性,但過度使用可能導致合約變得複雜。在決定是否使用庫時,要權衡代碼簡潔性和 gas 消耗。

2. **安全性**: 使用知名的、經過審計的庫可以提高合約的安全性。但同時也要注意,依賴外部庫可能引入潛在的風險。

3. **版本控制**: 在使用庫時,要注意版本兼容性。Solidity 的更新可能會影響庫的行為。

4. **自定義庫**: 雖然大多數情況下使用現有庫就足夠了,但了解如何創建自己的庫也是很有價值的技能。

5. **gas 優化**: 庫合約中的 internal 函數會被內聯到調用合約中,這可以節省 gas。而 public 和 external 函數則會觸發 delegatecall,可能增加 gas 消耗。

6. **跨合約調用**: 庫合約提供了一種在不同合約間共享代碼的方式,這對於構建模塊化和可維護的 DApp 非常有用。

總的來說,庫合約是 Solidity 中一個強大的工具,能夠幫助開發者編寫更高效、更安全的智能合約。初學者應該熟悉常用的庫合約,並學會如何在自己的項目中合理使用它們。

# 題目與解析
## Q1
通過庫合約名稱直接調用 toHexString() 函數的正確寫法是：

```solidity
// 直接通过库合约名调用    
function getString2(uint256 _number) public pure returns(string memory){
    return Strings.toHexString(_number);
}
```

這裡的解釋是：

1. `Strings` 是庫合約的名稱。

2. `toHexString` 是 Strings 庫中的函數，用於將 uint256 轉換為十六進制的字符串表示。

3. `_number` 是作為參數傳遞給 toHexString 函數的 uint256 值。

這種調用方式直接使用庫合約的名稱 `Strings`，後面接上要調用的函數 `toHexString`，然後在括號內傳入參數 `_number`。

這種方法的特點和優勢：

1. **明確性**：這種調用方式非常清晰，可以直接看出我們在調用哪個庫的哪個函數。

2. **靈活性**：不需要使用 `using for` 指令，可以在需要時隨時調用庫函數。

3. **可讀性**：對於不熟悉代碼的人來說，這種方式可能更容易理解庫函數的來源。

4. **避免命名衝突**：如果有多個庫定義了同名函數，這種方式可以明確指定使用哪個庫的函數。

需要注意的是，在使用這種方法之前，確保你已經正確地導入了 Strings 庫。通常，你需要在合約文件的開頭加上類似這樣的導入語句：

```solidity
import "@openzeppelin/contracts/utils/Strings.sol";
```

或者如果 Strings 庫在同一個項目中的其他文件裡，你可能需要使用相對路徑來導入。

這種直接通過庫名調用的方式和使用 `using for` 指令的方式在功能上是等價的，選擇哪種方式主要取決於個人偏好和項目的編碼風格。

## Q2
根據您的描述和提供的代碼片段，正確的填空應該是：

```solidity
// 利用using for指令
using Strings for uint256;
function getString1(uint256 _number) public pure returns(string memory){
    return _number.toHexString();
}
```

這裡的解釋是：

1. `using Strings for uint256;` 這行代碼將 Strings 庫的所有函數附加到 uint256 類型上。

2. 這意味著我們可以直接在 uint256 類型的變量上調用 Strings 庫中的函數，就像它們是 uint256 的成員函數一樣。

3. `_number` 是一個 uint256 類型的參數。

4. `.toHexString()` 是直接在 `_number` 上調用的，因為我們已經使用 `using for` 指令將這個函數附加到了 uint256 類型上。

這種方法的優點是使代碼更加簡潔和直觀。它允許我們像調用對象的方法一樣調用庫函數，這在某些情況下可以提高代碼的可讀性。

需要注意的是：

1. 使用這種方法時，`_number` 會自動作為 `toHexString()` 函數的第一個參數。

2. 如果 `toHexString()` 函數需要額外的參數，可以在 `.toHexString()` 後的括號中添加。

3. 這種方法和直接通過庫名調用（如 `Strings.toHexString(_number)`）在功能上是完全等同的，只是語法和使用方式不同。

4. 使用 `using for` 指令可以讓代碼更加簡潔，特別是當你需要多次調用同一個庫的函數時。

總的來說，這種方法展示了 Solidity 中庫使用的靈活性，允許開發者根據自己的偏好和項目需求選擇最合適的使用方式。

### 2024.10.05
以下是對Solidity中import語句的重述與解釋,以及一些補充思考:

## import語句簡介

在Solidity中,import語句用於在一個合約文件中引用其他文件的內容,提高代碼的可重用性和組織性。這對於大型項目和模塊化開發非常有用。

## import的基本用法

### 1. 通過相對路徑導入

```solidity
import './Yeye.sol';
```

這會導入同一目錄下的Yeye.sol文件。

### 2. 通過URL導入

```solidity
import 'https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/Address.sol';
```

這允許直接從網絡上導入合約。

### 3. 通過npm包導入

```solidity
import '@openzeppelin/contracts/access/Ownable.sol';
```

這用於導入通過npm安裝的依賴包。

### 4. 導入特定符號

```solidity
import {Yeye} from './Yeye.sol';
```

這只導入Yeye.sol文件中的Yeye合約。

## 使用位置

import語句通常放在solidity文件的頂部,在版本聲明之後,其他代碼之前。

## 補充思考

1. **模塊化設計**: import允許將大型合約拆分成多個小文件,提高代碼的可讀性和維護性。

2. **代碼重用**: 可以輕鬆重用自己或他人編寫的合約庫,如OpenZeppelin。

3. **版本控制**: 使用特定URL或npm包版本可以確保導入的代碼版本一致性。

4. **安全性考慮**: 從外部源導入代碼時,需要確保源代碼的安全性和可信度。

5. **gas優化**: 合理使用import可以減少重複代碼,潛在地降低部署成本。

6. **依賴管理**: 在大型項目中,需要仔細管理導入的依賴,避免版本衝突。

7. **編譯時間**: 過多的import可能會增加編譯時間,需要權衡。

通過掌握import的使用,開發者可以更好地組織和構建複雜的智能合約系統,提高開發效率和代碼質量。

Citations:
[1] https://vocus.cc/article/646d3ab0fd89780001f8cf5b
[2] https://binschool.org/solidity-basic/solidity-import.html
[3] https://blog.csdn.net/qq_52708261/article/details/127064930
[4] https://docs.soliditylang.org/zh/v0.8.16/path-resolution.html
[5] https://vocus.cc/article/6254ed24fd89780001a38745
[6] https://wtf.academy/docs/solidity-102/Import/
[7] https://remix-ide.readthedocs.io/zh-cn/latest/import.html
[8] https://blog.csdn.net/u013288190/article/details/123807010

### 題目
以下是對這些題目的回答:

1. Solidity中import的作用是:
   在一個合約文件中引用其他文件的內容,提高代碼的可重用性和組織性。
   C. 導入其他合約中的全局符號，解釋如下:
      import語句的主要作用是在一個合約文件中引用其他文件的內容,提高代碼的可重用性和組織性。
      通過import,可以導入其他合約文件中定義的全局符號,包括:合約、函數、結構體、枚舉等
   
        （a） import不能直接導入其他合約的私有變量或內部變量,這些只能在定義它們的合約內部訪問。
   
         (b) 雖然可以導入接口,但這只是全局符號導入的一種特殊情況,而不是import的主要目的。
   
         (d) import的作用範圍是全局的,可以導入任何公開的全局符號,而不僅限於某種特定類型。

所以,C選項"導入其他合約中的全局符號"最準確地概括了Solidity中import的主要作用。它允許開發者重用和組織代碼,提高開發效率。

3. 以下import寫法錯誤的是:
   A. import from "./Yeye.sol";

   這個選項是錯誤的。正確的寫法應該是:
   import "./Yeye.sol";
   或者
   import {Yeye} from "./Yeye.sol";

4. import導入文件中的全局符號可以單獨指定其中的:
   D. 以上都可以

   Solidity允許導入合約、函數、結構體等多種類型的全局符號。

5. 被導入文件中的全局符號想要被其他合約單獨導入,應該怎麼編寫?
   C. 與合約並列在文件結構中

   為了使全局符號能被單獨導入,它們應該定義在合約結構之外,與合約並列在文件結構中。這樣可以使這些符號成為真正的全局符號,能夠被其他文件單獨導入使用。

這些答案反映了Solidity中import語句的用法和特性。import提供了模塊化和代碼重用的能力,是Solidity開發中非常重要的一個特性。

Citations:
[1] https://vocus.cc/article/646d3ab0fd89780001f8cf5b
[2] https://binschool.org/solidity-basic/solidity-import.html
[3] https://www.wtf.academy/docs/solidity-102/Import/
[4] https://remix-ide.readthedocs.io/zh-cn/latest/import.html
[5] https://blog.csdn.net/qq_52708261/article/details/127064930
[6] https://blog.csdn.net/u013288190/article/details/123807010
[7] https://docs.soliditylang.org/zh/v0.8.16/path-resolution.html
[8] https://vocus.cc/article/6254ed24fd89780001a38745

### 2024.10.06

## 特殊回調函數:receive()和fallback()

Solidity支持兩種特殊的回調函數:receive()和fallback()。這兩個函數主要用於以下兩種情況:

1. 接收ETH
2. 處理合約中不存在的函數調用(用於代理合約)

**重要注意事項:**
在Solidity 0.6.x版本之前,只有fallback()函數,用於接收ETH和處理未匹配的函數調用。0.6版本後,Solidity將fallback()拆分為receive()和fallback()兩個函數。

### receive()函數

receive()函數在合約接收ETH時被調用。每個合約最多只能有一個receive()函數,其聲明方式特殊:

```solidity
receive() external payable { ... }
```

receive()函數不能有參數,不能返回值,必須是external和payable。

**最佳實踐:**
receive()函數應保持簡單,因為使用send和transfer方法發送ETH時,gas限制為2300。複雜的receive()可能導致Out of Gas錯誤。

### fallback()函數

fallback()函數在調用不存在的合約函數時觸發。它可用於接收ETH和實現代理合約功能。聲明如下:

```solidity
fallback() external payable { ... }
```

### receive()和fallback()的區別

兩者都能用於接收ETH,但觸發規則不同:

1. 如果msg.data為空且存在receive(),則觸發receive()
2. 如果msg.data不為空或不存在receive(),則觸發fallback()

如果兩者都不存在,直接發送ETH到合約將會失敗。

## 補充見解

1. **安全考慮:** 惡意合約可能在receive()或fallback()中嵌入耗費大量gas或故意失敗的代碼,影響正常的退款和轉賬邏輯。開發包含這些功能的合約時需特別注意。

2. **代理合約應用:** fallback()在代理合約中扮演重要角色,允許合約動態更新邏輯。

3. **事件記錄:** 在這些函數中發送事件是好的做法,有助於跟蹤和調試。

## 延伸思考

1. **合約設計:** 如何設計一個既安全又靈活的合約,能夠處理各種ETH接收情況?

2. **升級策略:** 考慮到Solidity版本的變化,如何設計向後兼容的合約?

3. **gas優化:** 在receive()和fallback()中如何平衡功能實現和gas消耗?

4. **跨鏈應用:** 這些特殊函數在不同區塊鏈平台上的實現有何異同?

5. **智能合約互操作性:** receive()和fallback()如何促進不同合約間的互動?

6. 這是一個很好的問題。讓我來解釋「不存在的合約函數」的概念,以及fallback()函數如何在這種情況下被觸發。

## 「不存在的合約函數」的概念，當我們說「不存在的合約函數」時,我們指的是:

1. 調用者試圖調用一個在合約中沒有定義的函數。
2. 調用的函數簽名(包括函數名和參數類型)與合約中的任何函數都不匹配。

## 如何觸發「不存在的函數」

雖然這些函數「不存在」,但它們仍然可以被「調用」,主要通過以下方式:

1. **直接調用:** 當外部賬戶或其他合約嘗試調用目標合約中不存在的函數時。

2. **低級調用:** 使用Solidity的低級調用方法(如call、delegatecall等)時,可以發送任意的函數簽名,即使該函數在合約中不存在。

3. **錯誤的接口:** 如果使用了錯誤或過時的合約接口(ABI),可能會導致調用不存在的函數。

4. **代理模式:** 在使用代理合約模式時,如果邏輯合約更新但代理合約的調用沒有相應更新,可能會嘗試調用不存在的函數。

## fallback()函數如何被觸發

當合約收到一個不匹配任何已定義函數的調用時,fallback()函數會自動被觸發。這個機制允許合約優雅地處理意外或錯誤的調用,而不是簡單地拋出錯誤。

例如:

```solidity
contract MyContract {
    fallback() external payable {
        // 處理未知調用
    }
}
```

如果有人嘗試調用MyContract中不存在的函數,fallback()將被執行。

## 實際應用

1. **錯誤處理:** 可以在fallback()中記錄錯誤調用,幫助調試。

2. **默認行為:** 為合約定義一個默認行為,處理所有未預期的交互。

3. **代理模式:** 在代理合約中,fallback()可以將調用轉發到實現合約。

4. **接收以太幣:** 如果合約沒有定義receive()函數,fallback()可以用來接收以太幣轉賬。

Understanding this mechanism is crucial for developing robust and flexible smart contracts. It provides a safety net for unexpected interactions and enables advanced contract patterns like upgradeable contracts.

Citations:
[1] https://dev.to/shlok2740/fallback-functions-in-solidity-13nb
[2] https://bitsbyblocks.com/everything-you-need-to-know-about-solidity-fallback-functions/
[3] https://docs.soliditylang.org/en/latest/contracts.html
[4] https://solidity-by-example.org/fallback/

### 題目
讓我們來逐一分析這些問題:

1. 下面哪個選項語法是正確的？

正確答案是 A. receive() external payable { }

解釋:
- receive()函數必須是external和payable的。
- 不需要使用function關鍵字。
- 不能有任何參數。
- 必須是payable的,因為它用於接收ETH。

2. fallback(or receive)函數能否在合約內部調用？

正確答案是 B. 不能

解釋:
- fallback和receive函數都必須是external的。
- external函數只能從合約外部調用,不能在合約內部直接調用。
- 這些函數的設計目的是處理外部調用,特別是處理未預期的調用或純ETH轉賬。

3. vitalik想部署一個能接收ETH和msg.data的合約，那麼他部署的合約中______________________

正確答案是 B. 必須含有fallback函數

解釋:
- receive()函數只能處理純ETH轉賬(沒有msg.data)。
- fallback()函數可以處理帶有msg.data的調用,同時如果聲明為payable,也可以接收ETH。
- 要同時處理ETH和msg.data,fallback()函數是必需的。
- 雖然同時包含receive()和fallback()函數可以更精確地處理不同情況,但題目只問最低要求,所以只需fallback()函數就足夠了。

這些問題很好地測試了對Solidity中特殊函數的理解。記住,receive()主要用於純ETH轉賬,而fallback()則更加靈活,可以處理各種未預期的調用情況。

Citations:
[1] https://docs.soliditylang.org/en/latest/contracts.html
[2] https://ethereum-blockchain-developer.com/2022-03-deposit-withdrawals/09-sending-ether-to-smart-contracts/
[3] https://coinsbench.com/fallback-and-receive-function-in-solidity-6e65fe2556f8?gi=3ee523785c67
[4] https://bitsbyblocks.com/everything-you-need-to-know-about-solidity-fallback-functions/

4. 根據合約的內容和問題描述，正確答案是 C. error：'Fallback' function is not defined，value和msg.data均發送失敗。
**解釋:**
- 合約中只有 `receive()` 函數，這個函數會在接收純 ETH 轉賬（即 `msg.data` 為空）時被調用。
- 當 `msg.data` 不為空（如 `0xaa`），`receive()` 不會被觸發。
- 由於合約中沒有定義 `fallback()` 函數，因此當帶有 `msg.data` 的交互發生時，合約無法處理這種情況，導致錯誤。

5. 根據提供的合約代碼，正確答案是 A. error：'Fallback' function is not defined，value和msg.data均發送失敗。

**解釋:**

- 合約中只有 `receive()` 函數，這個函數只會在接收純 ETH 轉賬時（即 `msg.data` 為空）被調用。
- 當 `msg.data` 不為空時（例如包含函數選擇器），`receive()` 不會被觸發。
- 合約中沒有定義 `fallback()` 函數，因此當帶有 `msg.data` 的交互發生時，合約無法處理這種情況，導致錯誤。

Citations:
[1] https://pplx-res.cloudinary.com/image/upload/v1728188437/user_uploads/klgmxzjrh/19840b7416712478526285cdcee6e76.jpg
[2] https://pplx-res.cloudinary.com/image/upload/v1728188294/user_uploads/hytotohit/48778bbd8fd53abdd6c7cbd727881bc.jpg

### 2024.10.07

## 發送 ETH 的三種方法

在 Solidity 中，有三種方法可以向其他合約發送 ETH：

1. transfer()
2. send()
3. call()

其中，call() 是目前被鼓勵使用的方法。

## 接收 ETH 合約

首先，我們來看一個接收 ETH 的合約範例：

```solidity
contract ReceiveETH {
    event Log(uint amount, uint gas);
    
    receive() external payable {
        emit Log(msg.value, gasleft());
    }
    
    function getBalance() view public returns(uint) {
        return address(this).balance;
    }
}
```

這個合約包含：
- 一個 Log 事件，記錄接收的 ETH 數量和剩餘的 gas
- 一個 receive() 函數，在接收 ETH 時被觸發
- 一個 getBalance() 函數，用於查詢合約的 ETH 餘額

## 發送 ETH 合約

接下來，我們實現一個可以發送 ETH 的合約：

```solidity
contract SendETH {
    constructor() payable {}
    receive() external payable {}
    
    // 以下將實現三種發送方法
}
```

### 1. transfer() 方法

```solidity
function transferETH(address payable _to, uint256 amount) external payable {
    _to.transfer(amount);
}
```

特點：
- gas 限制為 2300
- 轉賬失敗會自動 revert

### 2. send() 方法

```solidity
error SendFailed();

function sendETH(address payable _to, uint256 amount) external payable {
    bool success = _to.send(amount);
    if (!success) {
        revert SendFailed();
    }
}
```

特點：
- gas 限制為 2300
- 轉賬失敗不會自動 revert，需要手動處理
- 而且發送失敗不會自動revert交易，幾乎沒有人用它

### 3. call() 方法

```solidity
error CallFailed();

function callETH(address payable _to, uint256 amount) external payable {
    (bool success,) = _to.call{value: amount}("");
    if (!success) {
        revert CallFailed();
    }
}
```

特點：
- 沒有 gas 限制
- 最靈活，可支援複雜邏輯
- 轉賬失敗不會自動 revert，需要手動處理

## 補充見解

1. **安全性考慮**：雖然 call() 是最靈活的方法，但也需要格外小心。因為它沒有 gas 限制，可能會被惡意合約利用來耗盡 gas。

2. **重入攻擊**：使用 call() 時要特別注意重入攻擊（reentrancy attacks）的風險。建議遵循 checks-effects-interactions 模式來編寫代碼。

3. **錯誤處理**：send() 和 call() 方法需要手動處理錯誤，這可以提供更大的靈活性，但也增加了代碼的複雜性。

## 延伸思考

1. **為什麼 call() 成為推薦方法**？隨著以太坊網絡的發展，合約邏輯變得越來越複雜。call() 的靈活性使得它能夠適應各種場景，而 transfer() 和 send() 的 gas 限制可能會在某些情況下造成問題。

2. **gas 優化**：在使用這些方法時，如何平衡安全性和 gas 消耗？是否有辦法在使用 call() 的同時限制 gas 使用量？

3. **跨鏈轉賬**：隨著區塊鏈技術的發展，跨鏈轉賬變得越來越重要。這些方法如何適應跨鏈場景？未來可能會出現什麼新的轉賬方法？

4. **智能合約升級**：考慮到這些方法的限制和優缺點，在設計可升級的智能合約時，應該如何選擇和實現轉賬功能？

## 問題4

Vitalik 寫了一個合約，該合約在被部署時可以轉 ETH 進去。這意味著構造函數需要是 payable 的。讓我們逐一檢視選項：

A. constructor() payable{}
B. constructor() {}
C. constructor(uint256 _amount) payable{ (address(this)).transfer(_amount); }

正確答案是 **A. constructor() payable{}**

解釋：
- 選項 A 是正確的，因為它使用了 payable 關鍵字，允許在部署時接收 ETH。
- 選項 B 沒有 payable 關鍵字，所以不能在部署時接收 ETH。
- 選項 C 雖然也是 payable 的，但它多了一個不必要的參數和轉賬操作。在構造函數中，合約已經自動接收了發送的 ETH，不需要額外的轉賬操作。

## 問題5
5. 
error SendFailed(); 
function sendETH(address payable _to, uint256 amount) external payable{
            ______________________________________
    }
   
在問題 5 中，我們需要選擇一個選項，使得 `sendETH` 函數在執行失敗時自動 revert 交易。
該函數執行失敗時會自動revert交易，那麼下面哪個選項可以填入橫線處？
A. bool success = _to.send(amount); if( !success ){ revert SendFailed(); }
B. bool success = _to.call(amount); if( !success ){ revert SendFailed(); }
C. _to.send(amount);
D. bool success = _to.send{value: amount}(" "); if( !success ){ revert SendFailed(); }

### 選項分析

- **A.** `bool success = _to.send(amount); if( !success ){ revert SendFailed(); }`
  - `send()` 方法返回一個布爾值，表示成功或失敗。這個選項正確地檢查了返回值，並在失敗時使用 `revert` 來回滾交易。

- **B.** `bool success = _to.call(amount); if( !success ){ revert SendFailed(); }`
  - `call()` 方法的語法不正確。`call` 返回兩個值，不應直接賦值給單個布爾變量。

- **C.** `_to.send(amount);`
  - 這個選項沒有處理返回值，因此不會自動 revert。

- **D.** `bool success = _to.send{value: amount}(" "); if( !success ){ revert SendFailed(); }`
  - 語法錯誤，`send` 不接受 `{value: amount}` 語法，這是 `call` 的用法。

### 正確答案
正確答案是 **A**。這個選項使用了 `send()` 方法，並在失敗時通過檢查返回值來手動 revert 交易。這符合題目要求，即在執行失敗時自動 revert。

## 問題6
vitalik又寫了一個用call()發送ETH的函數：
該函數執行失敗時會自動revert交易，那麼下面哪個選項可以填入橫線處？
A. (bool success,) = _to.call{value: amount}(" "); if( !success ){ revert CallFailed(); }
B. bool success = _to.call{value: amount}(" "); if( !success ){ revert CallFailed(); }
C. _to.call(amount);
D. (bool success,) = _to.call(amount); if( !success ){ revert CallFailed(); }
error CallFailed();
function callETH(address payable _to, uint256 amount) external payable{
            ______________________________________
    }

首先，我們需要理解 `call()` 方法的特性：
1. `call()` 不會自動 revert 交易。
2. `call()` 返回兩個值：一個布爾值（表示成功或失敗）和一個 bytes 類型的數據（通常可以忽略）。
3. 發送 ETH 時，需要使用 `{value: amount}` 語法。

現在讓我們逐一檢查選項：

A. `(bool success,) = _to.call{value: amount}(" "); if( !success ){ revert CallFailed(); }`
   這是正確的語法和邏輯。它使用了 `call()` 方法發送 ETH，檢查了返回值，並在失敗時 revert。

B. `bool success = _to.call{value: amount}(" "); if( !success ){ revert CallFailed(); }`
   這個語法是錯誤的，因為 `call()` 返回兩個值，不能直接賦值給單個變量。

C. `_to.call(amount);`
   這個語法是錯誤的。它沒有使用 `{value: amount}` 來發送 ETH，也沒有檢查返回值或處理失敗情況。

D. `(bool success,) = _to.call(amount); if( !success ){ revert CallFailed(); }`
   這個語法也是錯誤的。它沒有使用 `{value: amount}` 來發送 ETH。

因此，正確的答案是 **A**。

完整的函數應該是這樣的：

```solidity
error CallFailed();

function callETH(address payable _to, uint256 amount) external payable {
    (bool success,) = _to.call{value: amount}("");
    if (!success) {
        revert CallFailed();
    }
}
```

這個實現正確地使用了 `call()` 方法發送 ETH，並在失敗時 revert 交易。雖然 `call()` 本身不會自動 revert，但通過手動檢查返回值並使用 `revert`，我們實現了在失敗時自動 revert 交易的效果。

## 問題7

7. 假設存在如下附件兩個合約(sendETH和ReceiveETH)，兩個合約目前ETH餘額皆為0，現在vitalik想通過SendETH合約的callETH函數往ReceiveETH合約轉入1ETH，他將交易的value設置為2ETH，同時交易成功執行，那麼此時sendETH合約和ReceiveETH的ETH餘額分別為？

A. 1ETH；1ETH
B. 0ETH；2ETH
C. 0ETH；1ETH
D. 2ETH；0ETH

在這個情境中，Vitalik 使用 `SendETH` 合約的 `callETH` 函數來向 `ReceiveETH` 合約轉入 1 ETH。交易的 `value` 設置為 2 ETH。

讓我們分析發生了什麼：

1. **交易開始時**，`SendETH` 合約有 2 ETH 的餘額（因為交易的 `value` 是 2 ETH）。
2. **執行 `callETH` 函數**：
   - 該函數從 `SendETH` 合約中提取 1 ETH 並使用 `call()` 發送到 `ReceiveETH` 合約。
   - 由於交易成功，1 ETH 被轉移到 `ReceiveETH` 合約。

3. **交易結束時**：
   - `SendETH` 合約剩下的餘額是 1 ETH（2 ETH 初始值 - 1 ETH 發送）。
   - `ReceiveETH` 合約收到 1 ETH。

因此，答案是：

**A. 1ETH；1ETH**

### 2024.10.08

## 調用已部署合約

在 Solidity 中，合約之間的互動是構建複雜去中心化應用（DApps）的關鍵。本章節將深入探討如何在已知合約代碼（或接口）和地址的情況下，調用已部署的合約。

### 目標合約

首先，讓我們來看一個名為 `OtherContract` 的簡單合約，它將作為我們調用的目標：

```solidity
contract OtherContract {
    uint256 private _x = 0;
    event Log(uint amount, uint gas);
    
    function getBalance() view public returns(uint) {
        return address(this).balance;
    }

    function setX(uint256 x) external payable {
        _x = x;
        if(msg.value > 0){
            emit Log(msg.value, gasleft());
        }
    }

    function getX() external view returns(uint x){
        x = _x;
    }
}
```

這個合約包含：
- 一個私有狀態變量 `_x`
- 一個 `Log` 事件，在收到 ETH 時觸發
- 三個函數：`getBalance()`、`setX()`、和 `getX()`

### 調用 OtherContract 合約的方法

有幾種方法可以調用已部署的合約：

1. **傳入合約地址**

   ```solidity
   function callSetX(address _Address, uint256 x) external {
       OtherContract(_Address).setX(x);
   }
   ```

2. **傳入合約變量**

   ```solidity
   function callGetX(OtherContract _Address) external view returns(uint x) {
       x = _Address.getX();
   }
   ```

3. **創建合約變量**

   ```solidity
   function callGetX2(address _Address) external view returns(uint x) {
       OtherContract oc = OtherContract(_Address);
       x = oc.getX();
   }
   ```

4. **調用合約並發送 ETH**

   ```solidity
   function setXTransferETH(address otherContract, uint256 x) payable external {
       OtherContract(otherContract).setX{value: msg.value}(x);
   }
   ```

### 重要概念

1. **合約引用**: 使用 `_Name(_Address)` 格式創建合約引用，其中 `_Name` 是合約名稱，`_Address` 是合約地址。

2. **函數調用**: 使用 `_Name(_Address).f()` 格式調用合約函數，其中 `f()` 是要調用的函數。

3. **發送 ETH**: 使用 `_Name(_Address).f{value: _Value}()` 格式在調用函數時發送 ETH。

4. **接口重要性**: 雖然本例中我們使用了完整的合約代碼，但在實際應用中，只需要知道合約的接口就足夠了。

### 實踐步驟

1. 在 Remix 中部署 `OtherContract`。
2. 部署包含調用函數的合約（如 `CallContract`）。
3. 複製 `OtherContract` 的地址。
4. 使用 `CallContract` 的函數，傳入 `OtherContract` 的地址進行調用。
5. 驗證調用結果，例如檢查 `x` 的值或合約的 ETH 餘額。

### 注意事項

- 確保您有正確的合約地址和接口。
- 在發送 ETH 時，確保目標函數是 `payable` 的。
- 使用 `view` 和 `pure` 函數不會改變區塊鏈狀態，不需要支付 gas。

### 總結

通過這些方法，開發者可以實現合約間的互動，這對於構建模塊化和可擴展的 DApps 至關重要。理解並掌握這些技術可以大大提高智能合約的功能性和靈活性.

Sources


<!-- Content_END -->
