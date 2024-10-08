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

<!-- Content_END -->
